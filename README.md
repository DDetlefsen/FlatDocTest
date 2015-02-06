# FlatDocTest
Here is my test of the FladDoc thingie

# Authentication Tokens

This service will authenticate an existing Zatar user and return an access token. Currently tokens expire after 12 hours from when they are created.

Create a new authentication token<code>POST https://api.zatar.com/v1/authentokens</code>

Verify an existing authentication token<code>GET https://api.zatar.com/v1/authentokens/{authentoken_resource_id}</code>
