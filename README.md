# Bug-Bounty-Notes
My go to reference for everything related to bug bounty stuff

# Tools

## Recon

### [Amass](https://github.com/OWASP/Amass)

Performs network mapping of attack surfaces and external asset discovery using open source information gathering and active reconnaissance techniques.

*example usage:* 
`amass enum -brute -active -d domain.com -o amass-output.txt`

### [Http Probe](https://github.com/tomnomnom/httprobe)
This can be combined with Amass to probe additional ports.Take a list of domains and probe for working http and https servers.

*example usage:* 
`cat amass-output.txt | httprobe -p
http:81 -p http:3000 -p https:3000 -p http:3001 -p https:3001 -p http:8000 -p
http:8080 -p https:8443 -c 50 | tee online-domains.txt`


### [Anew](https://github.com/tomnomnom/anew)
To find the difference between lists of new domains

*example usage:*
`cat new-output.txt | anew old-output.txt |
httprobe`

### [DNS Gen](https://github.com/ProjectAnte/dnsgen)
This tool generates a combination of domain names from the provided input. Combinations are created based on wordlist. Custom words are extracted per execution

*example usage:* 
`cat amass-output.txt | dnsgen - | httprobe`

### [Aquatone](https://github.com/michenriksen/aquatone)
Aquatone is a tool for visual inspection of websites across a large amount of hosts and is convenient for quickly gaining an overview of HTTP-based attack surface.

*example usage:*
`cat targets.txt | aquatone`

### [Wayback Machine Scanner](https://gist.github.com/mhmdiaa)
This will scrape /robots.txt for all domains I provide
and scrape as many years as possible

*example usage:*
`waybackpy --url akamhy.github.io --user_agent "my-user-agent" --known_urls`

### [ParamScanner](https://github.com/maK-/parameth)
A custom tool to scrape each endpoint discovered and search for
input names, ids and javascript parameters. This is a combination of [InputScanner](https://t.co/6isBiwTJVb) [LinkFinder](https://t.co/U3NjN8kstS) and [Parameth](https://t.co/1CVxXZrORj)

*example usage:*
`python parameth.py -u “http://example.com/`

# Attacks

## XSS
Cross-Site Scripting (XSS) attacks are a type of injection, in which malicious scripts are injected into otherwise benign and trusted websites. XSS attacks occur when an attacker uses a web application to send malicious code, generally in the form of a browser side script, to a different end user.


**Web Application Firewalls:** A web application firewall is a security policy enforcement point positioned between a web application and the client endpoint. This functionality can be implemented in software or hardware, running in an appliance device, or in a typical server running a common operating system. It may be a stand-alone device or integrated into other network components.

Here is a good [reference](https://github.com/0xInfection/Awesome-WAF) that describes WAF, and how to detect it, and how to systematically attack it. 

Proces for testing XSS and Filtering

- [ ] Test for Encoding or Weird Behavior 
    - payloads can be found [here](https://d3adend.org/xss/ghettoBypass) or [here](https://raw.githubusercontent.com/payloadbox/xss-payload-list/master/Intruder/xss-payload-list.txt)

- [ ] Reverse Engineer Developers Thoughts
    - What filter was created and why
    - Is it a black list or white list of tags allowed
    - Does it encode things? how does it encode them

- [ ] Test XSS Flow
    - How are non malicious tags handled or incomplete tags
    - what tags can you chain together 

- [ ] File Upload for Stored XSS
    - Are there any filters for file names
    - Are their filters for file types

## IDOR
Insecure Direct Object References (IDOR) occur when an application provides direct access to objects based on user-supplied input. As a result of this vulnerability attackers can bypass authorization and access resources in the system directly, for example database records or files.

In a nutshell, IDOR is about changing integer values (numbers) to another and seeing what happens.

**EXAMPLE**

```
{"example":"example","id":"1"}
{"example":"example","id":"2"}
```

## Follow up (process so far)
[reference](https://media.defcon.org/DEF%20CON%2029/DEF%20CON%2029%20workshops/DEF%20CON%2029%20Workshop%20Philippe%20Delteil%20Bug%20Bounty%20Workshop.pdf)
[attacking drupal] (https://book.hacktricks.xyz/network-services-pentesting/pentesting-web/drupal)


recon with subfinder/amass

look into nuclei templates

dalfox for xss

axiom for distributed scans



# References 
[Zseanos Methodology](https://www.bugbountyhunter.com/methodology/zseanos-methodology.pdf)
[Nahamsec Recon](https://www.youtube.com/watch?v=YT5Zl2jW3wg)
[Jason Haddix Recon](https://www.youtube.com/watch?v=p4JgIu1mceI)
