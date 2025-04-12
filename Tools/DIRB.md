# DIRB

A brute forcing tool for automation. It is recommended to use this in conjunction with other tools for automation (hakrawler)

the command below will use the enum-sandbox IP address and crawl it with a wordlist
dirb http://enum-sandbox

Depending on our wordlists and the application we're attempting to enumerate, we may need to add or modify the file extensions of the entries in the wordlist. Let's consider an example from Listing 10. DIRB identified a resource at http://enum-sandbox/banners. The word "banners" came from the wordlist we used.

if we were assessing a PHP web application that used the .php file extension. We could copy an existing wordlist and programmatically update it. However, DIRB allows us to specify extensions when we run a scan. run dirb without any other options to get the help text.
