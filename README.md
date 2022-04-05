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

## XSS

**Web Application Firewalls:** A web application firewall is a security policy enforcement point positioned between a web application and the client endpoint. This functionality can be implemented in software or hardware, running in an appliance device, or in a typical server running a common operating system. It may be a stand-alone device or integrated into other network components.

Here is a good [reference](https://github.com/0xInfection/Awesome-WAF) that describes WAF, and how to detect it, and how to systematically attack it. 

Proces for testing XSS and Filtering

- [ ] Step one: Test for Encoding or Weird Behavior 
    - payloads can be found [here](https://d3adend.org/xss/ghettoBypass) or [here](https://raw.githubusercontent.com/payloadbox/xss-payload-list/master/Intruder/xss-payload-list.txt)

- [ ] Reverse Engineer Developers Thoughts
    - What filter was created and why
    - Is it a black list or white list of tags allowed
    - Does it encode things? how does it encode them
    - Are the  




