# Client Server Architecture / request response model

client requests server responds

client: protocol + domain name + resource (https://www.google.com/maps) = url


# DNS:
Special server that is kind of like phonebook of the internet, domain name is just the name of actual ip address to make it humanly readable, basically it convers the domain name to actual ip address

# communiction protocol
It is the set of rules that allows two or more than two parties communicate over internet

# TCP / IP (transmission control protocol and internet protocol)

They are communication protocol that defines how the data is transferred across the internet. they set rules about how the data moves on the internet.

Basically the job of TCP is to break out the requests and response to thousand of chunk called packets before they are sent once they get to their destination they will reassemble all the packets so the data is transferred fast

and the job of IP is to send and route all of these packets over the internet, ensures all of the packets arrieves at the destination, using ip addresses on each packet,  

# HTTP (hyper text transfer protocol)
is communication protocol that allows clients and server to communicated by sending requests and receiving response messages from client to server and vice versa

### HTTP requests
- Start line: HTTP method + request target + HTTP version (GET /maps HTTP/1.1)
- HTTP request headers  : HOST: google.com
                          User-Agent: Mozilla/5.0
                          Accept-Language: en-US
- request body: only when sending data to the server <BODY>

### HTTP response
it quite looks the same as http requets with status code like 200, 404, 500

# HTTPS 
is encrypted with TLS or SSL. more secure that HTTP




So, client is browser it requests with url to DNS,  it match the web address to servers real ip address,and returns real url which looks like this (https://272.27.27.206:400) protocol + ip address + port number to the client (browser)

Once we have the real web address a TCP/IP socket connection is established between browswer and server and the connection is kept alive for the entire time it takes to transfer all the files of website (assets, js , html , css ) process is repeated for each file.

