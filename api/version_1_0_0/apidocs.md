# API v1.0.0

BASE_URL  http://host1813162.hostland.pro/api

## Registration

|attribute          |value         	        |
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

|attribute          |value         	        |
|----------------	|-------------------	|
| request method 	| POST              	|
| route          	| BASE_URL/login    	|
| error types    	| EmailError, PasswordError|

#### REQUEST DATA

```json
{
    "email": "example@mail.com",
    "password": "userpassword"
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

>*Note*: 1) Возвращаются только найденные ошибки; 2) Приведены все возможные ошибки 

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "EmailError",
            "message": "Пользователь с таким e-mail не зарегистрирован."
        },
        {
            "type": "PasswordError",
            "message": "Неверный пароль"
        }
    ],
    "token": null,
    "user": null
}
```

## Logout

|attribute          |value         	        |
|----------------	|-------------------	|
| request method 	| POST              	|
| route          	| BASE_URL/logout    	|
| required headers  | Authorization         |

>*Note*: Формально логаут это удаление токена, т.е. никакие дополнительные данные не нужны. Токен будет в приведенном хэдере запроса. 

## Password Reset Request

|attribute          |value         	        |
|----------------	|-------------------	|
| request method 	| POST              	|
| route          	| BASE_URL/reset-password|
| error types    	| EmailError            |

#### REQUEST DATA

```json
{
    "email": "example@mail.com"
}
```
#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Дальнейшие инструкции отправлены на ваш e-mail."

}
```
#### RESPONSE DATA [FAIL]

>*Note*: 1) Приведены все возможные ошибки 

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "EmailError",
            "message": "Пользователь с таким e-mail не зарегистрирован."
        }
    ],
    "message": null

}
```

## Password Reset

|attribute          |value         	        |
|----------------	|-------------------	|
| request method 	| POST              	|
| route          	| BASE_URL/reset/password|
| error types    	| InvalidTokenError, EmailError, PasswordValidationError, PasswordConfirmationError|

#### REQUEST DATA

```json
{
    "token": "unique_token_that_was_wrapped_to_email_sent_to_user",
    "email": "example@email.com",
    "password": "user_new_password",
    "password_confirmation": "user_new_password_confirmation"
}
```
#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Пароль был успешно изменен."

}
```
#### RESPONSE DATA [FAIL]

>*Note*: 1) Возвращаются только найденные ошибки; 2) Приведены все возможные ошибки 

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "InvalidTokenError",
            "message": "Ссылка, которой вы воспользовались для сброса пароля, устарела."
        },
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
            "type": "EmailError",
            "message": "Пользователь с таким e-mail не зарегистрирован."
        }
    ],
    "message": null
}

}
```

## Email Verification

|attribute          |value         	        |
|----------------	|-------------------	|
| request method 	| GET              	    |
| route          	| BASE_URL/verify/{token}|
| error types    	| InvalidTokenError, EmailError|

#### REQUEST DATA

```json
{
    "token": "verification_token_from_email_sent_to_user"
}
```
#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Почта успешно подтверждена."

}
```
#### RESPONSE DATA [FAIL]

>*Note*: 1) Возвращаются только найденные ошибки; 2) Приведены все возможные ошибки 

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "InvalidTokenError",
            "message": "Ссылка, которой вы воспользовались для подтверждения email, устарела. Пройдите регистрацию заново."
        },
        {
            "type": "EmailError",
            "message": "Ваша почта уже подтверждена."
        }
    ],
    "message": null
}
```
