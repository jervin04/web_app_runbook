# BashKungFu

list items in list format include size of all items, included hidden all files in human readable format and sort by newest time first


ls -lsaht


use the mouspad tool to open an edit a file... because everyone hates vim


sudo mousepad /etc/hosts


cat /etc/hosts



When using a brute forcing tool, selecting the right wordlist can directly impact our results. DIRB's default wordlist is often useful, but we may want to use different wordlists if we don't get many results. Kali Linux includes several wordlists at /usr/share/wordlists.


ls -alh /usr/share/wordlists


asking Linux to separate errors and 'good' results.


find / -name "passwd" 1>results.txt 2>errors.txt

Search for files that start with .hid. The search should be case insensitive from the root of the file system. Errors should be sent to /dev/null. Remember -iname searches for file name matches on a case insensitive basis. You can do this as follows:


find / -iname ".hid*" 2>/dev/null



Let us hunt for a specific file in the system. We are going to search from the root of the file system for files that contain the filename passwd. We will suppress errors based on permissions using 2>/dev/null.


find / -name "passwd" 2>/dev/null



find all files with permissions high suid permissions, and send get rid of all the errors from the scan, since this scans entire file system


find / -perm /4000 2>/dev/null



find all files in the etc directory, and grep for the string password, and surpress the errors


find /etc -iname "*.ini" -exec grep -i "password" {} /dev/null \; 2>/dev/null
