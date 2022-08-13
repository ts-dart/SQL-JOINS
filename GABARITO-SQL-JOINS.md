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

### Entendendo o FULL JOIN
  Agora você vai estudar o FULL JOIN, o metodo de junção FULL JOIN e mais ou menos a mesma coisa
  que os metodos LEFT JOIN e RIGHT JOIN, novamente a diferença esta no foco, o FULL JOIN busca todos 
  os valores em ambas tabelas, para os valores que não possuem correspondencia e retornado um NULL.
  Veja essa representação abaixo:

  <img height="210px" width="320px" src="https://cdn.pixabay.com/photo/2022/08/13/19/59/sql-7384369_960_720.jpg" alt="">

  #### Exemplo
  No exemplo a seguir perceba que a sintaxe e bem semelhante aos demais metodos,
  no exemplo a seguir, nos estamos fazendo uma query 

    SELECT u.user_id, h.song_id, h.reproduction_date FROM users AS u
    LEFT JOIN history AS h
    ON u.user_id = h.user_id;