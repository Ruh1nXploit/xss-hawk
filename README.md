<h1 align="center" style="color:#4CAF50;">XSS Hawk</h1>

<p align="center">
  <b style="color:#FFA500;">Fully Automated Bash Tool</b><br>
  <i style="color:#00CED1;">for Hunting Reflected, Stored & DOM-based XSS</i>
</p>

---

## <span style="color:#FFD700;">Features</span>

- <span style="color:#00FF00;">✓</span> Extracts <b>live subdomains</b> using <code>httpx</code>
- <span style="color:#00FF00;">✓</span> Collects URLs via <code>gau</code> & <code>waybackurls</code>
- <span style="color:#00FF00;">✓</span> Scans for <b>Reflected & Stored XSS</b> with <code>Dalfox</code>
- <span style="color:#00FF00;">✓</span> Detects <b>DOM XSS</b> with <code>kxss</code>
- <span style="color:#00FF00;">✓</span> Downloads fresh <b>proxy list</b> automatically
- <span style="color:#00FF00;">✓</span> <b>Colorful</b> and clean terminal output
- <span style="color:#00FF00;">✓</span> Results saved in organized <code>output/</code> folder

---

## <span style="color:#00BFFF;">Usage</span>

```bash
# Step 1: Make the script executable
chmod +x xss-hawk.sh

# Step 2: Run with your subdomain list
./xss-hawk.sh subdomains.txt
```

**Example:**
```bash
./xss-hawk.sh scope.txt
```

---

## <span style="color:#FFA07A;">Output Structure</span>

All results will be stored under the `output/` folder:

- `output/live.txt` – Live subdomains
- `output/urls.txt` – Extracted URLs
- `output/xss-results.txt` – Reflected/Stored XSS results (Dalfox)
- `output/xss-results.txt.dom` – DOM XSS results (kxss)
- `output/proxy-list.txt` – Auto-downloaded proxy list

---

## <span style="color:#7FFFD4;">Requirements</span>

- [httpx](https://github.com/projectdiscovery/httpx)
- [gau](https://github.com/lc/gau)
- [waybackurls](https://github.com/tomnomnom/waybackurls)
- [dalfox](https://github.com/hahwul/dalfox)
- [kxss](https://github.com/tomnomnom/kxss)

---

## <span style="color:#ADFF2F;">Happy Hunting!</span>

Made with love by [Ruh1nXploit](https://github.com/Ruh1nXploit)
