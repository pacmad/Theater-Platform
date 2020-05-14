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

#### [Диаграмма в draw.io](https://app.diagrams.net/?lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1&title=data_model.drawio#R7V1bk5s4Fv41rpo8tAsB5vKY7klnkkx2M5PLTJ5cxKbbTNvGi%2Bkk3b9%2BhY0wIIERIJA8JzW1a9MYY3TOp3P9zsS42fx8HXm71ftw6a8nurb8OTF%2Bnei6oTka%2Fr%2FkyNPxCHIt43jkPgqW6bHTgY%2FBs58eTD94%2Fxgs%2FX3hxDgM13GwKx5chNutv4gLx7woCn8UT7sL18Vv3Xn3PnXg48Jb00f%2FCpbx6njU0e3T8d%2F84H5FvhlZ7vEvG4%2BcnP6S%2Fcpbhj9yh4xXE%2BMmCsP4%2BGrz88ZfJ0%2BPPJe%2F3jz9tf79wXr99o%2F9%2F7zP1%2B8%2B%2FefL1fFitzwfyX5C5G%2Fj1pd%2Bfri7%2Fe2L%2Bc%2Ffuw%2B3f%2FzQXr%2F89vbqiizmd2%2F9mD6w9MfGT%2BQJ%2Bkv8QNO3YRSvwvtw661fnY5e%2B9vly2Sp8Amv%2Fnz2o%2FBT%2BN7bYom53sdeFJ%2F%2BtvG2y%2F9uk49kD1M7nBWFD9nyoOMVU1FyyFVy7xs%2Bj%2FS57cPHaOHXPIRZ%2Bpvxt9z7cd2JqdAkTyQnXenzfu2HGz%2BOnvAJP06ShrRUfFZ5KSMHI3%2FtxcH3oqx6qcjfZxfMvuNDGOCfrGtEP4mWpdppuFrxEsffnn4qLxylC5mlC%2BnlCx2fDXUh%2FCL3w0%2BHDrLHlsPPb5%2F9O0f%2F%2FCp88%2Fzq2%2F17a7m6uSJil5PDx2g9j8P5ItxsHrdB%2FETJJRahXfISy0EceOs%2FMXp42%2FuDQMbhLhWttX8Xpy%2Bj9Pknr7%2BFcRxu0jfeOrjf4tfHc6%2B%2F%2B%2Fh6GEBepocPF7u%2BC9brm3AdRvjINjzK8M5bBNv7349fYWqnQ3%2BmX2XiQyG%2B3t36IOurYLn0t8mthLEXe98OvyT52C55rocnPbvG%2F%2BFnf6NNZ5MZ%2Fpk3%2BD06vcf%2FJadH8U24xWrjBQcN8L19%2FMPfJ3e%2FjMLdJyLIh58dPm6X%2FpKoWr3e8WlW8qT8n7WaQORLK8oXmlnH93lNsRiaojvVOlEQQm6Ja4B8vBJWkCqGwDQStJJU9SVU5%2BQm%2BY2VQlCvs2UpyDbz9GYK%2B2UVThqWmMVnA7lFLf6nle%2FFfpR8cov%2F52O4wCs%2BudEnLzVaLn4Em7V3WNK7cBuTzTF5dotVsF7%2B7j2Fj8lvwBvX4oG8u16FUfCMz8fXPZ6c39d0q3DGx%2BSTRIP9PT7nA1kPlB363dsT0VuE67W32wffsjvZYBAIttd5kZQSCoiFmUcCh7lnmme3x5OGZl%2BnW%2Be%2Fjgk8VvHbvDWWji0WkevkIe47boK15kVOKuOjVM7x53Ttl9t36MUkubFk309WKHu5P4jrfOvHP8LoITtdfyFm10Swa%2BZVJQ8CJq039RB0XnGeihJ5TlFmWrWedENNh7FlZiL44R3sn1XIWa%2FuwvbPPiSBvfXPzhtP8rmN%2Fs8g%2Fjv9bPL6a%2FIaA8Tx3a8%2Fc3%2F69Ym82eLn9Xd2efzm%2BCmHvD197PCu8LkPfhTgB%2B5H6UG%2BLTXvtzJXAZF4inJ%2Bq1VyN5FRsvSa%2Bq2WW7qQNqzfSn5HThFSy1HX%2FnPcjMF67NN6LC%2F4rKE5h7QaX0I167EWDXKiyLAKwRoc2xqsx5FO1mATSezNBkB0yA5MQM4QCqrCv%2F5CKMKWnzYBt97GF4MwEKU9s7n2BCokEzJaVBbRgTmAFL5Fn1UsulRR2es33%2B%2FN7df5G0d7eLC%2Fvg2WwfOVSa39zotXSRJojZ1HQBaVkaWx4SxKuBpELABY4gbaKTWuMKXVpC1Vau0ljFaRyFMaospiT%2BciTyTKNTVn9uQU6UKT2jgXftNfuIopQOlDz0er2MHFVDakiVbppYxV6yoLwyldqBz2EhytmtE7rAqKkAo0mrQI22oF1TlpUoXytBd5tijbDWXeNCWT%2BRkVZ2sp85ZdvJBp6cPKPL3xf9wlu9VizXBWITTbPjR7hcrBeIM2%2BrK60MLOX5eoqgnOKhObZdSb7IkQQlhW3rDsrMqZ5gnLskVeVFyOUUQCYVnOGEplbYb8YVlGjQaEZeUKnvCDCiMsOzCouOcdB4CU2kV3KhZdfkghNlRu8Zf%2BfhEFuzgIt4AsKiOL7YyMLBZdtQDIwrXoVlUsXgFkoQOzJOOzC%2FeHanwAF3XBJavYHw9doMmnK7roFauuALpU55OTZ7PG8FLR3gMgoxDINA0yGjUxxm5yBqnlriAjPrfsTt3CP2GgQ8dfIi%2BG%2BIvaGGONjjEQgOmKMeIDMENhjE0HZIhhs18HSz8C7%2BkSQMcdG3RsiM10BB1bfGxGAOjoM2%2F%2F9sur18b7uf519X7ufwn%2BR6q3KnrTAWgGAhqGJDXEnuqUtT4g0DBli47S3L5DnYXqoqCmMYIU5aFalaVAGjZo0lBDyYKEVYoVjeLnKg7bNKXT69w7%2F1ltXYQ0VYrlCrCWXeSoVOBbLkcTXKLosHg15Bf4U525m5NdNNUMo1Z6WaXmbYvd22tCrb12VhNsQzJNuNK1qZb%2FZxQk2rAS9HZOf5610xTTnrp2fhMofItp4tUv3bpwAga1qUimST10Hvldy%2B6gPXx7T8%2Fa41gNtcdFkmkPskvGjV2Qa1tHifa0U5mDzjjF67nG8HrSIILIqSc5XZCw8WM6K1hi6IwuMAl78P3dBsmDFqEuRAvOm126ZOpikSbjTD%2F0drphm2cuJForGN0hSu0es5xq8Df4tfVZelYERIyVs5qATNl2DguZBQl29cQebstm5aDyVuG6KAGyYZWiAQmDzEphuhxq0dJ06rdflr0OpDtUQbUoe9SO0XKHQKWWWdstscAKVwbVnXPH6mePGNczR8TkaKAMmmTKYLlFK8ctt8CeVQaiRZY9sPD37zRAw3htAMpsKOW6bJSehlYMQKGCyJtuS%2Fw3DH1avNRsNnyQyVbbTWjpP48I97OmoaSsNEsaRbgytFIwqSC%2BmUHDqwlY5e1p8Vq64Q6vCmo7B21UYWTvWG%2BuC7K5ASdjLJVYy2or%2FWVyCRsNm6RDDM7zz3tWkR1wiHTgEDFnxWXO6GLO9hC1JHhWhkMkw4H8jKy9wPor4A%2FpTuusq0cggnRgEOlc%2BHlSVvX65pBOh7z8jResxcAMlHm2YmDlR5bRWUSQDl0snXFFXR6RrFOz0Ley3%2F8II0EWDEDLQNAyOo0IMqBXpSu0ZOqpIrTo1PIH%2B7m33ARAUKQ2tIxPIoIMYBHpjC16xbqrgC00jwhQKqqPK43JicUJFhCHdMYV8cwh4pafjudu8INc%2B3OAF%2FXhZTZ6HNeg47gAL5zwonAU16CjuBm54iqMYZ6W4gDjjB7ONSCc2xlgFA7nMnihb8LNxk%2FrL6Amoq%2BaCNtoWxNBqhsutiaCQR%2B9OMoglEVIXBZRyVktcVkEg6wayiJ49zurCv1U2O%2FoMDC%2B55i534EpPZopzY8t4xdGMKiqAVk4l92oWHYVkIUOBANpsPKwMn5RhNWgVwNgpX7ZqwIzKsAKHQAO9nN823dBtPEFuUcALwPBiwSFEQyye8AXznW3K9ZdBXyh47%2BLKOEEXs498IkUR5fRx6ogBs09oAvnursV6y41%2F3iFONChXvEztAFvhsKb0UesIAbvNNCQc0OOLT7COxzk0BFfoR23gDZDoc3os1WQTYd8b9%2BBgcOLNuKjvsOhDe1OXYfhw8aLHmixgIKKLiQTRpFk09Do7HLG01PkRTGrV7%2BmoIIglAIVFQ7tdWV7nvYLNoheTJLbMpB2WKHsZdEWT87UX4jZJaEAo3sBhl3lGPIUYDBVpDw7oz98dFgtnpn8QS0G797pVJlNve2d4mTBplMbS4yLcQCNE1KZ5vw4YzfEGb2G7qmjbEFWo7NZLj6rIWz5SV29ogSHhZEA2qTxrAx7UiA5dC1zUk9zyByYwWeyN%2BA%2BbMz6bMtGiHtllrgPZ6h0jcbchzN05kqiuQ%2BdBh3wvekE2TV7mcbHSWN7uE7rkS8NpNSVTUqNkmxlaTduKS1PhTFJQP2MlOJ1955yp6W7U80t6%2Bxbrrwzw3TqPoBfHO%2BhV6Vh0DX%2B5q0ZJGoQymkfyjHsoig0bo1BZSLaS2uNYbA4rrD4QVuMvFGZSs5IebtiGFSREIjh9JZ0dUvAGISOwF0hVwiGH1RGb4dh8EQCpPAtuvi6L2GLT0f5CW3FfrHyAVzUBpfRm2IYTJEALlyLblR5aQqAC6OF10uecvwEsKIyrIzfDMNgiQRc4cMVdTt4GUyO8SrphIFaUeWRZfRGGAZPJNSlc4OL%2BD7eoQpFTdqI%2BeizGu4gsdA%2BsWAjSCxUiB9t6Oyx%2BEFiQd7EglllWcmbWDBpiwoSC5x7nqkuObZJ2zxJcQhY0tJY0vyYMnpewQRC7K6Ioi4ftklnqrE1%2BriB%2BUBKg8ro%2BQQTSLC7goq6HNgzOlP9nCwRQIrCkDJ%2BLmEGwww7YkqmmApiCp2gFlq4CbAyEKyMnkiY0YFjSCRwI4tesfDqJRIY9DavvsP4jp4zCWbLRMLFD%2B9gMOD432Fyh9SZhEq%2BHXkzCTZkEjpvera6mQSbziQsgaJWOnuaH1hGTycwOEgAVvgWXd10AoMkZOnvF1Gwi4MQcgpKI8voOQUGEyAgC9%2Biq5tTYBDwBfv5LvI3gR9BakFpZBk%2FtcAk0QNo4Vh18bR54hafTi14371gndzwPCni3M%2B3j5tvfgQoozTKjJ5paMIXBShTizKXk2ZwGAXjMLjjUrBm9LkdDh3fhawmN9yID%2FAOBjd0wBfqJy4BaUaf2eHQAV8Y2cGNNOJjvkMhjUtHaj4FiwcfCijSlRDD8WgRXtHzrZjtpnUoU0Hh0sGc%2BCCAUEIhbwmFWxU%2FkreEwqXjRlBCwbnvuVW4J3%2FY0KWjObsoWEAuQiJ7mh9VRq%2BfcIExqSumqMuY5NJRm2A%2F%2FxY%2BJl8NuKIwroxePeHSASDAFb5FF0%2BWJGyKpkb7RGKrygFXhsGVxrUT4mb2arQfBKkG7uFgmnhPaLCZvRrtGgklwwKwGQhsjPHBBgaE9wE2FzQg3GlQFizvZEI0yc0lzKYUnptMOClMJcxmuVWMb6OlouP4wXQtzw92I1UIEg12M86MY2s82M0wzKlraqd%2FpQsjB2sAqlQA0cMJGWk4FdSCiDjiE%2FFs0CeHOvWsFqQbUEGtKLG6Wqi0fTfWCefMhYRP5KStg4%2BkqA4f%2FhLsgxhbUbp2nTzez3tWTS8kpdsnpU%2BwQ1CQUM6cG1xt19gHNUlpq%2Fh1EmelEaMi73GfUuFrv2CP%2BcUkua1k8miyQNnLU5wmOUt%2F0dnWhRT2eQVpk8JGleWCPDlspnbMhPlTjLrAnOxBPpvXs3KEB4n7kIXnh7vb376Y%2F%2Fy9%2B3D7xw%2Ft9ctvb69Y%2FGqfjuM6YJPsc5NEJXOraQWnfkEc%2BmwBpAPJoufFwLbHs%2B3Vw4aUlVvsW6bj07DTVe909coqdTaUfeu0lwjzeUfLTfQEKkMWbrFvmfbvAFL4Fl1dPi062Ootl9hG3QOoqAwqo1dtAS9FR4dcXVoK2hlaePvVfOnvH%2Ba7FV4rYKW4AIQZn%2FsGSCk6QowSjhCbrp1a%2BjywzO%2FCaB75dz7%2B%2FdDWojjMNCW%2FETfAAWCm40AgZWGGwTUMpKAXgiuzsbtwgW64I66oyzZMkw3vvHg1j8P5OrwPAViUBhZC9TZewxwAS0dOGxWA5frN93tz%2B3X%2BxtEeHuyvb4Nl8MyI5hJgwf5RDMiiNLLo2oBBXaZ4QVC3ObLU6qd6yEIHdTNkifzvgQ%2FD3NXGlqYNcsIEDKK5HbFF3WguMmm7hTDvadcphwh0PpSloKfOB1KWS8osm%2FovCOnV8qBYVWeFWNby8ZHWBxHbHlR3dm9qMKuMLSnKOyvumTazoL6T03s%2Fqa2COyGjlSHrtQL7WhYCihbY0rTKUxwBBaNJAQgouMGl0rVSkICC0U2An9J27y2S%2FCZgjuqY09SSF4g5LNIbAzCHE3MuiPQGMVz9E%2BbQkgGufQfX3rQLvratNwSErLbzYl17xHDtB9j6wK%2Fv7tcjBf16EioDv77DNogU9usRbWov8dObxwG0b0plZfOjy%2BjE%2BwgB835nbFGXeh8hukI9xs9vPV%2BEeyDfVxtcxu%2FjREC%2F3xlc1OXf1zV6%2BfPEhC8XMV448Nr79NqRRliOM%2F%2BlIRchMvRqOajx29UhI9Q1um3CS2TwLBthcUY1MBJK7eSfYEcdRsKsPBcYCfvpTs5UXWpGwop7p5swonANrr5E1ngLjLEbYozuiJIrRvoEYIVz2d2KZe%2FPGhe3%2FIy0hWCiSQCXgcCFRagyNLrQaQpI13MDzAB5CnES0KANo7fhGwQlepm7kRu18TW9Vt3cjcN1boPk8fyqcXvzZ0dlZPovzaiMK6uUnkd222EZbulKutlsRAxed%2B8pd1qqidW3nPUilG65%2Bs6QXfcB%2FOJ4D%2F3GJJrkXyScWEMmz2TTZjK9aTDIaWraTl7f0FQzrDM6d3j3wY8C%2FMT9qJXinZ%2Fx5DZWUYLT8qjov2fGE23HQiRZRCRZLwKoaemUjcmuAHP0s9KrdgWYS9u6p0AyhIWlDAufcEOh2i8XOPu7p1AzbVUvhYpc2jzcP0ZA3C9XxKYFtoxf%2BeUCOWVnZFGXnhK5dHEGwIrysDJ%2BzZcL3JSdYUVddkrk0oUMG%2Fwg1%2F4c0EV5dBmftx%2B5wFDZGV6U4KisSI3QNQzr4A5wRXFcGZ2oX9eAn7JzcYwSDJUV986YCgLst5cDMKMz9usahFs6A4wS4RYmwabZYPWlqo0p17hk2fsrbaohNMmXy0yRnh0Ql75XsG7GKmbOMxoe7pR8%2BUrloeg9Fc2UvuVcxQx2B7VuHyBV0X3V2LB1r74N7UMULh8XQA3bc%2F2AW1rqUwfrv6oTjS2RdIx0l0phUkJwo09eQjuahAbqmbqDevSRshuNfcvQjNYnubqpRC8a%2B9ahFU0ib7gnfBmyE415yzM6iAuQwrfoSvShsRcf2tAuFVgG7UJjC5dOCRc0ofGCywA01aLWn%2Fb0wbsX492XJr9cGU1TeJfUHcCUwXrfHtx0Od30Prz0YYee0U46eOacO51wx1zY4tN%2BObQFSGdBc2PKkE0B7CGt4Jl3hBTxjrmwtacdcwAUxQFlyHYAtlDRDjkACteaq8Fcz751unsVegEuA1gG7QRgCxcQ13dFFiV469m3TpfTQRuA6pAyZBMAW6qArr4rpCjBVs%2B%2BdUbcFjoALgVbhqz%2FZ4sXq6YKsIUHW9SN1pKC1jxlGV4L1oQdyEp2yEoapGYBspKUCNK%2BuHcQQUhKypuUzHBDnaykQbvlkJbk3OkMdR1zg3bMITEpnf3MjyujZyYN8M27ooq6vrlB%2B%2BYAKapDyui5SQNc8q6QorBLTldQQW7yQpBl%2FOSkCXVUXaFF3UIqky6kguSk8pgyenbSpIPIgCl8HW3qllKZdPgWspOXAy6jpydNqKbqCi7qBm1nNLjkCZJePsYrGK%2FUc6rSIkF%2BoEei5ZEGI%2B8gg0COJPHu2CbBOasCTZ4E57DkSDMWkyOQI7UmGxDO6SlOEuiUFJAjyWWK8%2BPL%2BORIMD%2BlK6SIH58ibPHplBSQI10GsEhAjkSnvIAciRtcxA9PEUaORCelCm4%2BVCQLqEgmzjq4%2BbQ80nmyU0kyuPmSbpCtyJWqJsPI6%2BaTYefg5veybVrCU2%2FiJIGOjoObL5c1zo8vo7v5FiTcukKK%2BISbsMWnY8jg5l8GsIzv5lt0WBrcfG5wEd8sIWz9GwSQexs19urPjbdd%2Frf7vDH%2FZxAn48W0qenO0vfH4WIuNsWP70%2BzxZI3T7k33SaLHcdw1TxS0nouzWCxKxe5Uzf%2Fb1KMMhjaVMv9043iNzQePOaUO6qz%2BMWZ0WN9BQkQHbSEehQR9Shk6A%2B0zpdFUKfjpqdyFAg5yRlyynBDndZ5nY6HQpyJ027Tqwx2%2BaswiZkGrfMye4T8uDJ667xOBzABVfhQRa9YdAVQhY4zAqSoDimjt87rMMy%2BK6SoO8tepwOM0Dp%2FIcgyfuu8DvWvXaFFfP2rsMWn61%2BhdV55TBm9dV6ng8iAKXyYIr7sVRjTDx2%2Bhdb5ywGX0VvnDTpsC%2BDCR5igbtDWarCzqJNsR5ORE%2B1EEuRJtM9sd6pVJ9p1NNVQLs9eSoU2zrPPCAHHWHl2uwFj2SULMpbf6Ol4qRl5%2BzX%2Ft9OlDu%2BexCgAYRGJyU5bCTzSaYpbqkhBJYHuqSQFGfq0fGkHf3Pu0qV7F605dN5OnOYQC7GT0pxE3XTNvLBjMLPRGYE%2FXO02SJ7R6a%2FdtoWzwj5Dsgm7TfCSmKG21k6cr2yzdKWZ1Uh8sUR4T7nTUiOt5pYd9i1X137NUN0H8IvjPfSrTQ2SlaBNddokj5KYFgbmogjhI2V45rCR8A5jV5li2BJzXee0CRBikb7VyLRrflT9vZ%2F5lCCFatBoAgqlhkJlgY2TDLXUJZ1Pl0pf05cuZU17pd8jViEa5K4lVYiCY3LyUxqqQs9GmSlfUTxZSVIm0dYmw3ek16jHlZO4Muj0V0FbTcXvqbxt7AR1Op8whIhVvwaDXED9GvhEpmzqV6a0JLFRbvWzSo5HFuzoW8GskktkuWdurHQ%2BuTGxCjNkP5e6CiOPHhhkNH1XPaDIY0TpQcUdV9%2BYo3c6v6Pe4LdRGMb50yNvt3ofLv3kjP8D)

![scheme_1](https://schstp.github.io/Theater-Platform/datastorage/database/version_1_1_0/data_model.png "Концептуальная модель данных")

