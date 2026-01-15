## Tools (Non-Exhaustive)

The following tools are used selectively based on scope, authorization, and target behavior. Tool usage is always aligned with responsible disclosure practices.

### Reconnaissance & Asset Discovery
- **Subfinder** – Passive subdomain enumeration  
- **Assetfinder** – Lightweight subdomain discovery  
- **Findomain** – Fast subdomain enumeration  
- **Amass** – Passive and active asset discovery (scope-aware)  
- **crt.sh** – Certificate transparency analysis  
- **Wayback Machine (CDX API)** – Historical endpoint discovery  
- **GitHub Subdomains** – Public repository domain exposure analysis  

### Asset Validation & Service Identification
- **DNSx** – DNS resolution and validation  
- **HTTPX** – Live host detection and service probing  
- **ASNMap** – ASN-based asset mapping (when in scope)  

### Content & Endpoint Discovery
- **Katana** – Web crawling and endpoint extraction  
- **Gau** – URL collection from public archives  
- **URLFinder** – Endpoint discovery  
- **FFUF** – Directory and subdomain fuzzing (controlled usage)  
- **Dirsearch** – Content discovery  

### Parameter & Input Discovery
- **Arjun** – Hidden GET/POST parameter discovery  
- **URO** – URL normalization and deduplication  

### Vulnerability Detection & Validation
- **Nuclei** – Template-based vulnerability detection (non-intrusive templates only)  
- **Manual Testing (Burp Suite)** – Request analysis, logic testing, and validation  

### CMS & Technology Analysis (When Applicable)
- **Wappalyzer** – High-level technology fingerprinting  
- **WPScan** – WordPress security analysis (only when WordPress is confirmed and in scope)  

### Notes
- Tools are not used blindly; manual analysis and context take priority.  
- No credentials, tokens, private endpoints, or undisclosed targets are tested or shared.  
- Automation supports analysis — it does not replace reasoning.
