# Hakrawler

https://github.com/hakluke/hakrawler

Hakrawler plus the wayback machine. it combines spidering techniques with they wayback machiine to provide a large list of previously used or archived domains that would otherwise need to be "busted" via tools like gobuster or wfuzz. 


## Installation

### Normal Install

First, you'll need to [install go](https://golang.org/doc/install).

Then run this command to download + compile hakrawler:
```
go install github.com/hakluke/hakrawler@latest
```

You can now run `~/go/bin/hakrawler`. If you'd like to just run `hakrawler` without the full path, you'll need to `export PATH="~/go/bin/:$PATH"`. You can also add this line to your `~/.bashrc` file if you'd like this to persist.

### Docker Install (from dockerhub)

```
echo https://www.google.com | docker run --rm -i hakluke/hakrawler:v2 -subs
```

########################### 2nd method to install - Not recommended


sudo apt install hakrawler

and to run
echo https://www.google.com | docker run --rm -i hakluke/hakrawler -subs


cd $HOME/go/bin
echo "https://URL-HERE.com/" > urls.txt
cat urls.txt |./hakrawler
