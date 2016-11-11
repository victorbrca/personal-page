+++
tags = [
]
categories = [
]
showthedate = false
date = "2016-09-02T00:01:59-05:00"
title = "How to Create a Quick Web Server"

+++

Have you ever had the need to create a web server to perform a test? Well, here are a few quick options on how to do this.

# **Got Netcat?**

If you have Netcat on the server (which is pretty easy to get), then you can do this.

**Example 1:** Display the date and the text "It works"

```
nc -kl 10001 -c 'echo -e "HTTPS/1.1 200 OK\r\n\r\n$(date)\r\n\r\nIt works"'
```

**Example 2:** Display an index.html file

```
nc -kl 10001 -c 'echo -e "HTTPS/1.1 200 OK\r\n\r\n$(cat index.html)"'
```

**Example 3:** Using HTTPS
a. First get a set of self-signed certificate and key (either generate or download here - <a href="http://www.selfsignedcertificate.com/" target="_blank">http://www.selfsignedcertificate.com/</a>)
b. Add the certificate to the server and run netcate with the following parameters

```
nc -l -p 10001 -k --ssl --ssl-cert ca.crt --ssl-key ca.key -c 'echo -e \
"HTTP/1.1 200 OK\r\n\r\n$(date)\r\n\r\nIt works"'
```

# Python

This is the easiest one, as long as you have Python on that system. Just run the commands below and you are set. If you have an index file on that folder, Python will display, otherwise it will do a directory listing.


```
$ python -m SimpleHTTPServer 8888
Serving HTTP on 0.0.0.0 port 8888 ...
```