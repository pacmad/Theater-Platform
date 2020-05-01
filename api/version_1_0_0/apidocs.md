# API v1.0.0

BASE_URL  http://host1813162.hostland.pro/api

## Registration

|        	        |                    	|
|----------------	|-------------------	|
| request method 	| POST              	|
| route          	| BASE_URL/register 	|
| error types    	| EmailError, PasswordValidationError, PasswordConfirmationError, EmailValidationError|

#### REQUEST DATA

```json
{
    "email": "example@mail.com",
    "password": "somepassword",
    "password_confirmation": "somepassword"
}
```
#### RESPONSE DATA [SUCCESS]

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
#### RESPONSE DATA [FAIL]

>*Note*: 1) Возвращаются только найденные ошибки; 2) Добавлены не все возможные ошибки 

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "PasswordValidationError",
            "message": "Слишком короткий пароль, должно быть минимум 8 символов."
        },
        {
            "type": "PasswordValidationError",
            "message": "Слишком длинный пароль пароль, допустимая длина - 127 символов."
        },
        {
            "type": "PasswordValidationError",
            "message": "Пароль должен содержать хотя-бы одну букву в верхнем регистре."
        },
        {
            "type": "PasswordValidationError",
            "message": "Пароль должен содержать хотя-бы одну букву в нижнем регистре."
        },
        {
            "type": "PasswordValidationError",
            "message": "Пароль может содержать только буквы латинского алфавита."
        },
        {
            "type": "PasswordValidationError",
            "message": "Пароль должен содержать хотя-бы одну цифру."
        },
        {
            "type": "PasswordValidationError",
            "message": "Пароль может содержать только следующие специальные символы: !@#$%^&*"
        },
        {
            "type": "PasswordConfirmationError",
            "message": "Введенные пароли не совпадают."
        },
        {
            "type": "EmailValidationError",
            "message": "E-mail адрес должен содержать символ @"
        }
    ],
    "token": null,
    "user": null
}
```

## Authorization

## Logout

## Password Reset Request

## Password Reset

## and so on...
