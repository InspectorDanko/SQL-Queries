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
