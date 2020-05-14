# API v2.0.0

>*updates*:
>1. добавлено API для изменения профиля пользователя
>2. добавлено API для получения профиля пользователя
>3. добавлено API для добавления новой закладки пользователя
>4. добавлено API для удаления закладки пользователя
>5. добавлено API для получения закладок пользователя
>6. добавлено API для получения истории покупок пользователя
>7. добавлено API для получения написанных пользователем отзывов
>8. добавлено API для добавления спектакля
>9. добавлено API для изменения спектакля
>10. добавлено API для получения спектакля
>11. добавлено API для получения спектаклей
>12. добавлено API для получения событий
>13. добавлено API для получения премьер
>14. добавлено API для получения прьмьер для слайдера
>15. добавлено API для добавления театра
>16. добавлено API для изменения театра
>17. добавлено API для получения театров
>18. добавлено API для получения театра
>19. добавлено API для получения превью театра
>20. добавлено API для получения тизера спектакля

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
    "message": null
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
    "message": null
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
    "message": null
}
```
## Update User Profile

|attribute          |value         	        |
|----------------	|-------------------	|
| request method 	| PATCH|
| route          	| BASE_URL/user/{{user_id}}|
| error types    	| UserNotFound|

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
        }
    ],
    "message": "В процессе обновления возникли ошибки. Новая информация о Вашем профиле не сохранена."
}
```
## Get User Profile

|attribute          |value         	        |
|----------------	|-------------------	|
| request method 	| GET|
| route          	| BASE_URL/user?id={{user_id}}|
| error types    	| UserNotFound|

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
        }
    ]
}
```
## Add User Bookmark

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| POST |
| route          	| BASE_URL/user/{{user_id}}/bookmarks|
| error types    	| UserNotFound, SpectacleNotFound |

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
        }
    ]
}
```
## Delete User Bookmark

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| DELETE |
| route          	| BASE_URL/user/{{user_id}}/bookmarks/{{spectacle_id}}|
| error types    	| UserNotFound, BookmarkNotFound |

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
        }
    ]
}
```

## Get User Bookmarks

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/user/{{user_id}}/bookmarks|
| error types    	| UserNotFound |

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
        }
    ]
}
```

## Get User Purchase History

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/user/{{user_id}}/tickets|
| error types    	| UserNotFound |

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
        }
    ]
}
```
## Get User Commetns

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/user/{{user_id}}/comments|
| error types    	| UserNotFound |

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
        }
    ]
}
```

## Add Spectacle

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| POST |
| route          	| BASE_URL/spectacles|
| error types    	| TheaterNotFound |

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
        }
    ]
}
```

## Update Spectacle

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| PATCH |
| route          	| BASE_URL/spectacles/{{spectacle_id}}|
| error types    	| SpectacleNotFound |

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

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "SpectacleNotFound",
            "message": "Спектакль с таким id не найден."
        }
    ]
}
```

## Get Spectacle

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/spectacles?id={{spectacle_id}}|
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
            "type": "TheaterNotFound",
            "message": "Театр с таким id не найден."
        }
    ]
}
```

## Get Spectacles

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

## Get Events

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/events?from={{date_range_start}}&to={{date_range_end}}&name={{spectacle_name}}&theater_id={{theater_id}}|
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
    ]
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
| error types    	|  |

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
    "message": "Театр успешно добавлен."
}
```

## Update Theater

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| PATCH |
| route          	| BASE_URL/theaters/{{theater_id}}|
| error types    	| TheaterNotFound |

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
#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "TheaterNotFound",
            "message": "Театр с таким id не найден."
        }
    ]
}
```

## Get Theater

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/theaters?id={{theater_id}}|
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
    ]
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

## Get Theater Preview

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/theaters?id={{theater_id}}/preview|
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
    ]
}
```

## Get Spectacle Trailer

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/spectacles?id={{spectacle_id}}/trailer|
| error types    	| SpectacleNotFound |

#### RESPONSE DATA [SUCCESS]

>*Note*: 1) Возвращаются тизер спектаклся чей id == theater_id.

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
    ]
}
```
