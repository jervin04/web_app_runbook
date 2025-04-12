# GoBuster


Endpoint Discovery
gobuster dir -u http://zda:80/ -w /usr/share/wordlists/dirb/common.txt -t 5 -b 301


subdomain discovery
gobuster dns -d DOMAIN.com -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -t 30
