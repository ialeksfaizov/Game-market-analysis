# Прогноз продаж в интернет-магазине


## Описание проекта
Из открытых источников доступны исторические данные о продажах игр, оценки пользователей и экспертов, жанры и платформы (например, Xbox или PlayStation).

Необходимо выявить определяющие успешность игры закономерности. Это позволит сделать ставку на потенциально популярный продукт и спланировать рекламные кампании.

*Примечание:*
*Мне предоставлены данные до 2016 года. Также, в наборе данных попадается аббревиатура ESRB (Entertainment Software Rating Board) — это ассоциация, определяющая возрастной рейтинг компьютерных игр. ESRB оценивает игровой контент и присваивает ему подходящую возрастную категорию, например, «Для взрослых», «Для детей младшего возраста» или «Для подростков».*


## Описание данных

- `Name` — название игры
- `Platform` — платформа
- `Year_of_Release` — год выпуска
- `Genre` — жанр игры
- `NA_sales` — продажи в Северной Америке (миллионы проданных копий)
- `EU_sales` — продажи в Европе (миллионы проданных копий)
- `JP_sales` — продажи в Японии (миллионы проданных копий)
- `Other_sales` — продажи в других странах (миллионы проданных копий)
- `Critic_Score` — оценка критиков (максимум 100)
- `User_Score` — оценка пользователей (максимум 10)
- `Rating` — рейтинг от организации ESRB 

## Задействованные библиотеки и модули
- Pandas
- Numpy
- SciPy
- Datetime
- tqdm 
- Matplotlib
- Seaborn

## Вывод
Был исследован набор данных интернет-магазина **"Стримчик"**, продавающий по всему миру видео игры. Данные содержали информацию о продажах игр, оценки пользователей и экспертов, жанры и платформы. В данных были выявлена и исправлена следующая информация:
- наименования столбцов приведены к нижнему регистру;
- тип данных в столбце `Year_of_Release` приведен к `datetime`;
- в столбце `User_Score` значения `tbd` изменено на пустые значения;
- тип данных столбца `User_Score` приведен к `float64`;
- пропуски в столбце `rating` заменены на абревиатуру `RP`, что означает - [рейтинг ожидается](https://ru.wikipedia.org/wiki/Entertainment_Software_Rating_Board#:~:text=%C2%ABRP%C2%BB%20(%C2%ABRating%20Pending%C2%BB)%20%E2%80%94%20%C2%AB%D0%A0%D0%B5%D0%B9%D1%82%D0%B8%D0%BD%D0%B3%20%D0%BE%D0%B6%D0%B8%D0%B4%D0%B0%D0%B5%D1%82%D1%81%D1%8F%C2%BB);
- значения `K-A` приведены к значению `E`, .т.к. `K-A` является [устаревшим](https://dic.academic.ru/dic.nsf/ruwiki/140779#:~:text=%C2%ABK%2DA%C2%BB%20(%C2%ABKids%20to%20Adults%C2%BB)%E2%80%94%20%C2%AB%D0%94%D0%BB%D1%8F%20%D0%B4%D0%B5%D1%82%D0%B5%D0%B9%20%D0%B8%20%D0%B2%D0%B7%D1%80%D0%BE%D1%81%D0%BB%D1%8B%D1%85%C2%BB) и по сути приравнивается к рейтингу `E`;
- данных в столбцах `name`, `platform`, `genre` и `rating` приведены к нижнему регистру;
- добавлен столбец `total_sales` с суммами продажи во всех регионах;
- в пропусках столбцов `critic_score` и `user_score` какие либо закономерности в данных и в документации не найти, следует обратиться к операторам по вводу данных;
- больше всего игр было выпущено в период с ~2002 по ~2012 годы - данные до 2002 не так важны для исследований на планирование рекламных компаний; 
- наиболее насыщенный период на выход игровых платформ - с 2004 по 2013 годы, но для планирования рекламных компаний данный период слишком велик, поэтому был принят под актуальным периодом интервал в `5` лет.
- все вышедшие игровые платформы на последний `актуальный период` падают по продажам;
- потенциально прибыльные платформы - это `ps3`, `x360`, `ps4`, `3ds`, `xone`
- у большинства платформ, вышедших за последний `актуальный период` наблюдаются выбросы в распределении - данные выбросы не влияют на медиану;
- выделяются платформы с медианой выше `0.1` млн - `ps3`, `x360`,  `ps3`, `wiiu`, `wii`, `xone`.
- зависимости продаж `total_sales` от отзывов критиков `critic_score` по платформе `xone` за последний `актуальный период` имеется, но очень слабая;
- зависимости продаж `total_sales` от отзывов пользователей `user_score` по платформе `xone` за последний `актуальный период` не выявлена;
- зависимости продаж `total_sales` от отзывов критиков `critic_score` по другим платформам за последний `актуальный период` имеется, но очень слабая;
- зависимости продаж `total_sales` от отзывов пользователей `user_score` по другим платформам за последний `актуальный период` не выявлена;
- следует учитывать, что в столбцах `critic_score` и `user_score` много пропусков;
- наиболее продаваемые жанры игр, за последний актулальный период - это `shooter`, `sports`, `platform`, `role-playing`, `racing`, `action`, `fighting`, `misc`, `simulation`;
- наименее продаваемые жанры игр за последний актулальный период - это `strategy`, `puzzle`, `adventure`.
- пользователи по региону `Серерная Америка` выбирают чаще консольные игры на платформах `pc`, `ps4`, `ps3`, `x360`, `3ds` в жанре `action`, `shooter`, `sports`, `role-playing`, `misc`;
- пользователи по региону `Япония` выбирают консольные игры на платформах `3ds`, `ps3`, `psp`, `psv`, `ps4` в жанре `role-playing`, `action`, `misc`, `fighting`, `platform`;
- пользователи по региону `Европа` выбирают консольные игры на платформах `x360`, `xone`, `ps3`, `ps4`, `3ds` в жанре `action`, `shooter`, `sports`, `role-playing`, `racing`;
- возврастной рейтинг безусловно влияет на продажи, так по регионам Серверная Америка и Европа наиболее популярны игры с рейтингом `m` - для взрозслых, а в регионе Япония наиболее популярные игры с рейтингом `e` - для всех и `t` - подросткам.


Также в ходе исследования были проверены следующие гипотезы:

*Примечание:*

*При проверке гипотез уровень значимости был выбран - 5%.*

**Гипотеза №1:**

- средние пользовательские рейтинги платформ `xone` и `pc` одинаковые;

`P-value` равно `0.6130712247638477` -  отвергнуть нулевую гипотезу не удалось. 


**Гипотеза №2:**
- средние пользовательские рейтинги жанров `action` и `sports` разные.

`P-value` равно `0.00000000000000000083` - отвергаем нулевую гипотезу.

