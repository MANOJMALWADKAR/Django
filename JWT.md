# ACCESS_TOKEN AND REFRESH_TOKEN

- when user login server sends both access token and refresh token when the access token expires then refresh token again generates access token till it expiration of refresh token if the refresh token has been also expired then user has login and authenticate itself again both tokens has to be gener

User Login:

When the user successfully logs in, the server issues both an access token and a refresh token.
The access token is used for accessing protected resources and has a short lifespan (e.g., 15 minutes to an hour).
The refresh token is used to obtain a new access token after the old one expires and typically has a longer lifespan (e.g., days or weeks).
Access Token Expiry:

After the access token expires, the client application cannot access protected resources with the expired access token.
The client sends the refresh token to the server in order to request a new access token.
Refreshing Access Token:

If the refresh token is valid (and hasn't expired or been revoked), the server issues a new access token and, optionally, a new refresh token.
The client can then use the new access token for further requests.
Refresh Token Expiry:

If the refresh token has expired (or been revoked), the server will deny the request for a new access token.
In this case, the user must log in again, and a new pair of access token and refresh token will be issued upon successful authentication.
Full Flow Summary:
Login:
Server returns both access token and refresh token.
Access Token Expiry:
The client detects the expiration of the access token.
The client sends the refresh token to the server to obtain a new access token.
Access Token Refreshed:
If the refresh token is still valid, the server issues a new access token.
The server may optionally issue a new refresh token as well.
Refresh Token Expiry:
If the refresh token has expired, the server returns an error (e.g., 401 Unauthorized or a specific token expired message).
The client prompts the user to log in again, and a new access token and refresh token are generated.
Security Considerations:
Access tokens are short-lived to minimize risks if they are compromised.
Refresh tokens are long-lived but should be stored securely (e.g., in an HTTP-only cookie or secure storage) and only used to refresh the access token.
Refresh tokens can be revoked by the server (e.g., upon user logout or password change).
This mechanism ensures both user convenience (by not requiring frequent re-logins) and sec
