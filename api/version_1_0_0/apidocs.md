# API v1.0.0

BASE_URL  http://host1813162.hostland.pro/api

## Registration

|        	        |                    	|
|----------------	|-------------------	|
| request method 	| POST              	|
| route          	| BASE_URL/register 	|
| error types    	| EmailError, PasswordValidationError, PasswordConfirmationError, EmailValidationError|

#### request data

```json
{
    "email": "example@mail.com",
    "password": "somepassword",
    "password_confirmation": "somepassword"
}
```
#### response data [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "token": "access_token_here",
    "user": {
        "id": 67,
        "email": "example@mail.com",
    }
}
```

## Authorization

## Logout

## Password Reset Request

## Password Reset

## and so on...
