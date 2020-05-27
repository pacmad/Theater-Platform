# Сценарии (версия 1.2.3)
Изменения:
#### Блок "Регистрация и авторизация"
+ Добалены ошибки к полю email
+ Разделены ошибки для поля пароль и подтверждение пароля
+ Модальное окно и кнопки в нем изменены
+ Добавлены ошибки при входе в аккаунт
+ Изменено содержание блок-окна


## Блок "Пользователь" 
### Регистрация пользователя в системе

|    Пользовательский сценарий                    |    Функциональный сценарий    |
|-------------------------------------------------|-------------------------------|
|Предусловие: Пользователь на главной странице|Предусловие: Открыта главная страница |  
|1. Пользователь нажимает на кнопку личного кабинета в правом верхнем углу. и попадает на страницу авторизации, где выбивает "Зарегистрироваться"|1. Система открывает страницу авторизации, затем страницу регистрации|
| *1.1 Если пользователь уже зарегистрирован, то он выбирает опцию Авторизации и переходит к сценарию “Авторизация пользователя”*| *1.1 Если пользователь уже зарегистрирован, то он выбирает опцию Авторизации и переходит к сценарию “Авторизация пользователя”*| 
|2. Пользователь заполняет поля: фамилия, имя, email, пароль, подтверждение пароля, нажимает чек-бокс для согласия с правилами сайта и обработки данных, нажимает кнопку “Создать аккаунт”| 2. Система позволяет пользователю создать аккаунт. Система получает данные: фамилия, имя, email, пароль, подтверждение пароля.|
|*2.1 Если поле "Имя" не соответствует требованиям, то под полем пользователь видит ошибки: "Имя должно состоять минимум из 2 букв", "Имя должно состоять максимум из 127 букв","Имя может содержать только символы кириллицы", "Данное поле необходимо заполнить"*|*2.1 Если поле "Имя" не соответствует требованиям, то система выдает ошибки: "Имя должно состоять минимум из 2 букв", "Имя должно состоять максимум из 127 букв", "Имя может содержать только символы кириллицы", "Данное поле необходимо заполнить"*|
|*2.2 Если поле "Фамилия" не соответствует требованиям, то под полем пользователь видит ошибки: "Фамилия должна состоять минимум из 2 букв", "Фамилия должна состоять максимум из 127 букв","Фамилия может содержать только символы кириллицы", "Данное поле необходимо заполнить"*|*2.1 Если поле "Фамилия" не соответствует требованиям, то система выдает ошибки: "Фамилия должна состоять минимум из 2 букв", "Фамилия должна состоять максимум из 127 букв", "Фамилия может содержать только символы кириллицы", "Данное поле необходимо заполнить"*|
|*2.3 Если поле "Email" не соответствует требованиям, то под полем пользователь видит ошибки: "Неверный формат email адреса", "Пользователь с таким email уже зарегистрирован", "Максимальная длина email - 95 символов", "Длина логина (символы до @) должна быть не менее 6 символов", "Длина логина (символы до @) должна быть не более 30 символов", "Длина домена (символы после @) должна быть не более 64 символов", "Данное поле необходимо заполнить".*|*2.3 Если поле "Email" не соответствует требованиям, то система выдает ошибки: "Неверный формат email адреса", "Пользователь с таким email уже зарегистрирован", "Максимальная длина email - 95 символов", "Длина логина (символы до @) должна быть не менее 6 символов", "Длина логина (символы до @) должна быть не более 30 символов", "Длина домена (символы после @) должна быть не более 64 символов", "Данное поле необходимо заполнить".*|
|*2.4 Если поле "Пароль" не соответствуют требованиям, то под полем пользователь видит ошибки: "Пароль должен состоять минимум из 8 символов", "Длина пароля не должна превышать 127 символов", "Пароль может содержать только буквы латинского алфавита, цифры и специальные символы: !@#$%^&* ", "Пароль должен содержать минимум одну букву в верхнем регистре", "Пароль должен содержать минимум одну букву в нижнем регистре", "Пароль должен содержать минимум одну цифру", "Данное поле необходимо заполнить".* |*2.4 Если поле "Пароль" не соответствуют требованиям, то система под полем выдает ошибки: "Пароль должен состоять минимум из 8 символов", "Длина пароля не должна превышать 127 символов", "Пароль может содержать только буквы латинского алфавита, цифры и специальные символы: !@#$%^&* ", "Пароль должен содержать минимум одну букву в верхнем регистре", "Пароль должен содержать минимум одну букву в нижнем регистре", "Пароль должен содержать минимум одну цифру", "Данное поле необходимо заполнить".*|
|*2.5 Если поле "Повторите пароль" не заполнено, то под полем пользователь видит ошибку: "Данное поле необходимо заполнить".*|*2.5 Если поле "Повторите пароль" не заполнено, то под полем система выводит ошибку: "Данное поле необходимо заполнить".*|
|*2.6 Если поле "Пароль" и "Повторите пароль" не совпадают, то под полем "Повторите пароль" пользователь видит ошибки: "Введенные пароли не совпадают".*|*2.6 Если поле "Пароль" и "Повторите пароль" не совпадают, то под полем "Повторите пароль" система выводит ошибки: "Введенные пароли не совпадают".*|
|*2.7 Если пользователь не кликнул на чек-бокс для согласия с правилами сайта и обработки данных, то при нажатии на кнопку "Создать аккаунт" поле с чек-боксом и текстом обводится красной рамкой”*| *2.7 Если чек-бокс не был активирован, то регистрация в системе невозможна. Запрос на создание аккаунта отклоняется и чек-бокс с полем обведен в красную рамку”*|
|3. Пользователь видит модальное окно с текстом “Регистрация прошла успешно! Вы были перенаправлены на страницу авторизации” и кнопку "Ок". После нажатия кнопки "Ок" пользователь переходит на страницу авторизации.|4. Если данные введены верно, система отправляет пакет данных для сохранения в БД и открывает модальное окно с текстом “Регистрация прошла успешно! Вы были перенаправлены на страницу авторизации” и кнопкой "Ок". После нажатия на кнопку "Ок" система закрывает модальное окно и открывает страницу авторизации.|
|**Итог:** Пользователь зарегистрирован в системе|[Прототип страницы регистрации](https://www.figma.com/proto/n63ePP2OoWwd6LMuziovJ2/Prototype-Tomsk-ver.3?node-id=343%3A430&scaling=scale-down-width)|

### Авторизация пользователя в системе

|    Пользовательский сценарий     |    Функциональный сценарий    |
|----------------------------------|-------------------------------|
|Предусловие: Пользователь на главной странице|Открыта главная страница|  
|1. Пользователь нажимает на кнопку личного кабинета в правом верхнем углу и попадает на страницу авторизации|1. Система открывает страницу авторизации|
|*2.1 Если пользователь еще не зарегистрирован, то переходит к сценарию “Регистрация пользователя в систему”*| *Система открывает страницу авторизации, по запросу* |
|2. Пользователь вводит email и пароль, затем нажимает на кнопку "Войти"|2. Система получает e-mail и пароль и делает проверку данных|
|*2.1 Если поле "Email" не соответствует требованиям, то под полем пользователь видит ошибки: "Неверный формат email адреса", "Данное поле необходимо заполнить".*|*2.1 Если поле "Email" не соответствует требованиям, то система выдает ошибки: "Неверный формат email адреса", "Данное поле необходимо заполнить".*|
|*2.2 Если поле "Пароль" не заполнено, то под полем пользователь видит ошибку: "Данное поле необходимо заполнить".*|*2.2 Если поле "Пароль" пустое, то система выдает ошибку: "Данное поле необходимо заполнить".*|
|*2.3 Если поле "Email" или "Пароль" введены неверно, то под полем пользователь видит ошибку: "Не удается войти. Неверный логин или пароль.".*|*2.3  Если поле "Email" или "Пароль" введены неверно, то система выдает ошибку: "Не удается войти. Неверный логин или пароль.".*|
|3. Пользователь успешно авторизован и попадает на главную страницу.| 4. Система входит в аккаунт пользователя. Открывает главную страницу.|
|**Итог:** Пользователь авторизовался в системе|[Прототип страницы авторизации](https://www.figma.com/proto/n63ePP2OoWwd6LMuziovJ2/Prototype-Tomsk-ver.3?node-id=343%3A447&scaling=scale-down-width)|

### Выход из аккаунта

|    Пользовательский сценарий     |    Функциональный сценарий    |
|----------------------------------|-------------------------------|
|Предусловие: Пользователь авторизован на сайте|Предусловие: Пользователь авторизован в системе| 
|1. Пользователь наводит курсор на кнопку личного кабинета. Появляется блок-окно для быстрого перехода в: профиль, мои покупки, избранное, мои отзывы, выход. |1. При попадании курсора в область кнопки личного кабинета, система открывает блок-окно для быстрого перехода в: профиль, мои покупки, избранное, мои отзывы, выход.|
|2. Пользователь нажимает кнопку "Выйти" и видит модальное окно с текстом "Хотите выйти?" и кнопками "Да" и "Нет"|2. Система открывает модальное окно для подтверждения выхода из системы с текстом "Хотите выйти?" и кнопками "Да" и "Нет"|
|3. Если пользователь выбирает "Да", то модальное окно закрывается и пользователь переходит на главную страницу. При наведении курсора на кнопку личного кабинета блок-окно не будет появляться. |3. Система выходит из личного кабинета пользователя, закрывает модальное окно и переходит на главную страницу. При наведении курсора на кнопку личного кабинета система не открывает блок-окно.|
|4. Если пользователь выбирает "Нет", то модальное окно закрывается и пользователь остается на прежней странице. При наведении курсора на кнопку личного кабинета блок-окно будет появляться.|3. Система не выходит из личного кабинета, закрывает модальное окно. При наведении курсора на кнопку личного кабинета система открывает блок-окно.|
|*Итог: поьзователь вышел из аккаунта*|[Прототип страницы выхода из аккаунта. Надо навести на кнопку личного кабинета](https://www.figma.com/proto/n63ePP2OoWwd6LMuziovJ2/Prototype-Tomsk-ver.3?node-id=244%3A122&scaling=scale-down-width)|

## Блок "Главная страница"

|    Пользовательский сценарий                    |    Функциональный сценарий    |
|-------------------------------------------------|-------------------------------|
|Предусловие: Пользователь на главной странице|Предусловие: Открыта главная страница|
|1. Пользователь может переходить в разделы, кликая по ним в меню навигации. Нажимая на логотип платформы, открывается главная страница. Нажимая на кнопку поиска, страница опускается вниз к разделу поиска мероприятия.|1. Система позволяет переходить на страницы разделов через меню навигации. Через логитип платформы идет переход на главную страницу. При нажатии на поиск система опускает страницу к полю поиска.|
|*1.1 Нажимая на разделы: логотип, расписание, театры, личный кабинет, пользователь переходит на другую страницу.*|*1.1 Нажимая на разделы: логотип, расписание, театры, личный кабинет, система открывает другую страницу.*|
|*1.2 Если пользователь авторизован, то при наведении курсора на кнопку личного кабинета появляется модальное окно с информацией о пользователе: фамилия, имя, email и кнопка "Выйти"*|*1.2 Если пользователь авторизован в системе, то при попадании курсора в область кнопки личного кабинета, система открывает модальное окно с информацией пользователя: фамилия, имя, email и кнопка "Выйти"*|
|*1.3 Если пользователь не авторизован, то при наведении курсора на кнопку личного кабинета модальное окно не появляется.*|*1.3 Если пользователь не авторизован в системе, то при попадании курсора в область кнопки личного кабинета модальное окно не появляется*|
|2. Пользователь под меню навигации видит слайдер, состоящий из n-го карточек состоящих из фотографий/видео о событии, названия и описания события и кнопки "Купить билет" (нажимая на нее, пользователь окажется на странице спектакля с подробным описанием). Пользователь видит карточку одного спектакля 5-10 секунд, затем появляется следующая. После последней карточки показ начинается заново. Также может сам переключать, нажав на стрелочки <>, либо на крулые кнопочки внизу.|2. При открытии главной страницы система запускает слайдер состоящий из фото/видео события, его названия, описания и кнопки "Купить билет" с гиперссылкой на страницу спектакля. Система автоматически переключает карточки через 5-10 секунд. По запросу пользователя, система может переключать карточки до истечения времени. После окончания показа всех карточек, система начинает показ заново.|
|*2.1 В описании события пользователь видит первые 7 строк, в конце последней строки троеточие.*|*2.1 Система отображает в описании события первые 7 строк, в конце последней строки ставит троеточие.*|
|3. Ниже меню навигации и слайдера, пользователь видит блок "Театры", где представлены 4 карточки театра, состоящие из названия и фото. После нажатия на "Театры", пользователь переходит в раздел "Театры" и видит полный список театров. Нажав на название театра, пользователь попадает на страницу театра.|3. Система отображает блок "Театры", где есть 4 карточки из названия и фото театра. Система позволяет переходить в раздел "Театры" (с их полным списком) через гиперссылку в названии "Театры". Также позволяет переходить на страницу театра через гиперссылку в названии театра.|
|4. Ниже раздела "Театры" есть функция поиска события с фильтрацией. Пользователь может вводить текст в поле поиска, выбирать театр через кнопку "Выберите театр", выбирать дату через календарик справа. После выбора фильтров пользователь нажимает кнопку "Найти". Открывается страница раздела "Расписание" с результатами поиска по данным параметрам.|4. Система отображает панель поиска с фильтрацией: поле для ввода, кнопку с выбором театра, кнопку календаря для выбора даты и кнопку "Найти". После запроса на поиск и считывания данных, система открывает страницу раздела "Расписание" и отображает результаты по параметрам поиска.|
|*4.1 При нажании на кнопку "Выберите театр" открывается модальное окно со списком тетров (первая кнопка в модальном окне "Все"). Если пользователь не выбирает театр, то в результатах поиска видит результаты по всем театрам*|*4.1 При нажании на кнопку "Выберите театр" система открывает модальное окно со списком тетров (первая кнопка в модальном окне "Все"). Если театр не выбран, то по умолчанию поиск проходит по всем театрам*|
|*4.2 При нажании на календарь открывается модальное окно с календарем текущего месяца. Если пользователь не выбирает дату, то в результатах видит результаты по всем датам*|*4.2 При нажании на календарь система открывает модальное окно с календарем на текущий месяц. Если дата не выбрана, то по умолчанию поиск проходит по всем датам*|
|5. В конце страницы пользователь видит слева меню навигации, через которое можно переходить в другие разделы. Справа располагается контактная информация о владельцах платформы|5. В конце страницы слева система отображает меню навигации, где есть гиперссылки для перехода в другие разделы. Справа располагается контактная информация о владельцах платформы|
|*Итог: Пользователь видит премьеры месяца в слайдере, может использовать функцию поиска и переходить на другие страницы*|[Прототип главной страницы](https://www.figma.com/proto/n63ePP2OoWwd6LMuziovJ2/Prototype-Tomsk-ver.3?node-id=161%3A0&scaling=scale-down-width)|

## Блок "Личный кабинет"

### Просмотр избранного

|    Пользовательский сценарий                    |    Функциональный сценарий    |
|-------------------------------------------------|-------------------------------|
|Предусловие: Пользователь в личном кабинете|Предусловие: Открыта страница личного кабинета|
|1. Пользователь переходит в раздел "Избранное"|1. Система проверяет наличие избранных спектаклей у пользователя и открывает страницу "Избранное"|
|2. Пользователь видит карточки спектаклей с индикатором "избранное" в правом верхнем углу|2. Система отображает спектакли, привязанные к id пользователя с индикатором "Избранное"|
|*2.1 Если избранных спектаклей нет, то есть кнопка "Добавить в избранное". При нажатии прользователь переходит в раздел "Расписание"*|*2.1 Если система не находит избранные спектакли, то открывает страницу с кнопкой, которая позволяет переходит на страницу "Расписание"*|
|3. Пользователь может удалять спектакли из избранного. Нажав на индикатор "избранное", появляется модальное окно с текстом "Вы действительно хотите удалить "Спектакль_1" из избранного?" и кнопками "Да", "Нет".|3. Если пользователь хочет изменить индикатор на "не избранное", то система открывает модальное окно с текстом "Вы действительно хотите удалить "Спектакль_1" из избранного?" и кнопками "Да", "Нет".|
|*3.1 Если пользователь подтверждает удаление, то индикатор меняет цвет и карточка исчезает из раздела "Избранное".*|*3.1 Если удаление подтверждено, то система меняет цвет индикатора, убирает карточку из раздела "Избранное" и удаляет данные из БД*|
|*3.2 Если пользователь не подтверждает удаление, то индикатор не меняет цвет и карточка остается в разделе "Избранное"*|*3.2 Если удаление не подтверждено, то система не меняет цвет индикатора, карточку остается в разделе "Избранное"*|
|4. Пользователь через карточку спектакля может переходить на страницу описания спектакля.|4. Система отображает карточки спектаклей с гиперссылкой на страницу описания спектакля.|
|*Итог: пользователь может добавлять, удалять карточки спектаклей из раздела "Избранное". Может быстро переходить на страницу описания спектакля.*|[Прототип страницы избранного](https://www.figma.com/proto/n63ePP2OoWwd6LMuziovJ2/Prototype-Tomsk-ver.3?node-id=247%3A80&scaling=scale-down-width)|

### Мои покупки

|    Пользовательский сценарий                    |    Функциональный сценарий    |
|-------------------------------------------------|-------------------------------|
|Предусловие: Пользователь в личном кабинете|Предусловие: Открыта страница личного кабинета|
|1. Пользователь переходит в раздел "Мои покупки"|1. Система проверяет наличие купленных билетов у пользователя и открывает страницу "Мои покупки"|
|*1.1 Если билетов нет, то в окне написан текст "Нет купленных билетов" и кнопка "Купить билет". Нажав на кнопку, пользователь перейдет в раздел "Расписание"*|*1.1 Если билетов нет, то система выводит в окне текст "Нет купленных билетов" и кнопку "Купить билеты" с гиперссылкой на раздел "Расписание"*|
|2. Пользователь видит остортированный по дате и времени оплаты список билетов. В списке указаны: название спектакля, театр, дата и время, сумма оплаты и код для получения билета в кассе.|2. Система автоматически сортирует билеты по дате в обратном порядке. В списке указаны: название спектакля, театр, дата и время, сумма оплаты и код для получения билета в кассе.|
|3. Пользователь может переходить на страницу спектакля по клику на название|3. Система позволяет переходить на страницу спектакля через его название|
|*Итог: Пользователь видит список купленных билетов*|[Прототип страницы покупок пользователя](https://www.figma.com/proto/n63ePP2OoWwd6LMuziovJ2/Prototype-Tomsk-ver.3?node-id=244%3A122&scaling=scale-down-width)|

### Мои отзывы

|    Пользовательский сценарий                    |    Функциональный сценарий    |
|-------------------------------------------------|-------------------------------|
|Предусловие: Пользователь в личном кабинете|Предусловие: Открыта страница личного кабинета|
|1. Пользователь переходит в раздел "Мои отзывы"|1. Система проверяет наличие отзывов к событиям у пользователя и открывает страницу "Мои отзывы"|
|*1.1 Если отзывов нет, то написан текст "Нет отзывов".*|*1.1 Если билетов нет, то система выводит текст "Нет отзывов".*|
|2. Пользователь видит остортированный по дате и времени список отзывов. В отзыве указано: название спектакля, театр, количество звезд,  дата, текст отзыва. |2. Система автоматически сортирует отзывы по дате в обратном порядке. В отзыве указано: название спектакля, театр, количество звезд,  дата, текст отзыва. |
|*2.1 В описание отзыва пользователь видит весь отзыв.*|*2.1 Система отображает весь текст отзыва.*|
|3. Пользователь может переходить на страницу спектакля по клику на название.|3. Система позволяет переходить на страницу спектакля через его название.|
|*Итог: Пользователь видит список купленных билетов*|[Прототип страницы с отзывами пользователя](https://www.figma.com/proto/n63ePP2OoWwd6LMuziovJ2/Prototype-Tomsk-ver.3?node-id=254%3A78&scaling=scale-down-width)|

## Блок "Театры"

### Страница всех театров

|    Пользовательский сценарий                    |    Функциональный сценарий    |
|-------------------------------------------------|-------------------------------|
|Предусловие: Пользователь на странице театров|Предусловие: Открыта страница театров|
|1. Пользователь видит список карточек театров. В карточке отображено: фото, название, рейтинг, количество звезд и общее количество отзывов, адрес, телефон для справок, описание театра и кнопка "Подробнее". Нажав на кнопку "Подробнее" или на название театра, пользователь переходит на страницу театра|1. Система отображает список карточек с содержанием: фото, название, рейтинг, количество звезд и общее количество отзывов, адрес, телефон для справок, описание театра и кнопка "Подробнее". Система позволяет переходить на страницу театра, нажав на название театра или на кнопку "Подробнее"|
|*1.1 В описании театра пользователь видит только первые 4 строчки. В конце четвертой строки ставится троеточие*|*1.1 В описании театра система отражает только 4 строки. В конце четвертой строки ставится троеточие*|
|*Итог: пользователь может выбрать театр и перейти на его страницу*|[Прототип страницы театров](https://www.figma.com/proto/n63ePP2OoWwd6LMuziovJ2/Prototype-Tomsk-ver.3?node-id=165%3A55&scaling=scale-down-width)|

### Страница театра, о театре

|    Пользовательский сценарий                    |    Функциональный сценарий    |
|-------------------------------------------------|-------------------------------|
|Предусловие: Пользователь на странице театра|Предусловие: Открыта страница театра|
|1. Пользователь видит название театра, ниже разделы: о театре, афиша, залы театра, контакты. Пользователь видит, что выбран раздел "О театре" и информацию о театре ниже.|1. При переходе на страницу театра система по умолчанию открывает раздел "О театре" Система отображает название театра и разделы: о театре, афиша, залы театра, контакты. Система позволяет переходить в эти разделы.|
|*Итог: пользователь может изучить информацию о театре и перейти в другие разделы театра*|[Прототип страницы театра и "О театре"](https://www.figma.com/proto/n63ePP2OoWwd6LMuziovJ2/Prototype-Tomsk-ver.3?node-id=169%3A141&scaling=scale-down-width)|

### Страница театра, Афиша

|    Пользовательский сценарий                    |    Функциональный сценарий    |
|-------------------------------------------------|-------------------------------|
|Предусловие: Пользователь на странице театра|Предусловие: Открыта страница театра|
|1. Пользователь нажимает на раздел "Афиша" и переходит в этот раздел|1. Система открывает страницу раздела театра "Афиша"|
|2. Пользователь видит заголовок "Сейчас идет" и список карточек событий. Карточки располагаются по 4 штуки в строке. Количество строк не ораничено|2. Система отображает заголовок "Сейчас идет" и список карточек событий, по 4 штуки в строке. Количество строк не ораничено|
|3. В карточке пользователь видит: фото, название, "Оценка зрителей:N,N (общее количество отзывов)", количество звезд и кнопка "Купить билеты". Пользователь может переходить на страницу покупки билета, нажав на кнопку "Купить билеты"|3. В карточке события система отображает: фото, название, "Оценка зрителей:N,N (общее количество отзывов)", количество звезд и кнопка "Купить билеты". Система позволяет переходить на страницу покупки билетов через кнопку "Купить билеты".|
|*Итог: пользователь может ознакомиться с событиями театра и перейти к покупке билета*|[Прототип страницы "Афиша"](https://www.figma.com/proto/n63ePP2OoWwd6LMuziovJ2/Prototype-Tomsk-ver.3?node-id=460%3A423&scaling=scale-down-width)|

### Страница театра, Залы театра

|    Пользовательский сценарий                    |    Функциональный сценарий    |
|-------------------------------------------------|-------------------------------|
|Предусловие: Пользователь на странице театра|Предусловие: Открыта страница театра|
|1. Пользователь нажимает на раздел "Залы театра" и переходит в этот раздел|1. Система открывает страницу раздела театра "Залы театра"|
|2. Пользователь видит название, фото и описание зала. Переходов на другие страницы нет.|2. Система отображает название, фото и описание зала. Переходов на другие страницы нет.|
|*Итог: пользователь может посмотреть и изучить информацию о залах театра*|[Прототип страницы "Залы театра"](https://www.figma.com/proto/n63ePP2OoWwd6LMuziovJ2/Prototype-Tomsk-ver.3?node-id=460%3A490&scaling=scale-down-width)|

### Страница театра, Контакты

|    Пользовательский сценарий                    |    Функциональный сценарий    |
|-------------------------------------------------|-------------------------------|
|Предусловие: Пользователь на странице театра|Предусловие: Открыта страница театра|
|1. Пользователь нажимает на раздел "Контакты" и переходит в этот раздел|1. Система открывает страницу раздела театра "Контакты"|
|2. Пользователь видит заголовок "Контакты", контактную информацию о театре и фото карты. Переходов на другие страницы нет.|2. Система отображает заголовок "Контакты", контактную информацию о театре и фото карты. Переходов на другие страницы нет.|
|*Итог: пользователь может узнать контакты и расположение театра*|[Прототип страницы "Контакты"](https://www.figma.com/proto/n63ePP2OoWwd6LMuziovJ2/Prototype-Tomsk-ver.3?node-id=460%3A691&scaling=scale-down-width)|


## Блок "Расписание"
### Страница блока "Расписание"

|    Пользовательский сценарий                    |    Функциональный сценарий    |
|-------------------------------------------------|-------------------------------|
|Предусловие: Пользователь на странице расписания|Предусловие: Открыта страница расписания|
|1. Пользователь видит список карточек театров. В карточке отображено: фото, название, рейтинг, количество звезд и общее количество отзывов, адрес, телефон для справок, описание театра и кнопка "Подробнее". Нажав на кнопку "Подробнее" или на название театра, пользователь переходит на страницу театра|1. Система отображает список карточек с содержанием: фото, название, рейтинг, количество звезд и общее количество отзывов, адрес, телефон для справок, описание театра и кнопка "Подробнее". Система позволяет переходить на страницу театра, нажав на название театра или на кнопку "Подробнее"|
|*1.1 В описании театра пользователь видит только первые 4 строчки. В конце четвертой строки ставится троеточие*|*1.1 В описании театра система отражает только 4 строки. В конце четвертой строки ставится троеточие*|
|*Итог: пользователь может выбрать театр и перейти на его страницу*|[Прототип страницы театров](https://www.figma.com/proto/n63ePP2OoWwd6LMuziovJ2/Prototype-Tomsk-ver.3?node-id=165%3A55&scaling=scale-down-width)|

### Поиск с фильтрацией

|    Пользовательский сценарий                    |    Функциональный сценарий    |
|-------------------------------------------------|-------------------------------|
|Предусловие: Пользователь на странице расписания|Предусловие: Открыта страница расписания|
|1. Пользователь видит поле для ввода названия и кнопку поиска, кнопка для выбора театра, кнопку календаря для выбора даты.|1. Система позволяет вводить в поле поиска данные, выбирать театр и дату.|
|2. Пользователь вводит данные, выбирает театр, дату и нажимает кнопку поиска.|2. Система считывает введенные данные и делает поиск в БД.|
|*2.1 При нажании на кнопку "Выберите театр" открывается модальное окно со списком тетров (первая кнопка в модальном окне "Все"). Если пользователь не выбирает театр, то в результатах поиска видит результаты по всем театрам*|*2.1 При нажании на кнопку "Выберите театр" система открывает модальное окно со списком тетров (первая кнопка в модальном окне "Все"). Если театр не выбран, то по умолчанию поиск проходит по всем театрам*|
|*2.2 При нажании на календарь открывается модальное окно с календарем текущего месяца. Если пользователь не выбирает дату, то в результатах видит результаты по всем датам*|*2.2 При нажании на календарь система открывает модальное окно с календарем на текущий месяц. Если дата не выбрана, то по умолчанию поиск проходит по всем датам*|
|3. Пользователь видит ниже панели поиска карточки спектаклей, найденные по запросу.|3. Система отображает найденные спектакли ниже панели поиска|
|*3.1 Если поиск не дал результатов, то пользователь видит текст "Поиск не дал результатов".*|*3.1 Если поиск не дал результатов, то система отображает текст "Поиск не дал результатов".*|
|*Итог: пользователь может выбрать театр и перейти на его страницу*|[Прототип страницы театров]()|

### Покупка билета

|    Пользовательский сценарий                    |    Функциональный сценарий    |
|-------------------------------------------------|-------------------------------|
|Предусловие: Пользователь на странице расписания|Предусловие: Открыта страница расписания|
|1. Пользователь видит список карточек спектаклей. В карточке отображено: фото, название, рейтинг, количество звезд и общее количество отзывов, адрес, телефон для справок, описание театра и кнопка "Купить билет". Нажав на кнопку "Купить билет" пользователь переходит на страницу для выбора мест и отплаты билетов |1. Система отображает список карточек с содержанием: фото, название, рейтинг, количество звезд и общее количество отзывов, адрес, телефон для справок, описание театра и кнопка "Подробнее". Система позволяет переходить на страницу театра, нажав на название театра или на кнопку "Подробнее"|
|*1.1 В описании театра пользователь видит только первые 4 строчки. В конце четвертой строки ставится троеточие*|*1.1 В описании театра система отражает только 4 строки. В конце четвертой строки ставится троеточие*|
|*Итог: пользователь может выбрать театр и перейти на его страницу*|[Прототип страницы театров](https://www.figma.com/proto/n63ePP2OoWwd6LMuziovJ2/Prototype-Tomsk-ver.3?node-id=165%3A55&scaling=scale-down-width)|


### Покупка незарегистрированным пользователем
### Страница спектакля
### Страница актера
### Отзыв