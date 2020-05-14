>*updates*:
>1. в сущность "Театр" добавлены атрибуты "путь к фото театра" и "путь к превью театра"
>2. в сущность "Социальная сеть" добавлен атрибут "путь к логотипу"
>3. в сущность "Спектакль" добавлен атрибут "путь к постеру для слайдера"
>4. в сущность "Событие" добавлен атрибут "признак премьеры выбранной для главной страницы"
>5. в сущность "Закладка пользователя" добавлен атрибут "Дата и время создания"
>6. из сущности "Закладка пользователя" удален атрибут "Комментарий"
>7. добавлена новая сущность "Режиссер" с атрибутами "id режиссера", "Фамилия", "Имя", "Отчество", "Биография", "Путь к фото"
>8. добавлена новая сущность "Режиссер спектакля" с атрибутами "id режиссера", "id спектакля", "id театра"
>9. добавлена новая сущность "Автор" с атрибутами "id автора", "Фамилия", "Имя", "Отчество", "Биография", "Путь к фото"
>10. добавлена новая сущность "Автор спектакля" с атрибутами "id автора", "id спектакля", "id театра"
>11. добавлена новая сущность "Художник" с атрибутами "id художника", "Фамилия", "Имя", "Отчество", "Биография", "Путь к фото"
>12. добавлена новая сущность "Худолжник спектакля" с атрибутами "id художника", "id спектакля", "id театра"
>13. в сущность "Актеры в театрах" добавлен атрибут "id театра"
>14. согласно приведенным апдейтам обновлена также КМД в draw.io



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
| признак премьеры выбранной для главной страницы | boolean|
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

#### [Диаграмма в draw.io](https://app.diagrams.net/?lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1&title=data_model.drawio#R7V1bd5u4Fv41XmvmIV6Iq3ls0qZNO52T6W2mT17UJjEntvEBkjb59UfYFgYkMDIIJM%2FumnWOIRgLtPenff00Mq5Wv95G3mbxMZz7y5GuzX%2BNjNcjXTe0iYb%2FLz3zvDuDXNvYnbmPgvn%2B3OHE5%2BDF35%2Fcf%2FH%2BMZj7ceHCJAyXSbApnpyF67U%2FSwrnvCgKfxYvuwuXxV%2FdePc%2BdeLzzFvSZ%2F8O5slid3aiO4fz7%2FzgfkF%2BGdnu7i8rj1y8f5J44c3Dn7lTxpuRcRWFYbL7tPp15S%2FTt0fey983z38v%2F3iw377%2FK%2F6f9%2FXyw5c%2Fv13sbnbN85XsESJ%2FnZx865eHu%2Bt338z%2F%2FrO5vf7rp%2Fb21Y%2F3FxdkMp%2B85eP%2Bhe0fNnkmb9Cf4xe6PwyjZBHeh2tv%2BeZw9tJfz1%2BlU4UvePPpxY%2FCL%2BFHb40l5jJOvCg5%2FG3lref%2FWadfyV6mtr0qCh%2By6UG7O%2B5FaULukjtu%2BD727y0OH6OZX%2FMSrP0z41%2B595O6C%2FdCk76RnHTt3%2FdbP1z5SfSML%2Fh5kDSk7cVnkZcycjLyl14SPBVl1duL%2FH12w%2Bw3bsMAP7KuEf0kWrbXTsPVirfYPfv%2BW3nhKN3ILN1IL99o926oG%2BEPuQc%2FnNrKHlsOv75%2F8e8m%2Btc34c3Lmx%2F3H%2B354uqCiF1ODh%2Bj5TQJp7NwtXpcB8kzJZdYhDbpRywHSeAtP2H08Nb3W4FMws1etJb%2BXbL%2FGO3ff%2Fr5R5gk4Wp%2F4C2D%2BzX%2BvLv28snH98MA8mp%2Fenuzy7tgubwKl2GEz6zDnQxvvFmwvv9j9xOmdjj1af9TJj4V4vvdLbeyvgjmc3%2BdDiVMvMT7sX2S9Gub9L1u37R1if%2FD7%2F5KG1sjCz%2FmFT5Gh2P8X3p5lFyFa6w2XrDVAN%2BLk59%2BnI5%2BHoWbL0SQt48dPq7n%2FpyoWr3e8WlW%2Bqb8X7WaQORLK8oXsuzdcV5TbIam6JNqnSgIIbfENUA%2BXgkrSBVDYBoJWkmquhKqY3KTPmOlENTrbFkKssV8P5jCelmFk4YtZvLZQG5Tk%2F9l4XuJH6XfXOP%2F%2BRzO8IyPrvTRK42Wi5%2FBaultp%2FQuXCdkcUzf3WwRLOd%2FeM%2FhY%2FoMeOGaPZCjy0UYBS%2F4enzf3cX5dU23C1d8Tr9JNNiP8TW3ZD5QduoPLyaiNwuXS28TBz%2BykawwCATry7xISgkFxMLMI8GEuWaaR5fHg4ZmP6fbx3%2BOCTx28de8JZaONRaRy%2FQlxi0XwVrzIieVyU4qp%2Fh7uvbb9Qf0%2BygdWLrupzOUfYy34jpd%2B8nPMHrILtd%2FF7NqIlg186qSBwGT1pt6CDquOM9FiTymKJZWrSftUHPCWDIzEbz9AOtnFXLWq7uw9bMLSWAv%2FdZx40k%2Bt9H%2FFST%2F7L%2Bbfv6efsYAsTt6%2FSv3p9fP5GCN39c%2F2e3xwe5bE3J4%2BNr2qPC9Wz8K8Av3o%2F1JviU177cyZwGReIpyfqtdcjeRUbL0mvqttlu6kdav30qeI6cIe8tR1%2F7cLcZgPXZpPZYn3GpoziGtxpdQzXqsRYOcKDKsQrAGh7YG63GklTXYRBI7swEQHbIDE5AzhIKq8K%2B7EIqw6adNwLW38sUgDERpjyyuHYEKyYQMFpVFdGAOIIVv0q2KSZcqKnt583Rvrr9Pbybaw4Pz%2FX0wD14uTGruN16ySJNAS%2Bw8ArKojCyNDWdRwtUgYgHAkjTQTqlxhSmtJm2pUnMvYbSKRJ72Iaos9nQs8kSiXGPTckaHSBca1ca58EF34SqmAO1fej5axQ4u7mVDmmiVXspYnVxlYUxKNyqHvQRHqyx6hVVBEfYCjUYnhG21guocNKlCeU4XebYoOw1l3jQlk3mLirOdKPO2U7yRaev9yjy98H%2FepKvVbMlwViE0e3po9gKVg%2FEGbfRldaGFlb8uUVUTnFUmNsuoN4mJEEJYVt6wrFXlTPOEZdkiLyouxygigbAsZwylsjZD%2FrAso0YDwrJyBU%2F4QYURlu0ZVNzjjgNASu2kTyomXX5IITZUbvLnfjyLgk0ShGtAFpWRxZkMjCw2XbUAyMI16XZVLF4BZKEDsyTjswnjbTU%2BgIu64JJV7A%2BHLtDk0xZd9IpZVwBdqvPJ6btZYnipaO8BkFEIZJoGGY2aGGM7OYPUcluQEZ9bdsdu4Z8w0KHjL5GXQPxFbYyxB8cYCMC0xRjxAZi%2BMMahAzLEsImXwdyPwHs6B9BxhwYdB2IzLUHHER%2BbEQA6uuXF77%2B9eWt8nOrfFx%2Bn%2Frfgf6R6q6I3HYBGXaDJ6ij6ABqmbNFRmusPqLVQnS3U1OqnUkjDBk0aaihZkLBKsaJR%2FFjF4SlN6bRIdM5%2FVlsXIU2VYrkC7MQuclQq8C2XowkuUZyweDXUEfjT69NtpyD0bnbcR416HYoe1QTHkEwTLiZOQYRPZwJ0xq6Th%2FnCbU0TjbXS4IRTLDSIfXCqR04FJCxZH1uFNQQdUygW1Qge33WQvmgRZe0ug3iEvWDokqmJTdojSf0DkSVeNXHMIzcSrRWMunYVFo0M%2FK2cavC3Jp1qbXWsCEgzGmoCMpF0qmAWJNjV8YrsnsrDM0Fj8l1yPxelQNavUjRoH5dZKUyXQy1ObHHq1opizwPpa1NQLcq%2BwMQ4cYVApWY%2Fxy3xVwpXBjXdioMyTOxu1ghOB6VrZSAmRwNl0CRTBtstWjluuXnvqDIQLbKdnoW%2Fe6cBWl3rxNwxG0q5LhsZoaFpYy33DxVE3nRPxH%2FD0MfFW1lW%2F86zo7abcKL%2FPCDcExP0ONrbsqH9haGVYvwF8c0MGl5NwCrvjIv30g23f1VQ2zk4RRUG9o715rogmxtwMMb2Emvbp0p%2FuS3eQf2mFxCDrflrzCoPAvaDFuwHplWc5ozo4mj3w4nUtMqwH2Q4kN%2FdJxZYOQLMB%2B0JaXX1qA%2BQDtwHrUvWDsqqXscP0umQl7%2FygqUYmIECtZO4I%2FmRZXD%2BA6RD%2FX1rXFGXASHrMStU3MfxzzASZMEAtPQELYMTICADquzbQkumnipCi05NfxBPvfkqAGoVtaFlePoDZAD%2FQWts0SvmXQVsoRkQgAxOfVxpTKsqTrCA8qA1rojnPBA3%2FXQ8d4Vf5NKfAryoDy%2BMrdn7hhc6jgvwwgkvCkdxDTqKm9HCLcIEdgJSHGAmg4dzDQjntgYYhcO5DEbbq3C18vf1F1AT0VVNhGOcWhNBqhvOtiaCQXw728kglEVIXBZRybYrcVkEg2YXyiJ41zu7Cv1UWO%2FoMDAec8Jc78CUHsyU5seW4QsjGCS7gCyc025UTLsKyEIHgoHuVHlYGb4owoZ9wFvDiviNwMVNPx0ADuIpHvZdEK18Qe4RwEtP8CJBYQSDphvwhXPenYp5VwFf6PjvLErZTOdTD3wixdFl8A0hEIOgG9CFc97dinlXj88UMXi0xe%2F%2BC3jTF94MvjkEYjDmAoEyN%2BQ44iO8%2FUEOHfEV2nELaNMX2gy%2BKwRy6JDv9QcwcHjRRnzUtz%2B0od2pyzB8WHnRAy0WUFDRhmTCKJJsGhqdXc54eoq8KGb17NcUVBCEUqCiYkJ7Xdmap%2F2GDaLfR%2BmwDKRtZyj7WLTF0yv138WsklCA0b4Aw6lyDHkKMJgqUmb97w4fJ6wWz0z%2BoBaDd%2B2cVJlNna2d4mTBoVMbc4yLSQCNE1KZ5vw44zTEGb2G7qmlbEFWo7VZLj6rIWz6SV29ogSHhS0BtFHjvTKcUYHk0LXNUT3NIXPDDD6TvQH3YWPWZ0c2QtwLs8R9aKHSPRpzH1royJ1Ecx9OGnTAd6YTZNUcYlul7X1O3vKlgZS6skmpUZKtLO3GLaXlXWFMElA%2FIqV43r3n3GX71almyDp7yJUjM8xJ3Rfwh90YOlUaBl3jO2%2FJIFGDUM7poRzDKYpC49YYVCaiPbfWGAaL4wKLH7TFyBuVqeSMlLcrhkEVCYEYTm9JV7cEjEHoCNwVcoVg%2BEFl8HYYBk8kQArfpIuv%2BxI2%2BXSUn9BWxLOFD%2BCiNrgM3hTDYIoEcOGadKPKS1MAXBgtvF76lpNngBWVYWX4ZhgGSyTgCh%2BuqNvBy2ByTBZpJwzUiiqPLIM3wjB4IqEunRtcxPfx9lUoatJGzGef1XAHiYXTEwsOgsRChfjRhk6MxQ8SC%2FImFswqy0rexIJJW1SQWOBc80x1ybFN2uZJi0PAkpbGkubHlMHzCiYQYrdFFHX5sE06U42t0ccV7A%2BkNKgMnk8wgQS7Laioy4Ft0Znql3SKAFIUhpThcwkWbGbYElMyxVQQU%2BgEtdDCTYCVnmBl8ESCRQeOIZHAjSx6xcSrl0hg0Nu8eYLtOzrOJJgnJhJ0s2bezyGRwGDA8Z9g5w6pMwmVfDvyZhIcyCS0XvQcdTMJDp1JmANFrXT2ND%2BwDJ5OYHCQAKzwTbq66QQGScjcj2dRsEmCEHIKSiPL4DkFBhMgIAvfpKubU2AQ8AXxdBP5q8CPILWgNLIMn1pgkugBtHDMunjavC4m%2F3X8p3n%2F7t2nx9XN7WxlLf66%2BX5%2FwUSW2SIMY389vQuj6Qq%2FoOnGuweY6Q9mGHLUEHnapxqESRqgTD3KNAaPojBUa7VE9gudv%2FSevGCZPtg0rRSPp%2BvH1Q8%2FAoxR2pSxGgZ2haUzm5DS%2FatB5rgpcz65zAmjKwV2BzoXrJkMjjV0EglKJ7jhRnwWqTe4obNKUKR1Bkijo8GRhs4qwb5A3EgjPrHU27ZAkwbJAHn5yNEox0aecZMf4yMfFbjIMwbnCtJmWihako7v5%2FI4nTMxCySiczaOkDA3pnM2DHPsmtrhX%2BnGaII1AFUqgGhKcpcOZqqgFkTEEZ%2BIZ%2FT%2BHOrUsVqQGiAFtaLE5WCj0uLdWCcmR24knIef9nI%2FEy8Xn%2F4WxEGCbShdu0xf79eYFWSDWt4WO8dlsENQ0KIj7cztapwa%2B6CmmFeljeNoF7nRxnGHml%2FYNE7q2l9U6b%2FzFP%2F2vWkc7ajDpnFtNo0TzqPVhSy8PNxdv%2Ftm%2Fvefze31Xz%2B1t69%2BvL9gdVV%2B2ZH0wSLZ5SKJSuZW072W9TNizmILoE4JoGiWSFj2eJa9etiQsuWFPWQ6MworXfVKV6%2BsUpd5sYdOe4mwK8dgmYmOQKXPdhf2kGn%2FDiCFb9LV7aKjg63efI5t1BhARWVQGbzTBepEWzrkShSjs6nYqamfefFiOvfjh%2BlmgecKykTPAGGG73iBKtG2m4kpCzG0H5QHlm3HS%2BTf%2Bfj5Z%2BAdqQ0zfXa8sHmhAGZa0oAqCzMMhhGgAjgTXGna5SKOCwBwpR2uqMsxQlOMkJ1Ql%2BF9CMCiNLCQ3qvBgAU4RtoWmasALJc3T%2Ffm%2Bvv0ZqI9PDjf3wfz4IURzSXAgv2jBJBFaWTRtR6DukzxgqBuc2Sp1U%2F1kIUO6mbIEvlPgQ9bOKmNLUaP0VymgEE0tyW2qBvNRSZtt3wJZg9%2B2qFxGT6mI4DOB0oKOup8IGW5pMyyqf%2BCkF4tD4pVdVaIJW3vJFuxLLQ%2BiFj2oLqzfVODWWVsSVHeWTFm2syC%2Bk5O7%2F2gtgquhIxWhqzXCuxrWegnTsCWplWewugnEKNJAfgnuMGl0rVSkICC0U2A39I69mZpfhMwR3XMaWrJC8QculDn%2BoMBmMOJOVVsR%2Bphjq7RNRV5ooNXsyQEB79bBx9pmlHwubN%2BzGPd28g4zcVXh9xA1%2BgyDC%2BVwaPsBkUSSmA4kDoYcIAddRgOsnQfMBx0U%2B2cqbrUDAcVY6eLOqJwCbXNEhnoJ2CM0xBj9IkouUJ05gVghXPa3Ypp7846Fzf9jAyHYOIKAJeewIXVoNU3urBCjuD%2Bc049Eh9yFCcBDco6OiPzJCjRCY9njrrz%2B%2F5edTye2%2FtcB%2Bnrea1xe%2FNHqTcz%2FZeGevPCLmXykXMq%2BaZbuhO1QXoF%2Byaed%2B85d9leE6uHnNU2lIZcPTLk1H0Bf9iNoduYBKKjpuKUpnNi6AN7baY3DYihx6YzyesbGmuGfUTntke3fhTgN%2B5HJynecc5ot7GKEpyWR0X%2FPZzRtB0LkWQRkWS9CKCm3TDFlHXFnG2xmEvbuodAMoSFpQwLH3BDoRoxFzgA26dUM21VsEbMZeyI9hgBEaBcEZsTsKVPJsCKMQPZRWtkUZfuArl0cQbAivKwMjwXoAtcF61hRV22C%2BTShQwr%2FCKX%2FhTQRXl0GZ4HELnAeNEaXpTgvKhIjdA1DMvgDnBFcVwZnPhP14DvonVxjBKMFxVjZ7CMApvO%2BQDM4AyAugbhltYAo0S4hUnYYTaYfalqY8o1Lln2%2FkIba6i08S3SsxPi0vcK1s3Yxcx51tbHnZIv36m8yVpHRTOlXzlWMYPdQa3dF0hVdFc1Nmzdq29Du43C%2BeMMqGY6rh9wS1N9ke0o%2BK%2FqRGNLJB0j3eylMC0huNJHr6AdTUID9UjdQT36SNmNxh4yNKN1SdZmKtGLxh46tKJJ5A13hC99dqIxh2zRQVyAFL5JV6IPjT350IZ2rsDSaxcaW7h0SrigCY0XXHqgvRI1%2F7SnD969GO%2B%2BxCR7YTRN4Z1TdwBTBut9e3DT5XTTu%2FDS%2ByVRp5108Mw5Vzrhjrmwyaf9cmgLkM6C5saUPpsC2Ju%2BgGfeElLEO%2BbC5p52zAFQFAeUPtsB2EJFO%2BQAKFxz3gMjjLDJp7tXoRfgPICl104AtnA1IE4BZKlFFvFU08Imny6ngzYA1SGlzyYAtlTR4WOAFD5IsSpmXQFIYcRtoQPgXLClz%2Fp%2FtnixaqoAW3iwRd1oLSlozVOW4bmIE1oEICvZIitpkJoFyEpSIkj74t5WBCEpKW9SMsMNdbKSBu2WQ1qSc6Uz1HXMDdoxh8SkdPYzP64Mnpk0wDdviyrq%2BuYG7ZsDpKgOKYPnJg1wydtCisIuOV1BBbnJM0GW4ZOTJtRRtYUWdQupTLqQCpKTymPK4NlJkw4iA6bwdbSpW0pl0uFbyE6eD7gMnp40oZqqLbioG7S1aHDJEyS9ekwWsL1Sx6lKmwT5gR6JlkcajLytDAI5ksSr4ykJTqsKNHkSnP2SI1ksJkcgRzqZbEA4p6c4SaBTUkCOJJcpzo8vw5Mjwf4pbSFF%2FPYpwiafTkkBOdJ5AIsE5Eh0ygvIkbjBRfzmKcLIkeikVMHNh4pkARXJxFkHN5%2BWRzpPdihJBjdf0gXyJHKlqp1h5HXzyWbn4OZ3smzawlNv4iSBjo6Dmy%2BXNc6PL4O7%2BTYk3NpCiviEm7DJp2PI4OafB7AM7%2BbbdFga3HxucBHfLCFs%2FhsEkDvbauzNp5W3nv%2Bn%2FX5j%2Fq8gSbcX08ama%2B2Pd5uLudgU3x0f9hZLD55zB%2B12Ftttw1XzSknruTQbi124yB27%2BX%2BjYpTB0MZa7p9uFH%2Bh8cZjk3JHdRa%2FOLL1WFdBAkQHLaEeRUQ9Ctn0B1rnyyKo03HTQzkKhJzkDDlluKFO67xOx0MhzsRpt%2BlVBrv8VZjETIPWeZk9Qn5cGbx1XqcDmIAqfKiiV0y6AqhCxxkBUlSHlMFb53XYzL4tpKi7l71OBxihdf5MkGX41nkd6l%2FbQov4%2Bldhk0%2FXv0LrvPKYMnjrvE4HkQFT%2BDBFfNmrMKYfOnwLrfPnAy6Dt84bdNgWwIWPMEHdoK3dYGVRJ9mORgMn2okkyJNotxx3rFUn2nU01lAuz15KhTbOs1uEgGOoPLvTgLHsnAUZy2%2F0vLuVRQ6%2F5%2F92uNX26FmMAhAWkYSstJXAI52muKWKFFQS6I5KUpChj8u3nuBfzt26NHbRmkPn7cRpDrEQWynNQdRN18wLOwYzBx0R%2BO3droP0HR3%2B2m5ZOCrsFpJN2B2Cl8QMdbTTxPnCMUt3suxG4oslwnvOXbY30mqGPGEPubr2y0J1X8AfdmPoVpsaJCtBm%2Bq0SR4lMW0MzEURwmfK8MxhI%2BEVxqkyxbAl5rqTwyJAiEW6ViPTqXmo%2BrEf%2BZYghWrQaAIKpYZCZYGNgwydqEs6ny6VfqYrXcqa9krPI1YhGuSuJVWIgmNy8FMaqkLHRpkpX1E8mUlSJnGqTYZHpNeox8UkdWXQ4a%2BClpqK56kcNnaCWl1PGELEql%2BDjVxA%2FRr4RKZs6lemtCSxUW71s0uORxbs6FrB7JJLZLtHBla6ngxMrML02c%2BlrsLIowcG2Zq%2BrR5Q5DGi9KBixNUDm%2Bitru9ab76%2Bf%2FHvJvrXN%2BHNy5sf9x%2Ft%2BeLqEEHPKc6XyFvH3iwJwjWlQ9A%2F1qZ%2FjFiDxPQgUa2j3WNayXhSuHusQgzp%2FHByEEPoIZOih%2BwIgkjZRFYxZp0SN%2Bgiqy5IOKKzUlckVIydjqDP8dubJgEUZw9U69QVuvTZSlYxZqAtao0tSmwUUjF2BnERfn%2FL6SxkUYcCuCgELn02lVWMGfZ4bg0uSmzyzBy7y3DXg9mDD5TEnXrqhlOOeaJmeo%2FsM%2FfUXYajvhVA8NHl9dFd9Vx0Fzz01gudq66D7jK28oyCGfjmEpnP%2FKgyuGvugmfeFlPUdcxd2i8P4umP8DH9acAVhXFlcK%2FcBae8La6o65MjjfaJ%2FCf8uMBTrjiuNCZ6IS2ZAmSL9oOuP6DWYvXvApeDhopDl1JjnysObWjXKPY9ABvlwcYYHmxo9%2Bj6A1gyvGAj3kUSADav4z%2FN%2B3fvPj2ubm5nK2vx1833%2Bwt68aGEQeZ%2Bd0sr9LuPNcMY1fa8n1iUW036UCq4Pa0Jnilmk%2F2c52vga6KAw5X66loxuZFVPfKW%2Bhr6kRt1VOmLSts5OEZ9iwg1Lu7rW3U44sMoDJP85ZG3WXwM5356xf8B)

![scheme_1](https://schstp.github.io/Theater-Platform/datastorage/database/version_1_1_0/data_model.png "Концептуальная модель данных")

