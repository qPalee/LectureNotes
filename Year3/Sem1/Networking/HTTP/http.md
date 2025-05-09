# HTTP
Ian's wife isn't very happy with him

### FTP
Shit
Very old, before tcp and ip
Used to move a level results around for some fucking reason
Extremely tied to the ARPANET

uucp is ass, also just doesn't work lmao

### Why HTTP?
- Hypertext Transport Protocol
- Originally designed to download HTML with support for hyperlinks
- Has a flexible concept of a URL which means that it can do many other tasks

Protocol is easy to implement
- Firewalls and NATs kinda just work
Decouples names from things

HTTP only used one TCP connection

Lines are terminated with \r\n
- Unix used \n, DOS convention is \r
- Microsoft just had to be different

### HTTPS
HTTP uses port 80
HTTPS uses port 443
HTTPS uses TLS to communicate

After setting up TLS, HTTP starts doing its thing
![[Pasted image 20241129091751.png]]

There are more operations other than GET
- mostly POST, PUT, DELETE, HEAD

The GET request only has a path, since back in the day IP was different

#### Response
![[Pasted image 20241129092643.png]]
First line gives the response code
- 200 is OK

- 1xx informational response – the request was received, continuing process
- 2xx successful – the request was successfully received, understood, and accepted
- 3xx redirection – further action needs to be taken in order to complete the request
- 4xx client error – the request contains bad syntax or cannot be fulfilled
- 5xx server error – the server failed to fulfil an apparently valid request

Ian: everyones laptop is sync'd up these days
- no

#### EoF
This is a fucking nightmare
HTTP uses a byte count to know when the file is joever

#### Cache Control
- Last modified and ETag is helpful for caching
- ETag is basically the hash of a file
- Tells you if content has changed from your cached data

#### Ranges
Accept-Ranges allows a client to ask for sections of the file

#### Keep Alive
USUALLY if there is a length header, then the connection usually wants to stay alive

#### Other things
HSTS: namespace can only use HTTPS, and all requests for HTTP should be fucked off and rewritten to the encrypted version

Strict-Transport-Security
- "you came here from http, fuck you don't do it again"
- Just ignores their ass if they try to use HTTP

### Flexibility
The requested name can be a file in a directory rooted somewhere in the file store
- It can easily be a key for a db, parameter for a program etc
- Server converts URNs into content however it wants

#### Convention
You can pass multiple parameters with
- `/some/path?var1=value1&var2=value2`

