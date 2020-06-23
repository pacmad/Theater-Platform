# API v3.1.0

>*updates*:
>1. Внесены корректировки в названии API маршрутов по моделям - events, spectacles, theaters, halls.

>*Note:* + в содержании отмечены API, которые реализованы и перешли на стадию тестирования.

>*Note:* ** в содержании отмечены API, которые должны быть реализованы в следующем пуле.

## Table Of Contents

1. [Registration](#registration) +
2. [Authorization](#authorization) +
3. [Logout](#logout) +
4. [Add User Bookmark](#add-user-bookmark) + **
5. [Delete User Bookmark](#delete-user-bookmark) + **
6. [Get User Bookmarks](#get-user-bookmarks) + **
7. [Get User Purchase History](#get-user-purchase-history) ** 
8. [Add Spectacle](#add-spectacle) +
9. [Update Spectacle](#update-spectacle) +
10. [Get Spectacle](#get-spectacle) +
11. [Get Spectacles](#get-spectacles) +
12. [Delete Spectacle](#delete-spectacle) +
13. [Add Event](#add-event) +
14. [Update Event](#update-event) +
15. [Get Event](#get-event) +
16. [Get Events](#get-events) + (на доработке)
17. [Delete Event](#delete-event) +
18. [Get Main Page Premieres](#get-main-page-premieres) +
19. [Add Theater](#add-theater) +
20. [Update Theater](#update-theater) +
21. [Get Theater](#get-theater) + 
22. [Get Theaters](#get-theaters) +
23. [Delete Theater](#delete-theater) +
24. [Add Social Network](#add-social-network) + ***
25. [Update Social Network](#update-social-social) + ***
26. [Get Social Network](#get-social-social) + ***
27. [Delete Social Network](#delete-social-social) + ***
28. [Add Theater Social Network Community Group](#add-theater-social-network-community-group) ***
29. [Update Theater Social Network Community Group](#update-theater-social-network-community-group) ***
30. [Get Theater Social Network Community Group](#get-theater-social-network-community-group) ***
31. [Get Theater Social Network Community Groups](#get-theater-social-network-community-groups) ***
32. [Delete Theater Social Network Community Group](#delete-theater-social-network-community-group) ***
33. [Add Hall](#add-hall) +
34. [Update Hall](#update-hall) +
35. [Get Hall](#get-hall) + 
36. [Get Theater Halls](#get-theater-halls)
37. [Delete Hall](#delete-hall) +
38. [Add Seats](#add-seats)
39. [Get Hall Seats](#get-hall-seats)
40. [Delete Seats](#delete-seats)
41. [Add Tickets](#add-tickets)
42. [Get Event Tickets](#get-event-tickets)
43. [Get Event Ticket](#get-event-ticket)
44. [Update Event Tickets](#update-event-tickets)
45. [Delete Tickets](#delete-tickets)
46. [Tickets Purchase](#tickets-purchase)
47. [Upload Theater Logo](#upload-theater-logo) +
48. [Upload Theater Preview](#upload-theater-logo) +
49. [Upload Spectacle Poster](#upload-spectacle-poster) +
50. [Upload Spectacle Preview](#upload-spectacle-preview) +
51. [Upload Spectacle Slider Poster](#upload-spectacle-sliderposter) +
52. [Upload Theater Photo](#upload-theater-photo) +
53. [Upload Hall Scheme](#upload-hall-scheme) +

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
}
```
#### RESPONSE DATA [SUCCESS]

```json
{
     
     
    "message": "Регистрация прошла успешно. Вы были перенаправлены на страницу авторизации.",
}
```

#### RESPONSE DATA [FAIL]

>*Note*: 1) Возвращаются только найденные ошибки

```json
{
    "message": "Указанные данные введены неверно.",
    "errors": {
        "email": [
            "Пользователь с таким email уже зарегистрирован."
        ],
        "password": [
            "Поле пароль не совпадает с полем подтверждения."
        ]
    }
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
     
     
    "token": "access_token_here",
    "user": {
        "id": 67,
        "email": "example@mail.com",
        "name": "Ivan",
        "surname": "Ivanov"
    }
}
```
#### RESPONSE DATA [FAIL]

>*Note*: 1) Возвращаются только найденные ошибки

```json
{
    "message": "Не удаётся войти. Неверный логин или пароль."
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
    "message": "Вы успешно вышли из системы.",
}
```
## Add User Bookmark

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| POST |
| route          	| BASE_URL/bookmark?user_id={user_id}&spectacle_id={spectacle_id}|
| error types    	| UserNotFound, SpectacleNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### REQUEST DATA

```json
{
    "spectacle_id": "spectacle_id_to_bookmark",
    "user_id": "user_id_to_bookmark"
}
```
#### RESPONSE DATA [SUCCESS]

```json
{  
    "message": "Спектакль добавлен в закладки",
}
```
#### RESPONSE DATA [FAIL]

>*Note*: 1) Возвращаются только найденные ошибки

```json
{
    "message": "Указанные данные введены неверно.",
    "errors": {
        "type": [
            "Пользователь с таким ID пользователя не найден."
        ],
        "spectacle_id": [
            "Спектакль с таким ID не найден."
        ],
        "permission": [
            "Отказано в доступе."
        ]
    }
}
```
## Delete User Bookmark

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| DELETE |
| route          	| BASE_URL/bookmark?id={bookmark_id}|
| error types    	| UserNotFound, BookmarkNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### RESPONSE DATA [SUCCESS]

```json
{  
    "message": "Закладка удалена",
}
```
#### RESPONSE DATA [FAIL]

>*Note*: 1) Возвращаются только найденные ошибки

```json
{
    "message": "Указанные данные введены неверно.",
    "errors": 
        {
            "type": "BookmarkNotFound",
            "message": "Закладка пользователя с таким ID не найдена."
        },
        {
            "type": "PermissionDenied"
            "message": "Отказано в доступе."
        ]
    }
}
```

## Get User Bookmarks

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/bookmarks?user_id={user_id}|
| error types    	| UserNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### RESPONSE DATA [SUCCESS]

>*Note*: 1) Возвращаются все закладки пользователя. В примере ответа от сервера приведено 2. 2) Если заметок нет, соответственно, bookmarks будет пустым списком.

```json
{    
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

## Add Spectacle

[<-- Back to Table Of Contents](#table-of-contents)

UPDATED

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| POST |
| route          	| BASE_URL/spectacle|
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
    "spectacle": {
        "id": 255,
    },
    "message": "Спектакль успешно добавлен."
}
```

#### RESPONSE DATA [FAIL]

```json
{   
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
| route          	| BASE_URL/spectacle?id={spectacle_id}|
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
    "message": "Спектакль успешно обновлен."
}
```

#### RESPONSE DATA [FAIL]

```json
{   
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
| route          	| BASE_URL/spectacle?id={spectacle_id}|
| error types    	| SpectacleNotFound |

#### RESPONSE DATA [SUCCESS]

>*Note*: 1) Возвращаются спектакль c id == spectacle_id.

```json
{  
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
| route          	| BASE_URL/spectacle?id={spectacle_id}|
| error types    	| SpectacleNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### RESPONSE DATA [SUCCESS]

```json
{
    "message": "Спектакль успешно удален",
}
```
#### RESPONSE DATA [FAIL]

```json
{  
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
| route          	| BASE_URL/event?theater_id={theater_id}&spectacle_id={spectacle_id}&hall_id={hall_id}|
| error types    	| SpectacleNotFound, HallNotFound, TheaterNotFound, PermissionDenied |
| required headers  | Authorization         |

1) Данные по атрибутам 'is_premiere', 'is_chosen_for_main_page' принимаются в формате boolean, где false = 0, а true = 1

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### REQUEST DATA

```json
{
    "name": "event_name",
    "dated_at": "event_date",
    "description": "event_description"
    "is_premiere": 1,
    "is_chosen_for_main_page": 0,
    "available_seats_number": 145,
    "age": "event_age",
    "duration": "event_duration",
    "price": "event_price",
    "genre": "event_genre",
    "hall_id": "event_hall_id",
    "theater_id": "event_theater_id",
    "spectacle_id": "event_spectacle_id"
}
```

#### RESPONSE DATA [SUCCESS]

```json
{  
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
            "type": "TheaterNotFound",
            "message": "Театр с таким id не найден."
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
| route          	| BASE_URL/event?id={event_id}|
| error types    	| EventNotFound, SpectacleNotFound, HallNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### REQUEST DATA

```json
{
    "event_name": "new_event_name",
    "dated_at": "new_event_date",
    "description": "new_event_description"
    "is_premiere": false,
    "is_chosen_for_main_page": false,
    "available_seats_number": 234,
    "spectacle_id": 12,
    "hall_id": 1,
    "theater_id": 2,
    "age": "event_age",
    "duration": "event_duration",
    "price": "event_price",
    "genre": "event_genre"
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
     
     
    "message": "Событие успешно обновлено."
}
```

#### RESPONSE DATA [FAIL]

>*Note*: 1) Возвращаются только найденные ошибки; 2) Перечислены все возможные ошибки.

```json
{
     
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
            "type": "TheaterNotFound",
            "message": "Театр с таким id не найден."
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
     
     
    "event": {
        "name": "event_name",
        "dated_at": "event_date",
        "description": "event_description"
        "is_premiere": true,
        "is_chosen_for_main_page": false,
        "available_seats_number": 145,
        "spectacle_id": 25,
        "hall_id": 2,
        "age": "event_age",
        "duration": "event_duration",
        "price": "event_price",
        "genre": "event_genre"
    }
}
```

#### RESPONSE DATA [FAIL]

```json
{
     
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
| route          	| BASE_URL/events?name={spectacle_name}&date_from={date_range_start}&date_to={date_range_end}&genre={event_genre}&price_from={ticket_price_start}&price_to={ticket_price_end}&duration_from={spectacle_duration_start}&duration_to={spectacle_duration_end}&theater={spectacle_theater_id}&genre={spectacle_genre}|
| error types    	| TheaterNotFound, DateFormatError |

1) Возвращаются все события, чья дата показа (dated_at) лежит в интервале [date_range_start;date_range_end], название спектакля содержит подстроку spectacle_name, а id театра равен theater_id. В примере ответа от сервера приведено 2 результата. 
2) price_from - price_to - недействительные. находятся на доработке. 
3) genre отвечает за колонку spectacle_genre и представляется в виде 5 значений - мелодрама, драма, мюзикл, комедия, трагедия. Данные записываются через запятую БЕЗ пробелов. Если поиск производится по одному значению, то формат вносимых данных будет таким: "genre": "мелодрама,_,_,_,_". При двух данных: "genre": "мелодрама,драма,_,_,_" 
4) Для вывода данных атрибуты date_from, date_to, genre ОБЯЗАТЕЛЬНЫ.
5) Если событий нет, соответственно, events будет пустым списком.

#### RESPONSE DATA [SUCCESS]

```json
{
    "events": [
        {
            "id": "event_id_1",
            "dated_at": "event_date_1",
            "name": "event_name_1",
            "description": "event_description_1",
            "is_premiere": "event_is_premiere_1",
            "is_chosen_for_main_page": "event_is_chosen_for_main_page_1",
            "theater_id": "event.theater_id_1",
            "spectacle_id": "event.spectacle_id_1",
            "hall_id": "event.hall_id_1",
            "available_seats_number": "available_seats_number_1",
            "spectacle": {
                "id": "spectacle_id_1",
                "name": "spectacle_name_1",
                "description": "spectacle_name_1",
                "slider_poster": "spectacle_slider_poster_1",
                "rate": "spectacle_rate_1",
                "year": "spectacle_year_1",
                "poster": "spectacle_poster_1",
                "trailer": "spectacle_trailer_1",
                "slider_poster": "spectacle_slider_poster_1",
                "theater_id": "theater_id_1",
            },
            "theater": {
                "id": "theater_id_1",
                "name": "theater_name_1",
                "logo": "theater_logo_1",
                "description": "theater_description_1",
                "address": "theater_address_1",
                "photo": "theater_photo_1",
                "preview": "theater_preview_1",
                "cash_desk_phone_number": "theater_cash_desk_phone_number_1"
                "phone_number_for_reference": "theater_phone_number_for_reference_1"
            },
        },
        {
                "id": "event_id_2",
                "dated_at": "event_date_2",
                "name": "event_name_2",
                "description": "event_description_2",
                "is_premiere": "event_is_premiere_2",
                "is_chosen_for_main_page": "event_is_chosen_for_main_page_2",
                "theater_id": "event.theater_id_2",
                "spectacle_id": "event.spectacle_id_2",
                "hall_id": "event.hall_id_2",
                "available_seats_number": "available_seats_number_2",
                "genre": "event_genre_2",
                "age": "event_age_2",
                "price": "event_price_2",
                "duration": "event_duration_2",
            },
            "spectacle": {
                "id": "spectacle_id_2",
                "name": "spectacle_name_2",
                "description": "spectacle_name_2",
                "slider_poster": "spectacle_slider_poster_2",
                "rate": "spectacle_rate_2",
                "year": "spectacle_year_2",
                "poster": "spectacle_poster_2",
                "trailer": "spectacle_trailer_2",
                "slider_poster": "spectacle_slider_poster_2",
                "theater_id": "theater_id_2",
            },
            "theater": {
                "id": "theater_id_2",
                "name": "theater_name_2",
                "logo": "theater_logo_2",
                "description": "theater_description_2",
                "address": "theater_address_2",
                "photo": "theater_photo_2",
                "preview": "theater_preview_2",
                "cash_desk_phone_number": "theater_cash_desk_phone_number_2"
                "phone_number_for_reference": "theater_phone_number_for_reference_2"
            },
        },
    ]
}
```
#### RESPONSE DATA [FAIL] (ДОРАБОТАТЬ)

>*Note*: 1) Возвращаются только найденные ошибки

```json
{
     
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
| route          	| BASE_URL/event?={event_id}|
| error types    	| EventNotFound, Permission Denied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### RESPONSE DATA [SUCCESS]

```json
{
     
     
    "message": "Событие успешно удалено",
}
```
#### RESPONSE DATA [FAIL]

```json
{
     
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

## Get Main Page Premieres

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| GET |
| route          	| BASE_URL/premieres?is_chosen_for_main_page=1|
| error types    	|  |

#### RESPONSE DATA [SUCCESS]

>*Note*: 1) Возвращаются все события, чей параметр is_chosen_for_main_page == 1. В примере ответа от сервера приведено 2 результата. 2) Если таких событий нет, соответственно, premieres будет пустым списком.

```json
{
     
     
    "premieres": [
        {
            "id": "event_id_1",
            "dated_at": "event_date_1",
            "name": "event_name_1",
            "description": "event_description_1",
            "is_premiere": 1,
            "is_chosen_for_main_page": 1,
            "theater_id": "event.theater_id_1",
            "spectacle_id": "event.spectacle_id_1",
            "hall_id": "event.hall_id_1",
            "available_seats_number": "available_seats_number_1",
            "genre": "event_genre_1",
            "age": 1,
            "duration": 243,
            "price": 2000,
            "spectacle": {
                "id": "spectacle_id_1",
                "name": "spectacle_name_1",
                "description": "spectacle_name_1",
                "slider_poster": "spectacle_slider_poster_1",
                "rate": "spectacle_rate_1",
                "year": "spectacle_year_1",
                "poster": "spectacle_poster_1",
                "trailer": "spectacle_trailer_1",
                "slider_poster": "spectacle_slider_poster_1",
                "theater_id": "theater_id_1",
            },
            "theater": {
                "id": "theater_id_1",
                "name": "theater_name_1",
                "logo": "theater_logo_1",
                "description": "theater_description_1",
                "address": "theater_address_1",
                "photo": "theater_photo_1",
                "preview": "theater_preview_1",
                "cash_desk_phone_number": "theater_cash_desk_phone_number_1"
                "phone_number_for_reference": "theater_phone_number_for_reference_1"
            },
        },
        {
                "id": "event_id_2",
                "dated_at": "event_date_2",
                "name": "event_name_2",
                "description": "event_description_2",
                "is_premiere": 1,
                "is_chosen_for_main_page": 1,
                "theater_id": "event.theater_id_2",
                "spectacle_id": "event.spectacle_id_2",
                "hall_id": "event.hall_id_2",
                "available_seats_number": "available_seats_number_2",
                "genre": "event_genre_2",
                 "age": 4,
                 "duration": 243,
                 "price": 2000,
            },
            "spectacle": {
                "id": "spectacle_id_2",
                "name": "spectacle_name_2",
                "description": "spectacle_name_2",
                "slider_poster": "spectacle_slider_poster_2",
                "rate": "spectacle_rate_2",
                "year": "spectacle_year_2",
                "poster": "spectacle_poster_2",
                "trailer": "spectacle_trailer_2",
                "slider_poster": "spectacle_slider_poster_2",
                "theater_id": "theater_id_2",
            },
            "theater": {
                "id": "theater_id_2",
                "name": "theater_name_2",
                "logo": "theater_logo_2",
                "description": "theater_description_2",
                "address": "theater_address_2",
                "photo": "theater_photo_2",
                "preview": "theater_preview_2",
                "cash_desk_phone_number": "theater_cash_desk_phone_number_2"
                "phone_number_for_reference": "theater_phone_number_for_reference_2"
            },
        },
    ]
}
```

## Add Theater

[<-- Back to Table Of Contents](#table-of-contents)

|attribute        |value         	      |
|----------------	|-------------------	|
| request method 	| POST |
| route          	| BASE_URL/theater|
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
    "phone_number_for_reference": "theater_phone_number_for_reference",
    "contacts": "theater_contacts"
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
     
     
    "theater": {
        "id": 255,
    },
    "message": "Театр успешно добавлен."
}
```

#### RESPONSE DATA [FAIL]

```json
{
     
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
| route          	| BASE_URL/theater?id={theater_id}|
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
    "phone_number_for_reference": "new_theater_phone_number_for_reference",
    "contacts": "theater_contacts"
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
     
     
    "message": "Театр успешно обновлен."
}
```

#### RESPONSE DATA [FAIL]

```json
{
     
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
| route          	| BASE_URL/theater?id={theater_id}|
| error types    	| TheaterNotFound |

#### RESPONSE DATA [SUCCESS]

>*Note*: 1) Возвращаются театр c id == theater_id.

```json
{
     
     
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
| route          	| BASE_URL/theater?={theater_id}|
| error types    	| TheaterNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### RESPONSE DATA [SUCCESS]

```json
{
     
     
    "message": "Театр успешно удален",
}
```
#### RESPONSE DATA [FAIL]

```json
{
     
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
     
     
    "social_network": {
        "id": 255,
    },
    "message": "Социальная сеть успешно добавлена."
}
```

#### RESPONSE DATA [FAIL]

```json
{
     
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
     
     
    "message": "Социальная сеть успешно обновлена."
}
```

#### RESPONSE DATA [FAIL]

```json
{
     
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
     
     
    "social_network": {
        "name": "social_network_name",
        "logo": "social_network_logo"
    }
}
```

#### RESPONSE DATA [FAIL]

```json
{
     
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
     
     
    "message": "Социальная сеть успешно удалена",
}
```

#### RESPONSE DATA [FAIL]

```json
{
     
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
     
     
    "social_network": {
        "id": 43
    },
    "message": "Группа театра в социальной сети успешно добавлена."
}
```

#### RESPONSE DATA [FAIL]

```json
{
     
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
     
     
    "message": "Группа театра в социальной сети успешно обновлена."
}
```

#### RESPONSE DATA [FAIL]

```json
{
     
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
     
     
    "url_to_community": "theater_social_network_community_group_url",
}
```

#### RESPONSE DATA [FAIL]

```json
{
     
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
     
     
    "message": "Информация о группе театра в социальной сети успешно удалена",
}
```
#### RESPONSE DATA [FAIL]

```json
{
     
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
| route          	| BASE_URL/hall?theater_id={theater_id}|
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
     
     
    "hall": {
        "id": 34
    }
    "message": "Зал успешно добавлен."
}
```

#### RESPONSE DATA [FAIL]

```json
{
     
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
| route          	| BASE_URL/hall?id={hall_id}|
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
     
     
    "message": "Зал успешно обновлен."
}
```

#### RESPONSE DATA [FAIL]

```json
{
     
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
| route          	| BASE_URL/hall?id={hall_id}|
| error types    	| HallNotFound |

#### RESPONSE DATA [SUCCESS]

```json
{
     
     
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
| route          	| BASE_URL/hall?id={hall_id}|
| error types    	| HallNotFound, PermissionDenied |
| required headers  | Authorization         |

>*Note*: PermissionDenied - ошибка проверки токена доступа, который лежит в хэдере Authorization (для неавторизованных пользователей выполнение операции невозможно).

#### RESPONSE DATA [SUCCESS]

```json
{
     
     
    "message": "Зал успешно удален",
}
```
#### RESPONSE DATA [FAIL]

```json
{
     
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
     
     
    "message": "Информация о местах в зале успешно удалена",
}
```
#### RESPONSE DATA [FAIL]

```json
{
     
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
    "message": "Информация о билетах успешно обновлена."
}
```

#### RESPONSE DATA [FAIL]

```json
{
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
    "message": "Информация о билетах успешно удалена",
}
```
#### RESPONSE DATA [FAIL]

```json
{
     
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
    "message": "Покупка прошла успешно."
}
```

#### RESPONSE DATA [FAIL]

```json
{ 
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
## Upload Theater Logo

[<-- Back to Table Of Contents](#table-of-contents)

|attribute          |value         	        |
|----------------	|-------------------	|
| request method 	| POST              	|
| route          	| BASE_URL/file/theater/logo    	|
| required headers  | Authorization         |

#### REQUEST DATA


```json
{
    "theater_logo": "theater_logo_image.png"
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "message": "Картинка успешно загружена на сервер по адресу:",
    "url": "URL_PHOTO",
}
```

## Upload Theater Preview

[<-- Back to Table Of Contents](#table-of-contents)

|attribute          |value         	        |
|----------------	|-------------------	|
| request method 	| POST              	|
| route          	| BASE_URL/file/theater/preview    	|
| required headers  | Authorization         |

#### REQUEST DATA


```json
{
    "theater_preview": "theater_preview_image.png"
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "message": "Картинка успешно загружена на сервер по адресу:",
    "url": "URL_PHOTO",
}
```

## Upload Spectacle Poster

[<-- Back to Table Of Contents](#table-of-contents)

|attribute          |value         	        |
|----------------	|-------------------	|
| request method 	| POST              	|
| route          	| BASE_URL/file/spectacle/poster    	|
| required headers  | Authorization         |

#### REQUEST DATA


```json
{
    "spectacle_poster": "spectacle_poster_image.png"
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "message": "Картинка успешно загружена на сервер по адресу:",
    "url": "URL_PHOTO",
}
```

## Upload Spectacle Preview

[<-- Back to Table Of Contents](#table-of-contents)

|attribute          |value         	        |
|----------------	|-------------------	|
| request method 	| POST              	|
| route          	| BASE_URL/file/spectacle/preview   	|
| required headers  | Authorization         |

#### REQUEST DATA


```json
{
    "spectacle_preview": "spectacle_preview_image.png"
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "message": "Картинка успешно загружена на сервер по адресу:",
    "url": "URL_PHOTO",
}
```

## Upload Spectacle Silder Poster

[<-- Back to Table Of Contents](#table-of-contents)

|attribute          |value         	        |
|----------------	|-------------------	|
| request method 	| POST              	|
| route          	| BASE_URL/file/spectacle/slider-poster    	|
| required headers  | Authorization         |

#### REQUEST DATA


```json
{
    "spectacle_sliderposter": "spectacle_sliderposter_image.png"
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "message": "Картинка успешно загружена на сервер по адресу:",
    "url": "URL_PHOTO",
}
```
## Upload Theater Photo

[<-- Back to Table Of Contents](#table-of-contents)

|attribute          |value         	        |
|----------------	|-------------------	|
| request method 	| POST              	|
| route          	| BASE_URL/file/theater/photo    	|
| required headers  | Authorization         |

#### REQUEST DATA


```json
{
    "theater_photo": "theater_photo_image.png"
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "message": "Картинка успешно загружена на сервер по адресу:",
    "url": "URL_PHOTO",
}
```
## Upload Hall Scheme

[<-- Back to Table Of Contents](#table-of-contents)

|attribute          |value         	        |
|----------------	|-------------------	|
| request method 	| POST              	|
| route          	| BASE_URL/file/hall/scheme    	|
| required headers  | Authorization         |

#### REQUEST DATA


```json
{
    "hall_scheme": "hall_scheme_image.png"
}
```

#### RESPONSE DATA [SUCCESS]

```json
{
    "message": "Картинка успешно загружена на сервер по адресу:",
    "url": "URL_PHOTO",
}
```
