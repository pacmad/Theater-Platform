# Тестирование API  v3.0.0

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

* Баг. Ответ не соответствует ожиданию. Нужно убрать has_error

* Предусловия:
  Body: x-www-from-urlencoded

```
{
    "email": "name1",
    "name": "Ivan",
    "surname": "Ivanov",
    "password": "12345",
    "password_confirmation": "12345",
}
```

* Шаги:  
  1) Отправить API запрос на сервер  

* Ожидаемый результат:  
  json

```
{
    "message": "Регистрация прошла успешно. Вы были перенаправлены на страницу авторизации.",
}
```

* Фактический результат

```
{
    "has_errors": false,
    "errors": [],
    "message": "Регистрация прошла успешно. Вы были перенаправлены на страницу авторизации."
}
```

## Тест 2

Невозможность регистрации если пароль не совпадает с паролем подтверждения    

* Баг. Можно регистрироваться с несовпадающими паролями

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

* Фактический результат

  ```
  {
      "has_errors": false,
      "errors": [],
      "message": "Регистрация прошла успешно. Вы были перенаправлены на страницу авторизации."
  }
  ```

  

## Тест 3

Невозможность регистрации с повторяющимся Email  

Успех.

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

* Фактический результат

  ```
  {
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

Баг. has_errors не нужен

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
    "token": "access_token_here",
    "user": {
        "id": 67,
        "email": "example@mail.com",
        "name": "Ivan",
        "surname": "Ivanov"
    }
}
```

* Фактический результат

```
{
    "has_errors": false,
    "errors": [],
    "user": {
        "id": 1,
        "name": "Ivan",
        "surname": "Ivanov",
        "email": "name8",
        "created_at": "2020-06-16T13:34:42.000000Z",
        "updated_at": "2020-06-16T13:34:42.000000Z"
    },
    "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiIxIiwianRpIjoiOGZiNjM0ZWVhNDNhNTIwZWRmMDRmZTg0ZDUyYjI3OGVmZWZkOGNkMjMwN2M1Y2ZjZWVkYWJiNDY4NmNjYzAzYzFhOWRlYjVmYWNhNTZlZGUiLCJpYXQiOjE1OTIzMTYxNTksIm5iZiI6MTU5MjMxNjE1OSwiZXhwIjoxNjIzODUyMTU5LCJzdWIiOiIxIiwic2NvcGVzIjpbXX0.VwHRiGgMrpa8A9ro1tOK85_RVYKa036D89YiXG0c7gMSK-ASJ9IrTmnDRNaU7jowepGurvLAI_OnioA3ObBqodX15JnOd8umjlOblTFJ70tmA4OHLn393WnPsn2IZNS139IZns34FztKDalwWOeHHcs18UeqicWQiTB-wxnEs4nifDS-BWkXFurRAvwX-QkY18PxZGnprT-jkWW_2EGt5ib5J6m8X6ZnXI6szOVIanRpI0pya7RKABf8mVrXveFpPNcrvZEoFTPJD-QEOJfraEAGc8wbM0z1A8nsM6QScyRqV1TG8GIvVRElDJtIHgLCSTryFv7-f9WAqUxqX5EcnQNJkqdPjr3IHui_EnGSTsBevm_lkIh0_FBxdGvFcM7MFzbojdLT-MNJlluj2RGLntKIpCnC4LetMZiYyljbvrpLgCVwcMkCl2ZyfKix06gEkHi0YfioS1QgELrwAWb-xInxWDXS_58TApyUC2O9YNwEaArfYv9wUZ_ychAkwd6myz3KIslCQYbt_F6dx5xP8ySWZrjvTCPrPWpgc-Df1Fhw4asQ5V_f8Nl-IOAn_y4yXAKxI9wjTpgLz8kwiNyJIYER9RMaEXcBKzzO6VN4Lb5P1baw1VAcMEnu5Rqwc_4DLZ0N3C_iH94PlrE89xm1gNtA-L5wJsrdbEUSx38Dy0k"
}
```


## 

## Тест 2

Авторизация с невалидными данными   

* Баг. has_error лишний

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
    "message": "Не удаётся войти. Неверный логин или пароль.",
    "token": "null",
    "user": "null"
}
```

* Фактический результат

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

Баг. has_error лишний

* Предусловия:

* Шаги:  
  1) Отправить API запрос на сервер  

* Ожидаемый результат:  
  json

```
{
    "message": "Вы успешно вышли из системы.",
}
```

```
{
    "has_errors": false,
    "errors": [],
    "message": "Вы успешно вышли из системы."
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
