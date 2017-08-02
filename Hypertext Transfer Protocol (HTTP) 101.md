## Hypertext Transfer Protocol (HTTP)

Have you ever spotted the http:// or https:// prefix in the address bar of your browser and wondered, what exactly is it? HTTP stands for Hypertext Transfer Protocol and in a nutshell it is the core communications protocol used to access the world wide web. From its creation it has came a very long way, initially used for retrieving static text-based resources, it now boasts the ability to serve us complex distributed applications.

The system used is relatively simple, HTTP operates on a message-based model in which the client (you) typically sends a Request to the server, which in turn handles the request and provides the client back a Response. The protocol is connection-less and by that I mean, your browser initiates a HTTP request and after a request is made, the client disconnects from the server and waits for a response. The server processes the request and re-establishes the connection with the client to send a response back. Although HTTP uses the stateful TCP protocol as its transport mechanism, each exchange of request and response is an autonomous transaction and may use a different TCP connection.

---

## HTTP Requests
HTTP Requests & Responses contain a number of headers seperated on new lines, followed by a white line then an optional message body.  See below for an example HTTP Request:

![standardhttprequest.JPG]({{site.baseurl}}/img/standardhttprequest.JPG)

Lets begin with you, the client. As a client you send HTTP Requests. A Request typically first line consists of three main items.

- **The HTTP Method:** In the image above we are sending a HTTP GET whose function is to retrieve a resource from the web server. GET requests do not have a message body, so no further data follows the blank line after the message headers.

- **The HTTP Version:** This is only really HTTP 1.0 or HTTP 1.1 and most browsers by default are using HTTP 1.1, in version 1.1 the HOST request header is mandatory.

- **The Requested URL:** This is typically the name of the resource we are requesting and could have some query string paramaters involved too, query string begins with a question mark (?) and a simple example may look something like this; http://www.mywebsite.com/api/getSomething?paramater=100

As previously mentioned, there can be multiple headers associated with a request (& response), some of notable interest are:

- **Referer Header:** Ironically this header was spelt incorrectly from day one and just kept that way and this header is essentially the location of which the request originated.

- **User-Agent Header:** Nice and simple, this is used to provide information about the browser or other client software that generated the request.

- **Host Header:** As previously mentioned this is mandatory when running HTTP 1.1 and this header specifies the host name that appeared in the full URL being accessed.

---

## HTTP Responses

A simple HTTP Response may look like this, below is a call to the NASA Demo API:

![standardhttpresponse.JPG]({{site.baseurl}}/img/standardhttpresponse.JPG)

The first line in the HTTP Response contains 3 useful pieces of information once again, these are:

- **HTTP Version:** Once again, the HTTP version will be returned straight away in the response.

- **Status Code:** A numerical value, 200 is the most common status code; it means that the request was successful and that the requested resource is being returned.

- **Status Code Name:** An accompanying name to the status code, typically for something like a status code: 200 the name would just be "OK" however this can have any value and is not really used for anything meaningful.

Just like with HTTP Requests, HTTP Responses can contain a number of headers, some examples of the types of headers we might occasionally see are:

- **Server Header:** This header is not always perfectly accurate and you should take it with a pinch of salt, however it typically contains information on the server.

- **Set-Cookie Header:**  This issues the browser a further cookie; this is submitted back in the Cookie header of subsequent requests to this server.

- **Pragma Header:** This is used for caching purposely and typically tells the browser **not** to store the response in its cache. The Expires header indicates that the response content expired in the past and therefore should not be cached. These instructions are frequently issued when dynamic content is being returned to ensure that browsers obtain a fresh version of this content on subsequent occasions.

- **Content-Length Header:** The length of the message body in the response, in bytes.

- **Content-Type Header:** Format of the message body in the response, e.g application/json or HTML etc.


---


## HTTP METHODS (well, some of them)
HTTP has a number of different of methods available and each serves an individual purpose. When dealing with web applications for example the most common methods you will encounter are HTTP GET and HTTP POST but a good overview for most methods is outlined below:

**HTTP POST:** This method is designed to perform actions, create resources, change state on the server. Parameters can be passed in the query string of the request as well as the request message body. Consider the example when a POST request is sent on your web application, pressing the back button would not re-issue the request (like it would for a HTTP GET request). POST is slightly less susceptible to CSRF (Cross Site Request Forgery) but you can read more about that on my other article.

**HTTP GET:** Relatively basic, designed to get resources from the server, consider when you are loading a web page, what you are actually doing is sending a GET request to the web server telling it, retrieve me the HTML for this page and display it on my browser. GET should never modify state on the server or create resources, why?

- It is much weaker vs CSRF based attacks

- Imagine a HTTP GET in your API that creates or deletes resources, google crawler could cause havoc on your server, running a pentesting tool could also absolutely ruin your server & data.

- GET should be safe & idempotent, it is also a violation of the HTTP standards. By idempotent we mean it can be cached and retried with zero risk.

**HTTP HEAD:** Same as a HTTP GET request except we tell the server not to give us back the message body, this can be used to check if a particular resource exists before making an attempt to retrieve with a GET.

**HTTP TRACE:** This is used for debugging and essentially loops back the HTTP Request in the response.

**HTTP OPTIONS:** Asking the server to give us back a list of supported HTTP methods for a particular resource, really helpful if you don't want to refer to API documentation etc. The HTTP Response will include an ALLOW header which will list each supported method, comma seperated.

**HTTP PUT:** Used to typically update existing resources on the server, we may POST to add a new resource on the server, however if we wanted to change a particular attribute of a resource we could HTTP PUT.

disclaimer: Other methods do exist!

---

### URL Deciphering
URL stands for Uniform Resource Locator and it is a unique identifier for a resource on the server which can be retrieved, URL format is usually structured as follows:

protocol://hostname[:port]/[path/]file[?param1=value&param2=value2]

**protocol**: http://

**hostname**: www.mywebsite.com

**port**: :82

**path**: /api/getPersonDetails

**params**: ?personID=100

Collectively the above example, gives us our URL which looks like so: http://www.simonkay.com:82/api/getpersonDetails?personID=100

---

## HTTP Headers In Detail - General Headers

I briefly touched on headers at the start of this article, HTTP supports a wide range of headers and some of them are universal in that they can be passed as both request & response headers, some are available only to requests and likewise some to responses.

**Connection:**  Tells the receiver end of the communication whether it should close the TCP connection after the HTTP transmission has completed or keep it open for further messages.

**Content-Encoding:**  Specify what type of encoding is being used for the entity/message body. This header is advisable as it can decrease payload size with the compression of the media type, however things like JPEG files are already compressed.

**Content Length:** The length of the message body in bytes. (Special scenario: in response to a HTTP Head request, this will return the length of the body as if it was a GET request).

**Content-Type:**  Specifies the type of content contained in the message body, such as application/json for Javascript Object Notation.

## HTTP Headers In Detail - Request Headers

**Accept**: We tell the server which type of content we (the client) are happy to accept, be it image types, HTML or JSON etc.

**Accept-Encoding:** Tells the server what kinds of content encoding the client is willing to accept.

**Authorization:**  Submits credentials to the server for one of the built-in HTTP authentication types, such as BASIC, NTLM & DIGEST (more on this later!).

**Cookie:** Submits cookies to the server that the server previously issued.

**Host:** Specifies the host name that appeared in the full URL being requested. (covered this one already).

**Origin:** Used in cross-domain Ajax requests to indicate the domain from which the request originated.

We've already covered user-agent & referer previously so I won't detail those two again, but you can read more on them above.

---

## HTTP Headers In Detail - Response Headers
**Access-Control-Allow-Origin:**  Indicates whether the resource can be retrieved via cross-domain Ajax requests.

**Cache-Control:** Passes caching directives to the browser (for example, no-cache, no-store, no transform & max-age etc (lots more available here).

**Expires:**  Sets how long the message body of the response is considered valid, cached version of this will be accessible until the expiration date/time passes, then the response will be considered stale.

**Location:** Often coupled with a status of 3xx to perform a redirect, the location header specifies a destination host in which to redirect the browser.

**Set-Cookie:** This issues the browser a further cookie; this is submitted back in the Cookie header of subsequent requests to this server.

**Pragma:** This is used for caching purposely and typically tells the browser not to store the response in its cache. The Expires header indicates that the response content expired in the past and therefore should not be cached. These instructions are frequently issued when dynamic content is being returned to ensure that browsers obtain a fresh version of this content on subsequent occasions.

**Server:** Provides information about the web server software being used.

**X-Frame-Options:** Used to control if the current response is allowed to be loaded in an IFRAME, this is useful in the prevention of click jacking. Try embed google into an IFRAME and you will see that it simply does not load/render the HTML when you view it locally.

---

## Cookies nomnom!
Cookies are a crucial part of HTTP and are used in most web applications today. They provide a means of sending data to the client which is stored on the client side and attached to all subsequent requests. A server may return a Set-Cookie header in the response, Set-Cookie: yourname=simon. Now if i communicate with the server later, it will attach a header to my request like so: Cookie: yourname=simon.

Cookies are essentially a key value pair where the value is a string without a space, multiple cookies can be sent as a response from the server by sending multiple Set-Cookie headers, however on subsequent requests by the client all cookies will be set on the cookie: header, seperated by a comma.

The Set-Cookie Response header can contain more than just the cookies name/value, it can also include a number of different attributes which can be used.

- Set a date the cookie valid until by specifying the **expires** attribute, when not set explicitly the - - cookie expiration will only live in the current browser session.

- Set the cookie only to be transmitted under HTTPS conditions by specifying the **secure** attribute

- Prevent the cookie being access via client side javascript (document.cookie; for example) using the **HttpOnly** attribute.

- Specify which domain the cookie is valid for using the **domain** attribute (strictly limited to the same or parent of the domain in which the cookie is received).

- Specify the URL path which the cookie is valid for using the **path** attribute.

---

## HTTP Status Codes

Every single HTTP response must contain a HTTP response code and these are typically grouped into 5 categories ranging from 1xx - 5xx.

- **1xx** - Information status codes
- **2xx** - Successful Request status codes
- **3xx** - Client Redirection status codes
- **4xx** - Erroneous Request status codes
- **5xx** - Server Error status codes

An overview of some of the most popular status codes are:

- **100 Continue:** Is sent in some circumstances when a client submits a request containing a body. The response indicates that the request headers were received and that the client should continue sending the body. The server returns a second response when the request has been completed.

- **200 OK:** Indicates that the request was successful and that the response body contains the result of the request.

- **201 Created:** Returned in response to a PUT request to indicate that the request was successful.

- **301 Moved Permanently:** Redirects the browser permanently to a different URL, which is specified in the Location header. The client should use the new URL in the future rather than the original.

- **400 Bad Request:** Indicates that the client submitted an invalid HTTP request. You will probably encounter this when you have modified a request in certain invalid ways, such as by placing a space character into the URL.

- **401 Unauthorized:** Indicates that the server requires HTTP authentication before the request will be granted. The WWW-Authenticate header contains details on the type(s) of authentication supported.

- **403 Forbidden:** Indicates that no one is allowed to access the requested resource, regardless of authentication.
- **404 Not Found:** Resource cannot be found.

- **405 Method Not Allowed:** Unsupported HTTP method type, use HTTP Options to see the list available.

- **500 Internal Server:** Error indicates that the server encountered an error fulfi lling the request. This normally occurs when you have submitted unexpected input that caused an unhandled error somewhere within the application’s processing. You should closely review the full contents of the server’s response for any details indicating the nature of the error.

- **503 Service Unavailable:** Normally indicates that, although the web server itself is functioning and can respond to requests, the application accessed via the server is not responding. You should verify whether this is the result of any action you have performed.

---

## HTTP( S) & HTTP Authentication






