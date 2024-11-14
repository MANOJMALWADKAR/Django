# GLobal Token Base Authentication

# settings.py 

INSTALLED_APPS = [

'rest_framework.authtoken'
]


REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES' : ['rest_framework.authentication.TokenAuthentication'],
    'DEFAULT_PERMISSION_CLASSES': ['rest_framework.permissions.IsAuthenticated']
}

Make Migrations and migrate

in admin create token for user

in postman 

add path and in header add 

    key as authorization
    value token token_key (from admin pannel)

How to obtain token in postman

urls.py

from rest_framework.authtoken.views import obtain_auth_token


    path('get-api-auth-token/',obtain_auth_token,name='api_token_auth')

in postman

add post request

http://127.0.0.1:8000/get-api-auth-token/

raw data json

add
 {
    "username":"manoj",
    "password":"admin@2611"
}

send req

op
 
 token same as that we created in admin panel for user




# how token-based authentication works, especially in the context of a Django REST Framework application

1. User Registers:

The user sends their registration details (username, password, etc.) to the server.

- Server Response:

The server confirms successful registration, typically returning a success message.


2. User Login

- User Sends Login Request:

The user provides their credentials (username and password) to log in

- Server Validates Credentials:

The server checks the database for the username and password.

- Token Generation:

If the credentials are valid, the server generates a token (e.g., JWT or a simple token) and sends it back in the response.

3. Token Storage

- Client Stores the Token:

The client (e.g., a web or mobile application) stores the token securely, often in local storage, session storage, or cookies.

4.  Access Protected Resources

- User Makes Subsequent Requests:

For any subsequent API requests, the user includes the token in the Authorization header.

5. Server Validates Token

- Token Validation:

The server checks the token in the request header. It verifies whether the token is valid and not expired.
If the token is valid, the server allows access to the requested resource.

- Response for Valid Token:

If valid, the server processes the request and returns the requested data.

- Response for Invalid Token:

If the token is invalid or expired, the server responds with an error message (e.g., 401 Unauthorized).

6. Token Expiration and Refresh (Optional)

- Token Expiration:

If using JWT, tokens typically have an expiration time. After expiration, the user must log in again to receive a new token.

- Refresh Token Flow (if implemented):

You can implement a refresh token mechanism to obtain a new access token without re-entering credentials.


# Summary

- Initial Login: Requires username and password.

- Token Usage: The token is used for subsequent requests, avoiding the need to re-enter credentials.

- Security: Tokens should be securely stored and handled to prevent unauthorized access.
