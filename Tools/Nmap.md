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


## Discovering running servies


running nmap set with -Pn to skip host discovery since we know its already up and running in the sandbox environment. 


nmap -Pn enum-sandbox


service and version detection are done with the -sV flag


nmap -sV enum-sandbox


running a script to discover HTTP methods


nmap -p 80 --script http-methods enum-sandbox



--open
Only show hosts that have open ports, and only show the open ports for those. Here, “open ports” are any ports that have the possibility of being open, which includes open, open|filtered, and unfiltered.


## Host Discovery
https://nmap.org/book/man-host-discovery.html

 
 If we know our target server is up, we can skip the host discovery phase with the -Pn option.

 
 nmap -Pn enum-sandbox


 Nmap can also perform service and version detection. There are several options we can configure for this, but the -sV flag for version detection is often sufficient during web application assessments.

 
 nmap -sV enum-sandbox


Nmap includes a scripting engine (NSE) that extends its functionality via Lua scripts. We can run scripts as part of our scan by setting the --script option, followed by the script name we want to run. We can optionally use wild cards (*) in the script name or specify categories. We won't review every available script here, as many of them go beyond the scope of web application assessments. However, there are many HTTP relevant scripts.


Let's try running a scan of port 80 with the http-methods script. This script will identify what HTTP methods the server has enabled. We'll specify -p 80 to limit the scan to port 80 and --script http-methods.


nmap -p 80 --script http-methods enum-sandbox




