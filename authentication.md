# Authentication vs Authorization
- Authentication - verifying identity (401 Unauthorized)
- Authorization - verifying permissions (403 Fordbidden)

# Types of authentication
- Stateful - sessions using cookies
- Stateless - token based, using JWT or OAuth


# Session/Cookie-based Authentication

## Flow
1. User submits credentials (email and password) to server
2. Server verifies credentials against DB
3. Server creates a temporary user session (state) and sends a cookie to user
4. User sends a cookie with each request to server, server validates it against
   session store and grants access.
5. When user logs out, server destroys session and clears cookie on user's side

## Features
- Sessions on the server are stored in DB, cache (Redis or Memcached) or memory
- Used in Server Side Applications (Rails, Spring, Laravel, Sinatra, etc.)
- Cookies are part of HTTP Header
- Consists of Name-Value pairs (also attributes/flags)

## Security
- Cookies are signed (HMAC) by the server to prevent tampering by client
- Rarely encrypted (AES) but no point since 1-1 relationship between client and
  server

## Attributes
- Domain & path - limits the URL scope of the cookie
- Expiration - browser can only use cookie until a specified date. If expiration
  date is ommitted, it becomes a *session cookie* and will get deleted when
  browser is closed.

## Flags
- HttpOnly - cannot be accessed by JS code on client side
- Secure - cookie can only be sent via HTTPS
- SameSite - cookie can only be sent from same domain

## CSRF attacks (Cross-Site Request Forgery)
- Performing actions on behalf of authenticated user by a 3rd party
- Mitigated with a CSRF token cookie, stored alongside SessionID cookies


# Token-based Authentication

## Flow
1. User submits credentials (email and password) to server
2. Server verifies credentials against DB
3. Server generates a temp token and embeds user data into it, sends it to user
   in HTTP body or header. Token isn't saved on server (stateless)
4. User stores token locally
5. User sends token with each request to server, server verifies it and grants
   access.
6. When user logs out, token is deleted from user storage

## Features
- Tokens are not stored on the server (stateless)
- Tokens are signed to prevent client tampering
- Tokens can be *opaque/self-contained* (require no DB lookups on the server)
- Tokens expire and can be refreshed with *refresh token*
- Tokens are used in Single-Page Applications, Web and mobile API's, etc.


# JWT - JSON Web Token
JWT is an open standard for authorization.

## Features
- Self-contained, URL-safe
- Signed with symmetric or assymetric key

## Server JWT response example

    HTTP/1.1 200 OK
    Content-type: application/json
    Authorization: Bearer header.payload.signature

Token example breakdown (JS):

    atob('header')
    // "{"alg":"HS256","typ":"JWT"}"
    //    algorithm:    type:

    atob('payload')
    // "{"sub":"subject like userID","name":"Johnny Depp","iat":0000000000}"
    //    subject: (e.g. user ID)     claim(s):            issued at: (seconds)

## Security
- Signed (HMAC) to prevent client tampering
- Rarely encrypted (because client must read payload of token)
- Should be short lived to minimize damage in case of an attack

## XSS
It is important to prevent XSS attacks when using JWT. Malicious XSS code
running on the client side, can access client storage and steal user data from
the JWT token or perform requests using that token.

## Types of browser storage
- localStorage
    - No expiration date
    - Isolated on domain basis
    - More storage than sessionStorage (5MB/domain vs 4KB/cookie)
    - Not secure by design (plain text)
    - String data only, hence need to serialize to store JSON
    - Can't be used by web workers
    - Stored permanently
    - Accessible to any JS code within a page (!: XSS)
- sessionStorage - gets cleared when page is closed


# Sessions vs JWT

## Sessions pros
- Session IDs are opaque and contain no meaningful data
- Cookies can be secured by flags like same origin, HTTPS only, etc.
- XSS proof

## Sessions cons
- Server must store sessions
- Session authentication must be secured by CSRF
- Horizontal, enterprise-level scaling is more complicated, because every server
  must have the cookie

## JWT pros
- Sever doesn't need to store tokens
- Horizontal scaling is easier - any server can verify token
- FE and BE architecture is decoupled

## JWT cons
- Server still has to maintain blacklist of old tokens (e.g. reset tokens have
  to be stored until expiry) or whitelist of active tokens
- When scaling, the HMAC secret has to be shared between servers
- Data in client's token can become out of sync with server (name, permissions,
  etc.)
- Vulnerable to XSS attacks unless all user input is sanitized


# Types of client storage (browser storage)

- Cookies - the oldest way to store data on the client side. Used for user
  personalization, session ID and access tokens.
- Web Storage API - used for smaller key-value data items, such as user's name,
  whether they are logged in, personalization, etc.
    - sessionStorage - persists data as long as browser is open
    - localStorage - persists data even when browser fully restarts
- IndexedDB API - a complete DB for storing complex data (e.g audio/video files)
- Cache API - designed to store HTTP responses to specific requests. Useful for
  storing website assets offline. Often used in combination with Service Worker
  API.