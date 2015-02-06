# FlatDocTest
Here is my test of the FladDoc thingie

# Authentication Tokens

This service will authenticate an existing Zatar user and return an access token. Currently tokens expire after 12 hours from when they are created.

Make sure your HTTP Header is as follows<pre><code>HTTP/1.1
Accept: application/json; charset=utf-8
Content-Type: application/json; charset=utf-8
</pre></code>

Parameters
| Parameter 	| Where Used 	| Requirement 	| Notes                                                                                                                                                                                                                     	|
|-----------	|------------	|-------------	|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|
| email     	| Payload    	| mandatory   	| email must be provided to uniquely identify the account must meet minimum email format requirements according to RFC                                                                                                      	|
| password  	| Payload    	| mandatory   	| alphanumeric string (a-z, 0-9) case sensitive must contain one upper case letter must contain one lower case letter must contain one number must contain one special character minimum 8 characters maximum 16 characters 	|
| token     	| Response   	|             	| the access token providing authentication for the user specified in the message payload                                                                                                                                   	|
| href      	| Response   	|             	| the URI of the associated user                                                                                                                                                                                            	|
| expires   	| Response   	|             	| the time when the issued authentication token will expire   

Creating a new authentication token<pre><code>POST https://api.zatar.com/v1/authentokens
//Example payload
{
   "email":"username@zatar.com",
   "password":"MyPassword&1"
}
//Example response
HTTP/1.1 201 Created
Cache-Control: no-cache, no-store
Location: https://api.zatar.com/v1/authentokens/ABCDEFGHIJKLMN
Last-Modified: Tue, 4 Jun 2013 18:00:00 GMT
Expires: Wed, 5 Jun 2013 06:00:00 GMT
Content-Type: application/json;charset=utf-8
Date: Thu, 4 Jun 2013 18:00:00 GMT
{
   "token":"1a2b3c4d-1a2b-1a2b-1a2b-1a2b3c4d5e6f",
   "href":"https://api.zatar.com/v1/users/NMLKJIHGFEDCBA"
   "expires":"1370412000",
}
</code></pre>

Verify an existing authentication token<pre><code>GET https://api.zatar.com/v1/authentokens/{authentoken_resource_id}</pre></code>

HTTP Response Codes<pre><code>200: OK
401: Unauthorized
404: Not Found
406: Not Acceptable
500: Internal Server Error
</pre></code>
