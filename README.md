# SQL-Queries
The repository contains a collection of SQL queries used to interact with the database. It contains queries for data selection, updates, deletions, and other operations required for data management.
---
- Выбрать все записи из таблицы actor
```sql
SELECT * FROM actor
```
- Получить все записи из таблицы address, для которых не указан почтовый индекс. Отсортировать результат по address_id.
```sql
SELECT *
FROM address
WHERE postal_code IS NULL
ORDER BY address_id
```
- Получить столбец name из таблицы language в алфавитном порядке.
```sql
SELECT name
FROM language
ORDER BY name
```
- Выберать все значения имён и фамилий актёров из таблицы actor.
```sql
SELECT first_name, last_name
FROM actor
```
- Получить список значений из колонки name таблицы language.
```sql
SELECT name
FROM language
```
- Выбрать названия фильмов из таблицы film. Отсортировать полученный список по алфавиту.
```sql
SELECT title
FROM film
ORDER BY title ASC
```
- Из таблицы customer выбрать все записи о фамилии - last_name, имени - first_name и адресе электронной почты email отсортировав их по фамилии в алфавитном порядке.
```sql
SELECT last_name, first_name, email
FROM customer
ORDER BY last_name
```
- SQL-запрос, который выводит список уникальных значений rating из таблицы film в алфавитном порядке.
```sql
SELECT DISTINCT rating
FROM film
ORDER BY rating ASC
```
- Получить названия пяти самых длинных фильмов, отсортированных по продолжительности в порядке убывания.
```sql
SELECT title
FROM film
ORDER BY length DESC
LIMIT 5
```
- Выберить название, описание и год выхода фильмов из таблицы film. Отсортировать полученный список по названию в алфавитном порядке и вывести первые десять строк.
```sql
SELECT title, description, release_year
FROM film
ORDER BY title
LIMIT 10
```
- Для удобства показа мы разобьем список фильмов на страницы по десять записей на каждой. Для формирования третьей страницы списка выберить название, описание и год выхода фильмов из таблицы film.
Отсортируйть полученный список по названию в алфавитном порядке и выведите десять строк начиная с двадцать первой.
```sql
SELECT title, description, release_year
FROM film
ORDER BY title
LIMIT 20, 10
```
- Выберить название, стоимость проката и продолжительность фильмов из таблицы film. Отсортировать полученный список по убыванию стоимости, фильмы с одинаковой стоимостью отсортировать по возрастанию продолжительности фильма.
```sql
SELECT title, rental_rate, length
FROM film
ORDER BY rental_rate DESC, length ASC
```
- Найти самый длинный фильм в таблице film. Если несколько фильмов имеют одинаковую продолжительность, выберить фильм с наименьшей ценой замены replacement_cost. Написать запрос, который возвращает два столбца: title и release_year.
```sql
SELECT title, release_year
FROM film
WHERE length = (SELECT MAX(length) FROM film)
ORDER BY replacement_cost
LIMIT 1
```
- Найти все фильмы продолжительностью более трёх часов. Написать запрос возвращающий результат состоящий из трёх столбцов: названия фильма, его описания и продолжительности в минутах отсортированный по длине фильма.
```sql
SELECT title, description, length
FROM film
WHERE length > 180
ORDER BY length
```
- Найти сотрудников, работающих в магазине номер 1, и получить все их данные.
```sql
SELECT *
FROM staff
WHERE store_id = 1
```
- Найдти всех активных в данный момент клиентов (active = 1) в таблице customer. Таблица результатов должна содержать следующие поля: customer_id, first_name и last_name.
```sql
SELECT customer_id, first_name, last_name
FROM customer
WHERE active = 1
```
- Найти актеров по имени Scarlett.
```sql
SELECT *
FROM actor
WHERE first_name = 'Scarlett'
```
- Найдите все фильмы, в описании которых есть слово Student. Выведите названия фильмов в алфавитном порядке.
```sql
SELECT title
FROM film
WHERE description LIKE '%Student%'
ORDER BY title ASC
```
- Найти все фильмы продолжительностью более 3 часов и получите их название, год выпуска и продолжительность, отсортированные по продолжительности в порядке возрастания.
```sql
SELECT title, release_year, length
FROM film
WHERE length > 180
ORDER BY length ASC
```
- Написать SQL-запрос, чтобы получить список фильмов, отсутствующих в прокате (таблица inventory). Отобразить названия этих фильмов в столбце с названием film_title в алфавитном порядке. Использовать для решения задачи соединение таблиц.
```sql
SELECT 
    f.title AS film_title
FROM 
    film f
LEFT JOIN 
    inventory i ON f.film_id = i.film_id
WHERE 
    i.film_id IS NULL
ORDER BY 
    f.title;
```
- Найдити фильмы из базы данных Sakila, для которых нет записей об учавствоваших в них актёрах. Вывести результирующую с полями title, release_year отсортированных по названию фильма.
```sql
SELECT film.title, film.release_year
FROM film
LEFT JOIN film_actor ON film.film_id = film_actor.film_id
WHERE film_actor.actor_id IS NULL
ORDER BY film.title
```
- Напиcать SQL-запрос, который выводит названия всех фильмов и их категорий из базы данных Sakila.
```sql
SELECT film.title, category.name
FROM film
JOIN film_category ON film.film_id = film_category.film_id
JOIN category ON film_category.category_id = category.category_id
```
- Написать SQL-запрос для получения списка языков из таблицы language, на которых нет доступных фильмов. Представить результат в таблице с одним столбцом - language, отсортированным по алфавиту. Использовать для решения задачи соединение таблиц.
```sql
SELECT 
    l.name AS language
FROM 
    language l
LEFT JOIN 
    film f ON l.language_id = f.language_id
WHERE 
    f.language_id IS NULL
ORDER BY 
    l.name;
```
- Извлечь имя и домен из адресов электронной почты клиентов в базе данных Sakila. Написать запрос, возвращающий три столбца: email, address – часть адреса электронной почты перед знаком «@» и domain — часть после «@». Отсортировать результат по полю email.
```sql
SELECT
email,
SUBSTRING_INDEX(email, '@', 1) AS address,
SUBSTRING_INDEX(email, '@', -1) AS domain
FROM
sakila.customer
ORDER BY
email
```
- Получить определения столбцов таблицы address.
```sql
SHOW COLUMNS FROM address
```  
- Получить список индексов таблицы film и их определений.
```sql
SHOW INDEX from film;
```
- Найти клиентов которые встречали друг друга в одном из пунктов проката. Вывести таблицу с полями meet_time - согласно времени аренды, store_id, customers список встречавшихся клиентов в формате JOHN SHOW,DAENERYS TARGARYEN - в порядке их фамилий. Результирующую таблицу отсортируйте по времени встречи и номеру пункта проката
(Клиенты встречались если брали в аренду фильмы в одном отделении в одно время.)
```sql
SELECT 
    r.rental_date AS meet_time,
    s.store_id,
    GROUP_CONCAT(CONCAT(c.first_name, ' ', c.last_name) ORDER BY c.last_name SEPARATOR ', ') AS customers
FROM 
    rental r
JOIN 
    customer c ON r.customer_id = c.customer_id
JOIN 
    staff s ON r.staff_id = s.staff_id
GROUP BY 
    r.rental_date, s.store_id
HAVING 
    COUNT(c.customer_id) > 1
ORDER BY 
    meet_time, store_id;
```
- Найти клиентов чьё имя является фамилией другого клиента. Вывести таблицу с полями customer_id, first_name, last_name для первого клиента и такие же поля customer_id, first_name, last_name для второго. Отсортиь по customer_id первого клиента.
```sql
SELECT
c1.customer_id, c1.first_name, c1.last_name,
c2.customer_id, c2.first_name, c2.last_name
FROM
customer c1
JOIN
customer c2 ON c1.first_name = c2.last_name
ORDER BY
c1.customer_id
```
