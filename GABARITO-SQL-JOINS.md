# Gabarito

### Resolução exercicios de fixação 1
* Faça uma query que busque os nomes dos usuários na tabela 'users' e busque também o plano de cada usuário e o valor do plano de cada usuário.

  Resolução:

      SELECT u.user, p.plan, p.value_plan FROM users AS u
      INNER JOIN plans AS p
      ON u.plan_id = p.plan_id;

### Resolução exercicios de fixação 2
* Faça uma query que busque todos os dados da tabela 'users' e busque os dados correspondentes da tabela 'followers' pelo campo 'user_id'. 

  Resolução:

      SELECT * FROM users AS u
      LEFT JOIN followers AS f
      ON u.user_id = f.artist;

### Resolução exercicios de fixação 3
* Faça uma query que busque todos os dados da tabela 'followers' e busque os dados correspondentes da tabela 'users' pelo campo 'user_id'.

  Resolução:

      SELECT * FROM followers AS f
      LEFT JOIN users AS u
      ON u.user_id = f.artist;

### Resolução exercicios de fixação 4
* Faça uma query utilizando o SELF JOIN, busque na tabela albums campos album_id e artist_id que possuem correspondência.

  Resolução:

      SELECT alid.album_id, arid.artist_id FROM albums AS alid
      INNER JOIN albums AS arid
      ON alid.album_id = arid.artist_id;

### Resolução exercicios agora a pratica 1
* Exercício 1: faça uma query e utilize o INNER JOIN, busque as cidades na tabela city e busque localizações referentes a essas cidades na
tabela address.

  Resolução:

      SELECT c.city, a.location FROM address AS a
      INNER JOIN city AS c
      ON a.city_id = c.city_id;

### Resolução exercicios agora a pratica 2
* Exercício 2: faça uma query e utilize o INNER JOIN, busque as cidades na tabela city, busque localizações referentes a essas cidades na
tabela address e busque também os países em que essas cidades estão.

  Resolução:
   
      SELECT c.city, a.location, co.country FROM address AS a
      INNER JOIN city AS c
      ON a.city_id = c.city_id
      INNER JOIN country AS co
      ON c.country_id = co.country_id;

### Resolução exercicios agora a pratica 3
* Exercício 3: faça uma query e utilize o LEFT JOIN, busque todos os valores em 'language_id' e 'name' na tabela language
e busque também os nomes de filmes na tabela filme que estejam nesse idioma.

  Resolução:

      SELECT l.language_id, l.name, f.title FROM language AS l
      LEFT JOIN film AS f
      ON l.language_id = f.language_id;

### Resolução exercicios agora a pratica 4
* Exercício bônus: faça uma query que busque o nome de todos os filmes na tabela film e a categoria que cada filme na tabela 
category.

  Resolução:

      SELECT f.title, a.first_name FROM film AS f
      RIGHT JOIN film_actor AS fa
      ON f.film_id = fa.actor_id
      INNER JOIN actor AS a
      ON fa.actor_id = a.actor_id

### Resolução exercicios agora a pratica 5
* Exercício 5: Faça uma query utilizando o SELF JOIN, busque na tabela city campos city_id e country_id que possuem correspondência.

    Resolução:

      SELECT cii.city_id, coi.country_id FROM city AS cii
      INNER JOIN city AS coi
      ON cii.city_id = coi.country_id

### Resolução exercicios agora a pratica 6
* Exercício 6: Faça uma query que busque todos os campos 'first_name' da tabela staff e apenas os campos 'first_name' correspondentes da 
tabela actor.

    Resolução:

      SELECT a.first_name, s.first_name FROM staff AS a
      LEFT JOIN actor AS s
      ON a.first_name = s.first_name;

### Resolução exercicios agora a pratica 7
* Exercício 7: Faça uma query que busque os campos 'staff_id', 'first_name' e 'last_name' na tabela staff, busque também o campo 'rental_date' na tabela rental que tenha correspondência com esse staff e busque também o campo 'amount' na tabela payment que tenha correspondência com esse rental.

    Resolução:

      SELECT 
        s.staff_id, 
        s.first_name, 
        s.last_name,  
        p.amount, 
        r.rental_date 
      FROM staff AS s
        INNER JOIN rental AS r
          ON s.staff_id = r.staff_id
        INNER JOIN payment AS p
          ON r.rental_id = p.rental_id; 

### Resolução de exercicios bônus
* Exercicio bônus: faça uma query que busque o nome de todos os filmes na tabela film e a categoria que cada filme na tabela 
category 

  Resolução:
  
      SELECT f.title, c.name FROM film AS f
      INNER JOIN film_category AS fc
      ON f.film_id = fc.film_id
      INNER JOIN category AS c
      ON fc.category_id = c.category_id;

