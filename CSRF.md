# Cross-Site Request Forgery (CSRF)

# Problem
CSRF vulnerability implies forging a malicious HTTP request by a 3rd party
site to the target site that the user is currently logged in to. The 3rd party
site will be able to use the user's cookies to the target site, making the
request seem legitimate to the target site. Consider the following request:

    POST /delete_acccount HTTP/1.1
    Host: example.com
    Content-Type: application/x-www-form-urlencoded
    Cookie: SessionID=f5a7dfe6

    delete=1

If the user is logged in to example.com, and visits a malicious link in another
tab, the malicious site can perform a request that deletes their account on
behalf of the user. Due to Same Origin Policy (SOP) the 3rd party website won't
be able to receive the response of the server, but for this attack to work it
doesn't need to.

# Solution
1. CSRF vulnerability is solved by using a CSRF Token. CSRF Token is a signed
   (HMAC) token that the server sends to the client on every request. The client
   sends this token back with every request to prove their identity.
   For example, with every form that the website sends to the user it must also
   send the CSRF Token. Once the user submits the form, this token must be sent
   back to the server to make sure it's a legitimate POST request. If a 3rd
   party website tries to forge this request, it can't send the secret CSRF
   token with it, making the request illegitimate.
2. Enable 'SameSite' cookies. Cookies can only be sent if the request is
   performed from the same site, which eliminates the possibility of 3rd party
   requests: `Set-Cookie: SessionID=f5a7dfe6; path=/; SameSite=lax`

# SOP and CORS
* Same Origin Poolicy (SOP) prevents the browser from being able to read the
  response from the server if the request is made from the wrong origin.
* Cross-Origin Resource Sharing (CORS) allows to specify exceptions for the SOP,
  making cross-origin requests possible between select hosts.
