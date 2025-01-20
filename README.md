# Домашнее задание к занятию "`SQL. Часть 2`" - `Марченко Вячеслав Игоревич`

### Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию:

- фамилия и имя сотрудника из этого магазина;
- город нахождения магазина;
- количество пользователей, закреплённых в этом магазине.


### Ответ

1. ![Task1](https://github.com/Takarigua/sys-pattern-homework12-04/blob/01a640f27be8789ba41e0a6cfc1d6260d1e1efdd/img/Task%201.png)

```
SELECT 
    CONCAT(staff.last_name, ' ', staff.first_name) AS full_name, 
    city.city, 
    COUNT(customer.customer_id) AS customer_count
FROM 
    store
JOIN 
    staff ON store.store_id = staff.store_id
JOIN 
    address ON store.address_id = address.address_id
JOIN 
    city ON address.city_id = city.city_id
JOIN 
    customer ON store.store_id = customer.store_id
GROUP BY 
    store.store_id, staff.staff_id, city.city
HAVING 
    COUNT(customer.customer_id) > 300;
```
---

### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

### Ответ

1. ![Task 2](https://github.com/Takarigua/sys-pattern-homework12-04/blob/e9045dd3c3557d63af10f8e5689e93fdc8df4e32/img/Task%202.png)


```
SELECT 
    COUNT(*) AS film_count
FROM 
    film
WHERE 
    length > (SELECT AVG(length) FROM film);
```
---

### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

### Ответ

1. ![Task 3](https://github.com/Takarigua/sys-pattern-homework12-04/blob/732794c122eb4c3266df2144fe771f110d331e86/img/Task%203.png)

```
SELECT 
    DATE_FORMAT(payment_date, '%Y-%m') AS month, 
    SUM(amount) AS total_payments, 
    COUNT(rental_id) AS rental_count
FROM 
    payment
GROUP BY 
    month
ORDER BY 
    total_payments DESC
LIMIT 1;
```
