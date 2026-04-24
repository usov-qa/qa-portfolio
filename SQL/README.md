# Проект 6: SQL-запросы к базе данных стартапов

Учебный проект в Яндекс Практикуме. Писал SQL-запросы для анализа данных о компаниях, инвестициях и сотрудниках.

## Моя работа
- Анализировал данные о компаниях, фондах и сделках
- Использовал агрегатные функции, JOIN, группировку и фильтрацию
- Работал с датами и условиями отбора через HAVING

Инструменты  
SQL, PostgreSQL

## Структура базы данных

- `company` — компании (id, название, страна, категория, сумма инвестиций, статус)
- `people` — сотрудники (id, имя, фамилия, никнейм)
- `education` — образование (id сотрудника, учебное заведение)
- `acquisition` — сделки (сумма, дата, тип оплаты)
- `fund` — фонды (страна, дата основания, количество инвестированных компаний)

## Задачи и решения

1. Количество закрытых компаний  

Нужно было посчитать, сколько компаний прекратили работу (статус 'closed').

```sql
SELECT COUNT(status)
FROM company
WHERE status = 'closed';
```
2. Привлечённые средства новостных компаний США

Нужно было вывести сумму привлечённых инвестиций для американских компаний из категории новостей, отсортировав по убыванию.

```sql
SELECT funding_total
FROM company
WHERE country_code = 'USA' AND category_code = 'news'
ORDER BY funding_total DESC;
```
3. Люди с ником, начинающимся на 'Silver'

Нужно было найти имя, фамилию и никнейм людей, у которых network_username начинается на 'Silver'.

```sql
SELECT first_name, last_name, network_username
FROM people
WHERE network_username LIKE 'Silver%';
```
4. Люди с 'money' в нике и фамилией на 'K'

Нужно было вывести всю информацию о людях, у которых никнейм содержит 'money', а фамилия начинается на 'K'.

```sql
SELECT *
FROM people
WHERE network_username LIKE '%money%'
  AND last_name LIKE 'K%';
```
5. Общая сумма инвестиций по странам

Нужно было для каждой страны посчитать общий объём инвестиций, которые получили местные компании, и отсортировать по убыванию.

```sql
SELECT country_code, SUM(funding_total)
FROM company
GROUP BY country_code
ORDER BY SUM(funding_total) DESC;
```
6. Сотрудники стартапов с учебными заведениями

Нужно было вывести имя и фамилию сотрудников, а также учебное заведение (если известно). Здесь я использовал LEFT JOIN, чтобы не потерять сотрудников без записи об образовании.

```sql
SELECT first_name, last_name, institution
FROM people AS p
LEFT OUTER JOIN education AS e ON p.id = e.person_id;
```
7. Сделки за наличные с 2011 по 2013 год

Нужно было посчитать общую сумму сделок по приобретению компаний за наличные в период с 2011 по 2013 год включительно.

```sql
SELECT SUM(price_amount)
FROM acquisition
WHERE acquired_at BETWEEN '2011-01-01' AND '2013-12-31'
  AND term_code = 'cash';
```
8. Страны с самыми активными фондами-инвесторами

Нужно было найти страны, чьи фонды (основанные с 2010 по 2012 год) инвестируют чаще всего. Для каждой страны я посчитал минимальное, максимальное и среднее число компаний, в которые инвестировали фонды. Исключил страны с нулевым минимумом. Отсортировал по среднему количеству компаний от большего к меньшему, затем по коду страны. Вывел топ-10.

```sql
SELECT f.country_code,
       MIN(f.invested_companies),
       MAX(f.invested_companies),
       AVG(f.invested_companies)
FROM fund AS f
WHERE f.founded_at BETWEEN '2010-01-01' AND '2012-12-31'
GROUP BY f.country_code
HAVING MIN(f.invested_companies) > 0
ORDER BY AVG(f.invested_companies) DESC, country_code ASC
LIMIT 10;
```
