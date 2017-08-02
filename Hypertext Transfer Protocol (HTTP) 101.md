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










