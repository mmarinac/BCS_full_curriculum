# HTTP HEADERS

HTTP is a request/response model protocol that we use to comunicate between client and servers.

HTTP headers are the core part of these HTTP requests and responses, and they carry information about the 
client browser, the server and more.

Headers can be grouped according to their contexts:

- General headers - apply to both requests and responses, but with no relation to the data transmitted in the body.
- Request headers - contain more information about the resource to be fetched, or about the client requesting the resource.
- Response headers - hold additional information about the response, like its location or about the server providing it.
- Entity headers - contain information about the body of the resource, like its content length or MIME type.

When you type a url in your address bar, your browser sends an HTTP request and it may look like this:

        GET /tutorials/other/top-20-mysql-best-practices/ HTTP/1.1
        Host: net.tutsplus.com
        User-Agent: Mozilla/5.0 (Windows; U; Windows NT 6.1; en-US; rv:1.9.1.5) Gecko/20091102 Firefox/3.5.5 (.NET CLR 3.5.30729)
        Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
        Accept-Language: en-us,en;q=0.5
        Accept-Encoding: gzip,deflate
        Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.7
        Keep-Alive: 300
        Connection: keep-alive
        Cookie: PHPSESSID=r2t5uvjq435r4q7ib3vtdjq120
        Pragma: no-cache
        Cache-Control: no-cache

First line is the "Request Line" which contains some basic info on the request.

It consists of 3 parts:

1. The method (GET,POST,PUT,DELETE).
2. The path, is generally the part of the url that comes after the host (domain).
3. The protocol, contains "HTTP" and the version, which is usually 1.1 in modern browsers.

The rest are the HTTP headers.

After that request, your browser receives an HTTP response that may look like this:

    HTTP/1.x 200 OK
    Transfer-Encoding: chunked
    Date: Sat, 28 Nov 2009 04:36:25 GMT
    Server: LiteSpeed
    Connection: close
    X-Powered-By: W3 Total Cache/0.8
    Pragma: public
    Expires: Sat, 28 Nov 2009 05:36:25 GMT
    Etag: "pub1259380237;gz"
    Cache-Control: max-age=3600, public
    Content-Type: text/html; charset=UTF-8
    Last-Modified: Sat, 28 Nov 2009 03:50:37 GMT
    X-Pingback: https://net.tutsplus.com/xmlrpc.php
    Content-Encoding: gzip
    Vary: Accept-Encoding, Cookie, User-Agent

The first line is the "Status Line", followed by HTTP headers.

In the Status Line we have the protocol, this is again usually HTTP/1.x or HTTP/1.1 on modern servers,
and the next part is the status code followed by a short message (see status codes in express block2).

During this course we are going to use just the Authorization request header, to send the authentication token
to the server, but if you would like more details about HTTP headers please visit this link :

[MDN - HTTP Headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)

We can use this Chrome extension to check the headers of a request/response : 

[Chrome HTTP Headers Extension](https://Chrome.google.com/webstore/detail/live-http-headers/eaiimeeggnhceafhencnejheejddlcpa?hl=en)