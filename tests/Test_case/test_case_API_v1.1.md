# Тестирование API  v1.1
# Ссылки на каждый блок<a name="Ссылки"></a>
1. [Registration](#Registration)  
2. [Authorization](#Authorization)  
3. [Logout](#Logout)  
4. [Add Theater](#AddTheater)  
5. [Update Theater](#UpdateTheater)  
6. [Get Theaters](#GetTheaters)   
7. [Get Theater](#GetTheater)  
8. [Delete Theater](#DeleteTheater)  
9. [Add Spectacle](#AddSpectacle)  
10. [Update Spectacle](#UpdateSpectacle)  
11. [Get Spectacles](#GetSpectacles)  
12. [Get Spectacle](#GetSpectacle)  
13. [Delete Spectacle](#DeleteSpectacle)   
14. [Add Hall](#AddHall)  
15. [Update Hall](#UpdateHall)  
16. [Get Hall](#GetHall)  
17. [Get Theater Halls](#GetTheaterHalls)  
18. [Delete Hall](#DeleteHall)   
19. [Add Event](#AddEvent)   
20. [Update Event](#UpdateEvent)   
21. [Get Event](#GetEvent)   
22. [Get Events](#GetEvents)   
23. [Delete Event](#DeleteEvent)   
24. [Upload Spectacle Poster](#UploadSpectaclePoster)  
25. [Upload Theater Logo](#UploadTheaterLogo)  
26. [Upload Spectacle Silder Poster](#UploadSpectacleSilderPoster)  
27. [Upload Spectacle Preview](#UploadSpectaclePreview)  
28. [Upload Theater Preview](#UploadTheaterPreview)  
29. [Result](#Result)  
  

# Registration <a name="Registration"></a>
[<-- Вернуться к списку](#Ссылки)
### Предусловия группы тестов

request method = POST  
route = http://host1813162.hostland.pro/api/register  
Headers:  
```
     Accept : application/json   
```


## Тест 1
Регистрация с валидными данными  
  
* Предусловия:
Body: x-www-from-urlencoded
```
{
    "email": "name1",
    "name": "Ivan",
    "surname": "Ivanov",
    "password": "123456",
    "password_confirmation": "123456",
}
```
* Шаги:  
1) Отправить API запрос на сервер  

* Ожидаемый результат:  
json
```
{
    "has_errors": false,
    "errors": [],
    "message": "Регистрация прошла успешно. Вы были перенаправлены на страницу авторизации.",
}
```

## Тест 2
Невозможность регистрации если пароль не совпадает с паролем подтверждения    
  
* Предусловия:
Body: x-www-from-urlencoded
```
{
    "email": "name2",
    "name": "Ivan",
    "surname": "Ivanov",
    "password": "123",
    "password_confirmation": "1234",
}
```
* Шаги:  
1) Отправить API запрос на сервер  

* Ожидаемый результат:  
В регистрации должно быть отказано.
json
```
{
    "has_errors": true,
    "message": "Указанные данные введены неверно.",
    "errors": {
        "password": [
            "Поле пароль не совпадает с полем подтверждения."
        ]
    }
}
```


## Тест 3
Невозможность регистрации с повторяющимся Email  
  
* Предусловия:
Body: x-www-from-urlencoded
```
{
    "email": "name1",
    "name": "Ivan",
    "surname": "Ivanov",
    "password": "123",
    "password_confirmation": "123",
}
```
* Шаги:  
1) Отправить API запрос на сервер 
2) Если записи на сервере нет, то ещё раз послать API запрос

* Ожидаемый результат:  
В регистрации должно быть отказано.  
json
```
{
    "has_errors": true,
    "message": "Указанные данные введены неверно.",
    "errors": {
        "email": [
            "Пользователь с таким email уже зарегистрирован."
        ]
    }
}
```


# Authorization <a name="Authorization"></a>
[<-- Вернуться к списку](#Ссылки)
### Предусловия группы тестов

request method = POST  
route = http://host1813162.hostland.pro/api/login  
Headers:  
```
     Accept : application/json   
```

## Тест 1
Авторизация с валидными данными  
   
* Предусловия:
Body: x-www-from-urlencoded
```
{
    "email": "name1",
    "password": "123456"
}
```
* Шаги:  
1) Отправить API запрос на сервер  

* Ожидаемый результат:  
json
```
{
    "has_errors": false,
    "errors": [],
    "token": "access_token_here",
    "user": {
        "id": 15,
        "email": "name1",
        "name": "Ivan",
        "surname": "Ivanov",
    }
}
```


## Тест 2
Авторизация с невалидными данными  
  
* Предусловия:
Body: x-www-from-urlencoded
```
{
    "email": "name1",
    "password": "1234567"
}
```
* Шаги:  
1) Отправить API запрос на сервер  

* Ожидаемый результат:  
json
```
{
    "has_errors": true,
    "message": "Не удаётся войти. Неверный логин или пароль.",
    "token": "null",
    "user": "null"
}
```

# Logout <a name="Logout"></a>
[<-- Вернуться к списку](#Ссылки)

### Предусловия группы тестов

request method = POST  
route = http://host1813162.hostland.pro/api/logout  
Headers:  
```
     Accept : application/json  
     Authorization : eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiIxIiwianRpIjoiMDc3ZmRmYzdmMzQ0MjJlYTkyZmIwM2ZiOGI0YjMzMzQ3MmMwMTA0MTI2YjEzNDMzNjcxYjY2M2E5MjcyNzExMDlmNjRiMGE1N2E1YmRhYmUiLCJpYXQiOjE1OTEwNTc3MjgsIm5iZiI6MTU5MTA1NzcyOCwiZXhwIjoxNjIyNTkzNzI4LCJzdWIiOiIxNSIsInNjb3BlcyI6W119.GsMb_6jUsqLZ9a890BtLdROcRC5wQfsUTSaNhcdkT_irtBfkg31Kc8izc6rgNO1YPIFSRLeconSL_Z2zU6SHWGNUzvjvJE0ZmMEiRUxUu_hg2Vja_JBf4ZHF00EDF46o46E2sJ6Sv8_ZHmeFqH_ubuy9IUcU5pVvkVheZ-OZ2xrYrgcnIpXBh4ToR-ZafkdazzCANydrNnvOecyv00LIgeJ-_RWPZcgqH-9we0CasAwNJVR0r4chpNP8dQ6Y-XXxfDMeZ2QxcYhGV1YLygQk6MjPtudoFJNoxpWyIwr86pJ_9UgI1msqcMFNN7tHvt37U7YJYgxxBZN89hpbhk-HDj8IIgTkrkkgkSLDpuQh00cv8WPr3iXkzcr02qsRxgMOTLuVxzONBSYD-rC1TmVcK8ZD7PrQApr_Ss6y61iIUXhYptSscKRL4iEFgTzx0iwOdzmvbvVHtv93-bqeo5e2bZFpNJcCjRBFIEV0lnGXmCos-ValHRS0IQXY3ra74lscIvnhlYUNGDwSejtLlCgRUH1EfFWnHesSne-gjPDGRxNgUozyRorCTTQXQSk-o50o5oj_gtfwvVed8R92dmFOfcIf3VJgPQIvNYtjxftp564Q_OVOX0DP4OmL-9rKpOpJvA6kTToIqSHJ_N5-GMYG9PzoSrT4YJd498GO8Crew84 
```

## Тест 1
Выход из учётной записи  
  
* Предусловия:

* Шаги:  
1) Отправить API запрос на сервер  

* Ожидаемый результат:  
json
```
{
    "has_errors": false,
    "errors": [],
    "message": "Вы успешно вышли из системы.",
}
```


# Add theater<a name="AddTheater"></a>
[<-- Вернуться к списку](#Ссылки)
### Предусловия группы тестов

request method = POST  
route = http://host1813162.hostland.pro/api/theaters  
Headers:  
```
     Accept : application/json  
     Authorization : Bearer ZcM8bJ1gubXy46lXYBeD33nNM7nZPlMEod-sREabNs9af0qZyuj_0SJAir0S-0Psqran2MKjcjMVD0WIPLMtPfooxbqXVjuBxnWx3SftqtbVUw_rTPEcb3oViAJV2I5cRzoSGQe_M8LZFytgPOHyW-OR6is7VosY4l5FwxfOGKaPJPkLXVnxXfq7iIGF_VrCF6fWZhs5bsf7UWHFeuIEAu0ktctsFFmDzrUx9-tLlEgxEXkP_sCXtesDKKxolr4slj9cPzo57E1Xt-zLc9HY4b3FT5m5RwGiUFzk9rwsBJFBljkv5dGv3mU3g0BZGU236TEtcESQPPBt8Q8KUqzMSV0pGSYdvWAEU6mymXYsPIQSsZozdRSMiINE1jOdhISwx9yF0V26XtSiEdFB_0-a-1Zk2LimmM34oyJji56zaBHuUJzjoj7ytzrJZB_mNRwCdrsl3M
```

## Тест 1
Добавление театра  
  
* Предусловия:
```
{
    "name": "Theater2",
    "description": "o lala kakoy teatr"
    "address": "qweasd",
    "logo": "theater_logo",
    "photo": "theater_photo",
    "preview": "theater_preview",
    "cash_desk_phone_number": "233211",
    "phone_number_for_reference": "1123321"
}
```

* Шаги:  
1) Отправить API запрос на сервер  

* Ожидаемый результат:  
json
```
{
    "has_errors": false,
    "errors": [],
    "theater": {
        "id": 5,
    },
    "message": "Театр успешно добавлен."
}
```


# Update Theater<a name="UpdateTheater"></a>
[<-- Вернуться к списку](#Ссылки)
### Предусловия группы тестов

request method = PATCH  
route = http://host1813162.hostland.pro/api/theaters/{theater_id}
Headers:  
```
     Accept : application/json  
     Authorization : Bearer ZcM8bJ1gubXy46lXYBeD33nNM7nZPlMEod-sREabNs9af0qZyuj_0SJAir0S-0Psqran2MKjcjMVD0WIPLMtPfooxbqXVjuBxnWx3SftqtbVUw_rTPEcb3oViAJV2I5cRzoSGQe_M8LZFytgPOHyW-OR6is7VosY4l5FwxfOGKaPJPkLXVnxXfq7iIGF_VrCF6fWZhs5bsf7UWHFeuIEAu0ktctsFFmDzrUx9-tLlEgxEXkP_sCXtesDKKxolr4slj9cPzo57E1Xt-zLc9HY4b3FT5m5RwGiUFzk9rwsBJFBljkv5dGv3mU3g0BZGU236TEtcESQPPBt8Q8KUqzMSV0pGSYdvWAEU6mymXYsPIQSsZozdRSMiINE1jOdhISwx9yF0V26XtSiEdFB_0-a-1Zk2LimmM34oyJji56zaBHuUJzjoj7ytzrJZB_mNRwCdrsl3M
```

## Тест 1
Изменение театра  

* Предусловия:
```
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

* Шаги:  
1) Отправить API запрос на сервер  

* Ожидаемый результат:  
json
```
{

    "message": "Театр успешно обновлен."
}
```


# Get theaters<a name="GetTheaters"></a>
[<-- Вернуться к списку](#Ссылки)
### Предусловия группы тестов

request method = GET  
route = http://host1813162.hostland.pro/api/theaters  
Headers:  
```
     Accept : application/json  
     Authorization : Bearer ZcM8bJ1gubXy46lXYBeD33nNM7nZPlMEod-sREabNs9af0qZyuj_0SJAir0S-0Psqran2MKjcjMVD0WIPLMtPfooxbqXVjuBxnWx3SftqtbVUw_rTPEcb3oViAJV2I5cRzoSGQe_M8LZFytgPOHyW-OR6is7VosY4l5FwxfOGKaPJPkLXVnxXfq7iIGF_VrCF6fWZhs5bsf7UWHFeuIEAu0ktctsFFmDzrUx9-tLlEgxEXkP_sCXtesDKKxolr4slj9cPzo57E1Xt-zLc9HY4b3FT5m5RwGiUFzk9rwsBJFBljkv5dGv3mU3g0BZGU236TEtcESQPPBt8Q8KUqzMSV0pGSYdvWAEU6mymXYsPIQSsZozdRSMiINE1jOdhISwx9yF0V26XtSiEdFB_0-a-1Zk2LimmM34oyJji56zaBHuUJzjoj7ytzrJZB_mNRwCdrsl3M
```

## Тест 1
Получение списка театров  
ПРОВАЛ. Список театров называется data, а должен - theaters. Сервер присылает дополнительные данные (время).
* Предусловия:  

* Шаги:  
1) Отправить API запрос на сервер  

* Ожидаемый результат:  
json
```
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

# Get Theater<a name="GetTheater"></a>
[<-- Вернуться к списку](#Ссылки)  

### Предусловия группы тестов

request method = GET   
Headers:  
```
     Accept : application/json  
     Authorization : Bearer ZcM8bJ1gubXy46lXYBeD33nNM7nZPlMEod-sREabNs9af0qZyuj_0SJAir0S-0Psqran2MKjcjMVD0WIPLMtPfooxbqXVjuBxnWx3SftqtbVUw_rTPEcb3oViAJV2I5cRzoSGQe_M8LZFytgPOHyW-OR6is7VosY4l5FwxfOGKaPJPkLXVnxXfq7iIGF_VrCF6fWZhs5bsf7UWHFeuIEAu0ktctsFFmDzrUx9-tLlEgxEXkP_sCXtesDKKxolr4slj9cPzo57E1Xt-zLc9HY4b3FT5m5RwGiUFzk9rwsBJFBljkv5dGv3mU3g0BZGU236TEtcESQPPBt8Q8KUqzMSV0pGSYdvWAEU6mymXYsPIQSsZozdRSMiINE1jOdhISwx9yF0V26XtSiEdFB_0-a-1Zk2LimmM34oyJji56zaBHuUJzjoj7ytzrJZB_mNRwCdrsl3M
```

## Тест 1
Получение театра по существующему id  
  
* Предусловия:
route = http://host1813162.hostland.pro/api/theaters/7 
* Шаги:  
1) Отправить API запрос на сервер  

* Ожидаемый результат:  
json
```
{
    "has_errors": false,
    "errors": [],
    "theater": {
            "id": 7,
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


## Тест 2
Получение театра по несуществующему id  
  
* Предусловия:
route = http://host1813162.hostland.pro/api/theaters/90 
* Шаги:  
1) Отправить API запрос на сервер  

* Ожидаемый результат:  
json
```
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


# Delete Theater<a name="DeleteTheater"></a>
[<-- Вернуться к списку](#Ссылки)  

### Предусловия группы тестов

request method = DELET   
Headers:  
```
     Accept : application/json  
     Authorization : Bearer ZcM8bJ1gubXy46lXYBeD33nNM7nZPlMEod-sREabNs9af0qZyuj_0SJAir0S-0Psqran2MKjcjMVD0WIPLMtPfooxbqXVjuBxnWx3SftqtbVUw_rTPEcb3oViAJV2I5cRzoSGQe_M8LZFytgPOHyW-OR6is7VosY4l5FwxfOGKaPJPkLXVnxXfq7iIGF_VrCF6fWZhs5bsf7UWHFeuIEAu0ktctsFFmDzrUx9-tLlEgxEXkP_sCXtesDKKxolr4slj9cPzo57E1Xt-zLc9HY4b3FT5m5RwGiUFzk9rwsBJFBljkv5dGv3mU3g0BZGU236TEtcESQPPBt8Q8KUqzMSV0pGSYdvWAEU6mymXYsPIQSsZozdRSMiINE1jOdhISwx9yF0V26XtSiEdFB_0-a-1Zk2LimmM34oyJji56zaBHuUJzjoj7ytzrJZB_mNRwCdrsl3M
```

## Тест 1
Удаление театра по существующему id  
  
* Предусловия:
route = http://host1813162.hostland.pro/api/theaters/3 
* Шаги:  
1) Отправить API запрос на сервер  

* Ожидаемый результат:  
json
```
{
    "has_errors": false,
    "errors": [],
    "message": "Театр успешно удален",
}
```


## Тест 2
Удаление театра по несуществующему id  
  
* Предусловия:
route = http://host1813162.hostland.pro/api/theaters/10  
* Шаги:  
1) Отправить API запрос на сервер  

* Ожидаемый результат:  
json
```
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


# Add Spectacle<a name="AddSpectacle"></a>
[<-- Вернуться к списку](#Ссылки)
### Предусловия группы тестов

request method = POST  
route = http://host1813162.hostland.pro/api/spectacles 
Headers:  
```
     Accept : application/json  
     Authorization : Bearer ZcM8bJ1gubXy46lXYBeD33nNM7nZPlMEod-sREabNs9af0qZyuj_0SJAir0S-0Psqran2MKjcjMVD0WIPLMtPfooxbqXVjuBxnWx3SftqtbVUw_rTPEcb3oViAJV2I5cRzoSGQe_M8LZFytgPOHyW-OR6is7VosY4l5FwxfOGKaPJPkLXVnxXfq7iIGF_VrCF6fWZhs5bsf7UWHFeuIEAu0ktctsFFmDzrUx9-tLlEgxEXkP_sCXtesDKKxolr4slj9cPzo57E1Xt-zLc9HY4b3FT5m5RwGiUFzk9rwsBJFBljkv5dGv3mU3g0BZGU236TEtcESQPPBt8Q8KUqzMSV0pGSYdvWAEU6mymXYsPIQSsZozdRSMiINE1jOdhISwx9yF0V26XtSiEdFB_0-a-1Zk2LimmM34oyJji56zaBHuUJzjoj7ytzrJZB_mNRwCdrsl3M
```

## Тест 1
Добавление спектакля  
  
* Предусловия:
```
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

* Шаги:  
1) Отправить API запрос на сервер  

* Ожидаемый результат:  
json
```
{
    "has_errors": false,
    "errors": [],
    "spectacle": {
        "id": 255,
    },
    "message": "Спектакль успешно добавлен."
}
```


# Update Spectacle<a name="UpdateSpectacle"></a>  
[<-- Вернуться к списку](#Ссылки)  
### Предусловия группы тестов

request method = PATCH  
route = http://host1813162.hostland.pro/api/spectacles/{spectacle_id}  
Headers:  
```
     Accept : application/json  
     Authorization : Bearer ZcM8bJ1gubXy46lXYBeD33nNM7nZPlMEod-sREabNs9af0qZyuj_0SJAir0S-0Psqran2MKjcjMVD0WIPLMtPfooxbqXVjuBxnWx3SftqtbVUw_rTPEcb3oViAJV2I5cRzoSGQe_M8LZFytgPOHyW-OR6is7VosY4l5FwxfOGKaPJPkLXVnxXfq7iIGF_VrCF6fWZhs5bsf7UWHFeuIEAu0ktctsFFmDzrUx9-tLlEgxEXkP_sCXtesDKKxolr4slj9cPzo57E1Xt-zLc9HY4b3FT5m5RwGiUFzk9rwsBJFBljkv5dGv3mU3g0BZGU236TEtcESQPPBt8Q8KUqzMSV0pGSYdvWAEU6mymXYsPIQSsZozdRSMiINE1jOdhISwx9yF0V26XtSiEdFB_0-a-1Zk2LimmM34oyJji56zaBHuUJzjoj7ytzrJZB_mNRwCdrsl3M
```

## Тест 1
Добавление спектакля  
  
* Предусловия:
```
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

* Шаги:  
1) Отправить API запрос на сервер  

* Ожидаемый результат:  
json
```
{

    "message": "Спектакль успешно обновлен."
}
```


# Get Spectacles<a name="GetSpectacles"></a>
[<-- Вернуться к списку](#Ссылки)  
### Предусловия группы тестов

request method = GET  
route = http://host1813162.hostland.pro/api/spectacles?id={spectacle_id} 
Headers:  
```
     Accept : application/json  
     Authorization : Bearer ZcM8bJ1gubXy46lXYBeD33nNM7nZPlMEod-sREabNs9af0qZyuj_0SJAir0S-0Psqran2MKjcjMVD0WIPLMtPfooxbqXVjuBxnWx3SftqtbVUw_rTPEcb3oViAJV2I5cRzoSGQe_M8LZFytgPOHyW-OR6is7VosY4l5FwxfOGKaPJPkLXVnxXfq7iIGF_VrCF6fWZhs5bsf7UWHFeuIEAu0ktctsFFmDzrUx9-tLlEgxEXkP_sCXtesDKKxolr4slj9cPzo57E1Xt-zLc9HY4b3FT5m5RwGiUFzk9rwsBJFBljkv5dGv3mU3g0BZGU236TEtcESQPPBt8Q8KUqzMSV0pGSYdvWAEU6mymXYsPIQSsZozdRSMiINE1jOdhISwx9yF0V26XtSiEdFB_0-a-1Zk2LimmM34oyJji56zaBHuUJzjoj7ytzrJZB_mNRwCdrsl3M
```

## Тест 1
Получение спектакля  
  
* Предусловия:
```
нет
```

* Шаги:  
1) Отправить API запрос на сервер  

* Ожидаемый результат:  
json
```
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

  

# Get Spectacle<a name="GetSpectacle"></a>
[<-- Вернуться к списку](#Ссылки)  
### Предусловия группы тестов

request method = GET  
route = http://host1813162.hostland.pro/api/spectacles?theater_id={theater_id} 
Headers:  
```
     Accept : application/json  
     Authorization : Bearer ZcM8bJ1gubXy46lXYBeD33nNM7nZPlMEod-sREabNs9af0qZyuj_0SJAir0S-0Psqran2MKjcjMVD0WIPLMtPfooxbqXVjuBxnWx3SftqtbVUw_rTPEcb3oViAJV2I5cRzoSGQe_M8LZFytgPOHyW-OR6is7VosY4l5FwxfOGKaPJPkLXVnxXfq7iIGF_VrCF6fWZhs5bsf7UWHFeuIEAu0ktctsFFmDzrUx9-tLlEgxEXkP_sCXtesDKKxolr4slj9cPzo57E1Xt-zLc9HY4b3FT5m5RwGiUFzk9rwsBJFBljkv5dGv3mU3g0BZGU236TEtcESQPPBt8Q8KUqzMSV0pGSYdvWAEU6mymXYsPIQSsZozdRSMiINE1jOdhISwx9yF0V26XtSiEdFB_0-a-1Zk2LimmM34oyJji56zaBHuUJzjoj7ytzrJZB_mNRwCdrsl3M
```

## Тест 1
Получение спектаклей  
  
* Предусловия:
```
нет
```

* Шаги:  
1) Отправить API запрос на сервер  

* Ожидаемый результат:  
json
```
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
  

# Delete Spectacle<a name="DeleteSpectacle"></a>
[<-- Вернуться к списку](#Ссылки)  
### Предусловия группы тестов

request method = DELETE  
route = http://host1813162.hostland.pro/api/spectacles/{spectacle_id}
Headers:  
```
     Accept : application/json  
     Authorization : Bearer ZcM8bJ1gubXy46lXYBeD33nNM7nZPlMEod-sREabNs9af0qZyuj_0SJAir0S-0Psqran2MKjcjMVD0WIPLMtPfooxbqXVjuBxnWx3SftqtbVUw_rTPEcb3oViAJV2I5cRzoSGQe_M8LZFytgPOHyW-OR6is7VosY4l5FwxfOGKaPJPkLXVnxXfq7iIGF_VrCF6fWZhs5bsf7UWHFeuIEAu0ktctsFFmDzrUx9-tLlEgxEXkP_sCXtesDKKxolr4slj9cPzo57E1Xt-zLc9HY4b3FT5m5RwGiUFzk9rwsBJFBljkv5dGv3mU3g0BZGU236TEtcESQPPBt8Q8KUqzMSV0pGSYdvWAEU6mymXYsPIQSsZozdRSMiINE1jOdhISwx9yF0V26XtSiEdFB_0-a-1Zk2LimmM34oyJji56zaBHuUJzjoj7ytzrJZB_mNRwCdrsl3M
```

## Тест 1
Получение спектакля  
  
* Предусловия:
```
нет
```

* Шаги:  
1) Отправить API запрос на сервер  

* Ожидаемый результат:  
json
```
{

    "message": "Спектакль успешно удален",
}

```

  

# Upload Spectacle Poster<a name="UploadSpectaclePoster"></a>
[<-- Вернуться к списку](#Ссылки)  

### Предусловия группы тестов

request method = POST   
route = http://host1813162.hostland.pro/api/file/spectacle/poster
Headers:  
```
     Accept : application/json  
     Authorization : Bearer ZcM8bJ1gubXy46lXYBeD33nNM7nZPlMEod-sREabNs9af0qZyuj_0SJAir0S-0Psqran2MKjcjMVD0WIPLMtPfooxbqXVjuBxnWx3SftqtbVUw_rTPEcb3oViAJV2I5cRzoSGQe_M8LZFytgPOHyW-OR6is7VosY4l5FwxfOGKaPJPkLXVnxXfq7iIGF_VrCF6fWZhs5bsf7UWHFeuIEAu0ktctsFFmDzrUx9-tLlEgxEXkP_sCXtesDKKxolr4slj9cPzo57E1Xt-zLc9HY4b3FT5m5RwGiUFzk9rwsBJFBljkv5dGv3mU3g0BZGU236TEtcESQPPBt8Q8KUqzMSV0pGSYdvWAEU6mymXYsPIQSsZozdRSMiINE1jOdhISwx9yF0V26XtSiEdFB_0-a-1Zk2LimmM34oyJji56zaBHuUJzjoj7ytzrJZB_mNRwCdrsl3M
```

## Тест 1
Загрузка постера спектакля  
  
* Предусловия:
```
{
    "spectacle_poster": "spectacle_poster_image.png"
}
```
* Шаги:  
1) Отправить API запрос на сервер  

* Ожидаемый результат:  
json
```
{
    "message": "Картинка успешно загружена на сервер по адресу:",
    "url": "URL_PHOTO",
}
```

# Upload Theater Logo<a name="UploadTheaterLogo"></a>
[<-- Вернуться к списку](#Ссылки)  

### Предусловия группы тестов

request method = POST   
route = http://host1813162.hostland.pro/api/file/theater/logo
Headers:  
```
     Accept : application/json  
     Authorization : Bearer ZcM8bJ1gubXy46lXYBeD33nNM7nZPlMEod-sREabNs9af0qZyuj_0SJAir0S-0Psqran2MKjcjMVD0WIPLMtPfooxbqXVjuBxnWx3SftqtbVUw_rTPEcb3oViAJV2I5cRzoSGQe_M8LZFytgPOHyW-OR6is7VosY4l5FwxfOGKaPJPkLXVnxXfq7iIGF_VrCF6fWZhs5bsf7UWHFeuIEAu0ktctsFFmDzrUx9-tLlEgxEXkP_sCXtesDKKxolr4slj9cPzo57E1Xt-zLc9HY4b3FT5m5RwGiUFzk9rwsBJFBljkv5dGv3mU3g0BZGU236TEtcESQPPBt8Q8KUqzMSV0pGSYdvWAEU6mymXYsPIQSsZozdRSMiINE1jOdhISwx9yF0V26XtSiEdFB_0-a-1Zk2LimmM34oyJji56zaBHuUJzjoj7ytzrJZB_mNRwCdrsl3M
```

## Тест 1
Загрузка лого театра  
  
* Предусловия:
```
{
    "theater_logo": "theater_logo_image.png"
}
```
* Шаги:  
1) Отправить API запрос на сервер  

* Ожидаемый результат:  
json
```
{
    "message": "Картинка успешно загружена на сервер по адресу:",
    "url": "URL_PHOTO",
}
```


# Upload Spectacle Silder Poster<a name="UploadSpectacleSilderPoster"></a>
[<-- Вернуться к списку](#Ссылки)  

### Предусловия группы тестов

request method = POST   
route = http://host1813162.hostland.pro/api/file/spectacle/slider-poster
Headers:  
```
     Accept : application/json  
     Authorization : Bearer ZcM8bJ1gubXy46lXYBeD33nNM7nZPlMEod-sREabNs9af0qZyuj_0SJAir0S-0Psqran2MKjcjMVD0WIPLMtPfooxbqXVjuBxnWx3SftqtbVUw_rTPEcb3oViAJV2I5cRzoSGQe_M8LZFytgPOHyW-OR6is7VosY4l5FwxfOGKaPJPkLXVnxXfq7iIGF_VrCF6fWZhs5bsf7UWHFeuIEAu0ktctsFFmDzrUx9-tLlEgxEXkP_sCXtesDKKxolr4slj9cPzo57E1Xt-zLc9HY4b3FT5m5RwGiUFzk9rwsBJFBljkv5dGv3mU3g0BZGU236TEtcESQPPBt8Q8KUqzMSV0pGSYdvWAEU6mymXYsPIQSsZozdRSMiINE1jOdhISwx9yF0V26XtSiEdFB_0-a-1Zk2LimmM34oyJji56zaBHuUJzjoj7ytzrJZB_mNRwCdrsl3M
```

## Тест 1
Загрузка постера на слайдер    
  
* Предусловия:
```
{
    "spectacle_sliderposter": "spectacle_sliderposter_image.png"
}
```
* Шаги:  
1) Отправить API запрос на сервер  

* Ожидаемый результат:  
json
```
{
    "message": "Картинка успешно загружена на сервер по адресу:",
    "url": "URL_PHOTO",
}
```



# Upload Spectacle Preview<a name="UploadSpectaclePreview"></a>
[<-- Вернуться к списку](#Ссылки)  

### Предусловия группы тестов

request method = POST   
route = http://host1813162.hostland.pro/api/file/spectacle/preview
Headers:  
```
     Accept : application/json  
     Authorization : Bearer ZcM8bJ1gubXy46lXYBeD33nNM7nZPlMEod-sREabNs9af0qZyuj_0SJAir0S-0Psqran2MKjcjMVD0WIPLMtPfooxbqXVjuBxnWx3SftqtbVUw_rTPEcb3oViAJV2I5cRzoSGQe_M8LZFytgPOHyW-OR6is7VosY4l5FwxfOGKaPJPkLXVnxXfq7iIGF_VrCF6fWZhs5bsf7UWHFeuIEAu0ktctsFFmDzrUx9-tLlEgxEXkP_sCXtesDKKxolr4slj9cPzo57E1Xt-zLc9HY4b3FT5m5RwGiUFzk9rwsBJFBljkv5dGv3mU3g0BZGU236TEtcESQPPBt8Q8KUqzMSV0pGSYdvWAEU6mymXYsPIQSsZozdRSMiINE1jOdhISwx9yF0V26XtSiEdFB_0-a-1Zk2LimmM34oyJji56zaBHuUJzjoj7ytzrJZB_mNRwCdrsl3M
```

## Тест 1
Загрузка превью спектакля      
  
* Предусловия:
```
{
    "spectacle_preview": "spectacle_preview_image.png"
}
```
* Шаги:  
1) Отправить API запрос на сервер  

* Ожидаемый результат:  
json
```
{
    "message": "Картинка успешно загружена на сервер по адресу:",
    "url": "URL_PHOTO",
}
```



# Upload Theater Preview<a name="UploadTheaterPreview"></a>
[<-- Вернуться к списку](#Ссылки)  

### Предусловия группы тестов

request method = POST   
route = http://host1813162.hostland.pro/api/file/theater/preview
Headers:  
```
     Accept : application/json  
     Authorization : Bearer ZcM8bJ1gubXy46lXYBeD33nNM7nZPlMEod-sREabNs9af0qZyuj_0SJAir0S-0Psqran2MKjcjMVD0WIPLMtPfooxbqXVjuBxnWx3SftqtbVUw_rTPEcb3oViAJV2I5cRzoSGQe_M8LZFytgPOHyW-OR6is7VosY4l5FwxfOGKaPJPkLXVnxXfq7iIGF_VrCF6fWZhs5bsf7UWHFeuIEAu0ktctsFFmDzrUx9-tLlEgxEXkP_sCXtesDKKxolr4slj9cPzo57E1Xt-zLc9HY4b3FT5m5RwGiUFzk9rwsBJFBljkv5dGv3mU3g0BZGU236TEtcESQPPBt8Q8KUqzMSV0pGSYdvWAEU6mymXYsPIQSsZozdRSMiINE1jOdhISwx9yF0V26XtSiEdFB_0-a-1Zk2LimmM34oyJji56zaBHuUJzjoj7ytzrJZB_mNRwCdrsl3M
```

## Тест 1
Загрузка превью театра      
  
* Предусловия:
```
{
    "theater_preview": "theater_preview_image.png"
}
```
* Шаги:  
1) Отправить API запрос на сервер  

* Ожидаемый результат:  
json
```
{
    "message": "Картинка успешно загружена на сервер по адресу:",
    "url": "URL_PHOTO",
}
```


# Result <a name="Result"></a>
[<-- Вернуться к списку](#Ссылки)


