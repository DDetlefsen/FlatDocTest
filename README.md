<h1 id="client-appliation-interface">Client Application Interface</h1>
<h1 id="client-application-introduction">Introduction</h1>
<p>There are a number of API calls available, which are summarized here, and described in more detail below.</p>


<h2 id="client-application-http-rest-detials">HTTP REST Details</h2>
<p>The Zatar Client Application API is a <a href="http://en.wikipedia.org/wiki/Representational_State_Transfer">REST</a> API.
REST means a lot of things, but first and foremost it means that we use the URL in the way that it&apos;s intended:
as a &quot;Uniform Resource Locator&quot;.</p>
<hr>
<p>All client application requests to Zatar come through our API server using TLS security.</p>
<pre><code>PROTOCOL AND HOST
https://api.zatar.com</code></pre>
<h3 id="introduction-http-header">HTTP Header</h3>
<p>Client application requests to Zatar must use the following REST headers.</p>
<pre><code>HTTP/1.1
Accept: application/json; charset=utf-8
Content-Type: application/json; charset=utf-8
</pre></code>
<h3 id="introduction-errors">Errors</h3>
<p>Zatar uses traditional HTTP response codes to provide feedback regarding the validity
of the client request and its success or failure. As with other HTTP resources, response codes in the 200 range
indicate success; codes in the 400 range indicate failure due to the information provided;
codes in the 500 range indicate failure within Zatar&apos;s server infrastructure.</p>
<pre><code>200 OK - API call successfully delivered to Zatar and executed.

400 Bad Request - Your request is not understood by Zatar,
    or the requested subresource (variable/function) has not been exposed.

401 Unauthorized - Your access token is not valid.

403 Forbidden - Your access token is not authorized to interface with this resource.

404 Not Found - The resource you requested is not currently locatable with the access level provided.

408 Timed Out - Zatar experienced a significant delay when trying to reach the resource.

500 Server errors - Fail whale. Something&apos;s wrong on our end.</code></pre>


<h2 id="client-application-authorization-tokens">Authentication Tokens</h2>
<p>This service will authenticate an existing Zatar user and return an access token. This access token is required in requests to access resources associated with a user account. This service can also verify whether or not a provided access token has expired.</p>
<hr>
<p>Create a new authentication token by doing an HTTP POST.</p>
<pre><code>POST ../v1/authentokens

<span class="comment">//Sample payload
//email is the email address of the existing Zatar user creating the token
//password is the password of the existing Zatar user creating the token</span>
{
   "email":"teamzatar@zatar.com",
   "password":"ZatarTeam&1"
}
</code></pre>
<hr>
<p>A successful request will provide a 201 response.</p>
<pre><code><span class="comment">//Sample Header Response</span>
HTTP/1.1 201 Created
Cache-Control: no-cache, no-store
Location: https://api.zatar.com/v1/authentokens/ABCDEFGHIJKLMN
Last-Modified: Tue, 4 Jun 2013 18:00:00 GMT
Expires: Wed, 5 Jun 2013 06:00:00 GMT
Content-Type: application/json;charset=utf-8
Date: Thu, 4 Jun 2013 18:00:00 GMT

<span class="comment">//Sample payload response
//token is the created authentication token
//href is the URI of the user who owns that authentication token
//expires is the value when the authentication token expires</span>
{
   "token":"1a2b3c4d-1a2b-1a2b-1a2b-1a2b3c4d5e6f",
   "href":"https://api.zatar.com/v1/users/NMLKJIHGFEDCBA"
   "expires":"1370412000",
}
</code></pre>
<hr>
<p>Verify that a token is valid by performing an HTTP GET.</p>
<pre><code>GET ../v1/authentokens/YOUR_AUTHENTICATION_TOKEN

<span class="comment">//Sample payload</span>
none
</code></pre>
<hr>
<p>A successful request will provide a 201 response.</p>
<pre><code><span class="comment">//Sample Header Response</span>
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Last-Modified: Tue, 4 Jun 2013 12:00:00 GMT
Expires: Wed, 5 Jun 2013 08:00:00 GMT
Content-Type: application/json;charset=utf-8
Date: Tue, 4 Jun 2013 12:00:00 GMT

<span class="comment">//Sample payload response</span>
none
</code></pre>



<h2 id="client-application-invitation-tokens">Invitation Tokens</h2>
<p>Invitation tokens allow a user to invite other users to join their home world and share information. This service can also verify whether or not a previously generated invite token has expired.</p>
<hr>
<p>Create a new invitation token by doing an HTTP POST.</p>
<pre><code>POST ../v1/invitetokens?token=YOUR_USER_TOKEN

<span class="comment">//Sample payload
//email is the email address of the person whom you wish to recieve your invitation
//world is the URI of the world you wish to create an invitation for</span>
{
   "email":"newzatarmember@example.com",
   "world": "https://api.zatar.com/v1/worlds/1234567890ABCDEF"
}
</code></pre>



<span class="comment">//Sample payload
//email is the email address of the existing Zatar user creating the token
//password is the password of the existing Zatar user creating the token</span>
{
   "email":"teamzatar@zatar.com",
   "password":"ZatarTeam&1"
}
</code></pre>



<hr>
<p>A successful request will provide a 201 response.</p>
<pre><code><span class="comment">//Sample Header Response</span>
201 Created
Content-Type: application/json; charset=utf-8
Cache-Control: no-cache,no-store
Date: Tue, Jun 4 2013 12:00:00 GMT
Expires: Wed, Jun 5 2013 12:00:00 GMT
Location: https://api.zatar.com/v1/invitetokens/2G03MOD1J6ENBZ1H

<span class="comment">//Sample payload response
//token is the invitation token created by the request
//expires is the value when the invitation token expires</span>
{
   "expires":1399727285503,
   "token":"05fc0f77-3c2f-4565-88a4-8bb340b2427z"
}
</code></pre>
<hr>
<p>Verify that an invitation token is valid by performing an HTTP GET.</p>
<pre><code>GET ../v1/authentokens/{YOUR AUTHENTICATION TOKEN}

<span class="comment">//Sample payload</span>
none
</code></pre>
<hr>
<p>A successful request will provide a 201 response.</p>
<pre><code><span class="comment">//Sample Header Response</span>
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Cache-Control: no-cache,no-store
Last-Modified: Tue, Jun 4 2013 12:00:00 GMT
Expires: Tue, Jun 4 2013 18:00:00 GMT
 
<span class="comment">//Sample payload response</span>
none
</code></pre>
<hr>


<h2 id="client-application-worlds">Worlds</h2>
<h3 id="client-application-avatar-definitions">Avatar Defintiions</h3>
<h4 id="client-application-firmwares">Firmwares</h4>
<h3 id="client-application-avatar-groups">Avatar Groups</h3>
<h3 id="client-application-avatar-profiles">Avatar Profiles</h3>
<h3 id="client-application-events">Events</h3>
<h3 id="client-application-notifications">Notifications</h3>
<h2 id="client-application-avatars">Avatars</h2>
<h3 id="client-application-avatar-history">Avatar History</h3>
<h3 id="client-application-jobs">Jobs</h3>