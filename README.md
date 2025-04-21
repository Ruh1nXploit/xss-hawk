# XSS Hawk 🦅  
A fast and simple Bash automation tool for hunting XSS vulnerabilities in live subdomains.

---

## ⚙️ Usage

1. Download the script:  
   Clone this repo or download `xss-hawk.sh`

2. Make it executable:  
   ```bash
   chmod +x xss-hawk.sh
   ```

3. Run the script:  
   ```bash
   ./xss-hawk.sh subdomains.txt
   ```

---

## 🔧 What It Does

- ✅ Checks for live subdomains using **httpx**
- 📂 Extracts URLs using **gau** and **waybackurls**
- 🎯 Scans for **Reflected/Stored XSS** using **dalfox**
- ⚡ Detects **DOM XSS** via **kxss**
- 🌐 Automatically fetches fresh proxy list for WAF evasion
- 🎨 Gives colorful, clean, and organized terminal output

---

## 📦 Requirements

Make sure the following tools are installed and accessible from your `$PATH`:

- [httpx](https://github.com/projectdiscovery/httpx)
- [gau](https://github.com/lc/gau)
- [waybackurls](https://github.com/tomnomnom/waybackurls)
- [dalfox](https://github.com/hahwul/dalfox)
- [kxss](https://github.com/tomnomnom/kxss)

You can install them via `go install` or your package manager.

---

## 👤 Author

Made with ❤️ by [Ruh1nXploit](https://github.com/Ruh1nXploit)
