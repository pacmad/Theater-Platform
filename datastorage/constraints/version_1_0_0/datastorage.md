# Ограничения на хранимые данные

### Регистрация

|Название|Обязательно|Ограничения|Формат|Ошибка|
|--------|-----------|-----------|------|------|
|Фамилия |да|может содержать только буквы кириллицы (А-я) обоих регистров. min 2 max 127 символов|строковый|если условия не соблюдаются, то ошибка “Введите фамилию буквами”|
|Имя|да|может содержать только буквы кириллицы (А-я) обоих регистров. min 2 max 127 символов|строковый|если условия не соблюдаются, то ошибка “Введите имя буквами”|
|Отчество|нет|может содержать только буквы кириллицы (А-я) обоих регистров. min 2 max 127 символов|строковый|если условия не соблюдаются, то ошибка “Введите отчество буквами”|
|Дата рождения|да|может содержать только цифры (0-9). max 8 символов|dd.mm.yyyy|если условия не соблюдаются, то __.__.____ подсвечивается красным|
|Номер телефона|да|может содержать только цифры (0-9). max 12 символов|+7-xxx-xxx-xx-xx|если условия не соблюдаются, то ошибка “Введите номер телефона”|
|e-mail|да|может содержать (A-z), арабских цифр (0-9) и символ @.Должен содержать специальный символ "@", который отделяет имя пользователя почтовой системы от доменного имени;Не должен содержать пробелов. После символа "@" должна быть как минимум одна "."; После последней точки должно быть не менее 2-х и не более 4-х символов, причем наличие цифр не допускается; Между последней точкой и символом "@" должно быть не менее 2-х символов. Слева от "@" должно быть не менее четырех символов|строковый|Если условия не соблюдаются, то ошибка “e-mail адрес введен некорректно. используйте (A-z),@,.”|
|Пароль|да|может содержать (A-z), арабских цифр (0-9) набор допустимых специальных символов: !@#$%^&* пароль должен содержать как минимум 1 букву в lowercase, 1 букву в uppercase и 1 цифру, наличие специальных символов не обязательно min 8 символов, максимум 127|строковый|Если пароль не содержит min 1 букву lowercase, uppercase и 1 цифру, то ошибка “введите пароль при помощи заглавных, строчных букв и цифр”. Если пароль меньше 8 символов, то ошибка “Слишком короткий пароль”. Если пароль более 127 символов, то ошибка “Слишком длинный пароль. max - 127 символов”|
|Подтверждение пароля|да|может содержать (A-z), арабских цифр (0-9) набор допустимых специальных символов: !@#$%^&* пароль должен содержать как минимум 1 букву в lowercase, 1 букву в uppercase и 1 цифру, наличие специальных символов не обязательно min 8 символов, максимум 127|строковый|Если пароль не содержит min 1 букву lowercase, uppercase и 1 цифру, то ошибка “введите пароль при помощи заглавных, строчных букв и цифр”. Если пароль меньше 8 символов, то ошибка “Слишком короткий пароль”. Если пароль более 127 символов, то ошибка “Слишком длинный пароль. max - 127 символов”. Если введенный пароль не совпадает с паролем в поле “Пароль”, то ошибка “Пароли не совпадают”|

### Авторизация

|Название|Обязательно|Ограничения|Формат|Ошибка|
|--------|-----------|-----------|------|------|
|e-mail|да|может содержать (A-z), арабских цифр (0-9) и символ @.Должен содержать специальный символ "@", который отделяет имя пользователя почтовой системы от доменного имени;Не должен содержать пробелов. После символа "@" должна быть как минимум одна "."; После последней точки должно быть не менее 2-х и не более 4-х символов, причем наличие цифр не допускается; Между последней точкой и символом "@" должно быть не менее 2-х символов. Слева от "@" должно быть не менее четырех символов |строковый|Если условия не соблюдаются, то ошибка “e-mail адрес введен некорректно. используйте (A-z),@,.”|
|Пароль|да|может содержать (A-z), арабских цифр (0-9) набор допустимых специальных символов: !@#$%^&* пароль должен содержать как минимум 1 букву в lowercase, 1 букву в uppercase и 1 цифру, наличие специальных символов не обязательно min 8 символов, максимум 127|строковый|Если пароль не содержит min 1 букву lowercase, uppercase и 1 цифру, то ошибка “введите пароль при помощи заглавных, строчных букв и цифр”. Если пароль меньше 8 символов, то ошибка “Слишком короткий пароль”. Если пароль более 127 символов, то ошибка “Слишком длинный пароль. max - 127 символов”|

### Восстановление пароля

|Название|Обязательно|Ограничения|Формат|Ошибка|
|--------|-----------|-----------|------|------|
|e-mail|да|может содержать (A-z), арабских цифр (0-9) и символ @.Должен содержать специальный символ "@", который отделяет имя пользователя почтовой системы от доменного имени;Не должен содержать пробелов. После символа "@" должна быть как минимум одна "."; После последней точки должно быть не менее 2-х и не более 4-х символов, причем наличие цифр не допускается; Между последней точкой и символом "@" должно быть не менее 2-х символов. Слева от "@" должно быть не менее четырех символов|строковый|Если условия не соблюдаются, то ошибка “e-mail адрес введен некорректно. используйте (A-z),@,.”|
|Пароль|да|может содержать (A-z), арабских цифр (0-9) набор допустимых специальных символов: !@#$%^&* пароль должен содержать как минимум 1 букву в lowercase, 1 букву в uppercase и 1 цифру, наличие специальных символов не обязательно min 8 символов, максимум 127|строковый|Если пароль не содержит min 1 букву lowercase, uppercase и 1 цифру, то ошибка “введите пароль при помощи заглавных, строчных букв и цифр”. Если пароль меньше 8 символов, то ошибка “Слишком короткий пароль”. Если пароль более 127 символов, то ошибка “Слишком длинный пароль. max - 127 символов”|
