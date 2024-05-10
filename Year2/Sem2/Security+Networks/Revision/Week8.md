# Week 8

### Cross Site Scripting (XSS)
Web browsers are dumb, they will execute anything the server sends to them
We can use this fact to force a website to send you information 

XSS is an input validation vulnerability
It allows an attacker to inject client side code into web pages

#### Steal Cookie Example
JS can access cookie and make remote connections
An XSS attack can be used to steal the cookie of anyone who looks at a page then send the cookie to an attacker
The attacker can than use this cookie to log in as the victim

#### Phishing attacks
An attacker can inject a script which looks and feels like a login page
The fake page asks for users credentials or other sensitive information

Example:
```html
<script>
	document.location = "http://evil.com"
</script>
```

#### Running exploits
The attacker can inject a script which launches a number of exploits against the users browser or its plugins which can install malware on the victims machine

This often leads to the victims machine becoming part of a botnet

#### Solution for injection - sanitisation
Sanitising all user inputs is difficult 
It is context and attack dependent

### Path Traversal
The user can type anything they want into the URL bar

`http://nameOfHost/../../../etc/shadow`
If the webserver is running with root permission this will give the attacker the password file

#### How to fix
User access control settings can stop path traversal

Best practice is to make a specific user account for the webserver and only give that account access to public files

