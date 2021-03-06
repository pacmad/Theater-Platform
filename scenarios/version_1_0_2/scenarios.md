# Сценарии (версия 1.0.2)
## Блок "Пользователь"
Изменения:
###### Регистрация: 
+ в 1. убрала дату рождния и телефон. 
+ в 2. добавила согласие с правилами пользования и обработкой данных. Шаблоны документов:
>[Письмо высылаемое при регистрации](https://schstp.github.io/Theater-Platform/scenarios/version_1_0_2/Письмо_Регистрации)

>[Письмо высылаемое при восстановлении пароля](https://schstp.github.io/Theater-Platform/scenarios/version_1_0_2/Письмо_восстановления)

>[Политика обработки персональных данных](https://schstp.github.io/Theater-Platform/scenarios/version_1_0_2/Политика_Данных)

>[Соглашение об использовании](https://schstp.github.io/Theater-Platform/scenarios/version_1_0_2/Правила_Пользования)

###### Авторизация: 
+ В пользовательском сценарии добавила, что открывается у пользователя после авторизации

###### Восстановление пароля: 
+ во 2 пункте добавила, что после ввода e-mail пользователь нажимает кнопку "Восстановление пароля"
 
### Регистрация пользователя в системе

|    Пользовательский сценарий                    |    Функциональный сценарий    |
|-------------------------------------------------|-------------------------------|
|Предусловие: Пользователь на странице регистрации|Открыта страница регистрации|  
|1. Пользователь заполняет поля: фамилия, имя, отчество, e-mail, пароль, подтверждение пароля| 1. Система получает данные: фамилия, имя, отчество, e-mail, пароль, подтверждение пароля|
|2. Пользователь слева в чек-боксе подтверждает, что согласен с правилами пользования и обработкой персональных данных. Нажимает кнопку “Зарегистрироваться” | 2. Система проверяет отметки в чек-боксах, если 2 чек-бокса отмечены, то позволяет пользователю зарегистрироваться|
| *2.1 Если пользователь не согласен с правилами пользования и политикой, то регистрация невозможна*|* 2.1  Если отметок в чек-боксах нет, то регистрация невозможна*|
| *2.2 Если пользователь ввел некорректные данные, то видит сообщение об ошибке*|3. Система выполняет проверку данных. Если данные введены некорректно, система выдает ошибку|
|3. Пользователь видит модальное окно “Мы отправили на вашу почту письмо. Пожалуйста, подтвердите регистрацию”|4. Если данные введены верно, система высылает на e-mail письмо с ссылкой для подтверждения регистрации|
|4. Пользователь открывает письмо в почтовом ящике и видит ссылку для подтверждения регистрации|5. Система отправляет пакет данных для отправки в БД|
|*4.1 Если ссылка была открыта через 30 минут после отправки письма, то пользователь видит ошибку "Ссылка просрочена. Пройдите регистрацию еще раз"*|*5.1 Если ссылка не активирована в течении 30 минут, то система удаляет пакет из БД*|
|5. Перейдя по ссылке, пользователь видит модальное окно с текстом “Регистрация прошла успешно”  |*5.2 Если ссылка активирована, то система сохраняет пакет в БД*|
|6. Пользователь видит раздел авторизации |6. Система открывает модальное окно с текстом “Регистрация прошла успешно”|
|**Итог:** Пользователь зарегистрирован в системе||

### Авторизация пользователя в системе

|    Пользовательский сценарий     |    Функциональный сценарий    |
|----------------------------------|-------------------------------|
|Предусловие: Пользователь на странице авторизации|Открыта страница авторизации|  
|1. Пользователь вводит e-mail и пароль, затем выбирает опцию входа в систему |1. Система получает e-mail и пароль|
|*1.1 Если пользователь еще не зарегистрирован, то переходит к сценарию “Регистрация пользователя в систему”*|2. Система выполняет проверку введенных данных|
|*1.2 Если пользователь ввел неверный логин или пароль, то видит сообщение об ошибке*|*2.1 Если пользователь ввел некорректные данные, то система выводит сообщение об ошибке*|
|2. Пользователь попадает в личный кабинет | *2.2 Если данные введены верно, то база данных отправляет системе  id пользователя и данные*|
|3. Пользователь успешно авторизовался.|3. Система получает id пользователя и переходит в личный кабинет пользователя|
|**Итог:** Пользователь авторизовался в системе||

### Восстановление пароля

|    Пользовательский сценарий     |    Функциональный сценарий    |
|----------------------------------|-------------------------------|
|Предусловие: Пользователь на странице восстановление пароля|Открыта страница восстановление пароля| 
|1. Пользователь забыл/хочет изменить пароль. Нажимает на опцию "Восстановить пароль"|1. Система принимает запрос на восстановление пароля|
|2. Пользователь вводит e-mail, нажимает кнопку "восстановить пароль" и видит модальное окно с текстом “На вашу почту отправлено письмо для смены пароля”|2. Система создает одноразовую ссылку на 30 минут и формирует письмо|
|3. Пользователь открывает письмо в почтовом ящике и переходит по ссылке|3.Система считывает e-mail и отправляет на почту письмо с ссылкой для смены пароля|
|4. Пользователь видит поля: e-mail, пароль, подтверждение пароля |4. Система отображает поля: e-mail, пароль, подтверждение пароля|
|5. Пользователь выбирает сохранить и видит модальное окно “Новый пароль сохранен”|5.Система считывает данные и отправляет данные для сохранения в БД|
|*5.1 Если пользователь ввел некорректные данные, то видит сообщение об ошибке*|*5.1 Система выполняет проверку данных. Если данные введены некорректно, система выдает ошибку*|
|**Итог:** Пользователь сменил пароль||

