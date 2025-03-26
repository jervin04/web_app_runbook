# References

Seclists Repo - https://gitlab.com/kalilinux/packages/seclists

NMAP Cheat sheet - https://hackertarget.com/nmap-cheatsheet-a-quick-reference-guide/

NMAP 7 NSE Scritps for recon - https://hackertarget.com/7-nmap-nse-scripts-recon/

NIST - https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-115.pdf

Tech Stack - https://www.mongodb.com/resources/basics/technology-stack



iz Research has uncovered a set of vulnerabilities—dubbed IngressNightmare—affecting the admission controller component of the Ingress NGINX Controller for Kubernetes (CVE-2025-1097, CVE-2025-1098, CVE-2025-24514, CVE-2025-24513 and CVE-2025-1974). When chained together, exploitation of these vulnerabilities can lead to full takeover of the Kubernetes cluster, including unauthorized access to all Kubernetes secrets across namespaces. We recommend following the guidance in this advisory to identify any vulnerable clusters in your environment, and updating to a patched version or implementing a workaround if any affected clusters are identified.

March 25, 2025 update: there has been a delay in adding the relevant built-in Controls for some customers - we are working to ensure their availability.

Wiz has added an exploitability check for IngressNightmare that is available to customers with Dynamic Scanner enabled. However, customers must enable exploitability validation in order for this detection to run (scan mode can be set to either "standard" or "comprehensive").
Technical Details

Ingress NGINX’s admission controller validates incoming ingress objects by generating temporary NGINX configurations and running nginx -t. However, it lacks authentication and sanitization, allowing attackers to inject malicious ingress objects that contain arbitrary NGINX configuration directives. The injected configuration can execute code during the validation phase, effectively leading to RCE. Attackers can exploit annotation fields such as auth-url, auth-tls-match-cn, and even the ingress UID to insert malicious payloads, leveraging directives like ssl_engine to load attacker-controlled shared libraries.

The vulnerability chain is further amplified by a secondary abuse vector: uploading a shared library to the pod using NGINX’s client body buffering mechanism. By exploiting this behavior, attackers can persist the file in memory and trigger execution through nginx -t once the admission controller processes a malicious request. This results in remote code execution with elevated privileges, compromising the entire Kubernetes cluster.

Wiz is not impacted by these vulnerabilities.
Affected Products

Ingress NGINX Controller for Kubernetes, specifically:

    Versions 1.12.0, prior to 1.12.1
    Versions 1.11.0, prior to 1.11.5 Older versions are also impacted, but are not maintained and so did not receive a fix. Ingress-NGINX installations where the admission controller is publicly accessible or not properly restricted are most at risk.

Remediation and mitigation

It is recommended to patch to the latest Ingress NGINX Controller versions (1.12.1 or 1.11.5) to mitigate the vulnerabilities. In addition, it is advised to ensure the admission controller webhook endpoint is not exposed to the internet and only accessible by the Kubernetes API Server.

If patching is not immediately possible, apply the following mitigations:

    Disable the admission controller if it’s unnecessary.
    Enforce strict network policies to limit access to the controller.

Assess the risk in your environment Prevention

    Use the Vulnerability Findings page to find all instances of these vulnerabilities in your environment, or filter results to instances related to critical issues.
    Wiz Advanced customers with Exploitability Validation enabled can filter for resources with the exploitable configuration using the following Host Configuration Rule.
    We recommend prioritizing the following scenarios for urgent remediation (each of these are detected by built-in Controls):
        Application endpoint exposing container with Ingress NGINX controller vulnerable to RCE (note that this detection requires customers to enable exploitability validation for the Dynamic Scanner.
        Kubernetes cluster with Ingress NGINX Controller vulnerable to RCE without network policy on ingress pod
        Kubernetes cluster with Ingress NGINX Controller vulnerable to RCE and an exposed pod vulnerable to SSRF or RCE

Detection

    Sensor customers can use the Events Explorer page to check for any evidence of exploitation of IngressNightmare in their Kubernetes clusters.
    Additionally, Sensor customers can check for potentially related post-exploitation activity expected in this scenario.

References

    Wiz Research blogpost
    Kubernetes advisory
    Kubernetes blogpost
    GCP advisory
    AWS advisory
    MSRC advisory
