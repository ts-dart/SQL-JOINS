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
