# Web Attacks

### Authenticating Users

#### Cookies
Cookies let server store a string on the client.
- HTTP Response: Set-Cookie: Adds a cookie
- HTTP Header: Cookie: gives a cookie

This can be used to:
- Identify the user
- Store user name/preferences/etc
- Track user

##### Fixed Cookies
Log in/out recorded on the server side
- Set cookie the first time browser connects
- Every page looks up cookie in database to get session state

### What can go wrong?
<span style="color:#ff0000">Everything</span>

If the connection is not encrypted, it is possible to eavesdrop, by:  
- ISP
- anyone on the route  
- anyone on your local network, e.g. using the same wi-fi

#### Countermeasures
- Use https all the time - it used to be spenny but its free now
- Set the secure flag - cookie only sent over secure connections

