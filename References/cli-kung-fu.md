# BashKungFu

list items in list format include size of all items, included hidden all files in human readable format and sort by newest time first


ls -lsaht


use the mouspad tool to open an edit a file... because everyone hates vim


sudo mousepad /etc/hosts


cat /etc/hosts



When using a brute forcing tool, selecting the right wordlist can directly impact our results. DIRB's default wordlist is often useful, but we may want to use different wordlists if we don't get many results. Kali Linux includes several wordlists at /usr/share/wordlists.


ls -alh /usr/share/wordlists


find all files with permissions high suid permissions, and send get rid of all the errors from the scan, since this scans entire file system


find / -perm /4000 2>/dev/null
