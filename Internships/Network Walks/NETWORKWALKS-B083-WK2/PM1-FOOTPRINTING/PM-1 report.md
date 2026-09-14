# FOOTPRINTING & RECONNAISSANCE ATTACKS WITH MULTIPLE KALI TOOLS (WK2-PM1)

**In this lab i learnded footprint the live website networkwalks.com using six built-in Kali Linux tools: whois, whatweb nslookup, curl, wafw00f and dnsrecon. Each tool reveals a different piece of the
target, and together they build a full profile of it.**

---
## 📌task1 -  whois

whois reveals the registrar, registration and expiry dates, and name servers. Here the name
servers point to HostGator, so an attacker instantly learns the hosting provider. Registration dates
and abuse contacts help with social engineering and planning.
### Command:
    ```
    whois networkwalks.com
   ```
### Screenshot:
    ![alt text](image.png)
### output:
```
    ┌──(root㉿kali)-[/home/anonymous]
└─# whois networkwalks.com
   Domain Name: NETWORKWALKS.COM
   Registry Domain ID: 2452319255_DOMAIN_COM-VRSN
   Registrar WHOIS Server: whois.godaddy.com
   Registrar URL: http://www.godaddy.com
   Updated Date: 2025-11-12T10:08:43Z
   Creation Date: 2019-11-06T22:51:46Z
   Registry Expiry Date: 2027-11-06T22:51:46Z
   Registrar: GoDaddy.com, LLC
   Registrar IANA ID: 146
   Registrar Abuse Contact Email: abuse@godaddy.com
   Registrar Abuse Contact Phone: 480-624-2505
   Domain Status: clientDeleteProhibited https://icann.org/epp#clientDeleteProhibited
   Domain Status: clientRenewProhibited https://icann.org/epp#clientRenewProhibited
   Domain Status: clientTransferProhibited https://icann.org/epp#clientTransferProhibited
   Domain Status: clientUpdateProhibited https://icann.org/epp#clientUpdateProhibited
   Name Server: NS6135.HOSTGATOR.COM
   Name Server: NS6136.HOSTGATOR.COM
   DNSSEC: unsigned
   URL of the ICANN Whois Inaccuracy Complaint Form: https://www.icann.org/wicf/
>>> Last update of whois database: 2026-09-14T11:40:37Z <<<

For more information on Whois status codes, please visit https://icann.org/epp

NOTICE: The expiration date displayed in this record is the date the
registrar's sponsorship of the domain name registration in the registry is
currently set to expire. This date does not necessarily reflect the expiration
date of the domain name registrant's agreement with the sponsoring
registrar.  Users may consult the sponsoring registrar's Whois database to
view the registrar's reported date of expiration for this registration.

TERMS OF USE: You are not authorized to access or query our Whois
database through the use of electronic processes that are high-volume and
automated except as reasonably necessary to register domain names or
modify existing registrations; the Data in VeriSign Global Registry
Services' ("VeriSign") Whois database is provided by VeriSign for
information purposes only, and to assist persons in obtaining information
about or related to a domain name registration record. VeriSign does not
guarantee its accuracy. By submitting a Whois query, you agree to abide
by the following terms of use: You agree that you may use this Data only
for lawful purposes and that under no circumstances will you use this Data
to: (1) allow, enable, or otherwise support the transmission of mass
unsolicited, commercial advertising or solicitations via e-mail, telephone,
or facsimile; or (2) enable high volume, automated, electronic processes
that apply to VeriSign (or its computer systems). The compilation,
repackaging, dissemination or other use of this Data is expressly
prohibited without the prior written consent of VeriSign. You agree not to
use electronic processes that are automated and high-volume to access or
query the Whois database except as reasonably necessary to register
domain names or modify existing registrations. VeriSign reserves the right
to restrict your access to the Whois database in its sole discretion to ensure
operational stability.  VeriSign may restrict or terminate your access to the
Whois database for failure to abide by these terms of use. VeriSign
reserves the right to modify these terms at any time.

The Registry database contains ONLY .COM, .NET, .EDU domains and
Registrars.
This WHOIS server is being retired. Please use our RDAP service instead. Rate limit exceeded. Try again after: 2562047h47m16.854775807s.

   ```
---
## 📌task2 -  whatweb
whatweb exposes the exact software and versions (here Wordpress 7.0.4 and WP Download
Manager 3.3.58). An attacker looks these versions up in vulnerability databases to find known
exploits. It also leaks the server IP and an email address.
### command:
```
    whatweb networkwalks.com
   ```
### screenshot:
![alt text](image-1.png)
### output:
```
    ┌──(root㉿kali)-[/home/anonymous]
└─# whatweb networkwalks.com
http://networkwalks.com [301 Moved Permanently] Apache, Cookies[__wpdm_client], Country[UNITED STATES][US], HTTPServer[Apache], HttpOnly[__wpdm_client], IP[192.232.216.135], RedirectLocation[https://networkwalks.com/], UncommonHeaders[permissions-policy,x-redirect-by,upgrade,referrer-policy,x-endurance-cache-level,x-nginx-cache]
                                                                                                                                                                                                                  
┌──(root㉿kali)-[/home/anonymous]
└─# whatweb https://networkwalks.com/
https://networkwalks.com/ [200 OK] Apache, Bootstrap[7.1], Cookies[__wpdm_client], Country[UNITED STATES][US], Email[info@networkwalks.com], Frame, HTML5, HTTPServer[Apache], HttpOnly[__wpdm_client], IP[192.232.216.135], JQuery[3.7.1], MetaGenerator[WordPress 7.1,WordPress Download Manager 3.3.58], Open-Graph-Protocol[website], Script[4684NR-IPIB&amp;pidnVar2=50511&amp;prtVar2=7&amp;scvVar2=12,application/json,application/ld+json,module,speculationrules,text/javascript], Title[Networkwalks Academy], UncommonHeaders[permissions-policy,link,upgrade,referrer-policy,x-endurance-cache-level,x-nginx-cache], WordPress[7.1]
 
   ```
---