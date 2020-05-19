>*updates*:
>1. в модели в draw.io у сущностей "Режисер спектакля", "Автор спектакля" и "Художник спектакля" удален ошибочно добавленный атрибут "Роль"
>2. сущности "Спектакль" добавлены атрибуты "Длительность" и "Год"
>3. в модели в draw.io соответственно изменена сущность "Спектакль"



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
| длительность | number |
| год | dattime |
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

#### [Диаграмма в draw.io](https://app.diagrams.net/?lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1&title=data_model.drawio#R7V1rc5tI1v41qnr3g1zcLx9jx06cTGad60zeLyosYYm1JLQIO7F%2F%2FTYSjYBuEC1o6Nac1NSuwAg19DlPn%2BvTI%2F1q9ftd5G0Wn8KZvxxpyuz3SH870jRdcRT0f8mZl%2F0Z1bX0%2FZl5FMzSc4cTX4NXPz2ZfnH%2BFMz8beHCOAyXcbApnpyG67U%2FjQvnvCgKfxUvewiXxV%2FdeHOfOPF16i3Js38Fs3ixP%2Bto9uH8ez%2BYL%2FAvq5a7%2F8vKwxenT7JdeLPwV%2B6Ufj3Sr6IwjPefVr%2Bv%2FGXy9vB7%2Bev25a%2FlH4%2FWuw%2Bft%2F%2F1vl9%2B%2FPbnj%2FH%2BZjcsX8keIfLX8cm3fn18uHn%2Fw%2FjP35u7m8%2B%2FlHdv7j%2BMx3gyn73lU%2FrC0oeNX%2FAb9GfohaaHYRQvwnm49pbXh7OX%2Fnr2JpkqdMH1l1c%2FCr%2BFn7w1kpjLbexF8eFvK289%2B%2Fc6%2BUr2MpXdVVH4mE2Pur9jKkoOvkvuuOH7SN%2FbNnyKpn7NSzDTZ0a%2FMvfjugtToUneSE660vf9zg9Xfhy9oAt%2BHSRNVVLxWeSlDJ%2BM%2FKUXB89FWfVSkZ9nN8x%2B4y4M0CNrCtZPrGWpduquUrzF%2FtnTb%2BWFo3Qjo3QjrXyj%2FbshboQ%2B5B78cGone3Q5%2FP7h1X9wtO%2FX4e3r9f38kzVbXI2x2OXk8ClaTuJwMg1Xq6d1EL8QcolEaJN8RHIQB97yC0IPbz3fCWQcblLRWvoPcfoxSt9%2F8vk%2BjONwlR54y2C%2BRp%2F3114%2B%2B%2Bh%2BCEDepKd3N7t8CJbLq3AZRujMOtzL8MabBuv5H%2FufMJTDqS%2FpTxnoVIju97DcyfoimM38dTKUMPZi7373JMnXNsl73b1p8xL9h979lXJhjkz0mFfoWD0co%2F%2BSy6P4KlwjtfGCnQb43jb%2B5W%2BT0c%2BicPMNC%2FLuscOn9cyfYVWr1zs2zUrelP%2B7VhOwfClF%2BVJNa3%2Bc1xSLoimaU60TBSFklrgGyMcqYQWpoghMI0ErSVVXQnVMbpJnrBSCep0tS0G2mKeDKayXVTipW3wmnw7kFjH53xa%2BF%2FtR8s01%2Bp%2Bv4RTN%2BOhKG71RSLn4FayW3m5KH8J1jBfH5N1NF8Fy9of3Ej4lz4AWrukjPrpchFHwiq5H991fnF%2FXNKtwxdfkm1iD%2FS265g7Ph5qd%2BsPbYtGbhsult9kG99lIVggEgvVlXiSFhAJsYeaRwKGumcbR5fGgodnPadbxn6MCj1X8NW%2BJpGONROQyeYnblotgrXmRk8p4L5UT9D1N%2Bb%2Bbj%2Bq%2FRsnAknU%2FmaHs43YnrpO1H%2F8Ko8fscu1ffFZNFVbNvKrkQcAg9aYego4rzktRIo8piqlU60k71HQoS2YmgncfYf2sQs56dee2fnYhCfSl3zxuPInnNvq%2Fg%2Fjv9LvJ55%2FJZwQQ%2B6O3v3N%2FevuCD9boff2d3R4d7L%2Fl4MPD13ZHhe%2Fd%2BVGAXrgfpSfZltS830qdBRXHU6TzW62Su6nqJUuvqd9quaUbKf36rfg5coqQWo6a8ud%2BMQbrsUvrsTzhZkNzTlVqfAnZrMdaNMiJIsUqBGtwaGuwHkdaWYNNJLEzG0AlQ3ZgAjKGUNQq%2FOsuhMJt%2BkkTcO2tfD4IA1HaI4trR6CCMyGDRWVVMjAHkMI26WbFpAsVlb28fZ4b65%2BTW0d5fLR%2FfghmwevYIOZ%2B48WLJAm0RM4jIIvMyNLYcOYlXA0iFgAscQPtFBpXqNJqkJYqMfcCRqtw5CkNUWWxp2ORJxzlujBMe3SIdKmj2jgXOuguXEUVoPSl56NV9OBiKhvCRKu0Usbq5CoL3SndqBz24hytMskVVgZFSAVaHZ0QtlUKqnPQpArlOV3k6aJsN5R5wxBM5k0iznaizFt28UaGpfUq87bc4K%2Byye8pKY7TZb5xNR0djcTD%2BYKkOifmJFSFHqI%2BIvBIhryX3GWpPVc5Wtss%2FIqqubWjKl9uFC5HH%2Fa%2F33F2xO1c%2BXIKJuBqc2EWFFY9pq60LCEa302QvGgeK5JLyRnStVMTTDsttSjBNpYlVv20jSM34p0zNOXOnmfKcJpXcerS1rEiqIreUBNUQxVOFYyCBLsacvbcU1PojnqBv4vv56oJkPWrFA0ivyIrheEyqMWJ3km3Tjp9HrBLKqFalA0vRz9xhVBLfrrtlkpPuSsDrdJOJmVwrG7WCMbYV9fKgE2OBsqgCKYMllu0ctyy331UGbAWWXbPwt%2B90wBRqjoxt42GUq6JVkeoK8qFkvunFkTecE%2FEf13XLoq3Mk31QunZIrLldhNO9J8HhHtsgh5He0s0tB%2Frinvh5v8VxDczaFg1Aam8fVG8l6a7TVWBNaQ1VsvlvLZSPzxLM%2Bu%2BwCmsZcvtq5yimQM761pz1RTNKznYhqmMWtapylhWD1ttFlruTPApfR%2Fft0nTZEn4ocS9RYn72DArUmY5kc34NQoVFCcWuctT466RyPu0TfsjyzIIpe1ilLZrVRWJlcVilNp2urzzq20nW3GhuJ21ElWranGVoLpdIyNw%2FsoLlnxgBqpQT6pCZUcWSoF738jSILoFuFI%2F7U7FtEuAKzrZMLrxtttfYcTJggFo6QlabGdoaNHJDlCAFrZpz9RTRmjRiOkPthNvtkoIjQBaJIaWjPpoQGwBurTW2KJVzLsM2EJ2DkC3r%2Fy4opOhvr5xBfryWuMK%2F848ftNPxnNX6EUu%2FQnAi%2FzwQiF57RteyDguwAsjvEgcxdXJKC6mFNgswhg4BSQHGGfwcK4O4dzWACNxONciw7lX4Wrlp%2FUXUBPRVU2ErZ9aE4GrG862JsIiw77TvQxCWYTAZRFWVahZ4LIIrHRQFtFivbOq0E%2BG9Y4MA6Mxx9T1DkzpwUxpdmwZvjDCakBOA8hSP%2B16xbTLgCxkIDhCdhPAitSwMnxRhAWMoq1hhT%2BlKL%2FpJwPAwXaChv0QRCufk3sE8NITvAhQGGE1aNUHfKmfd%2B4b4XCcfjL%2BO42SPbtmEw98IsnRpWl5hF4TYmwnXjYZXwZ0YZx3t2Leu0OXUuu1yw1tbMoeL5vkCaZLn1uwF%2FCmL7yxhscbMsB781FtLVf%2FMMix%2BUd4%2B4McMuLLteMW0KYvtHGHRxsy5HvzEQwcVrThH%2FXtD21Id%2BoyDB9XHuyj2DXJhF7k%2FNSVhtsLn9U%2B3HQpdEivK1vzanfhLtjisAG32AUYdpVjyFKAwW0H7grJpLV4whbcJ6%2BdTpXZJP4e3KpNpjZmCBfjABonhDLN2XHGbogz%2FLZhtCGr0dos55%2FV4Db9uK5eUoLDwg4Fyqjx1h32qEBy6FrGqJ7mkLp%2FB5vJ3oD7sDEJtS0aP%2B%2FYKHEfmmrpHo25D031yJ14cx86DTrgO9MJvGoOsYHg7j4n70DTQEpd0aRUL8lWlnZjltLyJjUGDqh3zZSra%2FQhV45MN5y6L%2FBhyqXQNb73lhQSNQjlnB7K0at22DsW2FXLRLTn1hpDYXFcIPGDthhxozKVnJHidsVQqCIhEMPoLWnyloBRCB2Bu0KsEAw7qAzeDkPhiQRIYZt0%2FnVf3CafjPJj2ortdOEDuMgNLoM3xVCYIgFcmCZdr%2FLSJAAXSguvl7zl%2BAVgRWZYGb4ZhsISCbjChivydvBSmBzjRdIJA7Wi0iPL4I0wFJ5IqEtnBhf%2Bfbx9FYoapBHz1ac13EFi4fTEgq1CYqFC%2FEhDZ4vEDxIL4iYWjCrLStzEgkFaVJBYYFzzDHnJsQ3S5kmKQ8CSFsaSZseUwfMKBhBit0UUefmwDTJTjazRpxXsDyQ1qAyeTzCABLstqMjLgW2SmerXZIoAUiSGlOFzCSZsZtgSUzLFlBBTyAQ118JNgJWeYGXwRIJJBo4hkcCMLFrFxMuXSKDQ21w%2Fw%2FYdHWcSjBMTCZpRM%2B%2FnkEigMOD4z7Bzh9CZhEq%2BHXEzCTZkElovera8mQSbzCTMgKJWOHuaHVgGTydQOEgAVtgmXd50AoUkZOZvp1GwiYMQcgpSI8vgOQUKEyAgC9uky5tToBDwBdvJJvJXgR9BakFqZBk%2BtUAl0QNoYZh1%2FrR5XUz%2B2%2B2fxvz9%2By9Pq9u76cpcfL79OR9TkWW6CMOtv548hNFkhV7QZOPNAWbkhpmmqQZukgYo0xxlalVVaJCh4yOZv%2FSevWCZDHiSVIpvJ%2Bun1b0fAcZIjTFmw8Aut3RmE1I6AJlaU%2BZ8cpkOpSsFdgc6F6xxBscaMokEpRPMcMM%2Fi9Qb3JBZJSjSOgOk0dTBkYbMKsG%2BQMxIwz%2Bx1Nu2QE6DZIC4fOTqKMdGnnGTH%2BMjHxW4yDMG5wrSZlIoWpKOp3N5nM4ZmwUC0TnrR0iYG9M567px4RrK4V%2FpxqqDNECtVADelOQuGcyUQS2wiKtsIp7R%2BzOoU8dqgWuAJNSKEpeDpZYW78Y64Ry5EXceftLL%2FYq9XHT6R7ANYmRDacpl8nq%2Fb2lBNqjlbbFzXAY7GAVNMtJO3a7GrrEPaop5Zdo4jnSRG20cd6j5hU3jhK79VSv9d5bi3743jSMdddg0rs2mcdx5tLqQhdfHh5v3P4z%2F%2FL25u%2Fn8S3n35v7DmNZV%2BW1P0geLZJeLpFoyt5rutaydEXMWXQA1QgB5s0TCssey7NXDhpAtL%2FQhk5lRWOmqV7p6ZRW6AoM%2BdNJLhF05BstMdAQqfba70IdM%2BncAKWyTLm8XHRls9WYzZKNuAVRkBpXBO12gTrSlQy5vnSjpDE297WIy87ePk80CzRWUiZ4Bwgzf8QJVom03E5MWYkg%2FKA8su46XyH%2Fw0fNPwTuSG2b67Hih80IBzLSkAZUWZigMI0AFcCa40rTLhR8XAOBKO1yRl2OEpBjBO6Euw3kIwCI1sODeq8GABThG2haZywAsl7fPc2P9c3LrKI%2BP9s8PwSx4pURzMbAg%2FygGZJEaWTSlx6AuVbwgqNscWWr1Uz5kIYO6GbJE%2FnPgwxZOcmOL3mM0lypgEM1tiS3yRnNVg7RbvgXTRz%2Fp0LgMn5IRQOcDIQUddT7gslxcZtnUf1FVrVoeJKvqrBBL0t6Jd2JZaH3gsexBdWf7pgajytgSoryzYsykmQX1nYze%2B0FtJVwJKa0MWa8V2Nei0E%2BcgC1Nqzy50U%2BolCYF4J9gBpdK10pCAgpKNwF6S%2ButN03ym4A5smNOU0ueI%2BaQhTo3H3XAHEbMqWI7kg9zNIWsqcgTHbyZxiE4%2BN06%2BKqi6AWfO%2BvHPNa9reqnufjykBtoClmG4SUyeJTdoEhCCQwHQgcDDrAjD8NBlu4DhoNuqp0zVRea4aBi7GRRRxQuobZZIAP9BIyxG2KM5vCSK5XMvACsME67WzHt3Vnn%2FKafkuHgTFwB4NITuNAatPpGF1rIEdx%2FxqlX%2BYcc%2BUlAg7KOzsg8MUp0wuOZo%2B78md6rjsdzd5%2BbIHk9bxVmb%2F4o9Wam%2F8JQb46tUiZftU8l33RLdyI2SK9g30Tz7r3kLks1sXrIWW1DacjVI1Ptui%2BgD%2FsxdBuTUMmoKT%2Bl6ZwY%2BsBem%2BlNA2LoC8N28vqmXii6dUTndkd3fhSgN%2B5HJynecc5ot7GKYpwWR0X%2FOZzRpB0LkWQekWStCKCG1TDFlHXFnG2xmEvauodAMoSFhQwLH3BDohoxFzgA26dUM22VsEbMpeyI9hQBEaBYEZsTsKVPJsCKMQPZRWtkkZfuQnXJ4gyAFelhZXguQBe4LlrDirxsF6pLFjKs0Itc%2BhNAF%2BnRZXgeQNUFxovW8CIF50VFaoSsYVgGD4ArkuPK4MR%2FmgJ8F62LY6RgvKgYO4VlFNh0zgdgBmcA1BQIt7QGGCnCLVTCDqPB7AtVG1Ouccll7xUlS9bvd7BVtWwjXH7ZewnLZuxi4jzr6mPOyKMBuRfYbMfJKdu8cG0tS9KXcq4dldGUHuFYDQ1yEFt%2BAddJd1V1Q9fG%2Bsa0uyicPU2BfKbjigLXKGb4x9keg0d70zDyn0NvGl0iyajpJpXCpKjgShu9gQY1AU3WI5UI9egjZH8afcjQntYlfZshRXcadegU0hroIhnYS%2B4IZfrsUKPLlkbIFrSQsGJLD6Q1vOaftMrBEudjiZd4IMd60wD8OdX2UmWw3g4Hk1pMk7oLi7pfCmTSoAYrmnGl425Ec5t8soYBinqFM6CZMaXPkl76lg1A8NASUvjTO3Cbe9IvB0CRHFD6LOalCxXpkAOgMM15D3wO3Caf7D2DSt7zAJZe63jpwtWA9gCQpRZZ%2BBPFcpt8shgGinhlh5Q%2BS3jpUkWGjwFS2CDFrJh1CSCFEreF%2Bt1zwZY%2Bq3fp4kWrfwBsYcEWeaO1mBg9TziE5mIbkyIAWckWWUkdlyxAVpIQQdIX93YiCElJcZOSGW7Ik5XUSbcc0pKMK50ur2Ouk445JCaFs5%2FZcWXwzKQOvnlbVJHXN9dJ3xwgRXZIGTw3qYNL3hZSJHbJyQoqyE2eCbIMn5w0oI6qLbTIW0hlkIVUkJyUHlMGz04aZBAZMIWtoU3eUiqDDN9CdvJ8wGXw9KQB1VRtwUXeoK1Jgkthl%2B2neAGbo3ScqrT04i7bQGWSk0cSjLydDAKRicCr4ykJTrMKNFkSnP0SmZg0HjYgMjmZbIA7Ix8%2FSSDjx0BkIqJBzo4ywxOZkOFpIDJhxhb%2BNOW85t%2BWeCdcwzVGxb057WPsnlSu0ONsn7XaLgyJp2oZBcs7M71ZWTwd%2FUI50HVivvEs6aFfuK5D7LnZMZ1n1cNUj7nucj7knBaZfSn4s1B6y6H0Fke9wJ8l5ZFMCB1qb8GfFdS4PIlFqGoDA3H9WbwnL%2FizndicFvccEz9JICMb4M%2BK6M%2Byo8zg%2FqxFlu%2BCP8uMLfwreLnNf4M9HTvzZ6%2B%2FrLz17N8dOLW%2Fgxj7tGZ6vN%2BwwkXL5v744NEmBy%2B5g3a7VeydwppXivshhfFzx67qIhc096%2FkEejJzh%2BHf5pe%2FIXGm1k45Ta%2FzNc44ux2ZdCrZHQOkqQ8kqRGcccS6OfMRFAjYxyHHCm4h2K6hxluyNPPqZGxC%2FAJGe02rcpeF780CJtp0M8pskPIjiuD93NqDRJcgCq1qKJVTLoEqEIWeAGkyA4pg%2FdzarA%2FaltIkXd7VI0MMEI%2F55kgy%2FD9nFqD8CVASy20VHH2SQAtZJ0n9HNKjymD93NqZBAZMIUNU%2FjXd3KjnyDDt9DPeT7gMng%2Fp06GbQFc2Lp45Q3aWg1WFnmS7epo4EQ7lgRxEu2m7V4o1Yl2Tb1Q1FyevZQKbZxnN41irXfveXa7AY3OOQtyrqnCHOVaKrK%2FVbRTdKwAuLU9xittJfAIpyluqSJFLQl0RyUpqq5dlG%2FtoF%2FO3bo0dt6aQ%2Bbt%2BGlOF%2F1D5Q4gNhE%2BKpl4T2txJNPG4IZtRls5TfbGtlG6k2k1kjXW1p%2BxY9KHzLWZx27ATCKUJOc74QqozbERrk43SiLfBMbNgXUj85Va64ZmoAXArrKUkKFUbJkrlb92pThVz1M97EE0rUH%2BTFBNKxhHB1upoZJ1vNYY4hXm4pnEqdpT1QmNSKvRp7GTmFPq4a%2Blzr6u9KnieSqHjQyxVtfjdny%2B6teA4RzUr4GpZ4imfmWuJxyfYVY%2Fyyw5GVYzf5xZwSxHoY24emCl6%2FHA%2BCpMnz0l8iqMOHqg4z1b2%2BoB0WzOSw8qRlw9MEdrdX3XevP9w6v%2F4Gjfr8Pb1%2Bv7%2BSdrtrg6RPFyivMt8tZbbxoH4ZrQIehhadPDgq1BbHpgZ%2F1oB8uJtAgidrBUiCGZo4oPYgh9LEL0sRxBECEbWSrGTIZEoZOlOil6RGeFzopWjJ1sOZihtzeJAygQHajeoit06bOdpWLMQKDdGlukYNCuGDuFOwW9v%2BVkGtKoxgBcJAKXPhtbKsYMmx%2B2Bhcpdj%2Bkjt2luOvB9NEHCsNOPXXdLsc81WZ6n1Finqun7lIc9Z0Ago8uro%2Fuyueiu%2BCht17oXHkddJeyx1UUTME3F8h8ZkeVwV1zFzzztpgir2Pukn55sJ3ch0%2FJTwOuSIwrg3vlLjjlbXFFXp9cVUifyH9GjwtUyZLjSmOyCdwWxkG2SD%2Fo5qPaWqz%2BWeBy0FB%2B6FJqLnL5oQ3pGm19D8BGerDRhwcb0j26%2BQiWDCvY8HeROIDN2%2B2fxvz9%2By9Pq9u76cpcfL79OR%2BTiw8hDCL33JpKoef2QtH1UW3f7YlFud02nlOlykmnOF%2FyXhv0E6bUV1OKyY2s6pG11FfXjtyoq23NSpTytl7fIkKMi%2Fl6taSoHAp9KVvV5vZBg9zhMQVlqPJVy928lN3P6At7mVLh3JKHJhkmKW5pBvlDIfOHZlVwRtz8oUk2BEH%2BkNGSzdRVvpgcZT9u4H4Vy0NmB5XB04eUnbgBUtgmXQqaRurQKTsJz%2FztNAo29E45QBZ5kGXwBCJlW2BAFqZJr9wIUwJkIcNsGQFsuE1CSgAuEoNLr5T1dAGDDXbaootWMesSoAuZ1MHokrybJYKX3b7zADJSg0xTDntu2UPKluEAMmwgw3%2FLnb6qFCwy%2FhJ5McRf5MYYa3CMgQBMW4zhH4DpC2MojODYsNkug5kfgfd0DqDjDg06NsRmWoKOzT82wwF0NNPbfvhx%2FU7%2FNNF%2BLj5N%2FB%2FBfykVUbMnZNlABFhymMmqKPqAGapkQYymOcrUqqZUILOYr2bBcn1vPEf6%2FytXz%2FPLG2dMGjYvvgd2TH8AQ5GhhphTDTBmjwBDlSowY%2BoBpjFwFIWhWoPFBRjSiokXvod8JegikR1mKOWf%2FcIMacdAwxpHpNHERpo%2B9xHproOk1V5rxCY7pzSB1MH20R4QWz8qFFxbPqyidKUhxxShDK2EPI37P%2FTiDiMGtx0PijTdhlHfz6EaZt31rP0c6DAKwzh%2FeeRtFp%2FCmZ9c8T8%3D)

![scheme_1](https://schstp.github.io/Theater-Platform/datastorage/database/version_1_1_1/data_model.png "Концептуальная модель данных")


