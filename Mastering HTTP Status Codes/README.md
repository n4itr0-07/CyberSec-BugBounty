# Comprehensive Guide to HTTP Status Codes

HTTP status codes are issued by a server in response to a client's request. These codes indicate whether a specific HTTP request has been successfully completed. They are grouped into five classes:

## 1xx: Informational Responses

These codes indicate that the request was received and understood. The server is continuing the process.

- **100 Continue:** The initial part of a request has been received, and the client should continue with the request.
- **101 Switching Protocols:** The server is changing protocols as requested by the client.
- **102 Processing (WebDAV):** The server has received and is processing the request, but no response is available yet.
- **103 Early Hints:** Used to return some response headers before the final HTTP message.

## 2xx: Success

These codes indicate that the client's request was successfully received, understood, and accepted.

- **200 OK:** The request was successful.
- **201 Created:** The request has been fulfilled, resulting in the creation of a new resource.
- **202 Accepted:** The request has been accepted for processing, but processing is not yet complete.
- **203 Non-Authoritative Information:** The request was successful, but the information returned is from a third party.
- **204 No Content:** The request was successful, but there is no content to send in the response.
- **205 Reset Content:** The request was successful, and the client should reset the view.
- **206 Partial Content:** The server is delivering only part of the resource due to a range header sent by the client.
- **207 Multi-Status (WebDAV):** Multiple status codes might be appropriate.
- **208 Already Reported (WebDAV):** The members of a DAV binding have already been enumerated in a previous reply.
- **226 IM Used (HTTP Delta encoding):** The server has fulfilled a GET request for the resource, and the response is a representation of the result of one or more instance manipulations.

## 3xx: Redirection

These codes indicate that the client must take additional action to complete the request.

- **300 Multiple Choices:** There are multiple options for the resource that the client may follow.
- **301 Moved Permanently:** The resource has been moved permanently to a new URL.
- **302 Found (Previously "Moved Temporarily"):** The resource resides temporarily under a different URL.
- **303 See Other:** The server sent this response to direct the client to get the requested resource at another URI with a GET request.
- **304 Not Modified:** The resource has not been modified since the version specified by the request headers.
- **305 Use Proxy (Deprecated):** The requested resource is only available through a proxy.
- **307 Temporary Redirect:** The request should be repeated with another URI, but future requests should still use the original URI.
- **308 Permanent Redirect:** The request and all future requests should be repeated using another URI.

## 4xx: Client Errors

These codes indicate that there was likely an error in the request from the client.

- **400 Bad Request:** The server cannot process the request due to a client error.
- **401 Unauthorized:** Authentication is required and has failed or has not been provided.
- **402 Payment Required:** Reserved for future use.
- **403 Forbidden:** The server understood the request, but refuses to authorize it.
- **404 Not Found:** The server can't find the requested resource.
- **405 Method Not Allowed:** The request method is known by the server but has been disabled and cannot be used.
- **406 Not Acceptable:** The server cannot produce a response matching the list of acceptable values defined in the request's headers.
- **407 Proxy Authentication Required:** The client must first authenticate itself with the proxy.
- **408 Request Timeout:** The server timed out waiting for the request.
- **409 Conflict:** The request could not be processed because of conflict in the request, such as an edit conflict between multiple simultaneous updates.
- **410 Gone:** The resource requested is no longer available and will not be available again.
- **411 Length Required:** The request did not specify the length of its content, which is required by the requested resource.
- **412 Precondition Failed:** The server does not meet one of the preconditions that the requester put on the request.
- **413 Payload Too Large:** The request entity is larger than limits defined by the server.
- **414 URI Too Long:** The URI provided was too long for the server to process.
- **415 Unsupported Media Type:** The request entity has a media type which the server or resource does not support.
- **416 Range Not Satisfiable:** The client has asked for a portion of the file, but the server cannot supply that portion.
- **417 Expectation Failed:** The server cannot meet the requirements of the Expect request-header field.
- **418 I'm a teapot (RFC 2324):** This code was defined in 1998 as an April Fools' joke and is not expected to be implemented by actual HTTP servers.
- **421 Misdirected Request:** The request was directed at a server that is not able to produce a response.
- **422 Unprocessable Entity (WebDAV):** The request was well-formed but was unable to be followed due to semantic errors.
- **423 Locked (WebDAV):** The resource being accessed is locked.
- **424 Failed Dependency (WebDAV):** The request failed because it depended on another request that failed.
- **425 Too Early:** Indicates that the server is unwilling to risk processing a request that might be replayed.
- **426 Upgrade Required:** The client should switch to a different protocol.
- **428 Precondition Required:** The server requires the request to be conditional to prevent lost update problems.
- **429 Too Many Requests:** The user has sent too many requests in a given amount of time ("rate limiting").
- **431 Request Header Fields Too Large:** The server is unwilling to process the request because its header fields are too large.
- **451 Unavailable For Legal Reasons:** The user-requested resource is unavailable due to legal reasons, such as censorship.

## 5xx: Server Errors

These codes indicate that the server failed to fulfill a valid request.

- **500 Internal Server Error:** A generic error message when the server encounters an unexpected condition.
- **501 Not Implemented:** The server either does not recognize the request method, or it lacks the ability to fulfill the request.
- **502 Bad Gateway:** The server received an invalid response from the upstream server.
- **503 Service Unavailable:** The server is not ready to handle the request, often due to maintenance or overload.
- **504 Gateway Timeout:** The server, while acting as a gateway, did not get a response in time from the upstream server.
- **505 HTTP Version Not Supported:** The server does not support the HTTP protocol version used in the request.
- **506 Variant Also Negotiates:** Transparent content negotiation for the request results in a circular reference.
- **507 Insufficient Storage (WebDAV):** The server is unable to store the representation needed to complete the request.
- **508 Loop Detected (WebDAV):** The server detected an infinite loop while processing a request.
- **510 Not Extended:** Further extensions to the request are required for the server to fulfill it.
- **511 Network Authentication Required:** The client needs to authenticate to gain network access.

---

These HTTP status codes are essential for understanding the outcome of requests and troubleshooting issues in web development. Having a good grasp of these codes can significantly improve debugging and communication between client and server.
