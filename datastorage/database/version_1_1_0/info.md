>*updates*:
>1. в сущность "Театр" добавлены атрибуты "путь к фото театра" и "путь к превью театра"
>2. в сущность "Социальная сеть" добавлен атрибут "путь к логотипу"
>3. в сущность "Спектакль" добавлен атрибут "путь к постеру для слайдера"
>4. в сущность "Закладка пользователя" добавлен атрибут "Дата и время создания"
>5. из сущности "Закладка пользователя" удален атрибут "Комментарий"
>6. добавлена новая сущность "Режиссер" с атрибутами "id режиссера", "Фамилия", "Имя", "Отчество", "Биография", "Путь к фото"
>7. добавлена новая сущность "Режиссер спектакля" с атрибутами "id режиссера", "id спектакля", "id театра"
>8. добавлена новая сущность "Автор" с атрибутами "id автора", "Фамилия", "Имя", "Отчество", "Биография", "Путь к фото"
>9. добавлена новая сущность "Автор спектакля" с атрибутами "id автора", "id спектакля", "id театра"
>10. добавлена новая сущность "Художник" с атрибутами "id художника", "Фамилия", "Имя", "Отчество", "Биография", "Путь к фото"
>11. добавлена новая сущность "Худолжник спектакля" с атрибутами "id художника", "id спектакля", "id театра"
>12. в сущность "Актеры в театрах" добавлен атрибут "id театра"
>13. согласно приведенным апдейтам обновлена также КМД в draw.io



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
| рейтинг спектакля | number 	|
| путь к постеру | string	|
| путь к постеру для слайдера| string	|
| путь к тизеру | string |
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

#### [Диаграмма в draw.io](https://app.diagrams.net/?lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1&title=data_model%20(1).drawio#R7V1bk5s4Fv41rpo8tAsB5vKY7klnkkx2M5PLTJ5cxKbbTNvGi%2Bkk3b9%2BhY0wIIERIJA8JzW1a9MYY3TOp3P9zsS42fx8HXm71ftw6a8nurb8OTF%2Bnei6oTka%2Fr%2FkyNPxCHKReTxyHwXL9NjpwMfg2U8Pph%2B8fwyW%2Fr5wYhyG6zjYFQ8uwu3WX8SFY14UhT%2BKp92F6%2BK37rx7nzrwceGt6aN%2FBct4dTzq6Pbp%2BG9%2BcL8i34ws9%2FiXjUdOTn%2FJfuUtwx%2B5Q8ariXEThWF8fLX5eeOvk6dHnstfb57%2BWv%2F%2BYL1%2B%2B8f%2Bf97n63ef%2FvPl6nixW56PZD8h8rdx60s%2FP9zd%2FvbF%2FOfv3YfbP35or19%2Be3t1ZRnHa3%2F31o%2FpA0t%2FbPxEnqC%2FxA80fRtG8Sq8D7fe%2BtXp6LW%2FXb5Mlgqf8OrPZz8KP4XvvS2WmOt97EXx6W8bb7v87zb5SPYwtcNZUfiQLQ86XjEVJYdcJfe%2B4fNIn9s%2BfIwWfs1DmKW%2FGX%2FLvR%2FXnZgKTfJEctKVPu%2FXfrjx4%2BgJn%2FDjJGlIS8VnlZcycjDy114cfC%2FKqpeK%2FH12wew7PoQB%2Fsm6RvSTaFmqnYarFS9x%2FO3pp%2FLCUbqQWbqQXr7Q8dlQF8Ivcj%2F8dOgge2w5%2FPz22b9z9M%2BvwjfPr77dv7eWq5srInY5OXyM1vM4nC%2FCzeZxG8RPlFxiEdolL7EcxIG3%2FhOjh7e9PwhkHO5S0Vr7d3H6Mkqff%2FL6WxjH4SZ9462D%2By1%2BfTz3%2BruPr4cB5GV6%2BHCx67tgvb4J12GEj2zDowzvvEWwvf%2F9%2BBWmdjr0Z%2FpVJj4U4uvdrQ%2ByvgqWS3%2Bb3EoYe7H37fBLko%2Ftkud6eNKza%2FwffvY32nQ2meGfeYPfo9N7%2FF9yehTfhFusNl5w0ADf28c%2F%2FH1y98so3H0ignz42eHjdukviarV6x2fZiVPyv9ZqwlEvrSifKGZdXyf1xSLoSm6U60TBSHklrgGyMcrYQWpYghMI0ErSVVfQnVObpLfWCkE9TpbloJsM09vprBfVuGkYYlZfDaQW9Tif1r5XuxHySe3%2BH8%2Bhgu84pMbffJSo%2BXiR7BZe4clvQu3Mdkck2e3WAXr5e%2FeU%2FiY%2FAa8cS0eyLvrVRgFz%2Fh8fN3jyfl9TbcKZ3xMPkk02N%2Fjcz6Q9UDZod%2B9PRG9Rbhee7t98C27kw0GgWB7nRdJKaGAWJh5JHCYe6Z5dns8aWj2dbp1%2FuuYwGMVv81bY%2BnYYhG5Th7ivuMmWGte5KQyPkrlHH9O1365fYdeTJIbS%2Fb9ZIWyl%2FuDuM63fvwjjB6y0%2FUXYnZNBLtmXlXyIGDSelMPQecV56kokecUZaZV60k31HQYW2Ymgh%2Fewf5ZhZz16i5s%2F%2BxDEthb%2F%2By88SSf2%2Bj%2FDOK%2F088mr78mrzFAHN%2F9%2BjP3p1%2BfyJstfl5%2FZ5fHb46fcsjb08cO7wqf%2B%2BBHAX7gfpQe5NtS834rcxUQiaco57daJXcTGSVLr6nfarmlC2nD%2Bq3kd%2BQUIbUcde0%2Fx80YrMc%2Brcfygs8amnNIq%2FElVLMea9EgJ4oMqxCswbGtwXoc6WQNNpHE3mwARIfswATkDKGgKvzrL4QibPlpE3DrbXwxCANR2jOba0%2BgQjIho0VlER2YA0jhW%2FRZxaJLFZW9fvP93tx%2Bnb9xtIcH%2B%2BvbYBk8X5nU2u%2B8eJUkgdbYeQRkURlZGhvOooSrQcQCgCVuoJ1S4wpTWk3aUqXWXsJoFYk8pSGqLPZ0LvJEolxTc2ZPTpEuNKmNc%2BE3%2FYWrmAKUPvR8tIodXExlQ5polV7KWLWusjCc0oXKYS%2FB0aoZvcOqoAipQKNJi7CtVlCdkyZVKE97kWeLst1Q5k1TMpmfUXG2ljJv2cULmZY%2BrMzTG%2F%2FHXbJbLdYMZxVCs%2B1Ds1eoHIw3aKMvqwst7Px1iaqa4KwysVlGvcmeCCGEZeUNy86qnGmesCxb5EXF5RhFJBCW5YyhVNZmyB%2BWZdRoQFhWruAJP6gwwrIDg4p73nEASKlddKdi0eWHFGJD5RZ%2F6e8XUbCLg3ALyKIystjOyMhi0VULgCxci25VxeIVQBY6MEsyPrtwf6jGB3BRF1yyiv3x0AWafLqii16x6gqgS3U%2BOXk2awwvFe09ADIKgUzTIKNRE2PsJmeQWu4KMuJzy%2B7ULfwTBjp0%2FCXyYoi%2FqI0x1ugYAwGYrhgjPgAzFMbYdECGGDb7dbD0I%2FCeLgF03LFBx4bYTEfQscXHZgSAjj7z9m%2B%2FvHptvJ%2FrX1fv5%2F6X4H%2BkequiNx2ARl2gyeoohgAapmzRUZrbd6izUF0s1NTqp1JIwwZNGmooWZCwSrGiUfxcxWGbpnRaJHrnP6uti5CmSrFcAdayixyVCnzL5WiCSxQdFq%2BGOgLfvj7dsgtC72bvh6hRr0PRs5pgG5JpwpVjF0S4PROgPXXtPMwXLmuaaKqVbk44xYLaZCPTpOK5q5hLUs%2FuWA31w0WS6QeyS%2BZLUV1sHeE%2Ft9w%2BDjrjFK%2FnGsPrSYMYIaee5HRBwtaO6axga6EzusCk5MH3dxskD1qEuhAtOG9Y6ZKpi0XaiDP90Nvphm2euZBorWD0fyi1e8xyqsHfwtfWK%2BlZEZBmNNQEZMq2c1iE8DyVYFfHW3rbrcJyUHmrcF2UANmwStGAZkFmpTBdDrVoaTr1622w14H0fyqoFmWf2TFa7hCo1BRruyWeV%2BHKoKb7fVIGx%2Bpnj%2BB05PtWBmJyNFAGTTJlsNyileOWm1zPKgPRIsseWPj7dxqgJbxOzG2zoZTrspF2Gpo21XL%2FUEHkTbcl%2FhuGPi1eajYbPshkq%2B0mtPSfR4T7WdNQUlZ8JY0iXBlaKZhUEN%2FMoOHVBKzy9rR4Ld1wh1cFtZ2DNqowsnesN9cF2dyAkzGWSqxltZX%2BMn2EjYZNwyEGq%2FnnPauMDlhCOrCEmLPiMmeEMGe7hFpSOCvDEpLhQH4K1l5ghRUwhHQnbtbVowhBOnCEdC7tPCmrep1xSKdDXv7GC9ZiYAYKOVtxrPIjy%2Bg8IUiHPpXOuKIuU0jWi1noTNnvf4SRIAsGoGUgaBmdKAQZ0I3SFVoy9VQRWnRq%2BYP93FtuAqAgUhtaxqcJQQbwhHTGFr1i3VXAFpopBEgT1ceVxvTD4gQLqEE644p4bhBxy0%2FHczf4Qa79OcCL%2BvAyGz2Oa9BxXIAXTnhROIpr0FHcjD5xFcYwMUtxgHFGD%2BcaEM7tDDAKh3MZzM834Wbjp%2FUXUBPRV02EbbStiSDVDRdbE8EgiF4cZRDKIiQui6hkpZa4LIJBRw1lEbz7nVWFfirsd3QYGN9zzNzvwJQezZTmx5bxCyMYZNSALJzLblQsuwrIQgeCgRZYeVgZvyjCatCrAbBSv%2BxVgRkVYIUOAAf7Ob7tuyDa%2BILcI4CXgeBFgsIIBp094AvnutsV664CvtDx30WUsP4u5x74RIqjy%2BiDUxCDyB7QhXPd3Yp1V4%2F3FzH45sVPyQa8GQpvRh%2BighjM0kA0zg05tvgI73CQQ0d8hXbcAtoMhTajT09BNh3yvX0HBg4v2oiP%2Bg6HNrQ7dR2GDxsveqDFAgoqupBMGEWSTUOjs8sZT0%2BRF8WsXv2aggqCUApUVDi015Xtedov2CB6MUluy0DaYYWyl0VbPDlTfyFml4QCjO4FGHaVY8hTgMFUkfJ0jP7w0WG1eGbyB7UYvHunU2U29bZ3ipMFm05tLDEuxgE0TkhlmvPjjN0QZ%2FQauqeOsgVZjc5mufishrDlJ3X1ihIcFkYCaJPGszLsSYHk0LXMST3NIXNgBp%2FJ3oD7sDHrsy0bIe6VWeI%2BnKHSNRpzH87QmSuJ5j50GnTA96YTZNccY%2FzY4TqtR740kFJXNik1SrKVpd24pbQ8FcYkAfUzUorX3XvKnZbuTjW3rLNvufLODNOp%2BwB%2BcbyHXpWGQdf4m7dmkKhBKKd9KMewi6LQuDUGlYloL601hsHiuMLiB20x8kZlKjkj5e2KYVBFQiCG01vS1S0BYxA6AneFXCEYflAZvR2GwRMJkMK36OLrvoQtPh3lJ7QV%2B8XKB3BRG1xGb4phMEUCuHAtulHlpSkALowWXi95yvETwIrKsDJ%2BMwyDJRJwhQ9X1O3gZTA5xqukEwZqRZVHltEbYRg8kVCXzg0u4vt4hyoUNWkj5qPPariDxEL7xIKNILFQIX60obPH4geJBXkTC2aVZSVvYsGkLSpILHDueaa65NgmbfMkxSFgSUtjSfNjyuh5BRMIsbsiirp82CadqcbW6OMG5gMpDSqj5xNMIMHuCirqcmDP6Ez1c7JEACkKQ8r4uYQZDDPsiCmZYiqIKXSCWmjhJsDKQLAyeiJhRgeOIZHAjSx6xcKrl0hg0Nu8%2Bg7jO3rOJJgtEwkXP7yDwYDjf4fJHVJnEir5duTNJNiQSei86dnqZhJsOpOwBIpa6expfmAZPZ3A4CABWOFbdHXTCQySkKW%2FX0TBLg5CyCkojSyj5xQYTICALHyLrm5OgUHAF%2Bznu8jfBH4EqQWlkWX81AKTRA%2BghWPVxdPmiVt8OrXgffeCdXLD86SIcz%2FfPm6%2B%2BRGgjNIoM3qmoQlfFKBMLcpcTprBYRSMw%2BCOS8Ga0ed2OHR8F7Ka3HAjPsA7GNzQAV%2Bon7gEpBl9ZodDB3xhZAc30oiP%2BQ6FNC4dqfkULB58KKBIV0IMx6NFeEXPt2K2m9ahTAWFSwdz4oMAQgmFvCUUblX8SN4SCpeOG0EJBee%2B51bhnvxhQ5eO5uyiYAG5CInsaX5UGb1%2BwgXGpK6Yoi5jkktHbYL9%2FFv4mHw14IrCuDJ69YRLB4AAV%2FgWXTxZkrApmhrtE4mtKgdcGQZXGtdOiJvZq9F%2BEKQauIeDaeI9ocFm9mq0aySUDAvAZiCwMcYHGxgQ3gfYXNCAcKdBWbC8kwnRJDeXMJtSeG4y4aQwlTCb5VYxvo2Wio7jB9O1PD%2FYjVQhSDTYzTgzjq3xYDfDMKeuqZ3%2BlS6MHKwBqFIBRA8nZKThVFALIuKIT8SzQZ8c6tSzWpBuQAW1osTqaqHS9t1YJ5wzFxI%2BkZO2Dj6Sojp8%2BEuwD2JsRenadfJ4P%2B9ZNb2QlG6flD7BDkFBQjlzbnC1XWMf1CSlreLXSZyVRoyKvMd9SoWv%2FYI95heT5LaSyaPJAmUvT3Ga5Cz9RWdbF1LY5xWkTQobVZYL8uSwmdoxE%2BZPMeoCc7IH%2BWxez8oRHiTuQxaeH%2B5uf%2Fti%2FvP37sPtHz%2B01y%2B%2Fvb1i8at9Oo7rgE2yz00SlcytphWc%2BgVx6LMFkA4ki54XA9sez7ZXDxtSVm6xb5mOT8NOV73T1Sur1NlQ9q3TXiLM5x0tN9ETqAxZuMW%2BZdq%2FA0jhW3R1%2BbToYKu3XGIbdQ%2BgojKojF61BbwUHR1ydWkpaGdo4e1X86W%2Ff5jvVnitgJXiAhBmfO4bIKXoCDFKOEJsunZq6fPAMr8Lo3nk3%2Fn490Nbi%2BIw05T8RtwAB4CZjgOBlIUZBtcwkIJeCK7Mxu7CBbrhjriiLtswTTa88%2BLVPA7n6%2FA%2BBGBRGlgI1dt4DXMALB05bVQAlus33%2B%2FN7df5G0d7eLC%2Fvg2WwTMjmkuABftHMSCL0siiawMGdZniBUHd5shSq5%2FqIQsd1M2QJfK%2FBz4Mc1cbW5o2yAkTMIjmdsQWdaO5yKTtFsK8p12nHCLQ%2BVCWgp46H0hZLimzbOq%2FIKRXy4NiVZ0VYlnLx0daH0Rse1Dd2b2pwawytqQo76y4Z9rMgvpOTu%2F9pLYK7oSMVoas1wrsa1kIKFpgS9MqT3EEFIwmBSCg4AaXStdKQQIKRjcBfkrbvbdI8puAOapjTlNLXiDmsEhvDMAcTsy5INIbxHD1T5hDSwa49h1ce9Mu%2BNq23hAQstrOi3XtEcO1H2DrA7%2B%2Bu1%2BPFPTrSagM%2FPoO2yBS2K9HtKm9xE9vHgfQvimVlc2PLqMT7yMEzPudsUVd6n2E6Ar1GD%2B%2F9XwR7oF8X21wGb%2BPEwH9fmdwUZd%2FX9fo5c8TE75cxHjhwGvv02tHGmE5zvyXhlyEyNCr5aDGb1eHjFDX6LYJL5HBs2yExRnVwEgotZN%2Fgh11GAmz8lxgJOynOzlTdakZCSvunW7CiMI1uPoSWeMtMMZuiDG6I0quGOkTgBXOZXcrlr0%2Fa1zc8jPSFoKJJgFcBgIXFqHK0OhCpykgXc8NMAPkKcRJQIM2jN6GbxCU6GXuRm7Uxtf0WnVzNw7XuQ2Sx%2FOrxu3Nnx2Vkem%2FNKMyrqxSeh7ZbYdluKUr6WazETF43b2n3GmpJlbfctaLULrl6jtDdt0H8IvjPfQbk2iSf5FwYg2ZPJNNm8n0psEgp6lpO3l9Q1PNsM7o3OHdBz8K8BP3o1aKd37Gk9tYRQlOy6Oi%2F54ZT7QdC5FkEZFkvQigpqVTNia7AszRz0qv2hVgLm3rngLJEBaWMix8wg2Far9c4OzvnkLNtFW9FCpyafNw%2FxgBcb9cEZsW2DJ%2B5ZcL5JSdkUVdekrk0sUZACvKw8r4NV8ucFN2hhV12SmRSxcybPCDXPtzQBfl0WV83n7kAkNlZ3hRgqOyIjVC1zCsgzvAFcVxZXSifl0DfsrOxTFKMFRW3DtjKgiw314OwIzO2K9rEG7pDDBKhFuYBJtmg9WXqjamXOOSZe%2BvtKmG0CRfLjNFenZAXPpewboZq5g5z2h4uFPy5SuVh6L3VDRT%2BpZzFTPYHdS6fYBURfdVY8PWvfo2tA9RuHxcADVsz%2FUDbmmpTx2s%2F6pONLZE0jHSXSqFSQnBjT55Ce1oEhqoZ%2BoO6tFHym409i1DM1qf5OqmEr1o7FuHVjSJvOGe8GXITjTmLc%2FoIC5ACt%2BiK9GHxl58aEO7VGAZtAuNLVw6JVzQhMYLLgPQVItaf9rTB%2B9ejHdfmvxyZTRN4V1SdwBTBut9e3DT5XTT%2B%2FDShx16Rjvp4Jlz7nTCHXNhi0%2F75dAWIJ0FzY0pQzYFsIe0gmfeEVLEO%2BbC1p52zAFQFAeUIdsB2EJFO%2BQAKFxrrgZzPfvW6e5V6AW4DGAZtBOALVxAXN8VWZTgrWffOl1OB20AqkPKkE0AbKkCuvqukKIEWz371hlxW%2BgAuBRsGbL%2Bny1erJoqwBYebFE3WksKWvOUZXgtWBN2ICvZIStpkJoFyEpSIkj74t5BBCEpKW9SMsMNdbKSBu2WQ1qSc6cz1HXMDdoxh8SkdPYzP66Mnpk0wDfviirq%2BuYG7ZsDpKgOKaPnJg1wybtCisIuOV1BBbnJC0GW8ZOTJtRRdYUWdQupTLqQCpKTymPK6NlJkw4iA6bwdbSpW0pl0uFbyE5eDriMnp40oZqqK7ioG7Sd0eCSJ0h6%2BRivYLxSz6lKiwT5gR6JlkcajLyDDAI5ksS7Y5sE56wKNHkSnMOSI81YTI5AjtSabEA4p6c4SaBTUkCOJJcpzo8v45MjwfyUrpAifnyKsMWnU1JAjnQZwCIBORKd8gJyJG5wET88RRg5Ep2UKrj5UJEsoCKZOOvg5tPySOfJTiXJ4OZLukG2Ileqmgwjr5tPhp2Dm9%2FLtmkJT72JkwQ6Og5uvlzWOD%2B%2BjO7mW5Bw6wop4hNuwhafjiGDm38ZwDK%2Bm2%2FRYWlw87nBRXyzhLD1bxBA7m3U2Ks%2FN952%2Bd%2Fu88b8n0GcjBfTpqY7S98fh4u52BQ%2Fvj%2FNFkvePOXedJssdhzDVfNISeu5NIPFrlzkTt38v0kxymBoUy33TzeK39B48JhT7qjO4hdnRo%2F1FSRAdNAS6lFE1KOQoT%2FQOl8WQZ2Om57KUSDkJGfIKcMNdVrndToeCnEmTrtNrzLY5a%2FCJGYatM7L7BHy48rorfM6HcAEVOFDFb1i0RVAFTrOCJCiOqSM3jqvwzD7rpCi7ix7nQ4wQuv8hSDL%2BK3zOtS%2FdoUW8fWvwhafrn%2BF1nnlMWX01nmdDiIDpvBhiviyV2FMP3T4FlrnLwdcRm%2BdN%2BiwLYALH2GCukFbq8HOok6yHU1GTrQTSZAn0T6z3alWnWjX0VRDuTx7KRXaOM8%2BIwQcY%2BXZ7QaMZZcsyFh%2Bo6fjpWbk7df8306XOrx7EqMAhEUkJjttJfBIpyluqSIFlQS6p5IUZOjT8qUd%2FM25S5fuXbTm0Hk7cZpDLMROSnMSddM188KOwcxGZwT%2BcLXbIHlGp7922xbOCvsMySbsNsFLYobaWjtxvrLN0pVmViPxxRLhPeVOS420mlt22LdcXfs1Q3UfwC%2BO99CvNjVIVoI21WmTPEpiWhiYiyKEj5ThmcNGwjuMXWWKYUvMdZ3TJkCIRfpWI9Ou%2BVH1937mU4IUqkGjCSiUGgqVBTZOMtRSl3Q%2BXSp9TV%2B6lDXtlX6PWIVokLuWVCEKjsnJT2moCj0bZaZ8RfFkJUmZRFubDN%2BRXqMeV07iyqDTXwVtNRW%2Fp%2FK2sRPU6XzCECJW%2FRoMcgH1a%2BATmbKpX5nSksRGudXPKjkeWbCjbwWzSi6R5Z65sdL55MbEKsyQ%2FVzqKow8emCQ0fRd9YAijxGlBxV3XH1jjt7p%2FI56g99GYRjnT4%2B83ep9uPSTM%2F4P)

![scheme_1](https://schstp.github.io/Theater-Platform/datastorage/database/version_1_1_0/data_model.png "Концептуальная модель данных")

