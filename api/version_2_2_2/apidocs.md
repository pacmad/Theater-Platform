# API v2.2.2

>*updates*:
>1. упразднены следущие API - Password Reset Request, Password Reset, Email Verification
>2. 

>*Note:* * в содержании отмечены API, которые должны быть реализованы в следующем пуле.

## Table Of Contents

1. [Registration](#registration)
2. [Authorization](#authorization)
3. [Logout](#logout)
4. [Update User Profile](#update-user-profile)
5. [Get User Profile](#get-user-profile)
6. [Add User Bookmark](#add-user-bookmark)
7. [Delete User Bookmark](#delete-user-bookmark)
8. [Get User Bookmarks](#get-user-bookmarks)
9. [Get User Purchase History](#get-user-purchase-history)
10. [Get User Commetns](#get-user-commetns)
11. [Add Comment](#add-comment)
12. [Update Comment](#update-comment)
13. [Get Spectacle Comments](#get-spectacle-comments)
14. [Comment Verification](#comment-verification)
15. [Delete Comment](#delete-comment)
16. [Add Spectacle](#add-spectacle) *
17. [Update Spectacle](#update-spectacle) *
18. [Get Spectacle](#get-spectacle) *
19. [Get Spectacles](#get-spectacles) *
20. [Delete Spectacle](#delete-spectacle) *
21. [Add Event](#add-event) *
22. [Update Event](#update-event) *
23. [Get Event](#get-event) *
24. [Get Events](#get-events) *
25. [Delete Event](#delete-event) *
26. [Get Premieres](#get-premieres) *
27. [Get Main Page Premieres](#get-main-page-premieres) *
28. [Add Theater](#add-theater) *
29. [Update Theater](#update-theater) *
30. [Get Theater](#get-theater) *
31. [Get Theaters](#get-theaters) *
32. [Delete Theater](#delete-theater) *
33. [Get Theater Preview](#get-theater-preview)
34. [Get Spectacle Trailer](#get-spectacle-trailer)
35. [Add Social Network](#add-social-network)
36. [Update Social Network](#update-social-social)
37. [Get Social Network](#get-social-social)
38. [Delete Social Network](#delete-social-social)
39. [Add Theater Social Network Community Group](#add-theater-social-network-community-group)
40. [Update Theater Social Network Community Group](#update-theater-social-network-community-group)
41. [Get Theater Social Network Community Group](#get-theater-social-network-community-group)
42. [Get Theater Social Network Community Groups](#get-theater-social-network-community-groups)
43. [Delete Theater Social Network Community Group](#delete-theater-social-network-community-group)
44. [Add Hall](#add-hall)
45. [Update Hall](#update-hall)
46. [Get Hall](#get-hall)
47. [Get Theater Halls](#get-theater-halls)
48. [Delete Hall](#delete-hall)
49. [Add Seats](#add-seats)
50. [Get Hall Seats](#get-hall-seats)
51. [Delete Seats](#delete-seats)
52. [Add Tickets](#add-tickets) *
53. [Get Event Tickets](#get-event-tickets) *
54. [Get Event Ticket](#get-event-ticket) *
55. [Update Event Tickets](#update-event-tickets) *
56. [Delete Tickets](#delete-tickets) *
57. [Tickets Purchase](#tickets-purchase)
58. [Add Actor](#add-actor)
59. [Update Actor](#update-actor)
60. [Get Actor](#get-actor)
61. [Delete Actor](#delete-actor)
62. [Add Actors to Spectacle](#add-actors-to-spectacle)
63. [Get Spectacle Actors](#get-spectacle-actors)
64. [Delete Actors From Spectacle](#delete-actors-from-spectacle)
65. [Add Producer](#add-producer)
66. [Update Producer](#update-producer)
67. [Get Producer](#get-producer)
68. [Delete Producer](#delete-producer)
69. [Add Producers to Spectacle](#add-producer-to-spectacle)
70. [Get Spectacle Producers](#get-spectacle-producers)
71. [Delete Producers From Spectacle](#delete-producers-from-spectacle)
72. [Add Author](#add-author)
73. [Update Author](#update-author)
74. [Get Author](#get-author)
75. [Delete Author](#delete-author)
76. [Add Authors to Spectacle](#add-authors-to-spectacle)
77. [Get Spectacle Authors](#get-spectacle-authors)
78. [Delete Authors From Spectacle](#delete-authors-from-spectacle)
79. [Add Artist](#add-artist)
80. [Update Artist](#update-artist)
81. [Get Artist](#get-artist)
82. [Delete Artist](#delete-artist)
83. [Add Artists to Spectacle](#add-artists-to-spectacle)
84. [Get Spectacle Artists](#get-spectacle-artists)
85. [Delete Artists From Spectacle](#delete-artists-from-spectacle)


BASE_URL  http://host1813162.hostland.pro/api

## Registration

[<-- Back to Table Of Contents](#table-of-contents)

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
    "password": "somepassword",
    "password_confirmation": "somepassword",
    "is_admin": false
}
```
#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Регистрация прошла успешно. Вы были перенаправлены на страницу авторизации.",
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

[<-- Back to Table Of Contents](#table-of-contents)

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
        "is_admin": false
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

[<-- Back to Table Of Contents](#table-of-contents)

|attribute          |value         	        |
|----------------	|-------------------	|
| request method 	| POST              	|
| route          	| BASE_URL/logout    	|
| required headers  | Authorization         |

>*Note*: Формально логаут это удаление токена, т.е. никакие дополнительные данные не нужны. Токен будет в приведенном хэдере запроса. 

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Вы успешно вышли из системы.",
}
```

## Update User Profile

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

## Add Comment

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| POST |
| route          	| BASE_URL/comments|
| error types    	| SpectacleNotFound, UserNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

>*Note*:  При добавлении комменатрия в нагрузке запроса отсутствуют атрибуты created_at (штампуется на стророне сервера) и is_confirmed (при создании комментарий не может быть подтвержден модератором, т.е. дефолтное значение is_confirmed = false).

#### REQUEST DATA

```json
{
    "content": "comment_content",
    "rate": 5,
    "spectacle_id": 232,
    "user_id": 23
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "comment": {
        "id": 233,
    },
    "message": "Комментарий успешно добавлен и ожидает подтверждения модератором."
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
            "type": "UserNotFound",
            "message": "Пользователь с таким id не найден."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе добавления комментария возникли ошибки."
}
```

## Update Comment

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| PATCH |
| route          	| BASE_URL/comments/{comment_id}|
| error types    	| CommentNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### REQUEST DATA

```json
{
    "content": "new_comment_content",
    "rate": 3,
    "is_confirmed": false
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Комментарий успешно обновлен и ожидает подтверждения модератором."
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "CommentNotFound",
            "message": "Комментарий с таким id не найден."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе обновления комментария возникли ошибки."
}
```

## Get Spectacle Comments

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/comments?spectacle_id={spectacle_id}&is_confirmed=true|
| error types    	| SpectacleNotFound |

>*Note*: Возвращаются все комментарии к спектаклю с id = spectacle_id, при этом только подтвердженные модератором (is_confirmed = true). В примере приведено 3 комменатрия. Если комментариев удовлетворяющих условиям нет, commets будет пустым списком.

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "comments": [
            {
                "id": 34,
                "content": "comment_content_1",
                "rate": 5,
                "createdAt": "comment_created_at_1"
            },
            {
                "id": 123,
                "content": "comment_content_2",
                "rate": 3,
                "createdAt": "comment_created_at_2"
            },
            {
                "id": 1233,
                "content": "comment_content_3",
                "rate": 4,
                "createdAt": "comment_created_at_3"
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
            "type": "SpectacleNotFound",
            "message": "Спекталь с таким id не найден."
        }
    ],
    "message": "В процессе получения комментариев к спектаклю возникли ошибки."
}
```

## Comment Verification

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/comments/verify/{comment_id}|
| error types    	| CommentNotFound, PermissionDenied|
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### RESPONSE DATA [SUCCESS]

>*Note*: 1) Атрибут is_confirmed комментария с id = comment_id устанавливается в true.

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Комментарий подтвержден"
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "CommentNotFound",
            "message": "Комментарий с таким id не найден."
        }
    ],
    "message": "В процессе верификации комментария произошли ошибки."
}
```

## Delete Comment

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| DELETE |
| route          	| BASE_URL/comments/{comment_id}|
| error types    	| CommentNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Комментарий успешно удален",
}
```
#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "CommentNotFound",
            "message": "Комментарий с таким id не найден."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе удаления комментария возникли ошибки."
}
```

## Add Spectacle

[<-- Back to Table Of Contents](#table-of-contents)

UPDATED

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
    "description": "spectacle_description",
    "rate": 0,
    "duration": 90,
    "year": 2019,
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

[<-- Back to Table Of Contents](#table-of-contents)

UPDATED

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
    "description": "new_spectacle_description",
    "rate": 0,
    "duration": 90,
    "year": 2019,
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

[<-- Back to Table Of Contents](#table-of-contents)

UPDATED

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
        "description": "spectacle_description",
        "rate": 4.7,
        "duration": 90,
        "year": 2019,
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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

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

## Delete Tickets

[<-- Back to Table Of Contents](#table-of-contents)

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

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| POST |
| route          	| BASE_URL/buytickets|
| error types    	| TicketNotFound, UserNotFound |

>*Note*: 1) В request data содержится информация о транзакции, id пользователя купившего билеты (user_id будет равен null если билеты будет покупать неавторизованный пользователь), а также список id билетов, которые были куплены (в примере приведено 3, в общем случае количество билетов в списке ограничено 5 билетами для одной транзакции). 2) Предполагается следующая последовательность записи данных в БД - 1. добавляется информация о транзакции; 2. теперь, когда у тебя есть id транзакции, ты добавляешь информацию в таблицу "Ticket Bought By User" о всех купленных билетах + в таблице "Ticket" у всех билетов с соответствующими id необходимо атрибут is_bought переопределить в true; 3. в конце добавляешь запись в таблицу "Spectacle Visited by User". 3) В случае если билеты покупает неавторизованный пользователь (user_id = null), можно вешать покупки на некоторого ананимного (зарезервированного) пользователя.

#### REQUEST DATA

```json
{
    "transaction": {
        "date_time": "performed_at_date",
        "total_cost": 23423
    },
    "user_id": 34,
    "event_id": 232,
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

## Add Actor

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| POST |
| route          	| BASE_URL/actors|
| error types    	| PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### REQUEST DATA

```json
{
    "surname": "actor_surname",
    "name": "actor_name"
    "middle_name": "actor_middle_name",
    "life": "actor_life",
    "photo": "actor_photo"
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "actor": {
        "id": 255,
    },
    "message": "Актер успешно добавлен."
}
```

#### RESPONSE DATA [FAIL]

>*Note*: 1) Возвращаются только найденные ошибки

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе добавления актера возникли ошибки."
}
```

## Update Actor

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| PATCH |
| route          	| BASE_URL/actors/{actor_id}|
| error types    	| ActorNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### REQUEST DATA

```json
{
    "surname": "new_actor_surname",
    "name": "new_actor_name"
    "middle_name": "new_actor_middle_name",
    "life": "new_actor_life",
    "photo": "new_actor_photo"
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Информация об актере успешно обновлена."
}
```

#### RESPONSE DATA [FAIL]

>*Note*: 1) Возвращаются только найденные ошибки; 2) Перечислены все возможные ошибки.

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "ActorNotFound",
            "message": "Актер с таким id не найден."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе обновления информации об актере возникли ошибки."
}
```

## Get Actor

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/actors?id={actor_id}|
| error types    	| ActorNotFound |

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "actor": {
        "surname": "actor_surname",
        "name": "actor_name"
        "middle_name": "actor_middle_name",
        "life": "actor_life",
        "photo": "actor_photo"
    }
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "ActorNotFound",
            "message": "Актер с таким id не найден."
        }
    ],
    "message": "В процессе получения информации об актере возникли ошибки."
}
```

## Delete Actor

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| DELETE |
| route          	| BASE_URL/actors/{actor_id}|
| error types    	| ActorNotFound, Permission Denied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Информация об актере успешно удалена",
}
```
#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "ActorNotFound",
            "message": "Актер с таким id не найден."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе удаления информации об актере возникли ошибки."
}
```

## Add Actors to Spectacle

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| POST |
| route          	| BASE_URL/theaters/{theater_id}/spectacles/{spectacle_id}/actors|
| error types    	| TheaterNotFound, SpectacleNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

>*Note*: В request data содержится список актеров спектакля (id актера и его роль в спектакле), которые необходимо добавить. В примере приведено 3, в общем случае количество актеров в списке не ограничено (может быть в разы больше). Предусмотри ситацию с пустым списком (если в запросе не будет элементов в списке).

#### REQUEST DATA

```json
{
    "actors": [
        {
            "actor_id": 434,
            "role": "role_in_spectacle"
        },
        {
            "actor_id": 32,
            "role": "role_in_spectacle"
        },
        {
            "actor_id": 1,
            "role": "role_in_spectacle"
        }
    ]
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Актеры успешно добавлены в спектакль."
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
            "type": "SpectacleNotFound",
            "message": "Спектакль с таким id не найден."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе добавления актеров в спектакль возникли ошибки."
}
```

## Get Spectacle Actors

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/actors?spectacle_id={spectacle_id}|
| error types    	| SpectacleNotFound, PermissionDenied |
| required headers  | Authorization         |

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "actors": [
        {   
            "id": 342,
            "surname": "actor_surname",
            "name": "actor_name"
            "middle_name": "actor_middle_name",
            "life": "actor_life",
            "photo": "actor_photo"
        },
        {   
            "id": 34,
            "surname": "actor_surname",
            "name": "actor_name"
            "middle_name": "actor_middle_name",
            "life": "actor_life",
            "photo": "actor_photo"
        },
        {   
            "id": 786,
            "surname": "actor_surname",
            "name": "actor_name"
            "middle_name": "actor_middle_name",
            "life": "actor_life",
            "photo": "actor_photo"
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
            "type": "SpectacleNotFound",
            "message": "Спектакль с таким id не найден."
        }
    ],
    "message": "В процессе получения информации об актерах спектакля возникли ошибки."
}
```

## Delete Actors From Spectacle

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| PATCH |
| route          	| BASE_URL/actors?spectacle_id={spectacle_id}|
| error types    	| SpectacleNotFound, ActorNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

>*Note*: Метод запроса - PATCH, это не ошибка. Дело в том, что необходимо иметь возможность удалять сразу несколько записей из таблицы "Spectacle Actor". В нагрузке запроса будет список id актеров, которые необходимо удалить из данной таблицы. Это один из подходов к решению проблемы о множественном удалении. Количество актеров для удаления из спектакля неограничено.

#### REQUEST DATA

```json
{
    "actors_to_delete": [23, 25, 324, 1234, 23, 123]
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Актеры успешно удалены из спектакля",
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
        },
        {
            "type": "ActorNotFound",
            "message": "Актер с id = {actor_id} не найден."
        },
    ],
    "message": "В процессе удаления актеров из спектакля возникли ошибки."
}
```

## Add Producer

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| POST |
| route          	| BASE_URL/producers|
| error types    	| PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### REQUEST DATA

```json
{
    "surname": "producer_surname",
    "name": "producer_name"
    "middle_name": "producer_middle_name",
    "life": "producer_life",
    "photo": "producer_photo"
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "producer": {
        "id": 255,
    },
    "message": "Продюсер успешно добавлен."
}
```

#### RESPONSE DATA [FAIL]

>*Note*: 1) Возвращаются только найденные ошибки

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе добавления продюсера возникли ошибки."
}
```

## Update Producer

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| PATCH |
| route          	| BASE_URL/producers/{producer_id}|
| error types    	| ProducerNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### REQUEST DATA

```json
{
    "surname": "new_producer_surname",
    "name": "new_producer_name"
    "middle_name": "new_producer_middle_name",
    "life": "new_producer_life",
    "photo": "new_producer_photo"
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Информация о продюсере успешно обновлена."
}
```

#### RESPONSE DATA [FAIL]

>*Note*: 1) Возвращаются только найденные ошибки; 2) Перечислены все возможные ошибки.

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "ProducerNotFound",
            "message": "Продюсер с таким id не найден."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе обновления информации о продюсере возникли ошибки."
}
```

## Get Producer

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/producers?id={producer_id}|
| error types    	| ProducerNotFound |

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "producer": {
        "surname": "producer_surname",
        "name": "producer_name"
        "middle_name": "producer_middle_name",
        "life": "producer_life",
        "photo": "producer_photo"
    }
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "ProducerNotFound",
            "message": "Продюсер с таким id не найден."
        }
    ],
    "message": "В процессе получения информации о продюсере возникли ошибки."
}
```

## Delete Producer

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| DELETE |
| route          	| BASE_URL/producers/{producer_id}|
| error types    	| ProducerNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Информация о продюсере успешно удалена",
}
```
#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "ProducerNotFound",
            "message": "Продюсер с таким id не найден."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе удаления информации о продюсере возникли ошибки."
}
```

## Add Producers to Spectacle

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| POST |
| route          	| BASE_URL/theaters/{theater_id}/spectacles/{spectacle_id}/producers|
| error types    	| TheaterNotFound, SpectacleNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

>*Note*: В request data содержится список продюсеров спектакля (id продюсера), которые необходимо добавить. В примере приведено 3, в общем случае количество продюсеров в списке не ограничено (может быть в разы больше). Предусмотри ситацию с пустым списком (если в запросе не будет элементов в списке).

#### REQUEST DATA

```json
{
    "producers": [
        {
            "id": 434
        },
        {
            "id": 32
        },
        {
            "id": 1
        }
    ]
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Продюсеры спектакля успешно добавлены."
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
            "type": "SpectacleNotFound",
            "message": "Спектакль с таким id не найден."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе добавления продюсеров в спектакль возникли ошибки."
}
```

## Get Spectacle Producers

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/producers?spectacle_id={spectacle_id}|
| error types    	| SpectacleNotFound, PermissionDenied |
| required headers  | Authorization         |

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "producers": [
        {   
            "id": 342,
            "surname": "producer_surname",
            "name": "producer_name"
            "middle_name": "producer_middle_name",
            "life": "producer_life",
            "photo": "producer_photo"
        },
        {   
            "id": 34,
            "surname": "producer_surname",
            "name": "producer_name"
            "middle_name": "producer_middle_name",
            "life": "producer_life",
            "photo": "producer_photo"
        },
        {   
            "id": 786,
            "surname": "producer_surname",
            "name": "producer_name"
            "middle_name": "producer_middle_name",
            "life": "producer_life",
            "photo": "producer_photo"
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
            "type": "SpectacleNotFound",
            "message": "Спектакль с таким id не найден."
        }
    ],
    "message": "В процессе получения информации о продюсерах спектакля возникли ошибки."
}
```

## Delete Producers From Spectacle

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| PATCH |
| route          	| BASE_URL/producers?spectacle_id={spectacle_id}|
| error types    	| SpectacleNotFound,  ProducerNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

>*Note*: Метод запроса - PATCH, это не ошибка. Дело в том, что необходимо иметь возможность удалять сразу несколько записей из таблицы "Spectacle Producer". В нагрузке запроса будет список id продюсеров, которые необходимо удалить из данной таблицы. Это один из подходов к решению проблемы о множественном удалении. Количество продюсеров для удаления из спектакля неограничено.

#### REQUEST DATA

```json
{
    "producers_to_delete": [23, 25, 324, 1234, 23, 123]
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Продюсеры успешно удалены из спектакля",
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
        },
        {
            "type": "ProducerNotFound",
            "message": "Продюсер с id = {producer_id} не найден."
        },
    ],
    "message": "В процессе удаления продюсеров из спектакля возникли ошибки."
}
```

## Add Author

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| POST |
| route          	| BASE_URL/authors|
| error types    	| PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### REQUEST DATA

```json
{
    "surname": "author_surname",
    "name": "author_name"
    "middle_name": "author_middle_name",
    "life": "author_life",
    "photo": "author_photo"
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "author": {
        "id": 255,
    },
    "message": "Автор успешно добавлен."
}
```

#### RESPONSE DATA [FAIL]

>*Note*: 1) Возвращаются только найденные ошибки

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе добавления автора возникли ошибки."
}
```

## Update Author

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| PATCH |
| route          	| BASE_URL/authors/{author_id}|
| error types    	| AuthorNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### REQUEST DATA

```json
{
    "surname": "new_author_surname",
    "name": "new_author_name"
    "middle_name": "new_author_middle_name",
    "life": "new_author_life",
    "photo": "new_author_photo"
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Информация об авторе успешно обновлена."
}
```

#### RESPONSE DATA [FAIL]

>*Note*: 1) Возвращаются только найденные ошибки; 2) Перечислены все возможные ошибки.

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "AuthorNotFound",
            "message": "Автор с таким id не найден."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе обновления информации об авторе возникли ошибки."
}
```

## Get Author

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/authors?id={author_id}|
| error types    	| AuthorNotFound |

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "author": {
        "surname": "new_author_surname",
        "name": "new_author_name"
        "middle_name": "new_author_middle_name",
        "life": "new_author_life",
        "photo": "new_author_photo"
    }
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "AuthorNotFound",
            "message": "Автор с таким id не найден."
        }
    ],
    "message": "В процессе получения информации об авторе возникли ошибки."
}
```

## Delete Author

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| DELETE |
| route          	| BASE_URL/authors/{author_id}|
| error types    	| AuthorNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Информация об авторе успешно удалена",
}
```
#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "AuthorNotFound",
            "message": "Автор с таким id не найден."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе удаления информации об авторе возникли ошибки."
}
```

## Add Authors to Spectacle

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| POST |
| route          	| BASE_URL/theaters/{theater_id}/spectacles/{spectacle_id}/authors|
| error types    	| TheaterNotFound, SpectacleNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

>*Note*: В request data содержится список авторов спектакля (id автора), которые необходимо добавить. В примере приведено 3, в общем случае количество авторов в списке не ограничено (может быть в разы больше). Предусмотри ситацию с пустым списком (если в запросе не будет элементов в списке).

#### REQUEST DATA

```json
{
    "authors": [
        {
            "id": 434
        },
        {
            "id": 32
        },
        {
            "id": 1
        }
    ]
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Авторы спектакля успешно добавлены."
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
            "type": "SpectacleNotFound",
            "message": "Спектакль с таким id не найден."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе добавления продюсеров в спектакль возникли ошибки."
}
```

## Get Spectacle Authors

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/authors?spectacle_id={spectacle_id}|
| error types    	| SpectacleNotFound, PermissionDenied |
| required headers  | Authorization         |

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "authors": [
        {   
            "id": 342,
            "surname": "author_surname",
            "name": "author_name"
            "middle_name": "author_middle_name",
            "life": "author_life",
            "photo": "author_photo"
        },
        {   
            "id": 34,
            "surname": "author_surname",
            "name": "author_name"
            "middle_name": "author_middle_name",
            "life": "author_life",
            "photo": "author_photo"
        },
        {   
            "id": 786,
            "surname": "author_surname",
            "name": "author_name"
            "middle_name": "author_middle_name",
            "life": "author_life",
            "photo": "author_photo"
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
            "type": "SpectacleNotFound",
            "message": "Спектакль с таким id не найден."
        }
    ],
    "message": "В процессе получения информации об авторах спектакля возникли ошибки."
}
```

## Delete Authors From Spectacle

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| PATCH |
| route          	| BASE_URL/authors?spectacle_id={spectacle_id}|
| error types    	| SpectacleNotFound,  AuthorNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

>*Note*: Метод запроса - PATCH, это не ошибка. Дело в том, что необходимо иметь возможность удалять сразу несколько записей из таблицы "Spectacle Author". В нагрузке запроса будет список id авторов, которые необходимо удалить из данной таблицы. Это один из подходов к решению проблемы о множественном удалении. Количество авторов для удаления из спектакля неограничено.

#### REQUEST DATA

```json
{
    "authors_to_delete": [23, 25, 324, 1234, 23, 123]
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Авторы успешно удалены из спектакля",
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
        },
        {
            "type": "AuthorNotFound",
            "message": "Автор с id = {author_id} не найден."
        },
    ],
    "message": "В процессе удаления авторов из спектакля возникли ошибки."
}
```

## Add Artist

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| POST |
| route          	| BASE_URL/artists|
| error types    	| PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### REQUEST DATA

```json
{
    "surname": "artist_surname",
    "name": "artist_name"
    "middle_name": "artist_middle_name",
    "life": "artist_life",
    "photo": "artist_photo"
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "author": {
        "id": 255,
    },
    "message": "Художник успешно добавлен."
}
```

#### RESPONSE DATA [FAIL]

>*Note*: 1) Возвращаются только найденные ошибки

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе добавления художника возникли ошибки."
}
```

## Update Artist

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| PATCH |
| route          	| BASE_URL/artists/{artist_id}|
| error types    	| ArtistNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### REQUEST DATA

```json
{
    "surname": "new_artist_surname",
    "name": "new_artist_name"
    "middle_name": "new_artist_middle_name",
    "life": "new_artist_life",
    "photo": "new_artist_photo"
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Информация о художнике успешно обновлена."
}
```

#### RESPONSE DATA [FAIL]

>*Note*: 1) Возвращаются только найденные ошибки; 2) Перечислены все возможные ошибки.

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "ArtistNotFound",
            "message": "Художник с таким id не найден."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе обновления информации о художнике возникли ошибки."
}
```

## Get Artist

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/artists?id={artist_id}|
| error types    	| ArtistNotFound |

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "artist": {
        "surname": "artist_surname",
        "name": "artist_name"
        "middle_name": "artist_middle_name",
        "life": "artist_life",
        "photo": "artist_photo"
    }
}
```

#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "ArtistNotFound",
            "message": "Художник с таким id не найден."
        }
    ],
    "message": "В процессе получения информации о художнике возникли ошибки."
}
```

## Delete Artist

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| DELETE |
| route          	| BASE_URL/artists/{artist_id}|
| error types    	| ArtistNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Информация о художнике успешно удалена",
}
```
#### RESPONSE DATA [FAIL]

```json
{
    "has_errors": true,
    "errors": [
        {
            "type": "ArtistNotFound",
            "message": "Художник с таким id не найден."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе удаления информации о художнике возникли ошибки."
}
```

## Add Artists to Spectacle

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| POST |
| route          	| BASE_URL/theaters/{theater_id}/spectacles/{spectacle_id}/artists|
| error types    	| TheaterNotFound, SpectacleNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

>*Note*: В request data содержится список художников спектакля (id автора), которые необходимо добавить. В примере приведено 3, в общем случае количество художников в списке не ограничено (может быть в разы больше). Предусмотри ситацию с пустым списком (если в запросе не будет элементов в списке).

#### REQUEST DATA

```json
{
    "artists": [
        {
            "id": 434
        },
        {
            "id": 32
        },
        {
            "id": 1
        }
    ]
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Художники спектакля успешно добавлены."
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
            "type": "SpectacleNotFound",
            "message": "Спектакль с таким id не найден."
        },
        {
            "type": "PermissionDenied",
            "message": "Отказано в доступе."
        }
    ],
    "message": "В процессе добавления художников в спектакль возникли ошибки."
}
```

## Get Spectacle Artists

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/artists?spectacle_id={spectacle_id}|
| error types    	| SpectacleNotFound, PermissionDenied |
| required headers  | Authorization         |

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "authors": [
        {   
            "id": 342,
            "surname": "artist_surname",
            "name": "artist_name"
            "middle_name": "artist_middle_name",
            "life": "artist_life",
            "photo": "artist_photo"
        },
        {   
            "id": 34,
            "surname": "artist_surname",
            "name": "artist_name"
            "middle_name": "artist_middle_name",
            "life": "artist_life",
            "photo": "artist_photo"
        },
        {   
            "id": 786,
            "surname": "artist_surname",
            "name": "artist_name"
            "middle_name": "artist_middle_name",
            "life": "artist_life",
            "photo": "artist_photo"
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
            "type": "SpectacleNotFound",
            "message": "Спектакль с таким id не найден."
        }
    ],
    "message": "В процессе получения информации о художниках спектакля возникли ошибки."
}
```

## Delete Artists From Spectacle

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| PATCH |
| route          	| BASE_URL/artists?spectacle_id={spectacle_id}|
| error types    	| SpectacleNotFound,  ArtistNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

>*Note*: Метод запроса - PATCH, это не ошибка. Дело в том, что необходимо иметь возможность удалять сразу несколько записей из таблицы "Spectacle Artist". В нагрузке запроса будет список id художников, которые необходимо удалить из данной таблицы. Это один из подходов к решению проблемы о множественном удалении. Количество художников для удаления из спектакля неограничено.

#### REQUEST DATA

```json
{
    "artists_to_delete": [23, 25, 324, 1234, 23, 123]
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "has_errors": false,
    "errors": [],
    "message": "Художники успешно удалены из спектакля",
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
        },
        {
            "type": "ArtistNotFound",
            "message": "Художник с id = {artist_id} не найден."
        },
    ],
    "message": "В процессе удаления художников из спектакля возникли ошибки."
}
```

