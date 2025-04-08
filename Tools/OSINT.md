# OSINT

We can use a tool like whois in Kali 

https://www.kali.org/tools/whois/



ICANN's website to obtain basic contact information for a domain or IP address.
https://lookup.icann.org/en

We can refer to this information when we are attempting to determine valid usernames, such as when we test login functionality. While out of scope for this Module, this information can also be useful for crafting phishing campaigns.



Corporate sites often include information about high-level employees. We can also use social media (LinkedIn) and public search engines to find information about employees. 

Some companies have public repositories on GitHub, GitLab, or similar sites. These repositories can be a useful source of information beyond employee names. Having an idea of what programming languages and frameworks we might encounter can help us pick the right attack payloads.



we can identify subdomains using tools likes DNSDumpster 
https://dnsdumpster.com/

or through certificate transparency using tools like crt.sh. 
https://crt.sh/

Certificate transparency details can include information such as an organization using a public certificate authority to issue certificates for private subdomains, thereby leaking those private subdomain names.


https://www.shodan.io/ free version that gives limited results is consider OSINT. 

Passive Information Gathering

We can use a tool like whois in Kali or the lookup tool on ICANN's website to obtain basic contact information for a domain or IP address.

whois megacorpone.com

We can also use social media and public search engines to find information about employees. Some companies have public repositories on GitHub, GitLab, or similar sites. These repositories can be a useful source of information beyond employee names. Having an idea of what programming languages and frameworks we might encounter can help us pick the right attack payloads.

While not necessary in our lab environment, we can identify subdomains using tools likes DNSDumpster or through certificate transparency using tools like crt.sh. Certificate transparency details can include information such as an organization using a public certificate authority to issue certificates for private subdomains, thereby leaking those private subdomain names.

Finally, specialty search tools such as Shodan can provide additional insight. Shodan is a search engine that crawls devices connected to the internet, including the servers that run websites, but also devices like routers and Internet of Things (IoT) devices. Shodan is not required to complete any material in this Module, but we would be remiss if we didn't mention it.


Banner Grabbing
 The process of capturing banner information—such as application type and version— that is transmitted by a remote port when a connection is initiated.

 Gathering this information allows us to determine the application's 
 programming language(s), 
 framework(s), 
 database, and 
 server components.



 
