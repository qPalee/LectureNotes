# Week 7

### Attacks against websites
Two main sources of vulnerabilities
- Input Validation
- Application Logic

#### Authenticating users after login
- IP address-based
	- NAT may cause several users to share the same IP
	- DHCP can cause the same user to have different IPs

- Certificate-based
	- Who has a certificate and what is it, and who will sign it?

- Cookie-based
	- The most common

#### Cookies
Cookies let server store a string on the client based on the server name

HTTP Response <span style="color:#00bfff">Set-Cookie</span>: Adds a cookie
HTTP header <span style="color:#00bfff">Cookie</span>: gives a 'cookie'

This can be used to:
- Identify the user
- Store user name, preferences etc
- Track the user: time of last visit etc

##### Stealing Cookies
If the attacker can steal a cookie, they don't need the username and password to login

If the website uses HTTPS (TLS) it is secure however many websites used to drop back to HTTP after a secure login

###### Countermeasures
Use HTTPS all the time
Set the secure flag so cookie os only sent over a secure connection
```java
Cookie secureCookie = new Cookie("credential", c);
secureCookie.setSecure(true);
```

### SQL Injection

#### Example
User searches for `' OR '1'='1' ) -- `

This will make the SQL Query
```SQL
SELECT * FROM items where (item='' OR '1'='1') -- ')
```
and since 1 is equal to 1, it will return the details of all items

#### Stopping SQL Attacks
You can prevent SQL attacks by sanitising the users input
You can do this in php using `mysqli_real_escape_string()`

Most languages these days have <span style="color:#00bfff">prepared statements</span> (even php)

```PHP
$stmt = $conn->prepare
	("INSERT INTO people (firstname, lastname) VALUES (?, ?)");

$stmt->bind_param("ss", $firstname, $lastname);

$firstname = "John";
$lastname = "Doe";
$stmt->execute();
```

Not just websites can have SQL injections:
![[Pasted image 20240510125425.png]]

