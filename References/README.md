# References

Seclists Repo - https://gitlab.com/kalilinux/packages/seclists

NMAP Cheat sheet - https://hackertarget.com/nmap-cheatsheet-a-quick-reference-guide/

NMAP 7 NSE Scritps for recon - https://hackertarget.com/7-nmap-nse-scripts-recon/

NIST - https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-115.pdf

Tech Stack - https://www.mongodb.com/resources/basics/technology-stack

A critical vulnerability, CVE-2025-29927, has been discovered in Next.js, one of the most widely adopted web frameworks. The flaw allows attackers to bypass authentication and other security mechanisms enforced via middleware by manipulating the x-middleware-subrequest header. It is recommended to upgrade to the patched versions as soon as possible.
Technical Details

The vulnerability stems from how Next.js middleware handles the x-middleware-subrequest header. By crafting this header to include specific values—such as middleware, src/middleware, or recursive combinations thereof—attackers can deceive the application into skipping middleware logic entirely. This effectively nullifies authentication, authorization, and redirect protections when applied at the middleware layer. In recent versions, bypassing the middleware requires stacking the same value five times to exceed a recursion depth threshold (MAX_RECURSION_DEPTH = 5), e.g., x-middleware-subrequest: middleware:middleware:....

Moreover, publicly available detection checks fail to reliably identify this flaw, especially in configurations using HTTP redirects (not rewrites). Researchers demonstrated that adding the x-nextjs-data: 1 header forces the server to leak additional internal headers (x-nextjs-redirect, x-nextjs-rewrite), enabling more precise detection and exploitation.
Affected Products

The following products are vulnerable to CVE-2025-29927:

    Next.js 15.x: Versions prior to 15.2.3
    Next.js 14.x: Versions prior to 14.2.25
    Next.js 13.x: Versions prior to 13.5.9
    Next.js 11.1.4 through 13.5.6

Remediation and mitigation

    It is recommended to upgrade to the patched versions of Next.js 15.2.3, 14.2.25, or 13.5.9.
    If you cannot patch immediately, block external requests containing the x-middleware-subrequest header at the edge (e.g., CDN, WAF, or reverse proxy) as a mitigation.

Assess the risk in your environment Prevention

    Use the Vulnerability Findings page to find all instances of CVE-2025-29927 in your environment, or filter results to instances related to critical issues. Alternatively, you can use the Security Graph to identify publicly exposed vulnerable VMs/serverless or containers.
    Wiz Advanced customers can filter on findings identified or validated by the Dynamic Scanner, and Wiz Sensor customers can filter on runtime validated findings.
    Wiz Code customers can filter on findings with one-click remediation to generate a pull request with fixes for vulnerable instances detected in code repositories.
    Customers can also use Wiz-CLI to scan images for the vulnerabilities before they're deployed.

References

    Github advisory
    zhero-web-sec blog post
    SearchLight blogpost
