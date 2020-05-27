# Ограничения на хранимые данные
Изменения:
+ Удален столбец "Ошибки"
+ Откорректированы ограницения на email
+ Убрано разделение по блокам

### Блок "Регистрация и авторизация"

|Название|Обязательно|Ограничения|Формат|
|--------|-----------|-----------|------|
|Фамилия |да|может содержать только буквы кириллицы (А-я) обоих регистров. min 2 max 127 символов|строковый|
|Имя|да|может содержать только буквы кириллицы (А-я) обоих регистров. min 2 max 127 символов|строковый|
|email|да|Может содержать (A-z), арабских цифр (0-9) и символ @. Максимальная длина email - 95 символов. Длина логина минимум - 6 символов, максимум - 30. Должен содержать специальный символ "@", который отделяет имя пользователя почтовой системы от доменного имени; Не должен содержать пробелов. После символа "@" должна быть как минимум одна "."; После последней точки должно быть не менее 2-х и не более 4-х символов, причем наличие цифр не допускается; Между последней точкой и символом "@" должно быть не менее одного символов. Справа от "@" должно быть не менее 3-х и не более 64 символов.|строковый|
|Пароль|да|Может содержать (A-z), арабских цифр (0-9) набор допустимых специальных символов: !@#$%^&* пароль должен содержать как минимум 1 букву в lowercase, 1 букву в uppercase и 1 цифру, наличие специальных символов не обязательно min 8 символов, максимум 127|строковый|
|Подтверждение пароля|да|Может содержать (A-z), арабских цифр (0-9) набор допустимых специальных символов: !@#$%^&* пароль должен содержать как минимум 1 букву в lowercase, 1 букву в uppercase и 1 цифру, наличие специальных символов не обязательно min 8 символов, максимум 127|строковый|

