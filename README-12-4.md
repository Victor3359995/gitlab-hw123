# Домашнее задание к занятию «SQL. Часть 2» Важинский В

Задание можно выполнить как в любом IDE, так и в командной строке.

### Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию: 
- фамилия и имя сотрудника из этого магазина;
- город нахождения магазина;
- количество пользователей, закреплённых в этом магазине.

```sql2
SELECT CONCAT_WS(" ", staff.first_name, staff.last_name) AS employee, city.city AS town, COUNT(customer.customer_id) AS customer_count
FROM store
JOIN staff ON store.store_id = staff.store_id
JOIN customer ON store.store_id = customer.store_id
JOIN address ON store.address_id = address.address_id
JOIN city ON address.city_id = city.city_id
GROUP BY employee, town
HAVING customer_count > 300; 
```
![sql2](./img/db5.png)

### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

```sql2
SELECT COUNT(film_id) FROM film WHERE length > (SELECT AVG(length) FROM film);
```
![sql2](./img/db6.png)

### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

```sql2
SELECT SUM(payment.amount) as sum_of_payments, DATE_FORMAT(payment.payment_date, '%m.%Y') AS month_of_payments, COUNT(payment.rental_id) AS rental_count
FROM payment
GROUP BY month_of_payments
ORDER BY sum_of_payments DESC
LIMIT 1;
```
![sql2](./img/db7.png)

### Задание 4*

Посчитайте количество продаж, выполненных каждым продавцом. Добавьте вычисляемую колонку «Премия». Если количество продаж превышает 8000, то значение в колонке будет «Да», иначе должно быть значение «Нет».

```sql2
SELECT CONCAT_WS(" ", staff.first_name, staff.last_name) as employee, COUNT(payment.payment_id) AS employee_sales, 
CASE
WHEN COUNT(payment.payment_id) > 8000 
THEN 'Yes'
ELSE 'No'
END AS 'bonus_payment'
FROM payment
JOIN staff ON payment.staff_id = staff.staff_id
GROUP BY employee;
```
![sql2](./img/db8.png)

### Задание 5*

Найдите фильмы, которые ни разу не брали в аренду.

```sql2
SELECT film.film_id, film.title, rental.rental_id
FROM film
LEFT JOIN inventory ON film.film_id = inventory.film_id
LEFT JOIN rental ON inventory.inventory_id = rental.inventory_id
WHERE rental.rental_id IS NULL;
```
![sql2](./img/db9.png)
