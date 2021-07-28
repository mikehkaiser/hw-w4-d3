-- Question 1 
-- List all customers who live in Texas with Joins.
-- Customer to address via address_id 

-- Join version
SELECT customer_id, first_name, last_name, district
FROM customer
JOIN address
ON customer.address_id = address.address_id
WHERE address.district = 'Texas';

-- Subquery version
SELECT customer_id, first_name, last_name
FROM customer
WHERE address_id IN(
	SELECT address_id
	FROM address
	WHERE district = 'Texas'
);

-- Question 2
-- Provide first_name, last_name for all payments above $6.99
SELECT first_name, last_name
FROM customer
JOIN payment
ON customer.customer_id = payment.customer_id
WHERE amount > 6.99;


-- Subquery does not return proper results

-- Question 3
-- 3. Show all customers names who have made payments over $175 (use subqueries)

SELECT first_name, last_name
FROM customer
WHERE customer_id IN(
	SELECT customer_id
	FROM payment
	GROUP BY customer_id
	HAVING SUM(amount) > 175
);

-- join method
SELECT customer.customer_id, first_name, last_name, SUM(amount)
FROM customer
JOIN payment
ON customer.customer_id = payment.customer_id
GROUP BY customer.customer_id
HAVING SUM(amount) > 175;

-- Question 4
-- List all customers who live in Nepal
SELECT customer_id, first_name, last_name, country
FROM customer
JOIN address
ON customer.address_id = address.address_id
JOIN city
ON address.city_id = city.city_id
JOIN country
ON city.country_id = country.country_id
WHERE country = 'Nepal';

-- Question 5
-- Which staff member had the most transactions 
-- If 'transaction' only equals those occurences where money was exchanged, staff_id 2 (Jon Stephens) has more
SELECT staff.staff_id, first_name, last_name, COUNT(payment_id)
FROM staff
JOIN payment
ON staff.staff_id = payment.staff_id
GROUP BY staff.staff_id
ORDER BY COUNT(payment_id) DESC;

-- Considering free rentals as a transaction
-- If a rental is a transaction, staff_id 1 (Mike Hillyer) has more
SELECT staff.staff_id, first_name, last_name, COUNT(rental_id)
FROM staff
JOIN rental
ON staff.staff_id = rental.staff_id
GROUP BY staff.staff_id
ORDER BY COUNT(rental_id) DESC

-- Question 6
-- How many movies of each rating are there?
SELECT rating, COUNT(rating)
FROM film
GROUP BY rating
ORDER BY COUNT(rating) ASC

-- Question 7
-- Show all customers who have made a single payment above $6.99 (Use Subqueries)
-- looks for just a single instance of a payment > 7.99
SELECT customer_id, first_name, last_name
FROM customer
WHERE customer_id IN(
	SELECT customer_id
	FROM payment
	WHERE amount > 6.99
	GROUP BY customer_id
	HAVING COUNT(payment_id) = 1
)

-- Question 8
-- How many free rentals did our stores giveaway?
-- count rental/payment_id/amount from payment where amount = 0.00
-- 24 rows returned
SELECT COUNT(rental_id)
FROM payment
WHERE amount = 0.00 -- I don't think this is right

-- or join on rental_id where there is not a payment_id
-- 1452 rentals that do not have a payment id
SELECT COUNT(rental.rental_id)
FROM rental
LEFT JOIN payment
ON rental.rental_id = payment.rental_id
WHERE payment.payment_id IS NULL
