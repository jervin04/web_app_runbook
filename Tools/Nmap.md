# Nmap

Nmap NSE scripts
cd /usr/share/nmap/scripts

To get an easy list of the installed scripts try locate nse | grep script. 


will list all scripts related to HTTP
ls -lsaht |grep -i 'http'

run script example
nmap -p 80 --script=http-enum $IP

HTTP methods. is one of the few scripts that accepts arguments. This will show which methods are available on aserver

nmap -p80 --script=http-methods --script-args http-methods.url-path='/wp-includes/' $IP


Discovering running servies

TEST (toook forever): nmap -v -A -O -sT -sU -p- -sV -T4 enum-sandbox

running nmap set with -Pn to skip host discovery since we know its already up and running in the sandbox environment. 
nmap -Pn enum-sandbox

service and version detection are done with the -sV flag
nmap -sV enum-sandbox


running a script to discover HTTP methods
nmap -p 80 --script http-methods enum-sandbox



--open
Only show hosts that have open ports, and only show the open ports for those. Here, “open ports” are any ports that have the possibility of being open, which includes open, open|filtered, and unfiltered.


Host Discovery
https://nmap.org/book/man-host-discovery.html


