>*updates*:
>1. в сущность "Театр" добавлены атрибуты "путь к фото театра" и "путь к превью театра"
>2. в сущность "Социальная сеть" добавлен атрибут "путь к логотипу"
>3. в сущность "Закладка пользователя" добавлен атрибут "Дата и время создания"
>4. из сущности "Закладка пользователя" удален атрибут "Комментарий"
>5. добавлена новая сущность "Режиссер" с атрибутами "id режиссера", "Фамилия", "Имя", "Отчество", "Биография", "Путь к фото"
>6. добавлена новая сущность "Режиссер спектакля" с атрибутами "id режиссера" и "id спектакля"
>7. добавлена новая сущность "Автор" с атрибутами "id автора", "Фамилия", "Имя", "Отчество", "Биография", "Путь к фото"
>8. добавлена новая сущность "Автор спектакля" с атрибутами "id автора" и "id спектакля"
>9. добавлена новая сущность "Художник" с атрибутами "id художника", "Фамилия", "Имя", "Отчество", "Биография", "Путь к фото"
>10. добавлена новая сущность "Худолжник спектакля" с атрибутами "id художника" и "id спектакля"


### Сущности системы
- Театр
- Социальная сеть
- Театр в социальной сети
- Зал театра
- Место в зале театра
- Спектакль
- Событие
- Билет на событие
- Транзакция по продаже билета(ов)
- Купленные пользователем билеты
- Пользователь
- Отзыв
- Закладки пользователя
- Посещенные пользователем спектакли
- Актер
- Актеры в спектакле
- Режиссер
- Режиссер спектакля
- Автор
- Автор спектакля
- Художник
- Худолжник спектакля


### Атрибуты сущностей

#### Театр

|атрибут          |тип данных, ограничения|
|----------------	|-------------------	|
| *id театра* 	| PRIMARY KEY |
| название театра | string 	|
| адрес театра | string |
| телефон кассы | string |
| телефон справки | string |
| описание | string |
| путь к фото театра | string |
| путь к превью театра | string |
| путь к логотипу | string |

#### Социальная сеть

|атрибут          |тип данных, ограничения|
|----------------	|-------------------	|
| *id социальной сети*	| PRIMARY KEY |
| название социальной сети | string |
| путь к логотипу | string |

#### Театр в социальной сети

|атрибут          |тип данных, ограничения|
|----------------	|-------------------	|
| *id театра* 	| PART OF COMPOSED PRIMARY KEY |
| *id социальной сети* | PART OF COMPOSED PRIMARY KEY |
| URL на группу театра в социальной сети | string |

#### Зал театра

|атрибут          |тип данных, ограничения|
|----------------	|-------------------	|
| *id зала*	|PRIMARY KEY|
| название | string |
| схема | string (path to the image) |
| количество посадочных мест| number |
| *id театра*	| FOREIGN KEY	|

#### Место в зале театра

|атрибут          |тип данных, ограничения|
|----------------	|-------------------	|
| *id места*	| PRIMARY KEY|
| ряд	| number |
| место	| number |
| зона	| string |
| *id зала*	| FOREIGN KEY	|

#### Спектакль

|атрибут          |тип данных, ограничения|
|----------------	|-------------------	|
| *id спектакля*	| PRIMARY KEY |
| название | string|
| описание | string|
| путь к постеру | string	|
| путь к тизеру | string |
| рейтинг спектакля | number 	|
| *id театра*	| FOREIGN KEY	|

#### Событие

|атрибут          |тип данных, ограничения|
|----------------	|-------------------	|
| *id события* 	| PRIMARY KEY|
| дата и время проведения | datetime|
| признак премьеры | boolean|
| количество свободных мест	| number|
| *id спектакля*	| FOREIGN KEY	|
| *id зала*	| FOREIGN KEY|

#### Билет на событие

|атрибут          |тип данных, ограничения|
|----------------	|-------------------	|
| *id билета* | PRIMARY KEY |
| цена билета | number|
| куплен | boolean |
| *id события* | FOREIGN KEY |
| *id места* 	| FOREIGN KEY |


#### Транзакция продажи билета(ов)

|атрибут          |тип данных, ограничения|
|----------------	|-------------------	|
| *id транзакции* | PRIMARY KEY|
| дата и время проведения транзакции | datetime|
| сумма платежа | number|

#### Купленные пользователем билеты

|атрибут          |тип данных, ограничения|
|----------------	|-------------------	|
| *id билета* | PRIMARY KEY |
| *id пользователя* 	| FOREIGN KEY |
| *id транзакции* | FOREIGN KEY|

#### Пользователь

|атрибут          |тип данных, ограничения|
|----------------	|-------------------	|
| *id пользователя*	| PRIMARY KEY |
| email | string|
| пароль | string|
| признак администратора | boolean |
| имя | string, optional	|
| отчетство | string, optional |
| путь к фото | string, optional 	|

#### Отзыв

|атрибут          |тип данных, ограничения|
|----------------	|-------------------	|
| *id отзыва*	| PRIMARY KEY |
| текст | string |
| оценка | number |
| признак валидации | boolean |
| дата и время создания | datetime |
| *id спектакля* | FOREIGN KEY|
| *id пользователя* | FOREIGN KEY|

#### Закладка пользователя

|атрибут          |тип данных, ограничения|
|----------------	|-------------------	|
| *id пользователя* 	| PART OF COMPOSED PRIMARY KEY |
| *id спектакля* | PART OF COMPOSED PRIMARY KEY |
| дата и время создания | datetime |

#### Посещенные пользователем спектакли

|атрибут          |тип данных, ограничения|
|----------------	|-------------------	|
| *id пользователя* 	| PART OF COMPOSED PRIMARY KEY |
| *id события* | PART OF COMPOSED PRIMARY KEY |

#### Актер

|атрибут          |тип данных, ограничения|
|----------------	|-------------------	|
| *id актера*	| PRIMARY KEY |
| фамилия | string |
| имя | string |
| отчество | string, optional |
| биография | string |
| путь к фото | string |

#### Актеры в спектаклях

|атрибут          |тип данных, ограничения|
|----------------	|-------------------	|
| *id актера* 	| PART OF COMPOSED PRIMARY KEY |
| *id спектакля* | PART OF COMPOSED PRIMARY KEY |
| роль | string |

#### Режиссер

|атрибут          |тип данных, ограничения|
|----------------	|-------------------	|
| *id режиссера*	| PRIMARY KEY |
| фамилия | string |
| имя | string |
| отчество | string, optional |
| биография | string |
| путь к фото | string |

#### Режиссер спектакля

|атрибут          |тип данных, ограничения|
|----------------	|-------------------	|
| *id режиссера* 	| PART OF COMPOSED PRIMARY KEY |
| *id спектакля* | PART OF COMPOSED PRIMARY KEY |

#### Автор

|атрибут          |тип данных, ограничения|
|----------------	|-------------------	|
| *id автора*	| PRIMARY KEY |
| фамилия | string |
| имя | string |
| отчество | string, optional |
| биография | string |
| путь к фото | string |

#### Автор спектакля

|атрибут          |тип данных, ограничения|
|----------------	|-------------------	|
| *id автора* 	| PART OF COMPOSED PRIMARY KEY |
| *id спектакля* | PART OF COMPOSED PRIMARY KEY |

#### Художник

|атрибут          |тип данных, ограничения|
|----------------	|-------------------	|
| *id художника*	| PRIMARY KEY |
| фамилия | string |
| имя | string |
| отчество | string, optional |
| биография | string |
| путь к фото | string |

#### Художник спектакля

|атрибут          |тип данных, ограничения|
|----------------	|-------------------	|
| *id художника* 	| PART OF COMPOSED PRIMARY KEY |
| *id спектакля* | PART OF COMPOSED PRIMARY KEY |

### Концептуальная модель данных

#### [Диаграмма в draw.io](https://app.diagrams.net/?lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1&title=Untitled%20Diagram.drawio#R7V1bc5vIEv41qto8RMVw5zF24uxukj3ZTbKXJxWWsMUx0ugAjmP%2F%2BjNIgIAZYIQ1w%2BDt1FathBGXme5verq%2F7p4Zl5sf72N%2Ft%2F6EV0E007XVj5nxdqbrhubo5H%2FZkcfDEce0Dgdu43B1OISOB76ET0F%2BUMuP3oerIKmdmGIcpeGufnCJt9tgmdaO%2BXGMH%2Bqn3eCoftedfxtQB74s%2FYg%2B%2Ble4SteHo67uHI%2F%2FHIS36%2BLOyPYOf9n4xcn5myRrf4UfKoeMdzPjMsY4PXza%2FLgMomzwinH565fHv6KPd%2Fb7X39P%2Fud%2Fu%2Fjw9bc%2FXx8udnXKT8pXiINtOvjST3c3Vz%2F%2Faf73793nq98ftPdvrn99%2Fdo2Dtf%2B7kf3%2BYDlL5s%2BFiMYrMiA5l9xnK7xLd760bvj0Ytgu3qTTRU54d0fT0GMv%2BJP%2FpYIzEWS%2BnF6%2FNvG367%2Bs81%2BUg6mtj8rxnfl9KDDFXNRcourVL5zjkc%2Bbgm%2Bj5dBxyBY%2BTuTu9wGadeJudBkI1KRrny83wd4E6TxIznh4ShpSMvFZ12VsuJgHER%2BGn6vy6qfi%2FxtecHyHp9xSF5Z1wr1LLQsV07D0%2BqXOLx7%2FquqcDQuZDYupDcvdBgb6kLkQ%2BXFj4f2sseWw2%2B%2FPgU3rv7tHf7l6d317Sd7tb58XYhdRQ7v42iR4sUSbzb32zB9pOSSiNAu%2B0jkIA396A%2BCHv72di%2BQKd7lohUFN2n%2BMc7HP%2Ft8jdMUb%2FIvfhTebsnnw7kX3wNyPQIgb%2FLD%2B4td3IRRdIkjHJMjW3yQ4Z2%2FDLe3Hw%2B3MLXjoT%2FyW5nkECbXu4n2sr4OV6tgmz0KTv3Uv96%2FSfazXTau%2B5G2Lsh%2FZOwvtbk1s8hrXpLv6Pid%2FJedHqeXeEvUxg%2F3GhD4SfoQJNnTr2K8%2B1oI8v618f12FawKVevWu3wWyAgEPxr4yaNstCYU8qXV5QtZ9uF7VVNshqbobrtO1ITwZInjQL5TJawmVQyB4RK0hlSdS6j65CZ7xz4hyNfo%2FB7HlbEqHB3q3YmThi1m8tlAjqjJ%2F7oO%2FDSIaRl4CDeRv5%2B%2BG7xNi4UwG6flOoxWH%2F1HfJ89L1mklnfFt4s1jsMncr4f5SdX1zDdrp3xJftloa1BQs75XAwoKg999JNCzJY4ivxdEl6XT7IhCh9uL6riN0DteRdUSjJa1R41lhVkaJTal5Zibea1jqnPb3dUx%2FJ%2Bev12Ln03NsjY9Zv5EZGELRGHi2wQk2cueJ02R0UC04MELsjvhCx1CJa6qsxXtdmkFaAbN%2Fo14LEuWr0Cb7fL%2B%2FOgjl7nPn%2BAla4N97qVlXdJPH2lEzb9JjX9W38TgDEtzZgWACqFPI4HKhYYz8%2BEFLNl0pWCFKYxr1Fz769WxEhNAFRU2aF34EwrqDiuPFBhyhW9JwNMEbUhVwxS6M3Q0k%2FWi1WQ3C12azJXi%2B395pq1OweEmQ7CIM0cGWLA5yfR56cWxND7oCqwLG5wvIiDm4C81BJ2R9OGGW4noyhZg92RPJgx1YIZm5p6YsQs43CXhngLuDJpXGHELOXiigO4Ig1XbLVwxaXNFz9dZwSJCN9iAJZJA4sr0Z%2FLlC4PgEUasLijAQtbNmmLpaRCaCExWbQveEkmfHapz95otFgAPWI4PaLJimLxFVwGDpSOlBPZEfZ06BG0qVOlR2g%2FXX1Ar2bZg2UUyGyGyo%2FJXlwX2yB9wPFdebr%2BSswiCayK57MqbG7FaWdVMBXF0tr15HmoSdtjFREEgkV9%2BeyXAKdFAs4WDT2HJLDdnBzOHvUY9MGPMP07%2F232%2BZ%2FsMwGIw7e3Pyp%2FevtYfNmS8fq7vDz5cviVW3w9%2Fmz%2Frfa7z0EckgEP4vzgYYwaRPphnH52MLHINeHj9I9H4bcpimSD%2BchL4be9xoW0hsgLpvAX71FRhNxy1LXfDovxv9l6PD%2BnvjnhFqc553ZA4dSMx07dr0giwygEY3AMY7BHDTqQ5SRjkEcSz0dc0Sl5AwtQnAMF9SfdSXXNItoCBIqtSj7ZIaDCoNjKzU9DtF8OIEUYpFjDIEXU5Jv0ikJNvsKbyrlp65WNJZprRvH3lq0l%2BdLcIZbbzXxfWm44e7abM8E7y3zOqxtLtmOgP4IoNje84Vw2nMYCyLuxNNzGhZo7VMEbS0YKy4SUAQ3xsGg1gT%2FK%2F0giXxTL6JV5s5%2BNI1TmLWpLPLAegu3UL5QBmlSZp23KL7tsaVtGDMMSvCjDvSivUdNvxk0f1Ic5UibjR2GEhpNCCMGFMikXitVi4I6Qpcx%2BPjreCy4UcfsdSzF2GyOcCi4U5V0oPaAiM0uZ%2FXxAa5MIKePx2tj8XTocCUz8F4Iso6cq25CrLJGJr1iycuEKYHDxdzhh1hADcJkOuIyfpcxTlBXQ5VzooiuGLoxE5RxdsrGJCLy0MPEBZCYEMrxORqPDx%2Fg8OYMkZYkgMzBL2Zt7tX%2FCQIf2v8R%2BCv6XaWOMPTrGgANGIsYMdMDIwhiHdsiIrngLSCMJabyxkcahHTJXH9CzpQrAplOZFQYb2kdDCYOCnKGWDKs%2B%2Fs%2BQbK7DcJyFM8TdVGVoLFIoZ6jJxxiYfoUadLtmwqFgwpDLSkhVX%2BCPjFFvVieMGp3SOyXCaGH49GqCY4yrCa91ba5V%2Fxk1iTbsDL3d45%2BtYZpiOnPPqS4CtbuYJpn9xqMLz1ycdg5vg26tzT3beYb2nLb2iNYe1%2BbUHm%2FkXlzIaRg3Tk2uHR1l2jNMZfY649av5xny9YRjP3%2BinlR0QUEa9tyqWWKoRxeYme7k%2Ba7CbKClqIvHyHtnm139cQ%2FBee9WQz%2F0YbpRNqRsu5BoreBphqDy6mFVVAN1K0bXunHinkW0IqDCeunVBGSOvHLYyKxJsKdn9vDQMhAuai4VnofmluSlgsEdn5RSmN4JajHQdGKpk3C1MHjz10ZXi%2BaO2jUGrhCokcDmeI3yacKVYeqbc9c%2Bzxqh2M4cFTYIhzL0OzzFrhFe3crxmglpvcpQaJHtSBb%2B828aIH3zNAeUySnl%2Bsi1sAyt7oBCNZE3vYH4bxj6vH4py5LvZHKmvU0YuH9WCe4tXlcS4qAci%2FXEGlrDmVQTX9Qs4cWrCUTDnXn9WrrhyVeFaW8OhqiCartjnV8XRt4GFLZXKbG2PVT6m6neDpIbpEOMYqHfkn9303EBGf2mVZ%2FmsnjDv6nreLfaVwTwPoGe4xPL5s9xpJWPNXo6P9Ihn18mHQtxFJuSWxNRp11ewcYPIzEwA0TPc1VF7EGW0XP6kQ6ccpm4olhWf5k3VUuPS5IHHAuyYABaJEHL6En9yICsfonQYiiW1o%2BK8GJl%2BsNk4a82IZQLmTa0jJ%2FSjwzI6ZeJLbpq2EJn9UOBs%2BnjyuidxpEBafwycUWxbuPIoP25GzKQUbAAeJk%2BvIzecBwZ0HJcJryo5sU12tuO79Y4hb7jEweY0RuPIwPcuTIBRjV3LqNK6yXebIKcfwGciHNxIhxjKCfipXc5QIxirsuDDAItYlq0iDbapjK0CEbpWKBFCFzvOLiLktc72g1M3i5lrndgSqtkSvdgy%2FjECEbhWEAWccjSX6tFMrLQjmAo4Tl5WBmfFGFDH1qZsDKwEa246acdwGGyIC94E8abQND2COBFErwoQIxglJ4GfBGHL%2F0ZvpLxhfb%2FLuOsKvBq4cOeaOLoMnqTA8QoOg3oIg5dvGHoIqsqMGKUiRbf0RbwRhbejN7wADHqTkMdcpGQ4wz08MqDHNrjKzTjFtBGFtqM3vQAObTL9%2BoDGDgC0Wag11ce2tDbqQuM7zZ%2BfEeLBRAq8vkZVGTCqBfZNDQ6ulzW6anXRTHbZ7%2BDUFEYNxNgVLj0rqtc87SfiEH0apY9loG0%2FQyVH%2Bu2eHam%2FkrMKgkEDCEEDKdlA9hOwGCqSLN3xvnw0WWleJbyB1wMgWunOyzfU5wsOHRoIw5uAvIeSwibKm6b9wCNwwk0eke9p2cKF4Q1ZNrlA8Mawqa%2FINZPtMJhrSeANuNuluHMalUOPducddc5ZHbMOIyUyOKH3GWfOQRLbPFDs1H80EKNa3AXP7RQz5VEFz90OVLgz6YTxap5lnZ8J9ax3V%2FnfD1fOKS0P%2B4iuFxtQ7bKuNvJUtpsC2MWHvUeKSXz7j9WTstXp45H1tmP3Ppkhul2%2FYB8ODzDWZWGUa%2FxZz9iVFEDX85wX47h1EWBOzcGNSvRvrTcGEYZxzURP8iLmZRbpq04pCppMYxakeCJEbdb4ujyIJUDxqjoCMUrlHfB9IDK6PkwjEKRACnCIGUg8UvY5NNu%2FqJuRbJcBwAu0waX0bNiGKUiAVxEgYuhWBIvo5Tj0s9GOX0EWJkyrIyfDcMoEwm4IgxXFEvhZZRyTNdZKgyQRSePLKNnwjAKRQIxXSS4DEzklcUUNWkj5kvAyriDwMLwwIKDILDQIn60oZMQ8YPAwqQCC2aLBaVKYMGkLSoILIhb80zFqmObtM2TkUPAklbZku7BlNHjCiZUxJaIKIoVxDbpSDWxRu830CBo0qAyejzBhCrYEkFFsSLYFh2pfsqmCCBlwpAyfizBgm6G8jDFUqyZYWEmyyJuAqxIgpXRAwkW7TiGQIJIZNGHIYusQAKjvs2779C%2F48yRBHNgIOHFd%2B9glMAJvkPrjqlFEtoK66gSSXAgkiBz0XMUiyQ4dCRhBTVqp2BP9wDL6OEERhESgBVhsKJYOIFRJGQVJMs43KUhhpjCpJFl9JgCoxQgIIswZFEspsCowBcmi10cbMIghtDCpJFl%2FNACs4oeQIsYaBlYN0%2Fc5NOhBf%2B7H0bZmy0yEmey2N5vroMYUGbSKDN6pIGnXhSgzLlQRvEwg8sgjEPnjpeCNaM37nBp%2Fy5ENUXCzUAHrzS4oR2%2BwJ94CUgzetMOl3b4Qs8OkUgz0OcrC2k82lPzNVzeBUCgEFrj0S7qivanYg5r1zEZBoVHO3PSvQAChWJSFAqvu13V6BQKj%2FYbAYVC3LrnKVY1yaO9Obs4hE4bitvTPagyOn%2FCg4pJEjFFsYpJHu21CZPFNb7Pbg24MmFcGZ094dEOIMAVYbgysFiSsDaaGr0nEssqB1yRgyvc3AlxTXs1eh8EoQaRzcE01VuEa%2FTWSGgxLAAbSWBjjA820CFcMtio3iHc5aAFq9uZEM0qfQnLLoV9nQlnta6EZS%2B3lvZth%2BEQ2X4wn9z%2Bxm5uv2EsuLGb0dOOjbuxm2GYc8%2FUjv8aF0Yu0QDUqgCimxMywnBTUItCxNFpIl42%2BjxBnUSrRZHJq75WNKq62qixfHPrhNtzIeEdOWnr4EtBqiOH%2FwyTMCVWlK5dZMP7LWFxeiEoPTwofYSdAgWLWlB9jaudDvugIyht12%2BncFQaMRh590leCl%2F7ieyYX82yx8o6j2YTVH48%2Bmmys%2FRXz7Z1IYTdryBnCmGjNlpgewybqR2WsP0UgxdYkT2IZwvcWXGs%2BqydlThZMGmTsWBuaRd5DApWTkErp9VYyYqspF46F9Lb5eEl0LmQ2cnnKpZOWBQnsyiaihO7kElHNGAlFLgSmopRuxCj1Ghpq0MAQ%2BEARh%2B28NK7xAUwGIVMIYAhElws1aOljAKkZJS2ib%2FMiuYA5kwdc3gteYGYwwqaGoA54jBH9aApYmz1j5hDSwZs7Z%2BxtS867BRUUJ0TEEqyw4vd2iPG1l7C0gf7eiH7eqT6vr5wlcG%2BXs4yiFTb1yPa1F6R0Vuk4QbythS3snvQZfTELYQgc0smtiiWuoUQo9s9Gb9oscQJJG9NG1xGz95CCNK3ZIKLYvlbukZPf5XY9maZkomDXfs5d%2B1IK9JYyv0LJ5cNGXq7HLwIMpuu0UWf%2FEwGe9ls9RqHwGib2iY%2FRyJ1GW26RvcgAEablGUzRwV1GG26RucGxTiCrb7a1ngfxjicGKO7ouSKET4BWBEHK94wa1zc9DPCFuuAWFzAEJo8uLAKKshGFzpMAeF6kQAzNE4hTgI4OgWcLXmzQImz5G1WUjX%2Fya%2FVlbe5v85VmA3PW2327JzM3lTLVu2XloBsN8LzyGlYv9zJll7jSrrJl2JM5t1%2FrJyWa2L7I5e5CI1Hbn8y5HT9gHw4PMN5fRI88RcFM56LzOUyW7nUG45CAHPTcav6huaaYffo3P7b5yAOyYgH8XkUr79GgMetohxoDDUCzlMjgLZjwZMswpOs1wGUu9s5cvVe6Z02A4xRRPnoSAa38FTcwqitOrMy3C9GuWbwBQsMoR4UW50QKmIUVk7uCbwB80txj00ftozP%2FGKUbQZkEYcsA1ttiZt%2BmpwBsDJ5WBmf8%2BXRJAuAFXGwMrCvlrjpp4kMGzKQUbAAdJk8uozf8xx5HIVTAV7OBi%2BuWvCiazSHIQpvAFcmjiu8Xc4FChbtVQZcEUeOaclcGA9XaD%2FLzk%2FXixQvInyLAV%2BmjS%2FW2J5cXQNvi0x8keZtIV9jjNNqgCn2d%2BtPeBVkZ%2Fwf)

![scheme_1](https://schstp.github.io/Theater-Platform/datastorage/database/version_1_0_0/data_model.png "Концептуальная модель данных")

