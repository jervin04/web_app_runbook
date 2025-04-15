# Wordlist

seclists

https://gitlab.com/kalilinux/packages/seclists

sudo apt install seclists
seclist -h
tree -d /usr/share/seclists


Payloads All The Things is another useful collection of wordlists focused on exploitation. As with SecLists, we can clone the repo from GitHub or install it with Kali's package manager.

sudo apt install payloadsallthethings


ls -lh /usr/share/payloadsallthethings



CeWL is a custom wordlist generator that is included in Kali Linux. It crawls a URL and creates a list of words from the pages it discovers. CeWL has many optional settings to control how it crawls, what words it tracks, and how it outputs the results.

cewl --write output.txt --lowercase -m 4 http://enum-sandbox/manual


tail output.txt


In addition to creating wordlists from web applications, there are other situations in which we may want to create wordlists. For example, if we know our target's operating system, we could build a wordlist of binaries that we might want to leverage in a command injection attack.

For example, we could use ls to get the contents of /usr/bin, pipe the results to grep, use -v / to exclude directories, and redirect the results to a file.

ls /usr/bin | grep -v "/" > binaries.txt


tail binaries.txt


