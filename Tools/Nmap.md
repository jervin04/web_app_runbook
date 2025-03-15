# Nmap

Nmap NSE scripts
cd /usr/share/nmap/scripts

will list all scripts related to HTTP
ls -lsaht |grep -i 'http'

run script example
nmap -p 80 --script=http-enum $IP

HTTP methods. is one of the few scripts that accepts arguments. This will show which methods are available on aserver

nmap -p80 --script=http-methods --script-args http-methods.url-path='/wp-includes/' $IP

