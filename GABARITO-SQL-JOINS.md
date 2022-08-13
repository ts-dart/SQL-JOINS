Resolução exercicios de fiação um
SELECT u.user, p.plan, p.value_plan FROM users AS u
INNER JOIN plans AS p
ON u.plan_id = p.plan_id;

Resolução exercicios de fiação dois
SELECT * FROM users AS u
LEFT JOIN followers AS f
ON u.user_id = f.artist;

Resolução exercicios de fiação tres
SELECT * FROM followers AS f
LEFT JOIN users AS u
ON u.user_id = f.artist;

AGORA A PRATICA EXERCICIO 1:
SELECT c.city, a.location FROM address AS a
INNER JOIN city AS c
ON a.city_id = c.city_id;

AGORA A PRATICA EXERCICIO 2:
SELECT c.city, a.location, co.country FROM address AS a
INNER JOIN city AS c
ON a.city_id = c.city_id
INNER JOIN country AS co
ON c.country_id = co.country_id;
