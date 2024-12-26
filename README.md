Предыстория:
У меня было под 2000 сотрудников, у них было около 8000 учток в разных сервисах, и чтобы их модерировать, нужно было находить их по ФИО, но к сожалению я не нашел ни 1 нормального поиска в гугл таблицах по ФИО. 
Также я не рассматривал решения из множества файлов и множества строчек кода, мне нужно было проверянное и понятное решение, которое я буду знать как работает. 
К счастью у меня сразу же была идея, как написать простой в понимании и рабочий метод поиска.

Коротко о том, как работает поиск:
Я обрезал во всех словах окончания, чтобы отсечь ошибки в написаниях окончаний,
также чтобы устранить ошибку последовательности слов (фамилия имя отчество или имя фамилия отчество)
я разделил слова и посчитал их по отдельности, а потом сложил и тем самым получил уникальное число
Чтобы учесть последовательность букв в слове, например (вася и ясав) одинаковое количество букв но разная последовательность,
я возвел число уникальной буквы в степень, и каждая последующая буква умножалась на степень выше, чем предыдущая, тем самым зафиксировав положение каждой буквы.
Сложив все числа букв возведенные в степень, мы получаем уникальное число одного слова, потом мы складываем все слова и получаем уникальное число ФИО
По этому уникальному числу ФИО мы ищем любые другие ФИО

Оптимизация:
Возведение в большую степень довольно затратная операция, и оптимальнее будет использовать умножение на разные числа, 
но если умножать на числа до "1000" то числа могут сгенерироваться недостаточно уникальными и будут ошибки, 
метод со степенями генерирует сверхуникальные числа, с которыми у меня не возникало ошибок. 
Можно попробовать умножать на числа от 10000 до 20000, возможно будет достаточная уникальность числа и меньше загрузка на математические вычисления

Установка:
Добавляете код из файла the search.txt в Apps Script, сохраняете и используете в таблице как =calculateFullNameValue(A1) или =calculateFullNameValue("Амперов Олаф Шольц")
функция для поиска =INDEX(B:B, MATCH(H3, C:C, 0))   (B:B - выведется найденная строка из данного столбца, H3 - ячейка с значением которое нужно найти, C:C - столбец, в котором будет искаться заданное значение)
