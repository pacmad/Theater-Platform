# Сценарии (версия 1.1.2)
Изменения:
##### Блок "Пользователь"
+ В конце таблицы добавлены ссылки на прототипы страниц
##### Добавлен блок "Главная страница"
+ В конце таблицы добавлены ссылки на прототипы страниц
##### Добавлен блок "Личный кабинет" 
+ В конце таблицы добавлены ссылки на прототипы страниц
##### Добавлен блок "Театр" 

## Блок "Пользователь" 
### Регистрация пользователя в системе
|    Пользовательский сценарий                    |    Функциональный сценарий    |
|-------------------------------------------------|-------------------------------|
|Предусловие: Пользователь на главной странице|Предусловие: Открыта главная страница |  
|1. Пользователь нажимает на кнопку личного кабинета в правом верхнем углу. и попадает на страницу авторизации, где выбивает "Зарегистрироваться"|1. Система открывает страницу авторизации, затем страницу регистрации|
|2. Пользователь заполняет поля: фамилия, имя, отчество, e-mail, пароль, подтверждение пароля нажимает кнопку “Зарегистрироваться”| 2. Система получает данные: фамилия, имя, отчество, пароль, подтверждение пароля|
| *2.1 Если пользователь уже зарегистрирован, то он выбирает опцию Авторизации и переходит к сценарию “Авторизация пользователя в систему”*| *2.1 Если пользователь уже зарегистрирован, то он выбирает опцию Авторизации и переходит к сценарию “Авторизация пользователя в систему”*| 
| *2.2 Если пользователь ввел некорректные данные, то видит сообщение об ошибке*|3. Система выполняет проверку данных. Если данные введены некорректно, система выдает ошибку|
|3. Пользователь видит модальное окно “Мы отправили на вашу почту письмо. Пожалуйста, подтвердите регистрацию”|4. Если данные введены верно, система высылает на e-mail письмо с ссылкой для подтверждения регистрации|
|4.Пользователь открывает письмо в почтовом ящике и видит ссылку для подтверждения регистрации|5. Система отправляет пакет данных для отправки в БД|
|*4.1 Если ссылка была открыта через 30 минут после отправки письма, то пользователь видит ошибку "Ссылка просрочена. Пройдите регистрацию еще раз"*|*5.1 Если ссылка не активирована, то система удаляет пакет из БД*|
|5.Перейдя по ссылке, пользователь видит модальное окно с текстом “Регистрация прошла успешно” и кнопку "Войти", нажав на нее открывается страница авторизации|*5.2 Если ссылка активирована, то система сохраняет пакет в БД*|
|6.Пользователь видит раздел авторизации |6. Система открывает модальное окно с текстом “Регистрация прошла успешно” и кнопкой "Войти" с гиперссылкой на страницу авторизации|
|**Итог:** Пользователь зарегистрирован в системе|[Прототип страницы регистрации](https://www.figma.com/proto/fk5oo6Er6uU6fo89jsOW7r/Prototype-Tomsk-ver.2?node-id=343%3A430&scaling=min-zoom)|

### Авторизация пользователя в системе
|    Пользовательский сценарий     |    Функциональный сценарий    |
|----------------------------------|-------------------------------|
|Предусловие: Пользователь на главной странице|Открыта главная страница|  
|1. Пользователь нажимает на кнопку личного кабинета в правом верхнем углу. и попадает на страницу авторизации|1. Система открывает страницу авторизации|
|2. Пользователь вводит e-mail и пароль, затем выбирает опцию входа в систему |2. Система получает e-mail и пароль|
|*2.1 Если пользователь еще не зарегистрирован, то переходит к сценарию “Регистрация пользователя в систему”*|3. Система выполняет проверку введенных данных|
|*2.2 Если пользователь ввел неверный логин или пароль, то видит сообщение об ошибке*|*3.1 Если пользователь ввел некорректные данные, то система выводит сообщение об ошибке*|
|3. Пользователь успешно авторизовался и попал в личный кабинет.| *3.2 Если данные введены верно, то база данных отправляет системе  id пользователя и данные*|
|4. Пользователь может выйти из аккаунта нажав справа кнопку "Выход"|4. Система получает id пользователя и переходит в личный кабинет пользователя (есть кнопка "Выход")|
|**Итог:** Пользователь авторизовался в системе|[Прототип страницы авторизации](https://www.figma.com/proto/fk5oo6Er6uU6fo89jsOW7r/Prototype-Tomsk-ver.2?node-id=343%3A447&scaling=min-zoom)|

### Восстановление пароля
|    Пользовательский сценарий     |    Функциональный сценарий    |
|----------------------------------|-------------------------------|
|Предусловие: Пользователь на странице восстановление пароля|Открыта страница восстановление пароля| 
|1. Пользователь забыл/хочет изменить пароль. Нажимает на опцию "Восстановить пароль"|1. Система принимает запрос на восстановление пароля|
|2. Пользователь вводит e-mail и видит модальное окно с текстом “На вашу почту отправлено письмо для смены пароля”|2. Система создает одноразовую ссылку на 30 минут и формирует письмо|
|3. Пользователь открывает письмо в почтовом ящике и переходит по ссылке|3.Система считывает e-mail и отправляет на почту письмо с ссылкой для смены пароля|
|4. Пользователь видит поля: e-mail, пароль, подтверждение пароля |4. Система отображает поля: e-mail, пароль, подтверждение пароля|
|5. Пользователь выбирает сохранить и видит модальное окно “Новый пароль сохранен” и кнопку "Войти", нажав на нее открывается страница авторизации|5.Система считывает данные и отправляет данные для сохранения в БД. Открывает модальное окно с текстом "Новый пароль сохранен" и кнопкой "Войти" с гиперссылкой на страницу авторизации|
|*5.1 Если пользователь ввел некорректные данные, то видит сообщение об ошибке*|*5.1 Система выполняет проверку данных. Если данные введены некорректно, система выдает ошибку*|
|**Итог:** Пользователь сменил пароль|[Прототип страницы восстановления пароля](https://www.figma.com/proto/fk5oo6Er6uU6fo89jsOW7r/Prototype-Tomsk-ver.2?node-id=347%3A605&scaling=min-zoom)|

### Выход из аккаунта
|    Пользовательский сценарий     |    Функциональный сценарий    |
|----------------------------------|-------------------------------|
|Предусловие: Пользователь находится в личном кабинете|Предусловие: Открыта страница личного кабинета| 
|1. Пользователь выбирает опцию "Выйти" |1. Система принимает запрос на выход из системы|
|2. Пользователь видит модальное окно с текстом "Хотите выйти?" и кнопками "Да" и "Нет"|2. Система открывает модальное окно для подтверждения выхода из системы|
|3. Если пользователь выбирает "Да", то модальное окно закрывается и открывается страница авторизации|3. Система выходит из личного кабинета пользователя и открывает страницу авторизации|
|4. Если пользователь выбирает "Нет", то модальное окно закрывается и пользователь остается в личном кабинете|3. Система не выходит из личного кабинета, закрывает модальное окно остается на странице личного кабинета|
|*Итог: поьзователь вышел из аккаунта*|[Прототип страницы выхода из аккаунта](https://www.figma.com/proto/fk5oo6Er6uU6fo89jsOW7r/Prototype-Tomsk-ver.2?node-id=164%3A362&scaling=min-zoom)|

## Блок "Главная страница"
|    Пользовательский сценарий                    |    Функциональный сценарий    |
|-------------------------------------------------|-------------------------------|
|Предусловие: Пользователь на главной странице|Предусловие: Открыта главная страница|
|1. Пользователь может переходить в разделы, кликая по ним в меню навигации. Нажимая на логотип платформы, открывается главная страница|1. Система позволяет переходить на страницы разделом через меню навигации. Через логитип платформы идет переход на главную страницу|
|*1.1 Нажимая на разделы: логотип, афиша, билеты, театры, личный кабинет, пользователь переходит на другую страницу. При нажатии на уведомления появляется модальное окно на главной страницу. Подробнее см сценарий "Уведомления"*|*Нажимая на разделы: логотип, афиша, билеты, театры, личный кабинет, система открывает другую страницу. При нажатии на уведомления открывает модальное окно на главной страницу. Подробнее см сценарий "Уведомления"*|
|2. Пользователь под меню навигации видит слайдер, состоящий из n-го карточек состоящих из фотографий/видео о событии, названия и описания события и кнопки "Купить билет" (нажимая на нее, пользователь окажется на странице спектакля с подробным описанием). Пользователь видит карточку одного спектакля 5-10 секунд, затем появляется следующая. После последней карточки показ начинается заново. Также может сам переключать, нажав на стрелочки <>, либо на крулые кнопочки внизу.|2. При открытии главной страницы система запускает слайдер состоящий из фото/видео события, его названия, описания и кнопки "Купить билет" с гиперссылкой на страницу спектакля. Система автоматически переключает карточки через 5-10 секунд. По запросу пользователя, система может переключать карточки до истечения времени. После окончания показа всех карточек, система начинает показ заново.|
|3. Ниже меню навигации и слайдера, пользователь видит блок "Театры", где представлены 4 карточки театра, состоящие из названия и фото. После нажатия на "Театры", пользователь переходит в раздел "Театры" и видит полный список театров. Нажав на название театра, пользователь попадает на страницу театра.|3. Система отображает блок "Театры", где есть 4 карточки из названия и фото театра. Система позволяет переходить в раздел "Театры" (с их полным списком) через гиперссылку в названии "Театры". Также позволяет переходить на страницу театра через гиперссылку в названии театра.|
|4. Ниже раздела "Театры" есть функция поиска события с фильтрацией (см. сценарий "поиск событий" в блоке "Билеты"). Пользователь вносит данные в фильтр, вводит название спектакля и нажимает кнопку "Поиск". Открывается страница раздела "Билеты" с результатами поиска по данным параметрам|4. Система отображает панель поиска с фильтрацией. После запроса на поиск и считывания данных, система открывает страницу раздела "Билеты" и отображает результаты по параметрам поиска. Сценарий функции "Поиск с фильтрацией" смотрите в блоке "Билеты"|
|5. В конце страницы пользователь видит слева меню навигации, через которое можно переходить в другие разделы. Справа располагается контактная информация о владельцах платформы|5. В конце страницы слева система отображает меню навигации, где есть гиперссылки для перехода в другие разделы. Справа располагается контактная информация о владельцах платформы|
|*Итог: Пользователь видит премьеры месяца в слайдере, может использовать функцию поиска и переходить на другие страницы*|[Прототип главной страницы](https://www.figma.com/proto/fk5oo6Er6uU6fo89jsOW7r/Prototype-Tomsk-ver.2?node-id=161%3A0&scaling=min-zoom)|

## Блок "Личный кабинет"
### Добавление фото
*Требования к фото:  размер не менее 200x200px, соотношение сторон от 0.25 до 3, сумма высоты и ширины не более 14000px, файл объемом не более 50 МБ, соотношение сторон не менее 1:20*
|    Пользовательский сценарий                    |    Функциональный сценарий    |
|-------------------------------------------------|-------------------------------|
|Предусловие: Пользователь в личном кабинете|Предусловие: Открыта страница личного кабинета| 
|1. Пользователь выбирает опцию "Добавить фото" |1. Система принимает запрос на добавление фото|
|2. Появляется модальное окно с текстом "Вы можете загрузить изображение в формате JPG или PNG." и кнопка выбрать файл|2. Система открывает модальное окно с кнопкой для загрузки фото|
|3. Пользователь выбирает файл и выбирает открыть|3. Система делает проверку файла на соответствие с требованиями|
|*3.1 Если файл не соответствует требованиям, пользователь видит ошибку "Попробуйте выбрать фотографию меньшего размера."*|*3.1 Если файл не соответсвует требованиям, то система не загружает его в БД*|
|4. Происходит загрузка фото. Пользователь может выбрать область фото, которая будет отобрачаться в профиле|4. Если файл соответствует требованиям, то система загружает фото в БД с привязкой к id профиля|
|5. Пользователь выбирает "Сохранить", модальное окно закрывается, страница обновляется и фото отображается|5. Система закрывает модальное окно, обновляет страницу и тображает фото в личном кабинете|
|*5.1 Если пользователь хочет отменить загрузку фото, то может выбрать "Отмена" на любом этапе*||
|Итог: у пользователя в личном кабинете есть фотография|[Прототип страницы для добавления фото](https://www.figma.com/proto/fk5oo6Er6uU6fo89jsOW7r/Prototype-Tomsk-ver.2?node-id=164%3A362&scaling=min-zoom)|

### Обновление фото
*Требования к фото:  размер не менее 200x200px, соотношение сторон от 0.25 до 3, сумма высоты и ширины не более 14000px, файл объемом не более 50 МБ, соотношение сторон не менее 1:20*
|    Пользовательский сценарий                    |    Функциональный сценарий    |
|-------------------------------------------------|-------------------------------|
|Предусловие: У пользователь есть фото в личном кабинете|Предусловие: Открыта страница личного кабинета с фото пользователя| 
|1. Пользователь выбирает опцию "Обновить фото" |1. Система принимает запрос на обновление фотографии|
|2. Появляется модальное окно с текстом "Вы можете загрузить изображение в формате JPG или PNG." и кнопка выбрать файл|2. Система открывает модальное окно с кнопкой для загрузки фото|
|3. Пользователь выбирает файл и выбирает открыть|3. Система делает проверку файла на соответствие с требованиями|
|*3.1 Если файл не соответствует требованиям, пользователь видит ошибку "Попробуйте выбрать фотографию меньшего размера."*|*3.1 Если файл не соответсвует требованиям, то система не загружает его в БД*|
|4. Происходит загрузка фото и пользователь может выбрать область фото, которая будет отобрачаться в профиле|4. Если файл соответствует требованиям, то система загружает фото в БД с привязкой к id профиля. Старое фото удаляет из БД|
|5. Пользователь выбирает "Сохранить", модальное окно закрывается, страница обновляется и фото отображается|5. Система закрывает модальное окно, обновляет страницу и отображает новое фото в личном кабинете|
|*5.1 Если пользователь хочет отменить загрузку фото, то может выбрать "Отмена" на любом этапе*||
|Итог: у пользователя в личном кабинете новая фотография|[Прототип страницы для обновления фото](https://www.figma.com/proto/fk5oo6Er6uU6fo89jsOW7r/Prototype-Tomsk-ver.2?node-id=164%3A362&scaling=min-zoom)|

### Просмотр избранного
|    Пользовательский сценарий                    |    Функциональный сценарий    |
|-------------------------------------------------|-------------------------------|
|Предусловие: Пользователь в личном кабинете|Предусловие: Открыта страница личного кабинета|
|1. Пользователь переходит в раздел "Избранное"|1. Система проверяет наличие избранных спектаклей у пользователя и открывает страницу "Избранное"|
|2. Пользователь видит карточки спектаклей с красным сердечком в правом верхнем углу|2. Система отображает спектакли, привязанные к id пользователя со статусом "Избранное"|
|*2.1 Если избранных спектаклей нет, то есть кнопка "Добавить в избранное". При нажатии прользователь переходит в раздел "Афиши"*|*2.1 Если система не находит избранные спектакли, то открывает страницу с кнопкой, которая позволяет переходит на страницу "Афиши"*|
|3. Пользователь может удалять спектакли из избранного, нажав на красное сердце. После обновления страницы спектакль не будет отображаться в избранном.|3. Если спектаклю обозначается статус "не избранное", то система готовит его данные для удаления из избранного в БД|
|*3.1 До обновления страницы пользователь может вернуть спектакль в избранное, нажав на белое сердце*|*3.1 Если статус не был изменен на избранное, то при обновлении или переходе на другую страницу данные удаляются из БД*|
|*3.2 Если пользователь переходит в другой раздел в личном кабинете, то убранные из избранного спектакли удаляются*|*3.2 Если статус был изменен на "избранное", то система возвращает данные в исходное состояние в БД*|
|4. Пользователь через карточку спектакля может переходить на страницы: описание спектакля, отзывы, режиссер-постановщик, художник-постановщик, театр.|4. Система отображает карточки спектаклей с гиперссылками на страницы: описание спектакля, отзывы, режиссер-постановщик, художник-постановщик, театр.|
|*Итог: пользователь может добавлять, удалять карточки спектаклей из раздела "Избранное". Может быстро переходить на определенные страницы.*|[Прототип страницы избранного](https://www.figma.com/proto/fk5oo6Er6uU6fo89jsOW7r/Prototype-Tomsk-ver.2?node-id=247%3A80&scaling=min-zoom)|

### Мои покупки
|    Пользовательский сценарий                    |    Функциональный сценарий    |
|-------------------------------------------------|-------------------------------|
|Предусловие: Пользователь в личном кабинете|Предусловие: Открыта страница личного кабинета|
|1. Пользователь переходит в раздел "Мои покупки"|1. Система проверяет наличие купленных билетов у пользователя и открывает страницу "Мои покупки"|
|*1.1 Если билетов нет, то в окне написан текст "Нет купленных билетов" и кнопка "Купить билет". Нажав на кнопку, пользователь перейдет в раздел "Билеты"*|*1.1 Если билетов нет, то система выводит в окне текст "Нет купленных билетов" и кнопку "Купить билеты" с гиперссылкой на раздел "Билеты"*|
|2. Пользователь видит остортированный по дате и времени оплаты список билетов. В списке указаны: название спектакля, театр, дата и время, сумма оплаты и код для получения билета в кассе.|2. Система автоматически сортирует билеты по дате в обратном порядке. В списке указаны: название спектакля, театр, дата и время, сумма оплаты и код для получения билета в кассе.|
|*2.1 Если купленных билетов нет, то появляется кнопка "Купить билет". Нажав на нее, пользователь окажется в разделе "Билеты"*|*2.1 Если купленных билетов нет, то система отображает кнопку "Купить билет"с ссылкой на раздел "Билеты"*|
|3. Пользователь может переходить на страницу спектакля по клику на название|3. Система позволяет переходить на страницу спектакля через его название|
|*Итог: Пользователь видит список купленных билетов*|[Прототип страницы покупок пользователя](https://www.figma.com/proto/fk5oo6Er6uU6fo89jsOW7r/Prototype-Tomsk-ver.2?node-id=244%3A122&scaling=min-zoom)|

### Мои отзывы
|    Пользовательский сценарий                    |    Функциональный сценарий    |
|-------------------------------------------------|-------------------------------|
|Предусловие: Пользователь в личном кабинете|Предусловие: Открыта страница личного кабинета|
|1. Пользователь переходит в раздел "Мои отзывы"|1. Система проверяет наличие отзывов к событиям у пользователя и открывает страницу "Мои отзывы"|
|*1.1 Если отзывов нет, то написан текст "Нет отзывов".*|*1.1 Если билетов нет, то система выводит текст "Нет отзывов".*|
|2. Пользователь видит остортированный по дате и времени список отзывов. В списке указаны: название спектакля, количество звезд, описание, дата и время, и кнопка "Подробнее". Нажав на кнопку "Подробнее", пользователь переходит на страницу спектакля, к своему отзыву.|2. Система автоматически сортирует отзывы по дате в обратном порядке. В списке указаны: название спектакля, количество звезд, описание, дата и время, и кнопка "Подробнее". При запросе "Подробнее" система открывает страницу спектакля, находит отзыв пользователя и отображает его.|
|*2.1 В описание отзыва пользователь видит только первые 3 строки. В конце третьей строки троеточие*|*2.1 Описание отзыва отображает только первые 3 строки. В конце третьей строки ставится троеточие*|
|3. Пользователь может переходить на страницу спектакля по клику на название|3. Система позволяет переходить на страницу спектакля через его название|
|*Итог: Пользователь видит список купленных билетов*|[Прототип страницы с отзывами пользователя](https://www.figma.com/proto/fk5oo6Er6uU6fo89jsOW7r/Prototype-Tomsk-ver.2?node-id=254%3A78&scaling=min-zoom)|

### Уведомления
|    Пользовательский сценарий                    |    Функциональный сценарий    |
|-------------------------------------------------|-------------------------------|
|Предусловие: Пользователь авторизован. Находится на любой странице.|Предусловие: Пройдена авторизация. Открыта любая страница|
|1. Пользователь видит 1 непрочитанное уведомление и нажимает кнопку уведомлений в меню навигации. Открывается модальное окно со списком всех уведомлений|1. Система создает уведомление и оптравляет его определенному пользователю|
|*1.1 Если уведомления нет, то в окне написан текст "Нет уведомлений"*|*1.1 Если уведомления нет, то система выводит в окне текст "Нет уведомлений"*|
|2. Пользователь видит количество уведомление над колокольчиком. Нажимает на него. Открывается окно с уведомлениями *текст уведомлений, где есть слово спектакль_1*|2. Система выводит количество непрочитанных уведомлений в правом верхнем углу колокольчика. Открывает модальное окно со списком уведомлений|
|*2.1 Если уведомлений больше четырех, то появляется скролл-бар*|*2.1 Если уведомлений больше четырех, система создает скролл-бар*|
|3. Пользователь может переходить на страницу спектакля кликнув на него|3. В уведомлении есть гиперссылка на страницу спектакля|
|4. Пользователь может закрыть окно уведомлений, нажав кнопку "Закрыть"|4. Система закрывает модальное окно, если нажать на кнопку "Закрыть" или кликнуть на любую область вне окна уведомлений|
|5. После закрытия окна, количество уведомлений над колокольчиком уменьшается, либо усчезает вообще|5. Система вычитает количество просмотренных уведомлений от количества непрочитанных. И отображает это количество над колокольчиком. Если оно равно нулю, то колокольчик отображается как в первоначальном положении|
|*Итог: Пользователь посмотрел новые уведомления. По необходимости, перешел на страницу театра*|[Прототип страницы с уведомлениями](https://www.figma.com/proto/fk5oo6Er6uU6fo89jsOW7r/Prototype-Tomsk-ver.2?node-id=161%3A0&scaling=min-zoom)|

## Блок "Театры"
### Страница всех театров
|    Пользовательский сценарий                    |    Функциональный сценарий    |
|-------------------------------------------------|-------------------------------|
|Предусловие: Пользователь на странице театров|Предусловие: Открыта страница театров|
|1. Пользователь видит список карточек театров. В карточке отображено: фото, название, рейтинг, количество звезд и общее количество отзывов, адрес, телефон для справок, описание театра и кнопка "Подробнее". Нажав на кнопку "Подробнее" или на название театра, пользователь переходит на страницу театра|1. Система отображает список карточек с содержанием: фото, название, рейтинг, количество звезд и общее количество отзывов, адрес, телефон для справок, описание театра и кнопка "Подробнее". Система позволяет переходить на страницу театра, нажав на название театра или на кнопку "Подробнее"|
|*1.1 В описании театра пользователь видит только первые 4 строчки. В конце четвертой строки ставится троеточие*|*1.1 В описании театра система отражает только 4 строки. В конце четвертой строки ставится троеточие*|
|*Итог: пользователь может выбрать театр и перейти на его страницу*|[Прототип страницы театров](https://www.figma.com/proto/fk5oo6Er6uU6fo89jsOW7r/Prototype-Tomsk-ver.2?node-id=165%3A55&scaling=min-zoom)|

### Страница театра, о театре
|    Пользовательский сценарий                    |    Функциональный сценарий    |
|-------------------------------------------------|-------------------------------|
|Предусловие: Пользователь на странице театра|Предусловие: Открыта страница театра|
|1. Пользователь видит название театра, ниже разделы: о театре, афиша, залы театра, авторы, контакты, жанры. Пользователь видит, что выбран раздел "О театре" и информацию о театре ниже.|1. При переходе на страницу театра система по умолчанию открывает раздел "О театре" Система отображает название театра и разделы: о театре, афиша, залы театра, авторы, контакты, жанры. Система позволяет переходить в эти разделы.|
|*Итог: пользователь может изучить информацию о театре и перейти в другие разделы театра*|[Прототип страницы театра и "О театре"](https://www.figma.com/proto/fk5oo6Er6uU6fo89jsOW7r/Prototype-Tomsk-ver.2?node-id=169%3A141&scaling=min-zoom)|

### Страница театра, Афиша
|    Пользовательский сценарий                    |    Функциональный сценарий    |
|-------------------------------------------------|-------------------------------|
|Предусловие: Пользователь на странице театра|Предусловие: Открыта страница театра|
|1. Пользователь нажимает на раздел "Афиша" и переходит в этот раздел|1. Система открывает страницу раздела театра "Афиша"|
|2. Пользователь видит заголовок "Сейчас идет" и список карточек событий. Карточки располагаются по 4 штуки в строке. Количество строк не ораничено|2. Система отображает заголовок "Сейчас идет" и список карточек событий, по 4 штуки в строке. Количество строк не ораничено|
|3. В карточке пользователь видит: фото, название, "Оценка зрителей:N,N (общее количество отзывов)", количество звезд и кнопка "Купить билеты". Пользователь может переходить на страницу покупки билета, нажав на кнопку "Купить билеты"|3. В карточке события система отображает: фото, название, "Оценка зрителей:N,N (общее количество отзывов)", количество звезд и кнопка "Купить билеты". Система позволяет переходить на страницу покупки билетов через кнопку "Купить билеты".|
|*Итог: пользователь может ознакомиться с событиями театра и перейти к покупке билета*|[Прототип страницы "Афиша"](https://www.figma.com/proto/fk5oo6Er6uU6fo89jsOW7r/Prototype-Tomsk-ver.2?node-id=460%3A423&scaling=min-zoom)|

### Страница театра, Залы театра
|    Пользовательский сценарий                    |    Функциональный сценарий    |
|-------------------------------------------------|-------------------------------|
|Предусловие: Пользователь на странице театра|Предусловие: Открыта страница театра|
|1. Пользователь нажимает на раздел "Залы театра" и переходит в этот раздел|1. Система открывает страницу раздела театра "Залы театра"|
|2. Пользователь видит название, фото и описание зала. Переходов на другие страницы нет.|2. Система отображает название, фото и описание зала. Переходов на другие страницы нет.|
|*Итог: пользователь может посмотреть и изучить информацию о залах театра*|[Прототип страницы "Залы театра"](https://www.figma.com/proto/fk5oo6Er6uU6fo89jsOW7r/Prototype-Tomsk-ver.2?node-id=460%3A490&scaling=min-zoom)|

### Страница театра, Авторы
|    Пользовательский сценарий                    |    Функциональный сценарий    |
|-------------------------------------------------|-------------------------------|
|Предусловие: Пользователь на странице театра|Предусловие: Открыта страница театра|
|1. Пользователь нажимает на раздел "Авторы" и переходит в этот раздел|1. Система открывает страницу раздела театра "Авторы"|
|2. Пользователь видит ФИО, фото и информацию об авторе. Количество авторов не ограничено. Пользователь может перейти на страницу автора, нажав на ФИО автора.|2. Система отображает ФИО, фото и информацию об авторе. Количество авторов не ограничено. Система позволяет перейти на страницу автора через ФИО автора.|
|*Итог: пользователь может изучить информацию об авторе*|[Прототип страницы "Авторы"](https://www.figma.com/proto/fk5oo6Er6uU6fo89jsOW7r/Prototype-Tomsk-ver.2?node-id=460%3A557&scaling=min-zoom)|

### Страница театра, Контакты
|    Пользовательский сценарий                    |    Функциональный сценарий    |
|-------------------------------------------------|-------------------------------|
|Предусловие: Пользователь на странице театра|Предусловие: Открыта страница театра|
|1. Пользователь нажимает на раздел "Контакты" и переходит в этот раздел|1. Система открывает страницу раздела театра "Контакты"|
|2. Пользователь видит заголовок "Контакты", контактную информацию о театре и фото карты. Переходов на другие страницы нет.|2. Система отображает заголовок "Контакты", контактную информацию о театре и фото карты. Переходов на другие страницы нет.|
|*Итог: пользователь может узнать контакты и расположение театра*|[Прототип страницы "Контакты"](https://www.figma.com/proto/fk5oo6Er6uU6fo89jsOW7r/Prototype-Tomsk-ver.2?node-id=460%3A691&scaling=min-zoom)|

### Страница театра, Жанры
|    Пользовательский сценарий                    |    Функциональный сценарий    |
|-------------------------------------------------|-------------------------------|
|Предусловие: Пользователь на странице театра|Предусловие: Открыта страница театра|
|1. Пользователь нажимает на раздел "Жанры" и переходит в этот раздел|1. Система открывает страницу раздела театра "Жанры"|
|2. Пользователь видит перечень жанров и информацию о них. Переходов на другие страницы нет.|2. Система отображает перечень жанров и информацию о них. Переходов на другие страницы нет.|
|*Итог: пользователь может посмотреть информацию о жанрах театра*|[Прототип страницы "Жанры"](https://www.figma.com/proto/fk5oo6Er6uU6fo89jsOW7r/Prototype-Tomsk-ver.2?node-id=460%3A758&scaling=min-zoom)|



