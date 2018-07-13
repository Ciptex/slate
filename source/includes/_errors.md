# Errors

<aside class="notice">
All status codes are standard HTTP status codes. The below ones are used in this API.
</aside>

The Kittn API uses the following error codes:

2XX | Success of some kind.
4XX | Error occurred in client’s part.
5XX | Error occurred in server’s part.


HTTP Status Codes | Meaning
---------- | -------
200 | OK 
201 | Created 
202 | Accepted (Request accepted, and queued for execution) 
400 | Bad request 
401 | Authentication failure 
403 | Forbidden 
404 | Resource not found 
405 | Method Not Allowed 
409 | Conflict 
412 | Precondition Failed 
413 | Request Entity Too Large 
500 | Internal Server Error 
501 | Not Implemented 
503 | Service Unavailable