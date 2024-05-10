# Web Attacks

### Cross Site Scripting (XSS)
Web browsers are dumb, they will execute anything sent to them
XSS is an input validation vulnerability
Would allow an attacker to inject client-side code into web pages
Only user issuing malicious request is affected

#### Stored XSS
The injected code is stored on the website and served to its visitors on all page views
- All users will be affected

##### Steal Cookie Example
- JavaScript can access cookies and make remote connections.  
- A XSS attack can be used to steal the cookie of anyone who looks at a page, and send the cookie to an attacker.  
- The attacker can then use this cookie to log in as the victim.

##### XSS Phishing attacks
- Attacked injects script that reproduces look-and-feel of login page
- Fake page asks for user credentials or other sensitive info
- Attacker can also redirect to a site

##### XSS - run exploits
The attacker injects a script that launches a number of exploits against the user’s browser or its plugins  
If the exploits are successful, malware is installed on the victim’s machine without any user intervention  
Often, the victims machine becomes part of a botnet

#### Sanitisation
Sanitisation is the solution for injection
Sanitising all user inputs is difficult
It is also context dependent
Sanitisation is attack-dependent

### Cross-site request forgery
- Victim is logged into vulnerable web site
- Victim visits malicious page on attacker web site
- Malicious content is delivered to victim
- Victim sends request to vulnerable web server
![[Pasted image 20240304152738.png]]

#### Solutions to CSRF
- Check value of Referer header - <span style="color:#ff0000">DOES NOT WORK</span>
	- Attacker cannot spoof the value of the Referer header in the users browser (but the user can).  
	- Legitimate requests may be stripped of their Referer header  
	- Proxies  
	- Web application firewalls

- Every time a form is served, add an additional parameter with a token and check that it is valid upon  submission  
- If the attacker can guess the token value, then no protection

- Every time a form is served, add an additional parameter with a token and check that it is valid upon  submission.  
- If the token is not regenerated each time a form is served, the  
- Application may be vulnerable to replay attacks (nonce).

### Path Traversal
The user can type anything they want into the URL bar, or even form the request by hand.  
http://nameOfHost

The user can type anything they want into the URL bar, or even form the request by hand.  
http://nameOfHost/../../../etc/shadow  
If the webserver is running with root permission this will give me the password file.

#### Prevention
- Use access control settings to stop Path Transversal  
- Best practice: make a specific user account for the webserver  
- Only give that account access to public files


