# W_A_R
Web Application Runbook

Web applications often represent the largest attack surface for an organization. Anyone with a browser and internet access can discover and interact with a public-facing web application. These users may range from valid users to malicious threat actors.

## SCOPE
Our first step in web application reconnaissance is determining the scope of our assessment. We can usually define scope as the collection of hostnames, URL, IP addresses, and application functionality that we will be testing.

Once we have our scope defined, we can begin gathering information about our target. We'll want to determine our target's digital footprint in terms of domain names, subdomains, and IP addresses.

RECON & PASSIVE INFO GATHERING
helpful to use OSINT.


### ENUMERATION


Discover Running Services
Discover HTTP Endpoints
Review Error Messages for Information Disclosure
Identify Outdated Components

use both approaches: use automated tools to crawl the site and manually explore the site in a browser.

we may encounter error messages. These messages can provide additional information about:
1. the application, 
2. its running state, 
3. and the underlying server. 


Banner Grabbing - The process of capturing banner information—such as application type and version— that is transmitted by a remote port when a connection is initiated.


Discovering the running services on the server. 

Use banner grabbing of the exposed portsto identify the 
services  
software versions 

Gathering this information allows us to determine the application's programming language(s), framework(s), database, and server components. This collection of technologies is also known as a tech stack. The different components of the tech stack can inform our enumeration and attacks.

example Tech Stack:
FRONTEND-
Browser (Desktop/Mobile)
Programming Language
Frameworks
BACKEND-
Database
Web Server
Operating System

modern tech stacks might include tools for containerization, performance monitoring, business intelligence, event processing, data lakes, cloud services, microservices, and analytics. 


For example, if we find a vulnerability that allows us to read files from the server, we'll need to know what operating system (OS) we're interacting with to properly construct file paths and determine what files we're interested in. We're unlikely to find /etc/password on a Windows host unless it's running the Windows Subsystem for Linux (WSL).


## BANNER GRABBING:
We can manually identify services and software versions of exposed ports with banner grabbing. There are several command line tools we can use to do this. We'll focus on using curl and Netcat. Both tools support a variety of network protocols, including those we're most likely to encounter with web applications, such as HTTP and HTTPS.
https://curl.se/
https://salsa.debian.org/debian/netcat

When using curl, we can use the -i or --include options to include response headers in the output. If we only want the headers, we can use -I or --head.

curl -I http://enum-sanbox

However, developers can modify or disable this header, so we can't always trust this value when we discover it without additional verification.




We can use netcat in a similar way when dealing with non-HTTP protocols, such as SSH. We can use the -v option to enable verbose output. When used this way, netcat opens a connection to the destination, so we'll need to actually complete the request or close it using CTRL+C.
netcat -v enum-sandbox 22


## Manual HTTP Endpoint Discovery
We're most interested in forms or other ways we can submit information so that the application processes our data. Most web application vulnerabilities occur from mishandling or misinterpreting the data sent

Some web applications include files that can assist our discovery efforts. Web developers use robots.txt to instruct web crawlers on what portions of the website they can crawl. XML sitemaps are an alternative to robots.txt and provide additional information about the site, such as the last time a page was modified.

We can think of these files as "Keep Out" signs for web crawlers. As attackers, we should investigate any URLs included in these files to identify potentially sensitive functionality.
https://developers.google.com/search/docs/crawling-indexing/sitemaps/build-sitemap#xml
https://developer.mozilla.org/en-US/docs/Glossary/Robots.txt



Automated HTTP Endpoint Discovery
While manually browsing a website allows us to gain an understanding of the site's purpose and functionality, it can take a lot of time to fully explore a large site. We can use automated tools to provide broad coverage and discovery, while leveraging manual exploration to focus on depth.

Automated discovery tools tend to either crawl sites or use wordlists to brute force (or "bust") the discovery of directories and files. There isn't a "right" tool to use in every situation. Context plays an important role.

Crawlers tend to mimic the behavior of regular users. Crawlers start by accessing one page and then following any links from that page, traversing this way until they have accessed all linked pages. Mimicking users in this way is a relatively stealthy approach.

In comparison, brute forcing tools tend to be "noisier" from a network perspective since they send multiple requests, many of which may be for invalid resources. However, they may discover pages or resources that aren't directly linked from the main site.
https://github.com/hakluke/hakrawler


Next, we'll use DIRB, which uses a wordlist to discover files. Most Kali Linux images typically include DIRB. If our particular Kali VM doesn't include it, we can install it with apt.


One of the first things we might notice is that DIRB took much longer to complete than Hakrawler. We also received different results. DIRB used the default wordlist at /usr/share/dirb/wordlists/common.txt and sent 4612 requests to the server. DIRB missed several of the URLs discovered by Hakrawler. However, it found http://enum-sandbox/server-status, which Hakrawler did not. Since DIRB (and other brute forcing tools) use wordlists, they might discover pages and resources that are present on the target server, but not linked directly from the main site, such as status pages or administration consoles.

When using a brute forcing tool, selecting the right wordlist can directly impact our results. DIRB's default wordlist is often useful, but we may want to use different wordlists if we don't get many results. Kali Linux includes several wordlists at /usr/share/wordlists.


## Information Disclosure


As we enumerate a web application, we might encounter error messages as a result of submitting various data. Depending on what information the application returns in error messages, we might be able to learn or infer useful information.

For example, we might be able to learn username or password requirements. This information can be crucial when attempting to brute force passwords as it allows us to tailor our attacks to only passwords that match the site's requirements. In some cases, an application might disclose if a username is valid as part of the login or password recovery process.

Error messages can also leak information about the application's tech stack if they contain unique identifiers. For example, Oracle database software typically include ORA in error codes.

In some cases, we might need to fuzz the application to generate error messages. Fuzzing typically uses automated tools to generate a large volume of semi-random data and send it to the target application or API. When fuzzing, our goal is to observe how the application responds to the unexpected input. We are trying to identify edge cases where the application leaks information or behaves in a way that its developers didn't intend in order to subvert the application's normal logic.

There are several fuzzing tools included in Kali Linux by default, such as Wfuzz and ffuf. These two tools are similar. We specify a URL, HTTP Method type, request body (if we're sending a POST, PUT, or PATCH), and a wordlist. We can specify a placeholder (typically FUZZ) where we want the tool to inject the contents of the wordlist. They each include additional features, such as the ability to filter output.



#Components with Vulnerabilities
As we explore web applications, we will likely encounter JavaScript frameworks, such as React, Angular, and jQuery. Many developers use these frameworks to simplify development.

However, like any other code, these frameworks can contain vulnerabilities. These vulnerabilities tend to be useful for client-side attacks, such as cross-site scripting (XSS).

We can manually check the versions of the JavaScript files and frameworks we encounter. However, this can be time consuming. We can leverage automated tools, such as Retire.js, to do this more effectively.

We can use Retire.js as a command line tool, as part of the build process, as a browser plugin, or as a Burp Suite extension (which requires Burp Suite Professional).

The command line version requires NodeJS and npm. Alternatively, these dependencies could be installed within a container. Both of these approaches go beyond the scope of this Module.



# Wordlists

While Kali Linux includes several wordlists at /usr/share/wordlists, we may want to expand our collection to cover different web applications, frameworks, and vulnerabilities.

SecLists contains multiple wordlists that cover discovery, fuzzing, common passwords, and web shells. We can install SecLists by cloning the repo to a directory of our choice or using Kali's package manager.


The installation via our package manager may take a few minutes as the collection is over a gigabyte in size. Once the installation is complete, we can find the different wordlists in /usr/share/seclists, organized by type of list.


Each directory contains sub-directories and files. We won't explore everything, but it's worth spending some time reviewing the contents to become familiar with them.

Payloads All The Things is another useful collection of wordlists focused on exploitation. As with SecLists, we can clone the repo from GitHub or install it with Kali's package manager.

## Custom Wordlists
Creating Custom Wordlists
In addition to the common wordlists we've reviewed in this Module, we may find it useful to create a custom wordlist based on the application we are assessing.

CeWL is a custom wordlist generator that is included in Kali Linux. It crawls a URL and creates a list of words from the pages it discovers. CeWL has many optional settings to control how it crawls, what words it tracks, and how it outputs the results.

Let's try using it against our sandbox application. We'll run cewl, --write the results to output.txt, force output to --lowercase, and set -m 4 to set the minimum word length to four characters, and then provide our target URL.

After CeWL finishes, we'll use tail to check some of the results in output.txt.

While this is just an example, let's suppose we generated a list of unique words specific to the site we were assessing. We could use those results in brute force attacks that would be more focused than a generic wordlist.

In addition to creating wordlists from web applications, there are other situations in which we may want to create wordlists. For example, if we know our target's operating system, we could build a wordlist of binaries that we might want to leverage in a command injection attack.

For example, we could use ls to get the contents of /usr/bin, pipe the results to grep, use -v / to exclude directories, and redirect the results to a file.

There is no limit to the wordlists we can create with creative use of Linux command line tools, like sed, cut, and grep.

We can also use LLMs to generate wordlists. Refer to the Using LLMS to Help Create Custom Wordlists Learning Module for more details.

https://portal.offsec.com/library/learning-modules/using-llms-to-help-create-custom-wordlists-177893/
