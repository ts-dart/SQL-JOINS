# Gabarito

### Resolução exercicios de fixação 1
  SELECT u.user, p.plan, p.value_plan FROM users AS u
  INNER JOIN plans AS p
  ON u.plan_id = p.plan_id;

### Resolução exercicios de fixação 2
  SELECT * FROM users AS u
  LEFT JOIN followers AS f
  ON u.user_id = f.artist;

### Resolução exercicios de fixação 3
  SELECT * FROM followers AS f
  LEFT JOIN users AS u
  ON u.user_id = f.artist;

### Resolução exercicios agora a pratica 1
  SELECT c.city, a.location FROM address AS a
  INNER JOIN city AS c
  ON a.city_id = c.city_id;

### Resolução exercicios agora a pratica 2
  SELECT c.city, a.location, co.country FROM address AS a
  INNER JOIN city AS c
  ON a.city_id = c.city_id
  INNER JOIN country AS co
  ON c.country_id = co.country_id;

### Resolução exercicios agora a pratica 3
  SELECT l.language_id, l.name, f.title FROM language AS l
  LEFT JOIN film AS f
  ON l.language_id = f.language_id;

### Resolução exercicios agora a pratica 4
    SELECT f.title, a.first_name FROM film AS f
    RIGHT JOIN film_actor AS fa
    ON f.film_id = fa.actor_id
    INNER JOIN actor AS a
    ON fa.actor_id = a.actor_id