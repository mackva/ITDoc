# Решение заданий из тренажёра [SQL Academy](https://sql-academy.org/ru/trainer)

> [!NOTE]- `Задание 1: Вывести имена всех когда-либо обслуживаемых пассажиров авиакомпаний` [(сайт)](https://sql-academy.org/ru/trainer/tasks/1)
> ```sql
>SELECT name
>FROM Passenger
> ```

> [!NOTE]- `Задание 2: Вывести названия всеx авиакомпаний` [(сайт)](https://sql-academy.org/ru/trainer/tasks/2)
> ```sql
>SELECT name
>FROM Company
> ```

> [!NOTE]- `Задание 3: Вывести все рейсы, совершенные из Москвы` [(сайт)](https://sql-academy.org/ru/trainer/tasks/3)
> ```sql
>SELECT *
>FROM Trip
>WHERE town_from = 'Moscow'
> ```

> [!NOTE]- `Задание 4: Вывести имена людей, которые заканчиваются на "man"` [(сайт)](https://sql-academy.org/ru/trainer/tasks/4)
> ```sql
>SELECT name
>FROM Passenger
>WHERE name LIKE '%man'
> ```

> [!NOTE]- `Задание 5: Вывести количество рейсов, совершенных на TU-134` [(сайт)](https://sql-academy.org/ru/trainer/tasks/5)
>```sql
>SELECT COUNT(*) AS COUNT
>FROM Trip
>WHERE plane = 'TU-134'
> ```

> [!NOTE]- `Задание 6: Какие компании совершали перелеты на Boeing` [(сайт)](https://sql-academy.org/ru/trainer/tasks/6)
> ```sql
>SELECT DISTINCT Company.name
>FROM Trip
>  JOIN Company ON Trip.company = Company.id
>WHERE Trip.plane = 'Boeing'
> ```

> [!NOTE]- `Задание 7: Вывести все названия самолётов, на которых можно улететь в Москву (Moscow)` [(сайт)](https://sql-academy.org/ru/trainer/tasks/7)
> ```sql
>SELECT DISTINCT plane
>FROM Trip
>WHERE town_to = 'Moscow'
> ```

> [!NOTE]- `Задание 8: В какие города можно улететь из Парижа (Paris) и сколько времени это займёт?` [(сайт)](https://sql-academy.org/ru/trainer/tasks/8)
> ```sql
>SELECT town_to,
>  (time_in - time_out) AS flight_time
>FROM Trip
>WHERE town_from = 'Paris'
> ```
> 

> [!NOTE]- `Задание 9: Какие компании организуют перелеты из Владивостока (Vladivostok)?` [(сайт)](https://sql-academy.org/ru/trainer/tasks/9)
> ```sql
>SELECT Company.name
>FROM Company
>  JOIN Trip ON Trip.company = Company.id
>WHERE Trip.town_from = 'Vladivostok'
> ```

> [!NOTE]- `Задание 10: Вывести вылеты, совершенные с 10 ч. по 14 ч. 1 января 1900 г.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/10)
> ```sql
>SELECT *
>FROM Trip
>WHERE time_out BETWEEN '1900-01-01 10:00:00' AND '1900-01-01 14:00:00'
> ```
> 

> [!NOTE]- `Задание 11: Выведите пассажиров с самым длинным ФИО. Пробелы, дефисы и точки считаются частью имени.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/11)
> ```sql
>SELECT name
>FROM Passenger
>WHERE LENGTH(name) = (
>   SELECT max(LENGTH(name))
>   FROM Passenger
>  )
> ```
> 

> [!NOTE]- `Задание 12: Выведите идентификаторы всех рейсов и количество пассажиров на них. Обратите внимание, что на каких-то рейсах пассажиров может не быть. В этом случае выведите число "0".` [(сайт)](https://sql-academy.org/ru/trainer/tasks/12)
> ```sql
>SELECT Trip.id,
>   COALESCE(COUNT(Pass_in_trip.ID), 0) AS COUNT
>FROM Trip
>   LEFT JOIN Pass_in_trip ON Pass_in_trip.trip = Trip.id
>GROUP BY Trip.id
> ```
> 

> [!NOTE]- `Задание 13: Вывести имена людей, у которых есть полный тёзка среди пассажиров.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/13)
> ```sql
>SELECT name
>FROM Passenger
>GROUP BY name
>HAVING COUNT(*) > 1;
> ```

> [!NOTE]- `Задание 14: В какие города летал Bruce Willis.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/14)
> ```sql
>SELECT town_to
>FROM Passenger
>   JOIN Pass_in_trip ON Passenger.id = Pass_in_trip.passenger
>   JOIN Trip ON Trip.id = Pass_in_trip.trip
>WHERE Passenger.name = 'Bruce Willis'
> ```
> 

> [!NOTE]- `Задание 15: Выведите идентификатор пассажира Стив Мартин (Steve Martin) и дату и время его прилёта в Лондон (London).` [(сайт)](https://sql-academy.org/ru/trainer/tasks/15)
> ```sql
>SELECT Passenger.id,
>   Trip.time_in
>FROM Trip
>   JOIN Pass_in_trip ON Trip.id = Pass_in_trip.trip
>   JOIN Passenger ON Pass_in_trip.passenger = Passenger.id
>WHERE Passenger.name = 'Steve Martin'
>   AND Trip.town_to = 'London'
> ```
> 

> [!NOTE]- `Задание 16: Вывести отсортированный по количеству перелетов (по убыванию) и имени (по возрастанию) список пассажиров, совершивших хотя бы 1 полет.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/16)
> ```sql
>SELECT name,
>   COUNT(*)
>FROM Pass_in_trip
>   JOIN Passenger ON Pass_in_trip.passenger = Passenger.id
>GROUP BY Passenger.name
>ORDER BY COUNT(*) DESC,
>   name ASC
> ```
> 

> [!NOTE]- `Задание 17: Определить, сколько потратил в 2005 году каждый из членов семьи. В результирующей выборке не выводите тех членов семьи, которые ничего не потратили.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/17)
> ```sql
>SELECT FamilyMembers.member_name,
>   FamilyMembers.status,
>   sum(Payments.unit_price * Payments.amount) AS costs
>FROM FamilyMembers
>   JOIN Payments ON Payments.family_member = FamilyMembers.member_id
>WHERE Payments.date BETWEEN '2005-01-01 00:00:00' AND '2005-12-31 23:59:59'
>GROUP BY FamilyMembers.member_name,
>   FamilyMembers.status
> ```
> 

> [!NOTE]- `Задание 18: Выведите имя самого старшего человека. Если таких несколько, то выведите их всех.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/18)
> ```sql
>SELECT member_name
>FROM FamilyMembers
>WHERE birthday = (
>   SELECT birthday
>   FROM FamilyMembers
>   ORDER BY birthday ASC
>   LIMIT 1
>   )
> ```
> 

> [!NOTE]- `Задание 19: Определить, кто из членов семьи покупал картошку (potato)` [(сайт)](https://sql-academy.org/ru/trainer/tasks/19)
> ```sql
>SELECT FamilyMembers.status
>FROM FamilyMembers
>  JOIN Payments ON FamilyMembers.member_id = Payments.family_member
>  JOIN Goods ON Goods.good_id = Payments.good
>WHERE Goods.good_name = 'potato'
>GROUP BY FamilyMembers.status
> ```
> 

> [!NOTE]- `Задание 20: Сколько и кто из семьи потратил на развлечения (entertainment). Вывести статус в семье, имя, сумму.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/20)
>```sql
>SELECT FamilyMembers.status,
>   FamilyMembers.member_name,
>   sum(Payments.amount * Payments.unit_price) AS costs
>FROM FamilyMembers
>   JOIN Payments ON FamilyMembers.member_id = Payments.family_member
>   JOIN Goods ON Payments.good = Goods.good_id
>   JOIN GoodTypes ON GoodTypes.good_type_id = Goods.type
>WHERE GoodTypes.good_type_name = 'entertainment'
>GROUP BY FamilyMembers.status,
>   FamilyMembers.member_name
>```
> 

> [!NOTE]- `Задание 21: Определить товары, которые покупали более 1 раза.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/21)
> ```sql
>SELECT Goods.good_name
>FROM Goods
>   JOIN Payments ON Goods.good_id = Payments.good
>GROUP BY Goods.good_name
>HAVING COUNT(Goods.good_name) > 1
> ```
> 

> [!NOTE]- `Задание 22: Найти имена всех матерей (mother).` [(сайт)](https://sql-academy.org/ru/trainer/tasks/22)
> ```sql
>SELECT member_name
>FROM FamilyMembers
>WHERE STATUS = 'mother'
> ```
> 

> [!NOTE]- `Задание 23: Найдите самый дорогой деликатес (delicacies) и выведите его цену.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/23)
> ```sql
>SELECT good_name,
>   unit_price
>FROM Payments
>   JOIN Goods ON Payments.good = Goods.good_id
>   JOIN GoodTypes ON GoodTypes.good_type_id = Goods.type
>WHERE GoodTypes.good_type_name = 'delicacies'
>ORDER BY Payments.unit_price DESC
>LIMIT 1
> ```
> 

> [!NOTE]- `Задание 24: Определить кто и сколько потратил в июне 2005.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/24)
> ```sql
>SELECT FamilyMembers.member_name,
>   sum(Payments.amount * Payments.unit_price) AS costs
>FROM FamilyMembers
>   JOIN Payments ON FamilyMembers.member_id = Payments.family_member
>WHERE EXTRACT('month' FROM Payments.date) = 6
>   AND EXTRACT('year'  FROM Payments.date) = 2005
>GROUP BY FamilyMembers.member_name
> ```
> 

> [!NOTE]- `Задание 25: Определить, какие товары не покупались в 2005 году.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/25)
> ```sql
>SELECT good_name
>FROM Goods
>WHERE good_id NOT IN (
>   SELECT good
>   FROM Payments
>   WHERE Extract('year' FROM date) = 2005
>   )
> ```
> 

> [!NOTE]- `Задание 26: Определить группы товаров, которые не приобретались в 2005 году` [(сайт)](https://sql-academy.org/ru/trainer/tasks/26)
> ```sql
>SELECT good_type_name
>FROM GoodTypes
>WHERE good_type_id NOT IN (
>   SELECT TYPE
>   FROM Goods
>   JOIN Payments ON Payments.good = Goods.good_id
>   WHERE EXTRACT('year' FROM Payments.date) = 2005
>   )
> ```
> 

> [!NOTE]- `Задание 27: Узнайте, сколько было потрачено на каждую из групп товаров в 2005 году. Выведите название группы и потраченную на неё сумму. Если потраченная сумма равна нулю, т.е. товары из этой группы не покупались в 2005 году, то не выводите её.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/27)
> ```sql
>SELECT GoodTypes.good_type_name,
>   sum(Payments.amount * Payments.unit_price) AS costs
>FROM GoodTypes
>   JOIN goods ON GoodTypes.good_type_id = Goods.type
>   JOIN Payments ON Payments.good = Goods.good_id
>WHERE Extract('Year' FROM Payments.date) = 2005
>GROUP BY GoodTypes.good_type_name
> ```
> 

> [!NOTE]- `Задание 28: Сколько рейсов совершили авиакомпании из Ростова (Rostov) в Москву (Moscow)?` [(сайт)](https://sql-academy.org/ru/trainer/tasks/28)
> ```sql
>SELECT COUNT(company)
>FROM Trip
>WHERE town_from = 'Rostov' AND town_to = 'Moscow'
> ```
> 

> [!NOTE]- `Задание 29: Выведите имена пассажиров улетевших в Москву (Moscow) на самолете TU-134. В ответе не должно быть дубликатов.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/29)
> ```sql
>select DISTINCT(Passenger.name)
>from Passenger
>   join Pass_in_trip on Pass_in_trip.passenger = Passenger.id
>   join Trip on Trip.id = Pass_in_trip.trip
>where Trip.town_to = 'Moscow' and Trip.plane = 'TU-134'
> ```
> 

> [!NOTE]- `Задание 30: Выведите нагруженность (число пассажиров) каждого рейса (trip). Результат вывести в отсортированном виде по убыванию нагруженности.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/30)
> ```sql
>SELECT Pass_in_trip.trip,
>   COUNT(Pass_in_trip.passenger)
>FROM Pass_in_trip
>GROUP BY Pass_in_trip.trip
>ORDER BY COUNT(Pass_in_trip.passenger) DESC
> ```
> 

> [!NOTE]- `Задание 31: Вывести всех членов семьи с фамилией Quincey.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/31)
> ```sql
>SELECT *
>FROM FamilyMembers
>WHERE member_name LIKE '%Quincey'
> ```
> 

> [!NOTE]- `Задание 32: Вывести средний возраст людей (в годах), хранящихся в базе данных. Результат округлите до целого в меньшую сторону.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/32)
> ```sql
>SELECT ROUND(avg(EXTRACT('year' FROM age(birthday)))) AS age
>FROM FamilyMembers
> ```
> 

> [!NOTE]- `Задание 33: Найдите среднюю цену икры на основе данных, хранящихся в таблице Payments. В базе данных хранятся данные о покупках красной (red caviar) и черной икры (black caviar). В ответе должна быть одна строка со средней ценой всей купленной когда-либо икры.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/33)
> ```sql
>SELECT avg(Payments.unit_price) AS cost
>FROM Payments
>   JOIN goods ON Goods.good_id = Payments.good
>WHERE Goods.good_name = 'red caviar' OR Goods.good_name = 'black caviar'
> ```
> 

> [!NOTE]- `Задание 34: Сколько всего 10-ых классов.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/34)
> ```sql
>SELECT COUNT(*)
>FROM Class
>WHERE name LIKE '10 %'
> ```
> 

> [!NOTE]- `Задание 35: Сколько различных кабинетов школы использовались 2 сентября 2019 года для проведения занятий?` [(сайт)](https://sql-academy.org/ru/trainer/tasks/35)
> ```sql
>SELECT COUNT(DISTINCT(classroom))
>FROM Schedule
>WHERE EXTRACT('day' FROM date) = 2
>   AND EXTRACT('month' FROM date) = 9
>   AND EXTRACT('year' FROM date) = 2019
> ```
> 

> [!NOTE]- `Задание 36: Выведите информацию об обучающихся живущих на улице Пушкина (ul. Pushkina)?` [(сайт)](https://sql-academy.org/ru/trainer/tasks/36)
> ```sql
>SELECT *
>FROM Student
>WHERE address like 'ul. Pushkina%'
> ```
> 

> [!NOTE]- `Задание 37: Сколько лет самому молодому обучающемуся ?` [(сайт)](https://sql-academy.org/ru/trainer/tasks/37)
> ```sql
>SELECT (EXTRACT('year' FROM age(birthday))) AS year
>FROM Student
>ORDER BY birthday DESC
>LIMIT 1
> ```
> 

> [!NOTE]- `Задание 38: Сколько учениц с именем Анна (Anna) учится в школе?` [(сайт)](https://sql-academy.org/ru/trainer/tasks/38)
> ```sql
>SELECT COUNT(*)
>FROM Student
>WHERE Student.first_name = 'Anna'
> ```

> [!NOTE]- `Задание 39: Сколько обучающихся в 10 B классе ?` [(сайт)](https://sql-academy.org/ru/trainer/tasks/39)
> ```sql
>SELECT COUNT(*)
>FROM Class
>   JOIN Student_in_class ON Class.id = Student_in_class.class
>WHERE Class.name = '10 B'
> ```
> 

> [!NOTE]- `Задание 40: Выведите название предметов, которые преподает Ромашкин П.П. (Romashkin P.P.). Обратите внимание, что в базе данных есть несколько учителей с такой фамилией.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/40)
> ```sql
>SELECT Subject.name AS subjects
>FROM Subject
>   JOIN Schedule ON Schedule.subject = Subject.id
>   JOIN Teacher ON Teacher.id = Schedule.teacher
>WHERE Teacher.last_name = 'Romashkin' AND Teacher.first_name LIKE 'P%'
>   AND Teacher.middle_name LIKE 'P%'
> ```
> 

> [!NOTE]- `Задание 41: Выясните, во сколько по расписанию начинается четвёртое занятие.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/41)
> ```sql
>SELECT Timepair.start_pair
>FROM Timepair
>WHERE id = 4
> ```
> 

> [!NOTE]- `Задание 42: Сколько времени обучающийся будет находиться в школе, учась со 2-го по 4-ый уч. предмет?` [(сайт)](https://sql-academy.org/ru/trainer/tasks/42)
> ```sql
>SELECT (max(end_pair) - min(start_pair)) AS time
>FROM Timepair
>WHERE id BETWEEN 2 AND 4
> ```
> 

> [!NOTE]- `Задание 43: Выведите фамилии преподавателей, которые ведут физическую культуру (Physical Culture). Отсортируйте преподавателей по фамилии в алфавитном порядке.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/43)
> ```sql
>SELECT Teacher.last_name
>FROM Teacher
>   JOIN Schedule ON Teacher.id = Schedule.teacher
>   JOIN Subject ON Schedule.subject = Subject.id
>WHERE Subject.name = 'Physical Culture'
>ORDER BY Teacher.last_name ASC
> ```
> 

> [!NOTE]- `Задание 44: Найдите максимальный возраст (количество лет) среди обучающихся 10 классов на сегодняшний день. Для получения текущих даты и времени используйте функцию NOW().` [(сайт)](https://sql-academy.org/ru/trainer/tasks/44)
> ```sql
>SELECT max(EXTRACT('year' FROM age(NOW(), birthday))) AS max_year
>FROM Student
>   JOIN Student_in_class ON Student.id = Student_in_class.student
>   JOIN Class ON Class.id = Student_in_class.class
>WHERE Class.name LIKE '10%'
> ```
> 

> [!NOTE]- `Задание 45: Какие кабинеты чаще всего использовались для проведения занятий? Выведите те, которые использовались максимальное количество раз.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/45)
> ```sql
>SELECT classroom
>FROM Schedule
>GROUP BY classroom
>HAVING COUNT(*) = (
>   SELECT COUNT(*)
>   FROM Schedule
>   GROUP BY classroom
>   ORDER BY COUNT(*) DESC
>  LIMIT 1
>   )
> ```
> 

> [!NOTE]- `Задание 46: В каких классах введет занятия преподаватель "Krauze" ?` [(сайт)](https://sql-academy.org/ru/trainer/tasks/46)
> ```sql
>SELECT DISTINCT(Class.name)
>FROM Class
>   JOIN Schedule ON Schedule.class = Class.id
>   JOIN Teacher ON Teacher.id = Schedule.teacher
>WHERE Teacher.last_name = 'Krauze'
> ```
> 

> [!NOTE]- `Задание 47: Сколько занятий провел Krauze 30 августа 2019 г.?` [(сайт)](https://sql-academy.org/ru/trainer/tasks/47)
> ```sql
>SELECT COUNT(*)
>FROM Schedule
>   JOIN Teacher ON Teacher.id = Schedule.teacher
>WHERE Teacher.last_name = 'Krauze'
>   AND extract('year' FROM Schedule.date) = 2019
>   AND extract('month' FROM Schedule.date) = 8
>   AND extract('day' FROM Schedule.date) = 30
> ```
> 

> [!NOTE]- `Задание 48: Выведите заполненность классов в порядке убывания` [(сайт)](https://sql-academy.org/ru/trainer/tasks/48)
> ```sql
>SELECT Class.name,
>   COUNT(Student_in_class.id) AS COUNT
>FROM Class
>   JOIN Student_in_class ON Class.id = Student_in_class.class
>GROUP BY Class.name
>ORDER BY COUNT(Student_in_class.id) DESC
> ```
> 

> [!NOTE]- `Задание 49: ВКакой процент обучающихся учится в "10 A" классе? Выведите ответ в диапазоне от 0 до 100 с округлением до четырёх знаков после запятой, например, 96.0201.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/49)
> ```sql
>SELECT ROUND(
>   (
>   SELECT COUNT(*)
>   FROM Class
>   JOIN Student_in_class ON Class.id = Student_in_class.class
>   WHERE Class.name = '10 A'
>   ) * 100.0 / COUNT(*), 4) AS percent
>FROM Student_in_class
> ```
> 

> [!NOTE]- `Задание 50: Какой процент обучающихся родился в 2000 году? Результат округлить до целого в меньшую сторону.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/50)
> ```sql
>SELECT floor(
>  (
>   SELECT COUNT(*)
>   FROM Student
>   WHERE EXTRACT('year' FROM birthday) = 2000
>  ) * 100.0 / COUNT(*)
> ) AS percent
>FROM Student
> ```
> 

> [!NOTE]- `Задание 51: Добавьте товар с именем "Cheese" и типом "food" в список товаров (Goods).` [(сайт)](https://sql-academy.org/ru/trainer/tasks/51)
> ```sql
>INSERT INTO Goods
>VALUES (
>   (
>   SELECT COUNT(*) + 1
>   FROM goods
>   ),
>   'Cheese',
>   (
>   SELECT good_type_id
>   FROM GoodTypes
>   WHERE good_type_name = 'food'
>   )
>)
> ```
> 

> [!NOTE]- `Задание 52: Добавьте в список типов товаров (GoodTypes) новый тип "auto".` [(сайт)](https://sql-academy.org/ru/trainer/tasks/52)
> ```sql
>INSERT INTO GoodTypes
>VALUES (
>   (
>   SELECT COUNT(*) + 1
>   FROM GoodTypes
>   ),
>   'auto'
>)
> ```
> 

> [!NOTE]- `Задание 53: Измените имя "Andie Quincey" на новое "Andie Anthony".` [(сайт)](https://sql-academy.org/ru/trainer/tasks/53)
> ```sql
>UPDATE FamilyMembers
>SET member_name = 'Andie Anthony'
>WHERE member_name = 'Andie Quincey'
> ```
> 

> [!NOTE]- `Задание 54: Удалить всех членов семьи с фамилией "Quincey".` [(сайт)](https://sql-academy.org/ru/trainer/tasks/54)
> ```sql
>DELETE FROM FamilyMembers
>where member_name like '%Quincey'
> ```
> 

> [!NOTE]- `Задание 55: Удалить компании, совершившие наименьшее количество рейсов.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/55)
> ```sql
>DELETE FROM Company
>WHERE id IN (
> SELECT company
> FROM Trip
> GROUP BY company
> HAVING COUNT(*) = (
>   SELECT COUNT(*) AS COUNT
>   FROM trip
>   GROUP BY company
>   ORDER BY COUNT
>   LIMIT 1
>   )
>)
> ```
> 

> [!NOTE]- `Задание 56: Удалить все перелеты, совершенные из Москвы (Moscow).` [(сайт)](https://sql-academy.org/ru/trainer/tasks/56)
> ```sql
>delete from Trip
>where town_from = 'Moscow'
> ```
> 

> [!NOTE]- `Задание 57: Перенести расписание всех занятий на 30 мин. вперед.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/57)
> ```sql
>Update Timepair
>set start_pair = start_pair + '30 minutes'::interval,
>   end_pair = end_pair + '30 minutes'::interval;
> ```
> 

> [!NOTE]- `Задание 58: Добавить отзыв с рейтингом 5 на жилье, находящиеся по адресу "11218, Friel Place, New York", от имени "George Clooney".` [(сайт)](https://sql-academy.org/ru/trainer/tasks/58)
> ```sql
>INSERT INTO Reviews
>VALUES (
> (
>  SELECT COUNT(*) + 1
>  FROM Reviews
> ),
> (
>  SELECT Reservations.id
>  FROM Reservations
>   JOIN Rooms ON Rooms.id = Reservations.room_id
>   JOIN Users ON Users.id = Reservations.user_id
>  WHERE Users.name = 'George Clooney'
>   AND Rooms.address = '11218, Friel Place, New York'
> ),
> 5
>)
> ```
> 

> [!NOTE]- `Задание 59: Вывести пользователей,указавших Белорусский номер телефона ? Телефонный код Белоруссии +375.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/59)
> ```sql
>select *
>from Users
>where phone_number like '+375%'
> ```

> [!NOTE]- `Задание 60: Выведите идентификаторы преподавателей, которые хотя бы один раз за всё время преподавали в каждом из одиннадцатых классов.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/60)
> ```sql
>SELECT Teacher
>FROM Schedule
> JOIN Class ON Schedule.class = Class.id
>WHERE name LIKE '11%'
>GROUP BY Teacher
>HAVING COUNT(DISTINCT Class.name) = (
>  SELECT COUNT(*)
>  FROM Class
>  WHERE name LIKE '11%'
> )
> ```
> 

> [!NOTE]- `Задание 61: Выведите список комнат, которые были зарезервированы хотя бы на одни сутки в 12-ую неделю 2020 года. В данной задаче в качестве одной недели примите период из семи дней, первый из которых начинается 1 января 2020 года. Например, первая неделя года — 1–7 января, а третья — 15–21 января.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/61)
> ```sql
>select Rooms.*
>from Rooms
> join Reservations on Reservations.room_id = Rooms.id
>where EXTRACT('year' from start_date) = 2020
>  and EXTRACT('week' from start_date) = 12
> ```
> 

> [!NOTE]- `Задание 62: Вывести в порядке убывания популярности доменные имена 2-го уровня, используемые пользователями для электронной почты. Полученный результат необходимо дополнительно отсортировать по возрастанию названий доменных имён.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/62)
> ```sql
>SELECT (substring(email FROM position('@' IN email) + 1)) AS domain,
> (COUNT(*)) AS COUNT
>FROM Users
>GROUP BY domain
>ORDER BY COUNT DESC, domain
> ```
> 

> [!NOTE]- `Задание 63: Выведите отсортированный список (по возрастанию) фамилий и имен студентов в виде Фамилия.И.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/63)
> ```sql
>SELECT (last_name || '.' || SUBSTRING(first_name FOR 1) || '.') AS name
>FROM Student
>ORDER BY last_name, first_name ASC
> ```

> [!NOTE]- `Задание 64: Вывести количество бронирований по каждому месяцу каждого года, в которых было хотя бы 1 бронирование. Результат отсортируйте в порядке возрастания даты бронирования.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/64)
> ```sql
>SELECT (EXTRACT('year' FROM start_date)) AS year,
> (EXTRACT('month' FROM start_date)) AS month,
> (COUNT(*)) AS amount
>FROM Reservations
>GROUP BY year, month
>ORDER BY year, month ASC
> ```
> 

> [!NOTE]- `Задание 65: Необходимо вывести рейтинг для комнат, которые хоть раз арендовали, как среднее значение рейтинга отзывов округленное до целого вниз.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/65)
> ```sql
>SELECT Reservations.room_id as room_id,
> floor(avg(Reviews.rating)) as rating
>FROM Reviews
> join Reservations on Reviews.reservation_id = Reservations.id
>Group by Reservations.room_id
> ```
> 

> [!NOTE]- `Задание 66: Вывести названия всеx авиакомпаний` [(сайт)](https://sql-academy.org/ru/trainer/tasks/66)
> ```sql
>select Rooms.home_type,
> Rooms.address,
> COALESCE(sum(EXTRACT('day'from (Reservations.end_date - Reservations.start_date))), 0) as days,
> COALESCE(sum(Reservations.total), 0) as total_fee
>FROM Rooms
>  left join Reservations on Reservations.room_id = Rooms.id
>where Rooms.has_tv = true
>   and Rooms.has_internet = true
>   and Rooms.has_kitchen = true
>   and Rooms.has_air_con = true
>GROUP by Rooms.home_type, Rooms.address
> ```
> 

> [!NOTE]- `Задание 67: Вывести время отлета и время прилета для каждого перелета в формате "ЧЧ:ММ, ДД.ММ - ЧЧ:ММ, ДД.ММ", где часы и минуты с ведущим нулем, а день и месяц без.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/67)
> ```sql
>select (TO_CHAR(time_out, 'HH24:MI, FMDD.FMMM') || ' - ' || TO_CHAR(time_in, 'HH24:MI, FMDD.FMMM')) as flight_time
>from Trip
> ```
> 

> [!NOTE]- `Задание 68: Для каждой комнаты, которую снимали как минимум 1 раз, найдите имя человека, снимавшего ее последний раз, и дату, когда он выехал` [(сайт)](https://sql-academy.org/ru/trainer/tasks/68)
> ```sql
>SELECT room_id,
> end_date,
> name
>FROM (
>  SELECT ROW_NUMBER() over (
>  PARTITION by Reservations.room_id
>   ORDER BY Reservations.end_date DESC
>  ) AS row_id,
>   Reservations.room_id,
>   Reservations.end_date,
>   USers.name
>  FROM Reservations
>  JOIN Users ON Users.id = Reservations.user_id
>)
>WHERE row_id = 1
> ```
> 

> [!NOTE]- `Задание 69: Вывести идентификаторы всех владельцев комнат, что размещены на сервисе бронирования жилья и сумму, которую они заработали` [(сайт)](https://sql-academy.org/ru/trainer/tasks/69)
> ```sql
>SELECT Rooms.owner_id,
> COALESCE(sum(Reservations.total), 0) as total_earn
>from Rooms
>  left join Reservations on Reservations.room_id = Rooms.id
>GROUP by Rooms.owner_id
> ```
> 

> [!NOTE]- `Задание 70: Необходимо категоризовать жилье на economy, comfort, premium по цене соответственно <= 100, 100 < цена < 200, >= 200. В качестве результата вывести таблицу с названием категории и количеством жилья, попадающего в данную категорию` [(сайт)](https://sql-academy.org/ru/trainer/tasks/70)
> ```sql
>SELECT (
> CASE
>  WHEN price <= 100 THEN 'economy'
>  WHEN price > 100 AND price < 200 THEN 'comfort'
>  WHEN price >= 200 THEN 'premium'
> END
> ) AS category,
> COUNT(price) AS count
>FROM Rooms
>GROUP bY category
> ```

> [!NOTE]- `Задание 71: Найдите какой процент пользователей, зарегистрированных на сервисе бронирования, хоть раз арендовали или сдавали в аренду жилье. Результат округлите до сотых.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/71)
> ```sql
>SELECT round(
> COUNT(*) * 100.0 / (
>  SELECT COUNT(*)
>  FROM Users
>),2) AS percent
>FROM (
>  SELECT Reservations.user_id AS id
>  FROM Reservations
>  UNION
>  SELECT Rooms.owner_id
>  FROM Rooms
>   JOIN Reservations ON Reservations.room_id = Rooms.id
>)
> ```
> 

> [!NOTE]- `Задание 72: Выведите среднюю цену бронирования за сутки для каждой из комнат, которую бронировали хотя бы один раз. Среднюю цену необходимо округлить до целого значения вверх.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/72)
> ```sql
>select room_id,
> ceil(avg(price)) as avg_price
>from Reservations
>GROUP By room_id
> ```
> 

> [!NOTE]- `Задание 73: Выведите id тех комнат, которые арендовали нечетное количество раз` [(сайт)](https://sql-academy.org/ru/trainer/tasks/73)
> ```sql
>select room_id,
> count(*) as count
>from Reservations
>GROUP By room_id
>HAVING count(*) % 2 = 1
> ```
> 

> [!NOTE]- `Задание 74: Выведите идентификатор и признак наличия интернета в помещении. Если интернет в сдаваемом жилье присутствует, то выведите «YES», иначе «NO».` [(сайт)](https://sql-academy.org/ru/trainer/tasks/74)
> ```sql
>SELECT id,
> case
>  when has_internet = true then 'YES'
>  else 'NO'
> end as has_internet
>from Rooms
> ```
> 

> [!NOTE]- `Задание 75: Выведите фамилию, имя и дату рождения студентов, кто был рожден в мае.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/75)
> ```sql
>SELECT first_name,
> last_name,
> birthday
>from Student
>where extract(month from birthday) = 5
> ```
> 

> [!NOTE]- `Задание 76: Вывести имена всех пользователей сервиса бронирования жилья, а также два признака: является ли пользователь собственником какого-либо жилья (is_owner) и является ли пользователь арендатором (is_tenant). В случае наличия у пользователя признака необходимо вывести в соответствующее поле 1, иначе 0.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/76)
> ```sql
>SELECT name,
>(
> case
>  when (
>   id in (SELECT owner_id from Rooms)
> ) then 1
> else 0
>end
>) as is_owner,
>(
>case
> when (
>   id in (SELECT user_id from Reservations)
>  ) then 1
> else 0
>end
>) as is_tenant
>from Users
> ```
> 

> [!NOTE]- `Задание 77: Создайте представление с именем "People", которое будет содержать список имен (first_name) и фамилий (last_name) всех студентов (Student) и преподавателей(Teacher).` [(сайт)](https://sql-academy.org/ru/trainer/tasks/77)
> ```sql
>CREATE view People as (
> SELECT first_name,
>  last_name
> from Student
>)
>UNION
>(
> SELECT first_name,
>  last_name
> from Teacher
>)
> ```

> [!NOTE]- `Задание 78: Выведите всех пользователей с электронной почтой в «hotmail.com»` [(сайт)](https://sql-academy.org/ru/trainer/tasks/78)
> ```sql
>select *
>from Users
>where email like '%@hotmail.com'
> ```
> 

> [!NOTE]- `Задание 79: Выведите поля id, home_type, price у всего жилья из таблицы Rooms. Если комната имеет телевизор и интернет одновременно, то в качестве цены в поле price выведите цену, применив скидку 10%.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/79)
> ```sql
>select id,
> home_type,
> (
>  case
>   when has_tv = true and has_internet then price * 0.9
>   else price
>  end
> ) as price
>from Rooms
> ```
> 

> [!NOTE]- `Задание 80: Создайте представление «Verified_Users» с полями id, name и email, которое будет показывает только тех пользователей, у которых подтвержден адрес электронной почты.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/80)
> ```sql
>CREATE VIEW Verified_Users as
>SELECT id,
> name,
> email
>from Users
>where email_verified_at is not null
> ```
> 

> [!NOTE]- `Задание 93: Какой средний возраст клиентов, купивших Smartwatch (использовать наименование товара product.name) в 2024 году?` [(сайт)](https://sql-academy.org/ru/trainer/tasks/93)
> ```sql
>SELECT avg(age) AS average_age
>FROM (
> SELECT Customer.age
> FROM Customer
>  JOIN Purchase ON Purchase.customer_key = Customer.customer_key
>  JOIN Product ON Product.product_key = Purchase.product_key
>  WHERE EXTRACT('year' FROM Purchase.date) = 2024
>   AND Product.name = 'Smartwatch'
>  GROUP BY Customer.customer_key
>)
> ```
> 

> [!NOTE]- `Задание 94: Вывести имена покупателей, каждый из которых приобрёл Laptop и Monitor (использовать наименование товара product.name) в марте 2024 года?` [(сайт)](https://sql-academy.org/ru/trainer/tasks/94)
> ```sql
>SELECT Customer.name
>FROM Customer
> JOIN Purchase ON Purchase.customer_key = Customer.customer_key
> JOIN Product ON Product.product_key = Purchase.product_key
>WHERE EXTRACT('year' FROM Purchase.date) = 2024
> AND EXTRACT('month'FROM Purchase.date) = 3
> AND Product.name IN ('Laptop', 'Monitor')
>GROUP BY Customer.name
>HAVING array_agg(Product.name)::text [] @> ARRAY ['Laptop', 'Monitor']::text []
> ```
> 

> [!NOTE]- `Задание 97: Посчитать количество работающих складов на текущую дату по каждому городу. Вывести только те города, у которых количество складов более 80. Данные на выходе - город, количество складов.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/97)
> ```sql
>select city,
> count(*) as warehouse_count
>from Warehouses
>Where date_close is null
>GROUP BY city
>HAVING count(*) > 80
> ```
> 

> [!NOTE]- `Задание 99: Посчитай доход с женской аудитории (доход = сумма(price * items)). Обратите внимание, что в таблице женская аудитория имеет поле user_gender «female» или «f».` [(сайт)](https://sql-academy.org/ru/trainer/tasks/99)
> ```sql
>SELECT sum(price * items) as income_from_female
>from Purchases
>where user_gender = 'female' or user_gender = 'f'
> ```
> 

> [!NOTE]- `Задание 101: Выведи для каждого пользователя первое наименование, которое он заказал (первое по времени транзакции).` [(сайт)](https://sql-academy.org/ru/trainer/tasks/101)
> ```sql
>SELECT user_id,
> item
>FROM (
> SELECT user_id,
>  item,
>  ROW_NUMBER() OVER(
>   PARTITION BY user_id
>   ORDER BY transaction_ts
> ) AS row_num
> FROM Transactions
>)
>WHERE row_num = 1
> ```
> 

> [!NOTE]- `Задание 103: Вывести список имён сотрудников, получающих большую заработную плату, чем у непосредственного руководителя.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/103)
> ```sql
>SELECT e.name
>from Employee as e
> left join Employee as c on c.id = e.chief_id
>WHERE e.salary > c.salary
> ```
> 

> [!NOTE]- `Задание 109: Выведите название страны, где находится город «Salzburg»` [(сайт)](https://sql-academy.org/ru/trainer/tasks/109)
> ```sql
>SELECT Countries.name as country_name
>from Countries
> join Regions on Regions.countryid = Countries.id
> join Cities on Cities.regionid = Regions.countryid
>WHERE Cities.name = 'Salzburg'
>limit 1
> ```
> 

> [!NOTE]- `Задание 111: Посчитайте население каждого региона. В качестве результата выведите название региона и его численность населения.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/111)
> ```sql
>SELECT Regions.name AS region_name,
> sum(Cities.population) AS total_population
>FROM Regions
> JOIN Cities ON Regions.id = Cities.regionid
>GROUP BY Regions.name
> ```
> 

> [!NOTE]- `Задание 114: Напишите запрос, который выведет имена пилотов, которые в качестве второго пилота (second_pilot_id) в августе 2023 года летали в New York.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/114)
> ```sql
>SELECT p.name
>from Flights as f
> JOIN Pilots as p on f.second_pilot_id = p.pilot_id
>where f.destination = 'New York'
> and EXTRACT(YEAR FROM f.flight_date) = 2023
> and EXTRACT(month FROM f.flight_date) = 8
> ```
> 

> [!NOTE]- `Задание 123: Необходимо написать SQL-запрос, который покажет всех сотрудников, у кого в работе менее трех задач. Результат предоставить в виде: имя сотрудника, количество задач в работе.` [(сайт)](https://sql-academy.org/ru/trainer/tasks/123)
> ```sql
>select Employee.emp_name,
> count(*) as task_count
>from Employee
> join Tasks on Employee.id = Tasks.assignee_id
>group by Employee.id, Employee.emp_name
>Having count(*) < 3
> ```

> [!NOTE]- `Задание 125: Дана база данных автоматизирующая работу библиотеки. В таблице Books хранится информация о произведениях, в таблице BookEditions - информация об изданиях этих произведений (одно произведение может издаваться много раз в разные годы).` [(сайт)](https://sql-academy.org/ru/trainer/tasks/125)
> ```sql
>SELECT Books.title
>FROM Books
> JOIN BookEditions ON Books.id = BookEditions.book_id
>GROUP BY Books.title
>HAVING COUNT(*) > 5
> ```

