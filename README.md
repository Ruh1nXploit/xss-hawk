#!/bin/bash

# Colors
RED='\033[0;31m'
GREEN='\033[0;32m'
BLUE='\033[1;34m'
YELLOW='\033[1;33m'
CYAN='\033[0;36m'
NC='\033[0m'

# Check input
if [ -z "$1" ]; then
  echo -e "${RED}[!] Usage: ./xss-hawk.sh subdomains.txt${NC}"
  exit 1
fi

INPUT="$1"
mkdir -p output
LIVE="output/live.txt"
URLS="output/urls.txt"
RESULT="output/xss-results.txt"
PROXY_LIST="output/proxy-list.txt"

echo -e "${CYAN}===================================================="
echo -e "${GREEN}     XSS Hawk | Bash Automation Tool"
echo -e "${CYAN}====================================================${NC}"

# Step 1: Live Subdomain Check
echo -e "${YELLOW}[*] Checking live subdomains from ${INPUT}...${NC}"
cat "$INPUT" | httpx -silent -status-code -threads 80 -rate-limit 150 | awk '/200/ {print $1}' | sort -u > "$LIVE"
echo -e "${GREEN}[+] Live subdomains saved to ${LIVE} (${RED}$(wc -l < $LIVE) live domains${GREEN})${NC}"

# Step 2: URL Extraction
echo -e "${YELLOW}[*] Extracting URLs with gau and waybackurls...${NC}"
cat "$LIVE" | gau --threads 40 | sort -u > "$URLS.temp"
cat "$LIVE" | waybackurls | sort -u >> "$URLS.temp"
sort -u "$URLS.temp" > "$URLS"
rm "$URLS.temp"
echo -e "${GREEN}[+] URLs saved to ${URLS} (${RED}$(wc -l < $URLS) total unique URLs${GREEN})${NC}"

# Step 3: XSS Scan with Dalfox
echo -e "${YELLOW}[*] Scanning URLs with Dalfox (Reflected & Stored)...${NC}"
cat "$URLS" | dalfox pipe --no-spinner --silence --waf-evasion --delay 150 --timeout 10 > "$RESULT"
echo -e "${GREEN}[+] Dalfox scan completed. Results saved to ${RESULT}${NC}"

# Step 4: DOM XSS Scan with kxss
echo -e "${YELLOW}[*] Scanning URLs for DOM XSS using kxss...${NC}"
cat "$URLS" | kxss --silent --timeout 10 --delay 150 > "$RESULT.dom"
echo -e "${GREEN}[+] DOM XSS scan completed. Results saved to ${RESULT}.dom${NC}"

# Step 5: Proxy List (Auto Download)
echo -e "${YELLOW}[*] Downloading fresh proxy list...${NC}"
curl -s https://www.proxy-list.download/api/v1/get?type=https > "$PROXY_LIST"
echo -e "${GREEN}[+] Proxy list saved to ${PROXY_LIST}${NC}"

# Step 6: Final Output Summary
echo -e "${CYAN}=================== ${RED}XSS FINDINGS${CYAN} ===================${NC}"
grep -Ei "vulnerable|poc|reflected|found|param" "$RESULT" --color=always || echo -e "${RED}[!] No Reflected/Stored XSS found.${NC}"
grep -Ei "dom-xss" "$RESULT.dom" --color=always || echo -e "${RED}[!] No DOM XSS found.${NC}"

echo -e "${CYAN}====================================================${NC}"
echo -e "${GREEN}[✓] All done! Happy Hunting, ${USER}.${NC}"
