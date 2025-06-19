# 🚀 Termux DNS Fix

This repo explains how to fix the common DNS resolution error in Termux, especially when using bots or scripts that send requests to external APIs like Discord:



```
ERROR - Error sending request: Cannot connect to host discord.com:443 ssl\:default \[Could not contact DNS servers]

````

---

## 📌 Problem

Your Termux bot or script cannot connect to `discord.com` or any domain due to DNS failure. This usually happens because:

- Android/Termux cannot access default DNS servers
- Mobile data firewall or captive portal issues
- No DNS configuration in `$PREFIX/etc/resolv.conf`

---

## ✅ Fix DNS in Termux (Manual)

1. **Open Termux**
2. Run the following:

```bash
mkdir -p $PREFIX/etc
echo 'nameserver 8.8.8.8' > $PREFIX/etc/resolv.conf
echo 'nameserver 1.1.1.1' >> $PREFIX/etc/resolv.conf
````

✅ This uses Google's and Cloudflare's DNS.

3. Test DNS:

```bash
ping discord.com
```

If it replies, your issue is fixed!

---

## 🧹 How to Remove DNS Fix (Reset)

If you want to remove this manual DNS override:

```bash
rm -f $PREFIX/etc/resolv.conf
```

Or edit it manually:

```bash
nano $PREFIX/etc/resolv.conf
```

Then clear the content or remove bad entries.

---

## 🛠 Optional Script to Auto-Fix

You can create a script to fix DNS quickly:

```bash
nano fix_dns.sh
```

Paste:

```bash
#!/data/data/com.termux/files/usr/bin/bash
mkdir -p $PREFIX/etc
echo 'nameserver 8.8.8.8' > $PREFIX/etc/resolv.conf
echo 'nameserver 1.1.1.1' >> $PREFIX/etc/resolv.conf
echo "[✔] DNS Fixed Successfully"
```

Make it executable:

```bash
chmod +x fix_dns.sh
./fix_dns.sh
```

---

## 🧪 Tested On

* Termux (F-Droid)
* Python 3.10 / 3.11
* Android 10, 11, 13

---

## 👨‍💻 Common Use Cases

* Discord bots using `aiohttp` or `requests`
* Web scraping scripts
* Telegram bots
* Crypto trading bots (e.g., `ccxt`)

---

## ❤️ Support

If this helped you, feel free to star the repo or contribute improvements!
