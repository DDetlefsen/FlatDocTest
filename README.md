# FlatDocTest
Here is my test of the FladDoc thingie

# Authentication Tokens

This service will authenticate an existing Zatar user and return an access token. Currently tokens expire after 12 hours from when they are created.

Make sure your HTTP Header is as follows<pre><code>HTTP/1.1
Accept: application/json; charset=utf-8
Content-Type: application/json; charset=utf-8
</pre></code>

# Authentication Token Parameters
<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg .tg-e3zv{font-weight:bold}
</style>
<table class="tg">
  <tr>
    <th class="tg-e3zv">Parameter</th>
    <th class="tg-e3zv">Where Used</th>
    <th class="tg-e3zv">Requirement</th>
    <th class="tg-e3zv">Notes</th>
  </tr>
  <tr>
    <td class="tg-031e">email</td>
    <td class="tg-031e">POST Payload</td>
    <td class="tg-031e">mandatory</td>
    <td class="tg-031e">email must be provided to uniquely identify the account<br>must meet minimum email format requirements according to RFC</td>
  </tr>
  <tr>
    <td class="tg-031e">password</td>
    <td class="tg-031e">POST Payload</td>
    <td class="tg-031e">mandatory</td>
    <td class="tg-031e">alphanumeric string (a-z, 0-9)<br>case sensitive<br>must contain one upper case letter<br>must contain one lower case letter<br>must contain one number<br>must contain one special character<br>minimum 8 characters<br>maximum 16 characters</td>
  </tr>
  <tr>
    <td class="tg-031e">token</td>
    <td class="tg-031e">Response</td>
    <td class="tg-031e"></td>
    <td class="tg-031e">the access token providing authentication for the user specified in the message payload</td>
  </tr>
  <tr>
    <td class="tg-031e">href</td>
    <td class="tg-031e">Response</td>
    <td class="tg-031e"></td>
    <td class="tg-031e">the URI of the associated user</td>
  </tr>
  <tr>
    <td class="tg-031e">expires</td>
    <td class="tg-031e">Response</td>
    <td class="tg-031e"></td>
    <td class="tg-031e">the time when the issued authentication token will expire</td>
  </tr>
</table>


Creating a new authentication token <pre><code>POST https://api.zatar.com/v1/authentokens
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
