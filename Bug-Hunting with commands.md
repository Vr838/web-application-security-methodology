# Web Application Recon & Bug Bounty Commands

**Target:** example.com  
**Purpose:** Authorized security testing and responsible disclosure

---

## Subdomain Enumeration

subfinder -d example.com -all -recursive -o subfinder.txt

assetfinder --subs-only example.com > assetfinder.txt

findomain -t example.com | tee findomain.txt

amass enum -active -d example.com -brute \
-w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt \
-silent -o amass_active.txt

---

## Certificate Transparency & Archive Sources

curl -s "https://crt.sh/?q=example.com&output=json" | jq -r '.[].name_value' | sed 's/\*\.//g' | sort -u > crtsh.txt

curl -s "http://web.archive.org/cdx/search/cdx?url=*.example.com/*&output=text&fl=original&collapse=urlkey" | sed -e 's_https*://__' -e 's/\/.*//' -e 's/:.*//' -e 's/^www\.//' | sort -u > wayback.txt

---

## GitHub Subdomain Discovery (API Key Hidden)

github-subdomains -d example.com -t $GITHUB_TOKEN -o github.txt

---

## Merge & Deduplicate

cat *.txt | sort -u > final.txt

---

## Subdomain Validation & Expansion

subfinder -d example.com | alterx | dnsx > alterx_mutations.txt

echo example.com | alterx -enrich | dnsx > alterx_enriched.txt

echo example.com | alterx -pp word=/usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt | dnsx > alterx_permutations.txt

ffuf -u "https://FUZZ.example.com" -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -mc 200,301,302 -o ffuf.json

jq -r '.results[].host' ffuf.json > ffuf_subdomains.txt

---

## ASN & Network Intelligence

asnmap -d example.com | dnsx -silent -resp-only

amass intel -active -asn ASN_NUMBER

amass intel -active -cidr X.X.X.X/32

---

## Alive Host Detection

cat final.txt | httpx-toolkit -ports 80,443,8080,8000,8888 -threads 200 > alive.txt

---

## URL & Endpoint Discovery

katana -u alive.txt -d 2 -o katana_urls.txt

cat alive.txt | gau | sort -u > gau_urls.txt

---

## Parameter Discovery

cat gau_urls.txt | grep '=' | uro > params.txt

arjun -u https://example.com/page.php -oT arjun.txt -m GET,POST --passive

---

## Vulnerability Testing Phase

XSS  
SQL Injection  
IDOR  
Access Control  
CORS Misconfigurations

---

## Sensitive File Discovery

nuclei -l alive.txt -bs 50 -c 30

cat alive.txt | grep -E "\.zip|\.env|\.bak|\.sql|\.log|\.conf|\.json|\.yml"

---

## Directory & File Bruteforcing

dirsearch -u https://www.example.com -e js,json,txt --exclude-status 403,404,429 --random-agent --delay 0.3 --threads 10

ffuf -u https://www.example.com/FUZZ -w directory-list-2.3-big.txt -fc 404

---

## CMS Detection (WordPress)

curl -I https://www.example.com | grep -i wp

wpscan --url https://www.example.com --api-token $WPSCAN_API_KEY --enumerate ap,at,u --plugins-detection aggressive --force

---

## Disclaimer

All commands are for educational purposes and authorized security testing only.
Unauthorized testing is illegal and unethical.
