# API v2.2.0

>*updates*:
>1. К payload регистрации добавлены фамилия, имя и отчество
>2. К payload авторизации в ответе, соответственно, добавлены фамилия, имя и отчество
>3. добавлено API для добавления мест в зале
>4. добавлено API для получения мест в зале
>5. добавлено API для удаления мест в зале
>6. добавлено API для добавления билетов
>7. добавлено API для получения билета
>8. добавлено API для получения билетов
>9. добавлено API для изменения билетов
>10. добавлено API для удаления билетов
>11. добавлено комплексное API для "покупки билета"

BASE_URL  http://host1813162.hostland.pro/api

## Registration

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| POST              	|
| route          	| BASE_URL/register 	|
| error types    	| EmailError          |

#### REQUEST DATA

```json
{
    "email": "example@mail.com",
    "name": "Ivan",
    "surname": "Ivanov",
    "middle_name": "Ivanovich",
    "password": "somepassword",
    "password_confirmation": "somepassword"
}
```
#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Письмо для активации почты отправлено на ваш email адрес",
}
```
#### RESPONSE DATA [FAIL]

>*Note*: 1) Возвращаются только найденные ошибки

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "EmailError",
            "message": "Пользователь с таким адресом электронной почты уже зарегистрирован"
        }
    ]
}
```

## Authorization

|attribute        |value         	      |
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
        "name": "Ivan",
        "surname": "Ivanov",
        "middle_name": "Ivanovich"
    }
}
```
#### RESPONSE DATA [FAIL]

>*Note*: 1) Возвращаются только найденные ошибки

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "EmailError",
            "message": "Пользователь с таким адресом электронной почты не зарегистрирован"
        },       
        {
            "type": "EmailError",
            "message": "Чтобы авторизоваться необходимо подтвердить email адрес"
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
            "message": "Пользователь с таким e-mail не зарегистрирован"
        }
    ],
    "message": "При отправке запроса на восстановление пароля возникли ошибки"
}
```

## Password Reset

|attribute          |value         	        |
|----------------	|-------------------	|
| request method 	| POST              	|
| route          	| BASE_URL/reset/password|
| error types    	| InvalidTokenError, EmailError|

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

>*Note*: 1) Возвращаются только найденные ошибки

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "InvalidTokenError",
            "message": "Ссылка, которой вы воспользовались для сброса пароля, устарела"
        },
        {
            "type": "EmailError",
            "message": "Пользователь с таким адресом электронной почты не зарегистрирован"
        }
    ],
    "message": "В процессе изменения пароля возникли ошибки"
}
```

## Email Verification

|attribute          |value         	        |
|----------------	|-------------------	|
| request method 	| GET              	    |
| route          	| BASE_URL/verify/{verification_token}|
| error types    	| InvalidTokenError, EmailError|

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Почта успешно подтверждена."

}
```
#### RESPONSE DATA [FAIL]

>*Note*: 1) Возвращаются только найденные ошибки

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "InvalidTokenError",
            "message": "Ссылка, которой вы воспользовались для подтверждения email, устарела. Пройдите регистрацию заново"
        },
        {
            "type": "EmailError",
            "message": "Ваша почта уже подтверждена."
        }
    ],
    "message": "В процессе верификации email позникли ошибки."
}
```
## Update User Profile

|attribute          |value         	        |
|----------------	|-------------------	|
| request method 	| PATCH|
| route          	| BASE_URL/user/{user_id}|
| error types    	| UserNotFound, PermissionDenied|
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### REQUEST DATA

```json
{
    "name": "new_user_name",
    "surname": "new_user_surname",
    "photo": "new_user_photo"
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Информация в Вашем профиле успешно обновлена."

}
```
#### RESPONSE DATA [FAIL]

>*Note*: 1) Возвращаются только найденные ошибки

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "UserNotFound",
            "message": "Пользователь с таким id не найден."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе обновления возникли ошибки. Новая информация о Вашем профиле не сохранена."
}
```
## Get User Profile

|attribute          |value         	        |
|----------------	|-------------------	|
| request method 	| GET|
| route          	| BASE_URL/user?id={user_id}|
| error types    	| UserNotFound, PermissionDenied|
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "user": {
        "id": 67,
        "email": "example@mail.com",
        "name": "user_name",
        "surname": "user_surname",
        "photo": "user_photo"
    }

}
```
#### RESPONSE DATA [FAIL]

>*Note*: 1) Возвращаются только найденные ошибки

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "UserNotFound",
            "message": "Пользователь с таким id не найден."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе получения информации о пользователе возникли ошибки."
}
```
## Add User Bookmark

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| POST |
| route          	| BASE_URL/user/{user_id}/bookmarks|
| error types    	| UserNotFound, SpectacleNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### REQUEST DATA

```json
{
    "spectacle_id": "spectacle_id_to_bookmark",
    "created_at": "timestamp"
}
```
#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Спектакль добавлен в закладки",
}
```
#### RESPONSE DATA [FAIL]

>*Note*: 1) Возвращаются только найденные ошибки

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "UserNotFound",
            "message": "Пользователь с таким id не найден."
        },
        {
            "type": "SpectacleNotFound",
            "message": "Спектакль с таким id не найден."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе добавления спектакля в закладки возникли ошибки."
}
```
## Delete User Bookmark

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| DELETE |
| route          	| BASE_URL/user/{user_id}/bookmarks/{spectacle_id}|
| error types    	| UserNotFound, BookmarkNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Закладка удалена",
}
```
#### RESPONSE DATA [FAIL]

>*Note*: 1) Возвращаются только найденные ошибки

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "UserNotFound",
            "message": "Пользователь с таким id не найден."
        },
        {
            "type": "BookmarkNotFound",
            "message": "Закладка пользователя с таким id не найдена."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе удаления спектакля из закладок пользователя возникли ошибки."
}
```

## Get User Bookmarks

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/user/{user_id}/bookmarks|
| error types    	| UserNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### RESPONSE DATA [SUCCESS]

>*Note*: 1) Возвращаются все закладки пользователя. В примере ответа от сервера приведено 2. 2) Если заметок нет, соответственно, bookmarks будет пустым списком.

```json
{
    "has_errors": false,
    "errors": [],
    "bookmarks": [
        {
            "spectacle_id": "id_of_bookmarked_spectacle_1",
            "name": "spectacle_name_1",
            "description": "spectacle_description_1",
            "rate": "spectacle_rate_1",
            "poster": "spectacle_poster_1",
            "theater_id": "theater_id_1"
        },
        {
            "spectacle_id": "id_of_bookmarked_spectacle_2",
            "name": "spectacle_name_2",
            "description": "spectacle_description_2",
            "rate": "spectacle_rate_2",
            "poster": "spectacle_poster_2",
            "theater_id": "theater_id_2"
        }
    ]
}
```
#### RESPONSE DATA [FAIL]

>*Note*: 1) Возвращаются только найденные ошибки

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "UserNotFound",
            "message": "Пользователь с таким id не найден."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе получения информации о закладках пользователя возникли ошибки."
}
```

## Get User Purchase History

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/user/{user_id}/tickets|
| error types    	| UserNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### RESPONSE DATA [SUCCESS]

>*Note*: 1) Возвращаются все купленные пользователем билеты. В примере ответа от сервера приведено 2. 2) Если покупок нет, соответственно, purchasedTickets будет пустым списком.

```json
{
    "has_errors": false,
    "errors": [],
    "purchasedTickets": [
        {
            "ticketData": {
                "id": "id_of_purchased_ticket_1",
                "price": "price_of_purchased_ticket_1"
            },
            "transactionData": {
                "id": "id_of_transaction_1",
                "purchasedAt": "datetime_of_transaction_1"          
            },
            "seatData": {
                "id": "seat_id_1",
                "row": "seat_row_1",
                "column": "seat_column_1",
                "zone": "seat_zone_1"
            },
            "eventData": {
                "id": "event_id_1",
                "datedAt": "date_of_event_1",
                "isPremiere": "true/false",
                "zone": "seat_zone_1"
            },
            "spectacleData": {
                "id": "spectacle_id_1",
                "name": "spectacle_name_1",
                "poster": "spectacle_poster_1"
            },
            "theaterData": {
                "id": "theater_id_1",
                "name": "theater_name_1",
                "address": "theater_address_1",
                "logo": "theater_logo_1",
                "cash_desk_phone_number": "theater_cash_desk_phone_number_1",
                "phone_number_for_reference": "theater_phone_number_for_reference_1"
            },
            "hallData": {
                "id": "hall_id_1",
                "name": "hall_name_1"
            }
        },
        {
            "ticketData": {
                "id": "id_of_purchased_ticket_2",
                "price": "price_of_purchased_ticket_2"
            },
            "transactionData": {
                "id": "id_of_transaction_2",
                "purchasedAt": "datetime_of_transaction_2"          
            },
            "seatData": {
                "id": "seat_id_2",
                "row": "seat_row_2",
                "column": "seat_column_2",
                "zone": "seat_zone_2"
            },
            "eventData": {
                "id": "event_id_2",
                "datedAt": "date_of_event_2",
                "isPremiere": "true/false",
                "zone": "seat_zone_2"
            },
            "spectacleData": {
                "id": "spectacle_id_2",
                "name": "spectacle_name_2",
                "poster": "spectacle_poster_2",
            },
            "theaterData": {
                "id": "theater_id_2",
                "name": "theater_name_2",
                "address": "theater_address_2",
                "logo": "theater_logo_2",
                "cash_desk_phone_number": "theater_cash_desk_phone_number_2",
                "phone_number_for_reference": "theater_phone_number_for_reference_2"
            },
            "hallData": {
                "id": "hall_id_2",
                "name": "hall_name_2"
            }
        }
    ]
}
```
#### RESPONSE DATA [FAIL]

>*Note*: 1) Возвращаются только найденные ошибки

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "UserNotFound",
            "message": "Пользователь с таким id не найден."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе получения информации о истории платежей пользователя возникли ошибки."
}
```
## Get User Commetns

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/user/{user_id}/comments|
| error types    	| UserNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### RESPONSE DATA [SUCCESS]

>*Note*: 1) Возвращаются все отзывы пользователя. В примере ответа от сервера приведено 2. 2) Если отзывов нет, соответственно, comments будет пустым списком.

```json
{
    "has_errors": false,
    "errors": [],
    "comments": [
        {
            "commentData": {
                "id": "comment_id_1",
                "content": "comment_content_1",
                "rate": "rate_was_estimated_by_user_1",
                "is_confirmed": "true/false",
                "createdAt": "comment_created_at_1"
            },
            "spectacleData": {
                "id": "spectacle_id_1",
                "name": "spectacle_name_1",
                "poster": "spectacle_poster_1",
                "theater_id": "theater_id_1"
            }
        },
        {
            "commentData": {
                "id": "comment_id_2",
                "content": "comment_content_2",
                "rate": "rate_was_estimated_by_user_2",
                "is_confirmed": "true/false",
                "createdAt": "comment_created_at_2"
            },
            "spectacleData": {
                "id": "spectacle_id_2",
                "name": "spectacle_name_2",
                "poster": "spectacle_poster_2",
                "theater_id": "theater_id_1"
            }
        },
    ]
}
```
#### RESPONSE DATA [FAIL]

>*Note*: 1) Возвращаются только найденные ошибки

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "UserNotFound",
            "message": "Пользователь с таким id не найден."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе получения комментариев пользователя возникли ошибки."
}
```

## Add Spectacle

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| POST |
| route          	| BASE_URL/spectacles|
| error types    	| TheaterNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### REQUEST DATA

```json
{
    "name": "spectacle_name",
    "description": "spectacle_description"
    "rate": 0,
    "poster": "spectacle_poster",
    "trailer": "spectacle_trailer",
    "slider_poster": "spectacle_slider_poster",
    "theater_id": "theater_id"
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "spectacle": {
        "id": 255,
    },
    "message": "Спектакль успешно добавлен."
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "TheaterNotFound",
            "message": "Театр с таким id не найден."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе добавления спектакля возникли ошибки."
}
```

## Update Spectacle

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| PATCH |
| route          	| BASE_URL/spectacles/{spectacle_id}|
| error types    	| SpectacleNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### REQUEST DATA

```json
{
    "name": "new_spectacle_name",
    "description": "new_spectacle_description"
    "rate": 0,
    "poster": "new_spectacle_poster",
    "trailer": "new_spectacle_trailer",
    "slider_poster": "new_spectacle_slider_poster"
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Спектакль успешно обновлен."
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "SpectacleNotFound",
            "message": "Спектакль с таким id не найден."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе обновления спектакля возникли ошибки."
}
```

## Get Spectacle

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/spectacles?id={spectacle_id}|
| error types    	| SpectacleNotFound |

#### RESPONSE DATA [SUCCESS]

>*Note*: 1) Возвращаются спектакль c id == spectacle_id.

```json
{
    "has_errors": false,
    "errors": [],
    "spectacle": {
        "name": "spectacle_name",
        "description": "spectacle_description"
        "rate": 4.7,
        "poster": "spectacle_poster",
        "slider_poster": "spectacle_slider_poster",
        "theater_id": "theater_id"
    }
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "SpectacleNotFound",
            "message": "Спектакль с таким id не найден."
        }
    ],
    "message": "В процессе получения информации о спектакле возникли ошибки."
}
```

## Get Spectacles

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/spectacles?theater_id={theater_id}|
| error types    	| TheaterNotFound, PermissionDenied|

#### RESPONSE DATA [SUCCESS]

>*Note*: 1) Возвращаются все спектакли с трибутом id театра == theater_id. В примере ответа от сервера приведено 2 результата. 2) Если спектаклей нет, spectacles будет пустым списком.

```json
{
    "has_errors": false,
    "errors": [],
    "spectacles": [
        {
            "id": 1,
            "name": "spectacle_name_1",
            "rate": 4.7,
            "poster": "spectacle_poster_1"
        },
        {
            "id": 2,
            "name": "spectacle_name_2",
            "rate": 4.1,
            "poster": "spectacle_poster_2"
        },
    ]
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "TheaterNotFound",
            "message": "Театр с таким id не найден."
        }
    ],
    "message": "В процессе получения информации о спектаклях театра возникли ошибки."
}
```

## Delete Spectacle

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| DELETE |
| route          	| BASE_URL/spectacles/{spectacle_id}|
| error types    	| SpectacleNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Спектакль успешно удален",
}
```
#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "SpectacleNotFound",
            "message": "Спектакль с таким id не найден."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе удаления спектакля возникли ошибки."
}
```

## Add Event

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| POST |
| route          	| BASE_URL/events|
| error types    	| SpectacleNotFound, HallNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### REQUEST DATA

```json
{
    "dated_at": "event_date",
    "description": "event_description"
    "is_premiere": true,
    "is_choosen_for_main_page": false,
    "available_seats_number": 145,
    "spectacle_id": 25,
    "hall_id": 2
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "event": {
        "id": 255,
    },
    "message": "Событие успешно добавлено."
}
```

#### RESPONSE DATA [FAIL]

>*Note*: 1) Возвращаются только найденные ошибки; 2) Перечислены все возможные ошибки.

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "SpectacleNotFound",
            "message": "Спектакль с таким id не найден."
        },
        {
            "type": "HallNotFound",
            "message": "Зал с таким id не найден."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе добавления события возникли ошибки."
}
```

## Update Event

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| PATCH |
| route          	| BASE_URL/events/{event_id}|
| error types    	| EventNotFound, SpectacleNotFound, HallNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### REQUEST DATA

```json
{
    "dated_at": "new_event_date",
    "description": "new_event_description"
    "is_premiere": false,
    "is_choosen_for_main_page": false,
    "available_seats_number": 234,
    "spectacle_id": 12,
    "hall_id": 1
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Событие успешно обновлено."
}
```

#### RESPONSE DATA [FAIL]

>*Note*: 1) Возвращаются только найденные ошибки; 2) Перечислены все возможные ошибки.

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "EventNotFound",
            "message": "Событие с таким id не найдено."
        },
        {
            "type": "SpectacleNotFound",
            "message": "Спектакль с таким id не найден."
        },
        {
            "type": "HallNotFound",
            "message": "Зал с таким id не найден."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе обновления информации о событии возникли ошибки."
}
```

## Get Event

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/event?id={event_id}|
| error types    	| EventNotFound |

#### RESPONSE DATA [SUCCESS]

>*Note*: 1) Возвращаются событие c id == event_id.

```json
{
    "has_errors": false,
    "errors": [],
    "event": {
        "dated_at": "event_date",
        "description": "event_description"
        "is_premiere": true,
        "is_choosen_for_main_page": false,
        "available_seats_number": 145,
        "spectacle_id": 25,
        "hall_id": 2
    }
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "EventNotFound",
            "message": "Событие с таким id не найдено."
        }
    ],
    "message": "В процессе получения информации о событии возникли ошибки."
}
```

## Get Events

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/events?from={date_range_start}&to={date_range_end}&name={spectacle_name}&theater_id={theater_id}|
| error types    	| TheaterNotFound, DateFormatError |

#### RESPONSE DATA [SUCCESS]

>*Note*: 1) Возвращаются все события, чья дата показа (dated_at) лежит в интервале [date_range_start;date_range_end], название спектакля содержит подстроку spectacle_name, а id театра равен theater_id. В примере ответа от сервера приведено 2 результата. 2) Если таких событий нет, соответственно, events будет пустым списком.

```json
{
    "has_errors": false,
    "errors": [],
    "events": [
        {
            "eventData": {
                "id": "event_id_1",
                "datedAt": "event_date_1",
                "description": "event_description_1",
                "is_premiere": "true/false",
                "available_seats_number": "available_seats_number_1"
            },
            "spectacleData": {
                "id": "spectacle_id_1",
                "name": "spectacle_name_1",
                "description": "spectacle_name_1",
                "poster": "spectacle_poster_1",
                "rate": "spectacle_rate_1"
            },
            "theaterData": {
                "id": "theater_id_1",
                "name": "theater_name_1",
                "logo": "theater_logo_1"
            },
        },
        {
            "eventData": {
                "id": "event_id_2",
                "datedAt": "event_date_2",
                "description": "event_description_2",
                "is_premiere": "true/false",
                "available_seats_number": "available_seats_number_2"
            },
            "spectacleData": {
                "id": "spectacle_id_2",
                "name": "spectacle_name_2",
                "description": "spectacle_name_2",
                "poster": "spectacle_poster_2",
                "rate": "spectacle_rate_2"
            },
            "theaterData": {
                "id": "theater_id_2",
                "name": "theater_name_2",
                "logo": "theater_logo_2"
            },
        },
    ]
}
```
#### RESPONSE DATA [FAIL]

>*Note*: 1) Возвращаются только найденные ошибки

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "TheaterNotFound",
            "message": "Театр с таким id не найден."
        },
        {
            "type": "DateFormatError",
            "message": "Неверный формат даты."
        }
    ],
    "message": "В процессе получения информации о событиях возникли ошибки."
}
```

## Delete Event

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| DELETE |
| route          	| BASE_URL/events/{event_id}|
| error types    	| EventNotFound, Permission Denied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Событие успешно удалено",
}
```
#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "EventNotFound",
            "message": "Событие с таким id не найдено."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе удаления события возникли ошибки."
}
```

## Get Premieres

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/events?is_premiere=true|
| error types    	|  |

#### RESPONSE DATA [SUCCESS]

>*Note*: 1) Возвращаются все события, чей параметр is_premiere == true. В примере ответа от сервера приведено 2 результата. 2) Если таких событий нет, соответственно, premieres будет пустым списком.

```json
{
    "has_errors": false,
    "errors": [],
    "premieres": [
        {
            "eventData": {
                "id": "event_id_1",
                "datedAt": "event_date_1",
                "description": "event_description_1",
                "available_seats_number": "available_seats_number_1"
            },
            "spectacleData": {
                "id": "spectacle_id_1",
                "name": "spectacle_name_1",
                "description": "spectacle_name_1",
                "poster": "spectacle_poster_1"
            },
            "theaterData": {
                "id": "theater_id_1",
                "name": "theater_name_1",
                "logo": "theater_logo_1"
            },
        },
        {
            "eventData": {
                "id": "event_id_2",
                "datedAt": "event_date_2",
                "description": "event_description_2",
                "available_seats_number": "available_seats_number_2"
            },
            "spectacleData": {
                "id": "spectacle_id_2",
                "name": "spectacle_name_2",
                "description": "spectacle_name_2",
                "poster": "spectacle_poster_2"
            },
            "theaterData": {
                "id": "theater_id_2",
                "name": "theater_name_2",
                "logo": "theater_logo_2"
            },
        }
    ]
}
```

## Get Main Page Premieres

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/events?is_choosen_for_main_page=true|
| error types    	|  |

#### RESPONSE DATA [SUCCESS]

>*Note*: 1) Возвращаются все события, чей параметр is_choosen_for_main_page == true. В примере ответа от сервера приведено 2 результата. 2) Если таких событий нет, соответственно, premieres будет пустым списком.

```json
{
    "has_errors": false,
    "errors": [],
    "premieres": [
        {
            "eventData": {
                "id": "event_id_1",
                "datedAt": "event_date_1",
                "description": "event_description_1",
                "available_seats_number": "available_seats_number_1"
            },
            "spectacleData": {
                "id": "spectacle_id_1",
                "name": "spectacle_name_1",
                "description": "spectacle_name_1",
                "sliderPoster": "spectacle_slider_poster_1"
            },
            "theaterData": {
                "id": "theater_id_1",
                "name": "theater_name_1",
                "logo": "theater_logo_1"
            },
        },
        {
            "eventData": {
                "id": "event_id_2",
                "datedAt": "event_date_2",
                "description": "event_description_2",
                "available_seats_number": "available_seats_number_2"
            },
            "spectacleData": {
                "id": "spectacle_id_2",
                "name": "spectacle_name_2",
                "description": "spectacle_name_2",
                "sliderPoster": "spectacle_slider_poster_2"
            },
            "theaterData": {
                "id": "theater_id_2",
                "name": "theater_name_2",
                "logo": "theater_logo_2"
            },
        }
    ]
}
```

## Add Theater

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| POST |
| route          	| BASE_URL/theaters|
| error types    	| PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### REQUEST DATA

```json
{
    "name": "theater_name",
    "description": "theater_description"
    "address": "theater_address",
    "logo": "theater_logo",
    "photo": "theater_photo",
    "preview": "theater_preview",
    "cash_desk_phone_number": "theater_cash_desk_phone_number",
    "phone_number_for_reference": "theater_phone_number_for_reference"
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "theater": {
        "id": 255,
    },
    "message": "Театр успешно добавлен."
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе добавления нового театра возникли ошибки."
}
```

## Update Theater

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| PATCH |
| route          	| BASE_URL/theaters/{theater_id}|
| error types    	| TheaterNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### REQUEST DATA

```json
{
    "name": "new_theater_name",
    "description": "new_theater_description"
    "address": "new_theater_address",
    "logo": "new_theater_logo",
    "photo": "new_theater_photo",
    "preview": "new_theater_preview",
    "cash_desk_phone_number": "new_theater_cash_desk_phone_number",
    "phone_number_for_reference": "new_theater_phone_number_for_reference"
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Театр успешно обновлен."
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "TheaterNotFound",
            "message": "Театр с таким id не найден."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе обновления информации о театре возникли ошибки."
}
```

## Get Theater

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/theaters?id={theater_id}|
| error types    	| TheaterNotFound |

#### RESPONSE DATA [SUCCESS]

>*Note*: 1) Возвращаются театр c id == theater_id.

```json
{
    "has_errors": false,
    "errors": [],
    "theater": {
            "id": 1,
            "name": "theater_name_1",
            "description": "theater_description_1"
            "address": "theater_address_1",
            "logo": "theater_logo_1",
            "photo": "theater_photo_1"
            "cash_desk_phone_number": "theater_cash_desk_phone_number_1",
            "phone_number_for_reference": "theater_phone_number_for_reference_1"
        }
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "TheaterNotFound",
            "message": "Театр с таким id не найден."
        }
    ],
    "message": "В процессе получения информации о театре возникли ошибки."
}
```

## Get Theaters

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/theaters|
| error types    	| |

#### RESPONSE DATA [SUCCESS]

>*Note*: 1) Возвращаются все театры. В примере ответа от сервера приведено 2 результата. 2) Если театров нет, theaters будет пустым списком.

```json
{
    "has_errors": false,
    "errors": [],
    "theaters": [
        {
            "id": 1,
            "name": "theater_name_1",
            "description": "theater_description_1"
            "address": "theater_address_1",
            "logo": "theater_logo_1",
            "photo": "theater_photo_1"
            "cash_desk_phone_number": "theater_cash_desk_phone_number_1",
            "phone_number_for_reference": "theater_phone_number_for_reference_1"
        },
        {
            "id": 2,
            "name": "theater_name_2",
            "description": "theater_description_2"
            "address": "theater_address_2",
            "logo": "theater_logo_2",
            "photo": "theater_photo_2"
            "cash_desk_phone_number": "theater_cash_desk_phone_number_2",
            "phone_number_for_reference": "theater_phone_number_for_reference_2"
        },
    ]
}
```

## Delete Theater

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| DELETE |
| route          	| BASE_URL/theaters/{theater_id}|
| error types    	| TheaterNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Театр успешно удален",
}
```
#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "TheaterNotFound",
            "message": "Театр с таким id не найден."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе удаления театра возникли ошибки."
}
```

## Get Theater Preview

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/theaters?id={theater_id}/preview|
| error types    	| TheaterNotFound |

#### RESPONSE DATA [SUCCESS]

>*Note*: 1) Возвращаются превью театра чей id == theater_id.

```json
{
    "has_errors": false,
    "errors": [],
    "preview": "theater_preview"
}
```
#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "TheaterNotFound",
            "message": "Театр с таким id не найден."
        }
    ],
    "message": "В процессе загрузки превью театра возникли ошибки."
}
```

## Get Spectacle Trailer

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/spectacles?id={spectacle_id}/trailer|
| error types    	| SpectacleNotFound |

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "trailer": "spectacle_trailer"
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "TheaterNotFound",
            "message": "Спектакль с таким id не найден."
        }
    ],
    "message": "В процессе загрузки трейлера спектакля возникли ошибки."
}
```

## Add Social Network

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| POST |
| route          	| BASE_URL/socialnetworks|
| error types    	| PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### REQUEST DATA

```json
{
    "name": "social_network_name",
    "logo": "social_network_logo"
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "social_network": {
        "id": 255,
    },
    "message": "Социальная сеть успешно добавлена."
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе добавления социальной сети возникли ошибки."
}
```

## Update Social Network

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| PATCH |
| route          	| BASE_URL/socialnetworks/{social_network_id}|
| error types    	| SocialNetworkNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### REQUEST DATA

```json
{
    "name": "new_social_network_name",
    "logo": "new_social_network_logo"
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Социальная сеть успешно обновлена."
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "SocialNetworkNotFound",
            "message": "Социальная сеть с таким id не найдена."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе обновления социальной сети возникли ошибки."
}
```

## Get Social Network

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/socialnetworks?id={social_network_id}|
| error types    	| SocialNetworkNotFound |

#### RESPONSE DATA [SUCCESS]

>*Note*: 1) Возвращаются социальная сеть c id == social_network_id.

```json
{
    "has_errors": false,
    "errors": [],
    "social_network": {
        "name": "social_network_name",
        "logo": "social_network_logo"
    }
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "SocialNetworkNotFound",
            "message": "Социальная сеть с таким id не найдена."
        }
    ],
    "message": "В процессе получения информации о социальной сети возникли ошибки."
}
```

## Delete Social Network

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| DELETE |
| route          	| BASE_URL/socialnetworks/{social_network_id}|
| error types    	| SocialNetworkNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Социальная сеть успешно удалена",
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "SocialNetworkNotFound",
            "message": "Социальная сеть с таким id не найдена."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе удаления социальной сети возникли ошибки."
}
```

## Add Theater Social Network Community Group

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| POST |
| route          	| BASE_URL/theaters/{theater_id}/socialnetworks/{social_network_id}|
| error types    	| PermissionDenied, TheaterNotFound, SocialNetworkNotFound |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### REQUEST DATA

```json
{
    "url_to_community": "theater_social_network_community_group_url"
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "social_network": {
        "id": 43
    },
    "message": "Группа театра в социальной сети успешно добавлена."
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        },
        {
            "type": "SocialNetworkNotFound",
            "message": "Социальная сеть с таким id не найдена."
        },
        {
            "type": "TheaterNotFound",
            "message": "Театр с таким id не найден."
        }
    ],
    "message": "В процессе добавления группы театра в социальной сети возникли ошибки."
}
```

## Update Theater Social Network Community Group

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| PATCH |
| route          	| BASE_URL/theaters/{theater_id}/socialnetworks/{social_network_id} |
| error types    	| SocialNetworkNotFound, TheaterNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### REQUEST DATA

```json
{
    "url_to_community": "new_theater_social_network_community_group_url"
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Группа театра в социальной сети успешно обновлена."
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        },
        {
            "type": "SocialNetworkNotFound",
            "message": "Социальная сеть с таким id не найдена."
        },
        {
            "type": "TheaterNotFound",
            "message": "Театр с таким id не найден."
        }
    ],
    "message": "В процессе обновления группы театра в социальной сети возникли ошибки."
}
```

## Get Theater Social Network Community Group

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/theaters/{theater_id}/socialnetworks/{social_network_id} |
| error types    	| SocialNetworkNotFound, TheaterNotFound, PermissionDenied |

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "url_to_community": "theater_social_network_community_group_url",
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        },
        {
            "type": "SocialNetworkNotFound",
            "message": "Социальная сеть с таким id не найдена."
        },
        {
            "type": "TheaterNotFound",
            "message": "Театр с таким id не найден."
        }
    ],
    "message": "В процессе получения информации о группе театра в социальной сети возникли ошибки."
}
```

## Get Theater Social Network Community Groups

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/theaters/{theater_id}/socialnetworks |
| error types    	| TheaterNotFound, PermissionDenied |

#### RESPONSE DATA [SUCCESS]

>*Note*: 1) Возвращаются все url на группы театра в социальной сети. В примере ответа от сервера приведено 2 результата. 2) Если групп нет, social_networks будет пустым списком.

```json
{
    "has_errors": false,
    "errors": [],
    "social_networks": [
        {
            "id": 1,
            "name": "social_network_name_1",
            "url_to_community": "theater_social_network_community_group_url_1",
            "logo": "social_network_logo_1"
        },
        {
            "id": 2,
            "name": "social_network_name_2",
            "url_to_community": "theater_social_network_community_group_url_2",
            "logo": "social_network_logo_2"
        }
    ]
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        },
        {
            "type": "TheaterNotFound",
            "message": "Театр с таким id не найден."
        }
    ],
    "message": "В процессе получения информации о группах театра в социальных сетях возникли ошибки."
}
```

## Delete Theater Social Network Community Group

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| DELETE |
| route          	| BASE_URL/theaters/{theater_id}/socialnetworks/{social_network_id} |
| error types    	| SocialNetworkNotFound, TheaterNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Информация о группе театра в социальной сети успешно удалена",
}
```
#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        },
        {
            "type": "SocialNetworkNotFound",
            "message": "Социальная сеть с таким id не найдена."
        },
        {
            "type": "TheaterNotFound",
            "message": "Театр с таким id не найден."
        }
    ],
    "message": "В процессе удаления группы театра в социальной сети возникли ошибки."
}
```
## Add Hall

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| POST |
| route          	| BASE_URL/halls|
| error types    	| TheaterNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### REQUEST DATA

```json
{
    "name": "hall_name",
    "scheme": "hall_scheme"
    "capacity": 156,
    "theater_id": "theater_id"
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "hall": {
        "id": 34
    }
    "message": "Зал успешно добавлен."
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "TheaterNotFound",
            "message": "Театр с таким id не найден."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе добавления зала возникли ошибки."
}
```

## Update Hall

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| PATCH |
| route          	| BASE_URL/halls/{hall_id}|
| error types    	| HallNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### REQUEST DATA

```json
{
    "name": "new_hall_name",
    "scheme": "new_hall_scheme"
    "capacity": 156
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Зал успешно обновлен."
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        },
        {
            "type": "HallNotFound",
            "message": "Зал с таким id не найден."
        }
    ],
    "message": "В процессе обновления информации о зале возникли ошибки."
}
```

## Get Hall

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/halls?id={hall_id}|
| error types    	| HallNotFound |

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "hall": {
        "id": 89,
        "name": "hall_name",
        "scheme": "hall_scheme"
        "capacity": 156,
        "theater_id": "theater_id"
    }
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "HallNotFound",
            "message": "Зал с таким id не найден."
        }
    ],
    "message": "В процессе получения информации о зале возникли ошибки."
}
```

## Get Theater Halls

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/halls?theater_id={theater_id}|
| error types    	| TheaterNotFound, PermissionDenied|

#### RESPONSE DATA [SUCCESS]

>*Note*: 1) Возвращаются все залы с трибутом id театра == theater_id. В примере ответа от сервера приведено 2 результата. 2) Если залов нет, halls будет пустым списком.

```json
{
    "has_errors": false,
    "errors": [],
    "halls": [
        {
            "id": 89,
            "name": "hall_name_1",
            "scheme": "hall_scheme_1"
            "capacity": 313,
            "theater_id": "theater_id_1"
        },
        {
            "id": 123,
            "name": "hall_name_2",
            "scheme": "hall_scheme_2"
            "capacity": 123,
            "theater_id": "theater_id_2"
        } 
    ]
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "TheaterNotFound",
            "message": "Театр с таким id не найден."
        }
    ],
    "message": "В процессе получения информации о залах театра возникли ошибки."
}
```

## Delete Hall

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| DELETE |
| route          	| BASE_URL/halls/{hall_id}|
| error types    	| HallNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Зал успешно удален",
}
```
#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "HallNotFound",
            "message": "Зал с таким id не найден."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе удаления зала возникли ошибки."
}
```

## Add Seats

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| POST |
| route          	| BASE_URL/seats|
| error types    	| HallNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

>*Note*: В request data содержится список "посадочных мест", которые необходимо добавить. В примере приведено 3, в общем случае количество мест в списке не ограничено (может быть в разы больше). Предусмотри ситацию с пустым списком (если в запросе не будет элементов в списке). local_id не сохраняется в базе!! см.комментарий к ответу на запрос

#### REQUEST DATA

```json
{
    "seats": [
        {
            "local_id": "0",
            "row": 23,
            "column": 15,
            "zone": "main",
            "hall_id": "hall_id_seat_is_bound_to"
        },
        {
            "local_id": "1",
            "row": 19,
            "column": 14,
            "zone": "parter",
            "hall_id": "hall_id_seat_is_bound_to"
        },
        {
            "local_id": "2",
            "row": 26,
            "column": 9,
            "zone": "balcony",
            "hall_id": "hall_id_seat_is_bound_to"
        }
    ]
}
```

#### RESPONSE DATA [SUCCESS]

>*Note*: В ответе тебе нужно вернуть id каждого добавленного в бд места, при этом завернуть его вместе с local_id, которое тебе пришло в запросе для однозначной обратной идентификации.

```json
{
    "has_errors": false,
    "errors": [],
    "seats": {
        {
            "local_id": 0,
            "id": 322
        },
        {
            "local_id": 1,
            "id": 323
        },
        {
            "local_id": 2,
            "id": 324
        }
    }
    "message": "Места в зале успешно добавлены."
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "HallNotFound",
            "message": "Зал с таким id не найден."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе добавления мест в зале возникли ошибки."
}
```

## Get Hall Seats

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/seats?hall_id={hall_id}|
| error types    	| HallNotFound |

>*Note*: 1) Возвращаются все места в зале атрибут hall_id которых равен id зала в запросе. В примере ответа от сервера приведено 3 результата. 2) Если записей о местах в зале нет, seats будет пустым списком.

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "seats": [
        {
            "id": "0",
            "row": 23,
            "column": 15,
            "zone": "main"
        },
        {
            "id": "1",
            "row": 19,
            "column": 14,
            "zone": "parter"
        },
        {
            "id": "2",
            "row": 26,
            "column": 9,
            "zone": "balcony"
        }
    ]
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "HallNotFound",
            "message": "Зал с таким id не найден."
        }
    ],
    "message": "В процессе получения информации о местах в зале возникли ошибки."
}
```

## Delete Seats

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| PATCH |
| route          	| BASE_URL/seats?hall_id={hall_id}|
| error types    	| HallNotFound, SeatNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

>*Note*: Метод запроса - PATCH, это не ошибка. Дело в том, что необходимо иметь возможность удалять сразу несколько записей из таблицы "Место". В нагрузке запроса будет список id мест, которые необходимо удалить. Это один из подходов к решению проблемы о множественном удалении. Количество мест для удаления неограничено.

#### REQUEST DATA

```json
{
    "seats_to_delete": [23, 25, 324, 1234, 23, 123]
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Информация о местах в зале успешно удалена",
}
```
#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "HallNotFound",
            "message": "Зал с таким id не найден."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        },
        {
            "type": "SeatNotFound",
            "message": "Место с id = {seat_id} не найдено."
        },
    ],
    "message": "В процессе удаления информации о местах в зале возникли ошибки."
}
```

## Add Tickets

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| POST |
| route          	| BASE_URL/tickets|
| error types    	| EventNotFound, SeatNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

>*Note*: В request data содержится список билетов, которые необходимо добавить. В примере приведено 3, в общем случае количество билетов в списке не ограничено (может быть в разы больше). Предусмотри ситацию с пустым списком (если в запросе не будет элементов в списке). local_id не сохраняется в базе!! см.комментарий к ответу на запрос. Атрибут is_bought не будет приходить в запросе, поскольку при добавлении билета его дефолтное значение is_bought = false.

#### REQUEST DATA

```json
{
    "tickets": [
        {
            "local_id": 0,
            "price": 1500,
            "event_id": 255,
            "seat_id": 24
        },
        {
            "local_id": 1,
            "price": 1400,
            "event_id": 255,
            "seat_id": 23
        },
        {
            "local_id": 2,
            "price": 2322,
            "event_id": 255,
            "seat_id": 16
        }
    ]
}
```

#### RESPONSE DATA [SUCCESS]

>*Note*: В ответе тебе нужно вернуть id каждого добавленного в бд билета, при этом завернуть его вместе с local_id, которое тебе пришло в запросе для однозначной обратной идентификации.

```json
{
    "has_errors": false,
    "errors": [],
    "tickets": {
        {
            "local_id": 0,
            "id": 322
        },
        {
            "local_id": 1,
            "id": 323
        },
        {
            "local_id": 2,
            "id": 324
        }
    }
    "message": "Билеты успешно добавлены."
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "EventNotFound",
            "message": "Событие с таким id не найдено."
        },
        {
            "type": "SeatNotFound",
            "message": "Место с id = {seat_id} не найдено."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе добавления билетов возникли ошибки."
}
```

## Get Event Tickets

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/tickets?event_id={event_id}|
| error types    	| EventNotFound |

>*Note*: 1) Возвращаются все билеты атрибут event_id которых равен id события в запросе. В примере ответа от сервера приведено 3 результата. 2) Если записей о билетах на событие нет, tickets будет пустым списком.

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "tickets": [
        {
            "ticket_id": 0,
            "price": 1500,
            "is_bought": false,
            "seat_id": 24
        },
        {
            "ticket_id": 1,
            "price": 1400,
            "is_bought": true,
            "seat_id": 23
        },
        {
            "ticket_id": 2,
            "price": 2322,
            "is_bought": false,
            "seat_id": 16
        }
    ]
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "EventNotFound",
            "message": "Событие с таким id не найдено."
        }
    ],
    "message": "В процессе получения информации о билетах возникли ошибки."
}
```

## Get Event Ticket

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/tickets?id={ticket_id}|
| error types    	| TicketNotFound |


#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "ticket": {
            "price": 1500,
            "is_bought": false,
            "seat_id": 24,
            "event_id": 255
        }
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "TicketNotFound",
            "message": "Билет с таким id не найден."
        }
    ],
    "message": "В процессе получения информации о билете возникли ошибки."
}
```

## Update Tickets

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| PATCH |
| route          	| BASE_URL/tickets|
| error types    	| TicketNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

>*Note*: В request data содержится список билетов, информацию о которых необходимо обновить. В примере приведено 3, в общем случае количество билетов в списке не ограничено (может быть в разы больше). Предусмотри ситацию с пустым списком (если в запросе не будет элементов в списке).

#### REQUEST DATA

```json
{
    "tickets": [
        {
            "ticket_id": 0,
            "price": 1500,
            "is_bought": true
        },
        {
            "ticket_id": 1,
            "price": 1400,
            "is_bought": true
        },
        {
            "ticket_id": 2,
            "price": 2322,
            "is_bought": false
        }
    ]
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Информация о билетах успешно обновлена."
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "TicketNotFound",
            "message": "Билет с таким id не найден."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе обновления билетов возникли ошибки."
}
```

## Delete Seats

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| PATCH |
| route          	| BASE_URL/ticket?event_id={event_id}|
| error types    	| EventNotFound, TicketNotFound PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

>*Note*: Метод запроса - PATCH, это не ошибка. Дело в том, что необходимо иметь возможность удалять сразу несколько записей из таблицы "Билет". В нагрузке запроса будет список id билетов, которые необходимо удалить. Это один из подходов к решению проблемы о множественном удалении. Количество билетов для удаления неограничено.

#### REQUEST DATA

```json
{
    "tickets_to_delete": [23, 25, 324, 1234, 23, 123]
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Информация о билетах успешно удалена",
}
```
#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "EventNotFound",
            "message": "Событие с таким id не найдено."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        },
        {
            "type": "TicketNotFound",
            "message": "Билет с id = {ticket_id} не найден."
        },
    ],
    "message": "В процессе удаления информации о билетах возникли ошибки."
}
```

## Tickets Purchase

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| POST |
| route          	| BASE_URL/buytickets|
| error types    	| TicketNotFound, UserNotFound |

>*Note*: 1) В request data содержится информация о транзакции, id пользователя купившего билеты (user_id будет равен null если билеты будет покупать неавторизованный пользователь), а также список id билетов, которые были куплены (в примере приведено 3, в общем случае количество билетов в списке ограничено 5 билетами для одной транзакции). 2) Предполагается следующая последовательность записи данных в БД - 1. добавляется информация о транзакции; 2. теперь, когда у тебя есть id транзакции, ты добавляешь информацию в таблицу "Ticket Bought By User" о всех купленных билетах + в таблице "Ticket" у всех билетов с соответствующими id необходимо атрибут is_bought переопределить в true. 3) В случае если билеты покупает неавторизованный пользователь (user_id = null), можно вешать покупки на некоторого ананимного (зарезервированного) пользователя.

#### REQUEST DATA

```json
{
    "transaction": {
        "date_time": "performed_at_date",
        "total_cost": 23423
    },
    "user_id": 34,
    "tickets_id": [23, 432, 23, 12, 4]
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Покупка прошла успешно."
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "TicketNotFound",
            "message": "Билет  с id = {ticket_id} не найден."
        },
        {
            "type": "UserNotFound",
            "message": "Пользователь с таким id не найден."
        }
    ],
    "message": "В процессе покупки билетов возникли ошибки."
}
```
