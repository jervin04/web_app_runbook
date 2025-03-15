# Wfuzz

export URL="http://zda:80/FUZZ"

wfuzz -c -z file,/usr/share/seclists/Discovery/Web-Content/raft-medium-files.txt --hc 301,404,403 "$URL"