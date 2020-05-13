>*updates*:
>1. в сущность "Театр" добавлены атрибуты "путь к фото театра" и "путь к превью театра"
>2. в сущность "Социальная сеть" добавлен атрибут "путь к логотипу"
>3. в сущность "Закладка пользователя" добавлен атрибут "Дата и время создания"
>4. из сущности "Закладка пользователя" удален атрибут "Комментарий"
>5. добавлена новая сущность "Режиссер" с атрибутами "id режиссера", "Фамилия", "Имя", "Отчество", "Биография", "Путь к фото"
>6. добавлена новая сущность "Режиссер спектакля" с атрибутами "id режиссера", "id спектакля", "id театра"
>7. добавлена новая сущность "Автор" с атрибутами "id автора", "Фамилия", "Имя", "Отчество", "Биография", "Путь к фото"
>8. добавлена новая сущность "Автор спектакля" с атрибутами "id автора", "id спектакля", "id театра"
>9. добавлена новая сущность "Художник" с атрибутами "id художника", "Фамилия", "Имя", "Отчество", "Биография", "Путь к фото"
>10. добавлена новая сущность "Худолжник спектакля" с атрибутами "id художника", "id спектакля", "id театра"
>11. в сущность "Актеры в театрах" добавлен атрибут "id театра"
>12. согласно приведенным апдейтам обновлена также КМД в draw.io



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
| *id театра* | FOREIGN KEY|

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
| *id театра* | FOREIGN KEY|

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
| *id театра* | FOREIGN KEY|

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
| *id театра* | FOREIGN KEY|

### Концептуальная модель данных

#### [Диаграмма в draw.io](https://app.diagrams.net/?lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1&title=data_model.drawio#R7V1bc5vItv41qpo8WEVz5zH2xJkkM3tnJsnM5ElFJGyxLQkdhOPYv%2F40Eo2Abu40dCsrNbW3hBFC9Fpfr%2Bu3ZtrN9sfb0N2v%2FwhW3mamKqsfM%2B3Xmapqiq3g%2F4uPPJ%2BOIMfUTkfuQ3%2BVHDsf%2BOS%2FeMnB5IP3j%2F7KO%2BROjIJgE%2Fn7%2FMFlsNt5yyh3zA3D4Cl%2F2l2wyX%2Fr3r33qAOflu6GPvqPv4rWp6O2ap2P%2F%2Bb592vyzch0Tn%2FZuuTk5Jcc1u4qeMoc0t7MtJswCKLTq%2B2PG28TPz3yXP559%2FzP5vcH8%2B37Pw%2F%2F5365%2FvD5P39fnS522%2BYj6U8IvV3U%2BdIvD3e3v%2F2t%2F%2B%2Ff%2FcfbP5%2BUt6%2B%2Fvb%2B6Iov53d08Jg8s%2BbHRM3mC3go%2F0ORtEEbr4D7YuZs356PX3m71Ol4qfMKbv168MPgc%2FOHusMRcHyI3jM5%2F27q71X938UfSh6kczwqDh3R50OmKiSjZ5CqZ9w2fR%2FLcDsFjuPQqHoKR%2FGb8LfdeVHViIjTxE8lIV%2FK833rB1ovCZ3zC01nSkJKIzzorZeRg6G3cyP%2Bel1U3Efn79ILpd3wMfPyTVYXoJ9GyRDs1R8lf4vTbk09lhaNwIb1wIbV4odOzoS6EX2R%2B%2BPnQUfbYcvjl%2FYt3Z6tf3gTvXt58u%2F%2FDXK1vrojYZeTwMdwsomCxDLbbx50fPVNyiUVoH7%2FEchD57uYvjB7u7v4okFGwT0Rr491Fycswef7x629BFAXb5I278e93%2BPXp3OvvHr4eBpDXyeHjxa7v%2FM3mJtgEIT6yC04yvHeX%2Fu7%2B99NX6Mr50F%2FJV%2Bn4UICvd7c5yvraX628XXwrQeRG7rfjL4k%2Fto%2Bf6%2FFJG9f4P%2Fzsb5S5MTPwz7zB79H5Pf4vPj2MboIdVhvXP2qA5x6iJ%2B8Q3%2F0qDPafiSAff3bwuFt5K6Jq1XrXTrPiJ%2BX9qNQEIl9KXr6QYZ7eZzXFZGiKapfrRE4IW0tcA%2BRrK2E5qWIITCNBK0jVUEJVJzfxbywVgmqdLUpBupknN5PbL8twUjP5LD4byE1q8T%2BvPTfywviTO%2Fw%2Fn4IlXvHZjTp7rdBy8eRvN%2B5xSe%2BCXUQ2x%2FjZLdf%2BZvW7%2Bxw8xr8Bb1zLB%2FLueh2E%2Fgs%2BH1%2F3dHJ2X1PN3Bmf4k8SDfYO%2BJyPZD1Qeuh390BEbxlsNu7%2B4H9L72SLQcDfXWdFUkgoIBZmFgls5p6p126PZw1Nv04167%2BOCTxm%2FtvcDZaOHRaR6%2FghHnpugpXmRUYqo5NULvDnVOWX2w%2Fo1Sy%2BsXjfj1cofXk4iuti50VPQfiQnq6%2B4rNrItg1s6qSBQGd1ptqCKpXnOe8RNYpiqGU60k%2F1LQZW2Yqgh8%2FwP5ZhpzV6s5t%2FxxCEthbv1FvPInnNno%2F%2FOjf5LPx66%2FxawwQp3e%2F%2Fsj86ddn8maHn9e%2F6eXxm9OnbPL2%2FLHju9znPnqhjx%2B4FyYH222pWb%2BVuQqIxFOk81vNgruJtIKl19RvNZ3ChZRx%2FVbyOzKKkFiOqvKf02YM1uOQ1mNxwY2G5hxSKnwJ2azHSjTIiCLDKgRrcGprsBpHelmDTSRxMBsA0SE7MAFbhlBQGf4NF0Lhtvy0Cbhztx4fhIEobc3mOhCokEzIZFFZRAfmAFLaLbpRsuhCRWWv332%2F13dfF%2B9s5eHB%2BvreX%2FkvVzq19ns3WsdJoA12HgFZRkMWhuw0BJtSZGlsOPMSrgYRi58aWBrjRV4WyhV5ElxhiqZOW6rU2gsYrSKRpyRElcae6iJPJMo11w1rdo50oVllnAu%2FGS5cxZSK5KFno1Xs4GIiG8JEq9RCxqpzlYVmFy5UDHtxjlYZ9A4rgyIkAo1mHcK2Sk51zppUojzdRZ4tylZDmdd1wWTeoOJsHWXetPIX0k11XJmnN%2F5P%2B3hXW24YziqEZruHZq9QMRiv0UZfWhea2%2FlVpVY%2BWcFZaWKzjHqTAxFCCMuKG5Y1ypzpNmFZtsjzissxikggLNsyhlJamyF%2BWJZRowFhWbHCsu1BhRGWHRlUnHrHASClctHtkkUXH1KIDZVZ%2FJV3WIb%2BPvKDHSCLzMhi2RMji0lXLQCytFr0VD0lRBY6MEsyPvvgcKzGB3CRF1zSiv3p0AWafPqii1qy6hKgS3k%2BOX42GwwvJe09ADISgUzTIKNWEWPsJ2eQWu4LMnrJqg8HMs7cyf3jBjp0%2FCV0I4i%2FyI0x5uQYAwGYvhjDPwAzFsZYdEAm2ycKSCMx0jhTI41FB2RuP6DeUvVzgY3FPyYzGtjQMRpKGASsGSpp26yr%2F%2BnSIkrLxOBsRJVZSmFqhor1GB17OlGh3K7Yxcy5YMhmdbmLL%2FDnqk8nI7tormhapfSyCj%2B7lp5214RKFK3VBEsTTBOuVGWuZP9pOYnWzBi97fOfjW6aoltzx8puArlv0XW8%2BoVb594OLTcxwDyuTswiv2NaPbSn3d4zsPbYZkPtcZBg2oOsgnFj5eTaUlGsPd1U5qgzdv56jja%2BnjTw51vqSUYXBCzDnhs5SwzV6AKTPgPf360fP2ge6kK0oN7sUgVTF5O0%2FKX6oXbTDUuvuRBvrWDUaku1exgZ1WjfbtPVZxlYERAxVmo1Aemi7Rwm0nMS7KixPdyVW8ZGxa3CcVAMZOMqRYOWaJGVQndaqEVH02nY7jX2OpBeLQnVouhR21rHHQIVGtgsp8DJyF0ZZHfObXOYPWJazxwRk6OBMiiCKYPp5K0cp9iQVqsMRItMa2ThH95pgPbNygCU3lDKVdEI9jQlH4BCOZHXnY74r2nqPH8pwxg%2FyGTJ7SZ09J8nhHujaSgpLZQQRhGuNKUQTMqJb2rQtNUErPLWPH8tVXPGVwW5nYMuqjCxd6w21wXR3ICzMZZIrGl2lf5iq7eFxk3SIQYD8ZcDq2EAOvp7dPTrRn6ZU%2FKG2or%2BjnSr0nT0pziQnVhz4FiBBd38%2FUlWVfna%2BZEK%2Ffy9y7HOyipfFwtS6ZCXt3X9DR%2BYgULPTkyr7ZFl8p5%2BpEJNeW9ckberP%2B2byrXHHQ5PQcjJggFoGQlaJm%2FqRxp09feFllQ9ZYQWlVp%2B%2F7BwV1sf6ELkhpbpW%2FqRBj39vbFFLVl3GbCF7uoHgjP5caUxVSg%2FwYI2%2Ft64wr%2BPn9%2Fy0%2FHcLX6QG28B8CI%2FvDDGjY8NL3QcF%2BClJbxIHMXV6ChuSnW2DiKYbiM5wNiTh3M1COf2BhiJw7kMltabYLv1kvoLqIkYqibC0rrWRFz6lAPEIHNdnmQQyiIELosoZZAVuCyCQR0LZRFt9zuzDP1k2O%2FoMDC%2B54i534EpPZkp3R5bpi%2BMYBDHArK0XHatZNllQBY6EAwUntLDyvRFESbMtu4NK%2FyHW%2FNbfjoA7B8W%2BLbv%2FHDrcXKPAF5GghcBCiMY1NOALy3X3SpZdxnwhY7%2FLsOYFXi1cMEnkhxdJh9ygBik04AuLdfdKVl3%2BViBEYMmmv9EW8CbsfBm8oEHiME7DTzkrSHH4h%2FhHQ9y6Igv145bQJux0GbyoQfIokO%2Btx%2FAwGmLNvyjvuOhDe1OXQfBw9YNH2ixgIKKPiQTWp5kU1Po7HLK05PnRdHLV7%2BioIIglAQVFTbtdaV7nvILNohezeLb0pByXKH0Zd4Wj89UX%2FHZJaEAo38BhlXmGLYpwGCqSHF2xnD4aLNaPFP5g1qMtnunXWY2DbZ38pMFi05trDAuRj40TghlmrfHGashzqgVdE89ZQuyGr3Ncv5ZDW7LT%2BrqJSU4zI0EUGaNZ2VYsxzJoWPqs2qaQ%2BbAjHYmewPuw8asz5ZohLhXeoH70ECFazTmPjRQzZV4cx%2FaDTrgB9MJsmsOMo2vJY3t8TqdR740kFJHNCnVCrKVpt1aS2lxKoxOAuo1UorX3X3OnJbsThW3rLJvufTONN2u%2BgB%2BcbqHQZWGQdf4m7thkKhBKKd7KEez8qLQuDUGFYloL601hsHiuMbiB20x4kZlSjkjxe2KYVBFQiCmpbekylsCxiB0BO4KsUIw7UFl8nYYBk8kQEq7Redf98Vt8ekoP6GtOCzXHoCL3OAyeVMMgykSwKXVomtlXpoE4MJo4XXjpxw9A6zIDCvTN8MwWCIBV9rhirwdvAwmx2gdd8JAraj0yDJ5IwyDJxLq0luDC%2F8%2B3rEKRXXaiPnksRruILHQPbFgIUgslIgfbegcsPhBYkHcxIJeZlmJm1jQaYsKEgst9zxdXnJsnbZ54uIQsKSFsaTbY8rkeQUdCLH7Ioq8fNg6nanG1ujjFuYDSQ0qk%2BcTdCDB7gsq8nJgG3Sm%2BiVeIoAUiSFl%2BlyCAcMMe2JKqpgSYgqdoOZauAmwMhKsTJ5IMOjAMSQSWiOLWrLw8iUSGPQ2b77D%2BI6BMwl6x0TCxQ%2FvYDDgeN9hcofQmYRSvh1xMwkWZBJ6b3qWvJkEi84krICiVjh7uj2wTJ5OYHCQAKy0W3R50wkMkpCVd1iG%2Fj7yA8gpSI0sk%2BcUGEyAgCztFl3enAKDgM8%2FLPaht%2FW9EFILUiPL9KkFJokeQEuLVedPm8dv8enUgvvd9TfxDS%2FiIs7DYve4%2FeaFgDJSo8zkmYYmfFGAMpUoczlpBptRMA6DOy4Fayaf22HT8V3IaraGG%2F4B3tHghg74Qv3EJSDN5DM7bDrgCyM7WiMN%2F5jvWEjj0JGaz%2F7ywYMCimQl%2BHA8moRXtL4Vs9u0DmkqKBw6mBMdBRBKKMQtoXDK4kfillA4dNwISiha7ntOGe6JHzZ06GjOPvSXkIsQyJ5ujyqT1084wJjUF1PkZUxy6KiNf1h8Cx7jrwZckRhXJq%2BecOgAEOBKu0XnT5bEbYqmQvtEfKvKAVfGwZXGtRP8ZvYqtB8EqYbWw8EU%2Fp7QaDN7Fdo14kqGBWAzEtho04MNDAgfAmwuaEC43aAsWNzJhGiWmUuYTimsm0w4y00lTGe5lYxvo6Wi5%2FjBZC3rB7uRKgSBBrtpNePYGg920zR97ujK%2BV%2FhwsjGGoBKFYD3cEJGGk4GtSAijtqJeDros4U6DawWpBtQQq0osLqaqLB9N9YJu%2BZC3Cdy0tbBJ1JUhw%2F%2F7R%2F8CFtRqnIdP94vB1ZNLySluyelz7BDUJBQztQNrrYq7IOKpLSZ%2FzqBs9KIUZH3eEio8JVfsMf8ahbfVjx5NF6g9OU5ThOfpb7qbetCCrteQbqksFFpuWCbHDZTOwxu%2FhSjLjAje5DPbutZ2dyDxEPIwsvD3e1vf%2Bv%2F%2B3f%2F8fbPJ%2BXt62%2Fvr1j8ap9P4zpgkxxyk0QFc6tpBad6QRz6bAGkA8m858XAttdm26uGDSErt9i3TMenYacr3%2BmqlVXobCj71mkvEebzTpabGAhUxizcYt8y7d8BpLRbdHn5tOhgq7taYRv1AKAiM6hMXrUFvBQ9HXJ5aSloZ2jpHtaLlXd4WOzXeK2AleICEGZ67hsgpegJMVI4Qmy6dmrps8CyuAvCRejdefj3Q1uL5DDTlPyG3wAHgJmeA4GkhRkG1zCQgl4IrhhTd%2BEC3XBPXJGXbZgmG9670XoRBYtNcB8AsEgNLITqbbqGOQCWnpw2MgDL9bvv9%2Fru6%2BKdrTw8WF%2Ff%2Byv%2FhRHNJcCC%2FaMIkGU8ZGEIT0OwKc8%2BKyMGdZniBUHdamRpjBh5YShXZXGQhQ7qpsgSet99D4a5y40tTRvkuAkYRHPHwxZVLHcI6bTdQpj3lOuEQwQ6H4pLO1DnAynLJWWWTf0XhNRyeZCsqrNELCv5%2BEjrA49tD6o7%2Bzc16GUZdCHKO0vumTazoL6zpfd%2BVluh%2FXf2vTNaGdJeK7CvRSGg6IAtTas8%2BRFQMJoUgICiNbiUBoQlJKBgdBPgp7Q7uMs4vwmYIzvmNLXkOWIOi%2FRGA8xpiTkXRHqDGK7%2BGXNoyQDXvodrr1s5X9tSGwJCWtt5sa49Yrj2I2x94Nf39%2BuRhH49CZWBX99jG0QS%2B%2FWINrVX%2BOktIh%2FaN4Wystujy%2BTE%2BwgB835vbJGXeh8hukI9ws9vs1gGByDflxtcpu%2FjREC%2F3xtc5OXfVxV6%2BbPEhK%2BXEV448NqH9NqRQliOU%2F%2BlIRch0tRyOajw2%2BUhI1QVum3CjWWwlo0wP6MaGAmFdvLPsCMPI2FanguMhMN0J6eqLjQjYcm9000YYbABV18ga7wDxlgNMUa1eckVI30CsNJy2Z2SZR%2FOGue3%2FIy0BWeiSQCXkcCFRagyNrrQaQpI17cGmBHyFPwkoEEbxmDDNwhKDDJ3IzNq42tyraq5G8fr3Prx4%2FlVae3N147KSPVfmFEZV2YhPY%2BsrsMynMKVVL3ZiBi87u5z5rREE8tvOe1FKNxy%2BZ0hq%2BoD%2BMXpHoaNSTTJvwg4sYZMnkmnzaR602CQ01y37Ky%2BobmimTU6d3z30Qt9%2FMS9sJPi1c94chqrKMFpcVT055nxRNuxEEnmEUlW8wCqmyplY7IrwGy1VnrlrgBzaFv3HEiGsLCQYeEzbkhU%2B%2BUAZ3%2F%2FFGqqrfKlUJFDm4eHxxCI%2B8WK2HTAlukrvxwgp%2ByNLPLSUyKHLs4AWJEeVqav%2BXKAm7I3rMjLTokcupBhix%2FkxlsAukiPLtPz9iMHGCp7w4sUHJUlqRG6hmHj3wGuSI4rkxP1qwrwU%2FYujpF47JDCmAoC7LeXAzCTM%2FarCoRbegOMFOEWJmum3mD1haqNKda4pNn7K2WuIDTLlsvMkZoeaJ%2B%2BL6TQhy%2BkmS4pb%2BYz5ykNT%2BuUfPFKxaHoAxXNFL6lrmIGu4NKvw%2BQquihamzYulfdhvYxDFaPy5%2BbGraGFbpcC8vrB5zCUp87WH%2BqTjS2RNIx0n0ihXEJwY06ew3taAIaqIy6gxrNqQCkNmUH3LrR2PcHzWgTkaufgKG12cpPEqAVTex5DV3wZcxONOb9GXQQFyCFG6Q4nSCF3%2BJDG9qlAsuoXWhs4VIp4YImNI7gUjYZaCpwoT198O75ePeFyS9XWtMU3iV1BzBlsNq3BzddGje9tZc%2B7tAz2kkHz5zfTtfNMee2%2BLRfDm0BMljQ1ZgyZlMAe0greObjQUpHx5zb2tOOOQCK5IAyZjsAW6hohxwAhRegoI7eOLfFp7tXoRfgMoBl1E4AtnABcf2IyKIJhix0OR20AcgOKWM2AbClCujqR4QUQzBIYcRtoQPgUrBlzPp%2FtnixaqoAWzhhi2DRWlLQmqUsw2vBmrADWclkMbpkJTVS6g1ZSUoEaV%2FcPYogJCWlSkqeoETcrKRGu%2BWQluS302mCOeYa7ZhDYlIG%2B7kGVybPTGrgm4%2BIKoL55hrtmwOkyA4pk%2BcmNXDJR4QU0VxyuoIKcpMXgizTJyd1qKMaEVoEK6TS6UIqSE5KjymTZyd1OogMmMKta1KwUiqdDt9CdvJywGXy9KQO1VQjgotgQVuDBpcsQdLrx2j9c49X4pCqNElCDuiRaHmkwcg9yiCQIwm8Ow6U4DRKwFEUciSDxeQI5EhjkA3onbZNfpJAp6SAHEl4U7wGX6YnR4L5KSNCSj1B7LjkSHRKCsiRLgNYBCBHolNeQI7EE1xsscDFpJNSOTcfKpI5VCQTZx3cfFoe6TzZuSQZ3HxBN8ihyJVKBjSI4uaTYefg5o%2B9bZrdUm%2F8JIGOjoObL7w1XoMvk7v5JiTcRoSUjgk3botPx5DBzb8MYJnezTfpsDS4%2BTzBpWOzBLf1bxBAHmzU2Ju%2Ftu5u9d%2F%2B88a8H34UjxdT5rpjJO9Pw8UcbIqf3p9ni8VvnjNvBp4sdprLVfGMGzSYcx0sduUgZ%2B5k%2F83yUQZNmSuZf6qW%2F4bGg8fsYkd1Gr%2BoGT02VJAA0UFLqEfhUY9Chv5A63xRBFU6bnouR4GQkzQhJ1TSJyBK67xKx0MhzsTPbhNtRCwx06B1XjKPsAZXJm%2BdV%2BkAJqAKN1RRBUMVOs4IkCI7pEzeOq%2FCMPsRIaVb3Su%2FxacDjNA6fyHIMn3rvAr1ryNCS8f6V26LT9e%2FQuu89Jgyeeu8SgeRAVO4YUrHslduTD90%2BBZa5y8HXCZvndfosC2ACzeuH8GCtmaDnUWeZDuaiZZob7DefBPthuXMlfJEu4rmCsrk2Qup0MZ5doMQcEyVZ7caMJZdsiBjcQ2fT5cyyNuv2b%2BdL3V89zySAhDin4hsvaVINLWmOIWKFFQQ6IFKUpCmzouXtvE3Zy5duHfemkPn7fhpDrEQeynNWdR1R88KOwYzC9UI%2FPFqt378jM5%2FHXhbqBV2o75HgK%2BwWwQviRlqKd3E%2BcrSC1cyzEbiiyXCfc6clhhpFbdss2%2B5vPbLQFUfwC9O9zCsNjVIVoI2tdCmCZVENzEw50UIHynCcwsbCe8wVpkphi0xx7HPmwAhERpajXSr4kdV33vNpzgpVINGE1AoORQqDWycZaijLqntdKnwNUPpUtq0V%2Fg9fBWiQe5aUIXIOSZnP6WhKvA2yvTJi%2BLJSpIyia42Gb4jtUI9ruzYlUHnv3Laakp%2BT%2BltYyeo1%2FmEIYSv%2BjUY5ALq18Unqi8T4at%2BRUpLEhttrX5mwfFImUuGVjCz4BKZTs2NFc4nN8ZXYcbs57oYhZlQDzQymr6vHlDkMbz0oOSOy2%2FMVnud31Nv8NswCKLs6aG7X%2F8RrLz4jP8H)

![scheme_1](https://schstp.github.io/Theater-Platform/datastorage/database/version_1_1_0/data_model.png "Концептуальная модель данных")

