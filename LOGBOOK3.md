
# Trabalho realizado na Semana #3

## Identificação

- Targeted application: vSphere Client
- Type of vulnerability: RCE vulnerability due to lack of input validation in the Virtual SAN Health Check plug-in which is enabled by default in vCenter Server. 
- A malicious actor may exploit this issue to execute commands with unrestricted privileges on the operating system after gaining acess via an exploit.
- 52 products affected, vulnerability widely spread globally as many organizations make use of this application, this can be confirmed with the map available on https://arstechnica.com/gadgets/2021/05/vulnerability-in-vmware-product-has-severity-rating-of-9-8-out-of-10/.

## Catalogação

- Report date: Tuesday, May 25, 2021, VMware published security advisory VMSA-2021-0010.
- Reporter: VMware credited Ricter Z of 360 Noah Lab for reporting this issue.
- First exploitation date: June 5, 2021: Exploitation is now occurring in the wild
- The vulnerabilty has a CVSS Score of 10.0

## Exploit

- "Successful exploitation requires network access to port 443 and allows attackers to execute commands with unrestricted privileges on the host operating system" - RCE.
- Although there is no known automation for this exploit, the link https://github.com/alt3kx/CVE-2021-21985_PoC contains clear instructions for an exploit possibility (Proof of Concept).
- This PoC does not guarantee RCE on its own, though, as the non-verified input is still limited by some things. However, there are workarounds, via manipulation of arguments and methods, guaranteeing RCE capabilities.
- In a more technical way, the exploit was summed up on Jang's writeup on https://testbnull.medium.com/a-quick-look-at-cve-2021-21985-vcenter-pre-auth-rce-9ecd459150a5:
"-Unauthenticated /rest endpoint
-MethodInvoker bean allows to invoke arbitrary static methods
-TypeConverter automatically converts data to the appropriate format
-JNI_OnLoad trigger code execution"

## Ataques

- The damage potential of this vulnerabilty is very high, which is reflected is its CVSS score.
- Researcher Kevin Beaumont: “vCenter is a virtualization management software” ; “If you hack it, you control the virtualization layer (e.g., VMware ESXi)—which allows access before the OS layer (and security controls)."
- Even though concrete attacks on large companies are not being reported widely in the news, they are occuring on samller companies that don´t patch their systems regularly - exploitation occuring in the wild.
- The process of discovery and exploitation of the vulnerability has also been discussed widely on Twitter, even by users certified on cybersecurity: https://twitter.com/GossiTheDog/status/1400868390726733831.

## Sources

-https://arstechnica.com/gadgets/2021/05/vulnerability-in-vmware-product-has-severity-rating-of-9-8-out-of-10/
-https://cybersophia.net/vulnerability/vmware-patches-vulnerabilities-cve-2021-21985-cve-2021-21986/
-https://www.rapid7.com/blog/post/2021/05/26/cve-2021-21985-vcenter-server-what-you-need-to-know/
-https://twitter.com/GossiTheDog/status/1400868390726733831
-https://testbnull.medium.com/a-quick-look-at-cve-2021-21985-vcenter-pre-auth-rce-9ecd459150a5
-https://attackerkb.com/topics/X85GKjaVER/cve-2021-21985/rapid7-analysis?referrer=blog
-https://cwe.mitre.org/data/definitions/20.html
-https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-21985
-https://nvd.nist.gov/vuln/detail/CVE-2021-21985#vulnCurrentDescriptionTitle
-https://www.cvedetails.com/cve/CVE-2021-21985/
-https://blogs.vmware.com/vsphere/2021/05/vmsa-2021-0010.html
