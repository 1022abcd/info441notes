# Sections

- [HTTP](#http)

# HTTP

- It is an acronym of the **H**yper **T**ext **T**ransfer **P**rotocal(HTTP).

[httpRequest]:
 ./img/httpRequest.png

### HTTPS : HTTP + Transport Layer Security(TLS)
- When using TLS, all requests and responses are encrypted as they are sent across the network so that an attacker in the middle can't read the contents. 

### Host
- The host is the name of the computer we want to talk to.
- The host and associated IP address can get you connected to a server across the Internet, server might be listening for network requests on many different ports.
- The host can be a domain name such as **example.com**, or it can be a sub-domain like **api.example.com**
- To make a network connection, the client needs to translate the host name into a numeric IP address. It does this useign the **Domain Name System(DNS)**.
    - It can be used to resolve a host name to an IP address.
    - **nslookup** terminal canbe used to resolve addresses.

### Port
- You can think of an IP address like the street address of an apartment building, while the **port number** is the number of a specific apartment inside.
-**To connect to a web server, we need both the host/IP and a port number.**

### Origin
- Origins are the primary security boundary within the browser.

### Resource Path 
- After the host and optional port number, the segment up until the **?** is known as the **resource path**.
    - Technically, this can take any form that the server knows how to interpret, so it doesn't strictly need to look like a file path, but that path syntax is useful for modeling any set of hierarchically-organized resources.

### Query String, Parameters, and Values
- The last part of URL above contains the query string, which allows the client to pass additional paramters and values that are relevant for the requested resource.
-The query string starts with a **?** and is followed by one or more name/value pairs. 

### HTTP Requests
``` HTTP
    GET /some/path HTTP/1.1
    Host: api.example.com
    Origin: example.com
    ...more headers...

```
- The first line is composed of method, path, and protocal version. 
- The second and after lines are headers. 

``` Text 
    GET     : return the current state of resource
    PUT     : completely replace the current state of the resource
    PATCH   : partially update the current state of the resource
    POST    : add a new child resource
    DELETE  : delete teh resource
    LINK    : link the resource to some other resource
    UNLINK  : unlink the resource from some other resource
    OPTIONS : list the methods the current user is allowed to use on this resource
```

### Headers
- A header is a name/value pair, like a parameter, that provides some additional meta-data about the request.
-The **Host** header is required on all requests and must be set to the host name the client thinks it is talking to.
    -This allows a single server to host several different web sites at the same time: it can use the Host header to determine which site the client is requesting.
    ``` Text
    Authorization     : Some sort of token that identifies an authenticated session or a user account. The server defines what it accepts in this header.

    Content-Length    : If you are sending content to the server, this specifies how many bytes you are sending. This is typically set for you automatically by the library you use to make the request. This tells the server how much data to expect so it knows when its done reading the request off the network.

    Content-Type      : If you are sending content, this specifies the MIME type you are using for that data (e.g., JSON, XML, HTML, or some sort of media type).

    Cookie            : A value the server provided in the Set-Cookie response header during a previous request. Cookies are handled automatically within the browser and by most HTTP client libraries that offer a "cookie jar" implementation.

    If-Modified-since : If set to a date/time, the server will respond with the resource's state only if that state has been modified since the specified date/time. Useful when requesting large resources that don't change very often (video, large images, etc).

    ```