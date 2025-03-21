# W_A_R
Web Application Runbook

Web applications often represent the largest attack surface for an organization. Anyone with a browser and internet access can discover and interact with a public-facing web application. These users may range from valid users to malicious threat actors.

SCOPE
Our first step in web application reconnaissance is determining the scope of our assessment. We can usually define scope as the collection of hostnames, URL, IP addresses, and application functionality that we will be testing.

Once we have our scope defined, we can begin gathering information about our target. We'll want to determine our target's digital footprint in terms of domain names, subdomains, and IP addresses.

RECON & PASSIVE INFO GATHERING
helpful to use OSINT.


ENUMERATION


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


BANNER GRABBING:
We can manually identify services and software versions of exposed ports with banner grabbing. There are several command line tools we can use to do this. We'll focus on using curl and Netcat. Both tools support a variety of network protocols, including those we're most likely to encounter with web applications, such as HTTP and HTTPS.

When using curl, we can use the -i or --include options to include response headers in the output. If we only want the headers, we can use -I or --head.

curl -I http://enum-sanbox

However, developers can modify or disable this header, so we can't always trust this value when we discover it without additional verification.




We can use netcat in a similar way when dealing with non-HTTP protocols, such as SSH. We can use the -v option to enable verbose output. When used this way, netcat opens a connection to the destination, so we'll need to actually complete the request or close it using CTRL+C.

netcat -v enum-sandbox 22