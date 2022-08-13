# JOINs o que são, o que comem, onde vivem?
## O que vamos aprender?
Hoje você vai estudar um conteúdo muito importante para avançar no seu
aprendizado de SQL, hoje aprenderemos sobre SQL JOINs, no dia de hoje você vai estudar,
alguns dos JOINs mais utilizados no dia dia de uma pessoa desenvolvedora, o JOIN e 
uma cláusula muito importante dentro da linguagem sql, essa cláusula é usada para operações
cujo objetivo é juntar colunas de diferentes tabelas, possibilitando que vocè
escreva querys mais sofisticadas e complexas que atendam melhor a um determinado
objetivo. Existem diferentes tipos de JOINs sendo eles os mais comuns:

* INNER JOIN: faz uma junção retornando valores de diferentes tabelas 
  correspondente a condição.

* RIGHT JOIN: faz uma junção retornado os valores da tabela à esquerda e retornando
  os valores correspondentes a condição da tabela à direita.

* LEFT JOIN: faz uma junção retornado os valores da tabela à direita e retornando
  os valores correspondentes a condição da tabela à esquerda.

Não se preocupe, pode parecer complicado mas é mais simples do que parece :stuck_out_tongue_winking_eye:, e no
dia de hoje vamos estudar a fundo esse assunto para que você possa aperfeçoar seu conhecimento
em SQL, vamos nessa? :rocket::rocket:

### Você será capaz de:
Com o conteúdo de hoje você será capaz de usar INNER JOIN, RIGTH JOIN, LEFT JOIN,
FULL JOIN E CROSS JOIN em suas querys

## Porque isso é importante?
Os JOINs dentro da linguaguem SQL, são uma ferramenta de suma iportancia que 
todo dev que trabalha com SQL precisa ter em sua caixa de ferramentas! os Joins 
tem como função, juntar dados de acordo com condições especificas e são fundamentais
na escrita de querys, quando se precisa buscar dados em mais de uma tabela, dada sua importancia 
vamos com tudo para o conteudo de hoje. :books: 

<img src="https://media4.giphy.com/media/J4JSpIwM6y3Q6xnHgg/200.webp?cid=ecf05e47dngwjz1ezw618lkzhkti3msp24vvocxexjr32crf&rid=200.webp&ct=g" alt="Um gif mostrando uma mão saindo de um monitor de computador antigo branco e uma mulher apertando essa mão que sai da tela do computador">
  
## Conteúdos

  ### Criando nossa base de dados
  Antes de começarmos a ver o conteúdo de hoje nós vamos criar um banco de dados,
  nós usaremos esse banco durante o dia de hoje em momentos onde você colocará a mão 
  no código, por isso vamos colocar a mão na massa.
 

  <img height="200px" width="200px" src="https://media0.giphy.com/media/o0vwzuFwCGAFO/200w.webp?cid=ecf05e47o5dmmlcgmouwv0vyvxnai024lw3y4in5ugkoccqg&rid=200w.webp&ct=g" alt="">

  O código SQL abaixo cria uma base de dados, copie o código abaixo e cole no seu
  Workbench, execute o código para criar a base de dados.

    CREATE DATABASE IF NOT EXISTS SpotifyClone;
    USE SpotifyClone;

    CREATE TABLE plans (
      plan_id INTEGER NOT NULL,
      plan VARCHAR(100) NOT NULL,
      value_plan DOUBLE NOT NULL,
      CONSTRAINT PRIMARY KEY(plan_id)
    );

    INSERT INTO plans(plan_id, plan, value_plan)
    VALUES 
      (1, 'gratuito', 0),
      (2, 'familiar', 7.99),
      (3, 'universitario', 5.99),
      (4, 'pessoal', 6.99);

    CREATE TABLE artists (
      artist_id INTEGER NOT NULL AUTO_INCREMENT,
      artist VARCHAR(100) NOT NULL,
      CONSTRAINT PRIMARY KEY(artist_id)
    );

    INSERT INTO artists(artist_id, artist)
    VALUES
      (1,	'Walter Phoenix'),
      (2,	'Peter Strong'),
      (3,	'Lance Day'),
      (4,	'Freedie Shannon'),
      (5,	'Tyler Isle'),
      (6,	'Fog');

    CREATE TABLE users(
      user_id INTEGER NOT NULL AUTO_INCREMENT,
      user VARCHAR(100) NOT NULL,
      age INTEGER NOT NULL,
      plan_id INTEGER NOT NULL,
      signature_date DATE NOT NULL,
      CONSTRAINT PRIMARY KEY(user_id),
      FOREIGN KEY (plan_id) REFERENCES plans (plan_id)
    );

    INSERT INTO users (user_id, user, age, plan_id, signature_date)
    VALUES
      (1,	'Thati',	23,	1,	'2019-10-20'),
      (2,	'Cintia',	35,	2,	'2017-12-30'),
      (3,	'Bill',	20,	3,	'2019-06-05'),
      (4,	'Roger',	45,	4,	'2020-05-13'),
      (5,	'Norman',	58,	4,	'2017-02-17'),
      (6,	'Patrick',	33,	2,	'2017-01-06'),
      (7,	'Vivian',	26,	3,	'2018-01-05'),
      (8,	'Carol',	19,	3,	'2018-02-14'),
      (9,	'Angelina',	42,	2,	'2018-04-29'),
      (10, 'Paul',	46,	2,	'2017-01-17');

    CREATE TABLE albums(
      album_id INTEGER NOT NULL AUTO_INCREMENT PRIMARY KEY,
      album VARCHAR(100) NOT NULL,
      artist_id INTEGER NOT NULL,
      release_date YEAR NOT NULL,
      FOREIGN KEY (artist_id) REFERENCES artists (artist_id)
    );

    INSERT INTO albums (album_id, album, artist_id, release_date)
    VALUES
      (1,	'Envious',	1,	1990),
      (2,	'Exuberant',	1,	1993),
      (3,	'Hallowed Steam',	2,	1995),
      (4,	'Incandescent',	3,	1998),
      (5,	'Temporary Culture',	4,	2001),
      (6,	'Library of liberty',	4,	2003),
      (7,	'Chained Down',	5,	2007),
      (8,	'Cabinet of fools',	5,	2012),
      (9,	'No guarantees',	5,	2015),
      (10, 'Apparatus',	6,	2015);

    CREATE TABLE followers(
      id INTEGER NOT NULL AUTO_INCREMENT,
      user_id INTEGER NOT NULL,
      artist_id INTEGER NOT NULL,
      CONSTRAINT PRIMARY KEY(id, user_id),
      FOREIGN KEY (user_id) REFERENCES users(user_id),
      FOREIGN KEY (artist_id) REFERENCES artists (artist_id)
    );

    INSERT INTO followers (id, user_id, artist_id)
    VALUES
      (1,	1, 1),
      (2,	1, 4),
      (3,	1, 3),
      (4,	2, 1),
      (5,	2, 3),
      (6,	3, 2),
      (7,	3, 1),
      (8,	4, 4),
      (9,	5, 5),
      (10, 5,	6),
      (12, 6,	6),
      (13, 6,	3),
      (14, 6,	1),
      (15, 7,	2),
      (16, 7,	5),
      (17, 8,	1),
      (18, 8,	5),
      (19, 9,	6),
      (20, 9,	4),
      (21, 9,	3),
      (22, 10, 2),
      (23, 10, 6);

    CREATE TABLE songs(
      song_id INTEGER NOT NULL AUTO_INCREMENT PRIMARY KEY,
      song VARCHAR(100) NOT NULL,
      duration_seconds INTEGER NOT NULL,
      album_id INTEGER NOT NULL,
      FOREIGN KEY (album_id) REFERENCES albums (album_id)
    );

    INSERT INTO songs (song_id, song, duration_seconds, album_id)
    VALUES
      (1,	'Soul For Us', 200,	1),
      (2,	'Reflections Of Magic',	163,	1),
      (3,	'Dance With Her Own',	116,	1),
      (4,	'Troubles Of My Inner Fire',	203,	2),
      (5,	'Time Fireworks',	152,	2),
      (6,	'Magic Circus',	105,	3),
      (7,	'Honey, So Do I',	207,	3),
      (8,	"Sweetie, Let's Go Wild",	139,	3),
      (9,	'She Knows',	244,	3),
      (10, 'Fantasy For Me',	100,	4),
      (11, 'Celebration Of More',	146,	4),
      (12, 'Rock His Everything',	223,	4),
      (13, 'Home Forever',	231,	4),
      (14, 'Diamond Power',	241,	4),
      (15, "Let's Be Silly",	132,	4),
      (16, 'Thang Of Thunder',	240,	5),
      (17, 'Words Of Her Life',	185,	5),
      (18, 'Without My Streets',	176,	5),
      (19, 'Need Of The Evening',	190,	6),
      (20, 'History Of My Roses',	222,	6),
      (21, 'Without My Love',	111,	6),
      (22, 'Walking And Game',	123,	6),
      (23, 'Young And Father',	197,	6),
      (24, 'Finding My Traditions',	179,	7),
      (25, 'Walking And Man',	229,	7),
      (26, 'Hard And Time',	135,	7),
      (27, "Honey, I'm A Lone Wolf",	150,	7),
      (28, "She Thinks I Won't Stay Tonight",	166,	8), 
      (29, "He Heard You're Bad For Me",	154,	8), 
      (30, "He Hopes We Can't Stay",	210,	8), 
      (31, 'I Know I Know',	117,	8),
      (32, "He's Walking Away",	159,	9),
      (33, "He's Trouble",	138,	9), 
      (34, 'I Heard I Want To Bo Alone',	120,	9),
      (35, 'I Ride Alone',	151,	9),
      (36, 'Honey',	79,	10),
      (37, 'You Cheated On Me',	95,	10),
      (38, "Wouldn't It Be Nice",	213,	10),
      (39, 'Baby',	136,	10),
      (40, 'You Make Me Feel So..',	83,	10);

    CREATE TABLE history(
      id INTEGER NOT NULL AUTO_INCREMENT,
      song_id INTEGER NOT NULL,
      reproduction_date DATETIME NOT NULL,
      user_id INTEGER NOT NULL,
      CONSTRAINT PRIMARY KEY(id, song_id),
      FOREIGN KEY (song_id) REFERENCES songs (song_id),
      FOREIGN KEY (user_id) REFERENCES users (user_id)
    );

    INSERT INTO history (id, song_id, reproduction_date, user_id)
    VALUES
      (1,	36,	'2020-02-28 10:45:55',	1),
      (2,	25,	'2020-05-02 05:30:35',	1),
      (3,	23,	'2020-03-06 11:22:33',	1),
      (4,	14,	'2020-08-05 08:05:17',	1),
      (5,	15,	'2020-09-14 16:32:22',	1),
      (6,	34,	'2020-01-02 07:40:33',	2),
      (7,	24,	'2020-05-16 06:16:22',	2),
      (8,	21,	'2020-10-09 12:27:48',	2),
      (9,	39,	'2020-09-21 13:14:46',	2),
      (10,	6,	'2020-11-13 16:55:13',	3),
      (11,	3,	'2020-12-05 18:38:30',	3),
      (12,	26,	'2020-07-30 10:00:00',	3),
      (13,	2,	'2021-08-15 17:10:10',	4),
      (14,	35,	'2021-07-10 15:20:30',	4),
      (15,	27,	'2021-01-09 01:44:33',	4),
      (16,	7,	'2020-07-03 19:33:28',	5),
      (17,	12,	'2017-02-24 21:14:22',	5),
      (18,	14,	'2020-08-06 15:23:43',	5),
      (19,	1,	'2020-11-10 13:52:27',	5),
      (20,	38,	'2019-02-07 20:33:48',	6),
      (21,	29,	'2017-01-24 00:31:17',	6),
      (22,	30,	'2017-10-12 12:35:20',	6),
      (23,	22,	'2018-05-29 14:56:41',	6),
      (24,	5,	'2018-05-09 22:30:49',	7),
      (25,	4,	'2020-07-27 12:52:58',	7),
      (26,	11,	'2018-01-16 18:40:43',	7),
      (27,	39,	'2018-03-21 16:56:40',	8),
      (28,	40,	'2020-10-18 13:38:05',	8),
      (29,	32,	'2019-05-25 08:14:03',	8),
      (30,	33,	'2021-08-15 21:37:09',	8),
      (31,	16,	'2021-05-24 17:23:45',	9),
      (32,	17,	'2018-12-07 22:48:52',	9),
      (33,	8,	'2021-03-14 06:14:26',	9),
      (34,	9,	'2020-04-01 03:36:00',	9),
      (35,	20,	'2017-02-06 08:21:34',	10),
      (36,	21,	'2017-12-04 05:33:43',	10),
      (37,	12,	'2017-07-27 05:24:49',	10),
      (38,	13,	'2017-12-25 01:03:57',	10);

    Agora com a nossa base de dados que será usada em exemplos criada podemos 
    prosseguir com o conteúdo

  ### Entendendo o INNER JOIN
  Dentro dos métodos de junção o INNER JOIN talvez seja um dos mais utilizados,
  o que INNER JOIN faz é juntar os valores de diferentes tabelas se esses valores estiverem
  relacionados. Veja essa representação abaixo:

  <img height="210px" width="320px" src="https://cdn.pixabay.com/photo/2022/08/12/17/14/sql-7382120_960_720.jpg" alt="">

  #### Sintaxe
  Agora nós veremos a sintaxe. No exemplo a seguir, nós vemos um código, uma query SQL 
  que utiliza o INNER JOIN.

    SELECT * FROM tabela-a AS a
    INNER JOIN tabela-b AS b
    ON a.coluna = b.coluna;

  Esse código SQL utiliza o INNER JOIN e faz uma query em um banco fictício, ele
  busca todas as colunas da tabela 'a' e busca também todas as colunas da tabela 'b', 
  desde que essas colunas satisfação a condição estabelecida pela cláusula ON, satisfeita
  A condição da cláusula ON a query retorna uma representação das tabelas 'a' e 'b' unidas.

  #### Exemplo 
  No exemplo a seguir nós vamos usar a base de dados criado anteriormente, nós vamos
  fazer uma query, que vai buscar os nomes dos artistas na tabela artistas e vai buscar
  também o nome dos álbuns que esse artista possui, na tabela álbuns. Copie e cole o codigo abaixo no 
  seu Worckench e veja o que essa query te retorna! O código ficaria assim:

    SELECT a.artist, al.album FROM artists AS a
    INNER JOIN albums AS al
    ON a.artist_id = al.artist_id

  Também é possível acrescentar um outro join em nossa query, para buscarmos também
  as músicas pertencentes a cada álbum. Copie e cole o codigo abaixo no 
  seu Worckench e veja o que essa query te retorna! O código ficaria assim:

    SELECT a.artist, al.album, s.song FROM artists AS a
    INNER JOIN albums AS al
    ON a.artist_id = al.artist_id
    INNER JOIN songs AS s
    ON al.album_id = s.album_id;

  #### O que e esse AS no codigo?
  O comando AS e um acrônimo para aliases, uma palavra em inglês que pode ser traduzida 
  para apelido em portugues, é exatamente isso que esse comando faz em nossa query, ele dá
  um apelido para a tabela, o comando AS renomeia temporariamente uma tabela, 
  isso existe como uma forma organizar melhor a query e prevenir erros. Copie e cole o codigo 
  abaixo no seu Worckench e veja o que essa query te retorna! Um código sem
  o comando AS ficaria assim:

    SELECT artist, album, song FROM artists
    INNER JOIN albums
    ON artist_id = artist_id
    INNER JOIN songs
    ON album_id = album_id;

  Essa query falharia e retornaria o seguinte erro:

    Column 'album_id' in on clause is ambiguous

  Esse erro ocorre porque na última linha, no comando ON ele encontra duas vezes 
  'album_id' e não consegue diferenciar de qual tabela eles estão vindo.

  #### Exercícios de fixação
  * Faça uma query que busque os nomes dos usuários na tabela 'users' e busque também
  o plano de cada usuário e o valor do plano de cada usuário.

  ### Entendendo o LEFT JOIN
  Outro metodo muito utilizado para fazer a união entre tabelas e o metodo LEFT JOIN,
  o LEFT JOIN não e muito difetente do INNER JOIN, enquanto o INNER JOIN busca apenas
  os valores correspondentes, o LEFT JOIN tem seu foco na tabela
  a esquerda, retornando todos os dados presentes na tabela a esquerda, e retornando da tabela 
  a direita apenas os dados que possuem correspondencia, caso não exista dado correspondente
  e retornado um NULL. Veja essa representação abaixo:

  <img height="210px" width="320px" src="https://cdn.pixabay.com/photo/2022/08/12/22/51/sql-7382584_960_720.jpg" alt="">

  #### Sintaxe
  Agora nós veremos a sintaxe do LEFT JOIN, analise a query a seguir e perçeba as
  semelhanas que existem com o INNER JOIN

    SELECT * FROM tabela1 AS t1
    LEFT JOIN tabela2 AS t2
    ON t1.coluna = t2.coluna;

  A sintaxe do LEFT JOIN e praticamente a mesma do INNER JOIN, a mudança esta no foco,
  a query de exemplo acima faz uma busca em uma base de dados ficticia, ela busca todos 
  os valores da 'tabela1' que e a tabela que está a esquerda, e busca apenas os valores 
  que possuem correspondencia na 'tabela2' que e a tabela que está a direita.

  #### Exemplo
  No exemplo a seguir, nos temos uma query que busca todos os valores da tabela 'artistas'
  e busca apenas os valores correspondentes na tabela 'albums'. Copie e cole o codigo abaixo no 
  seu Worckench e veja o que essa query te retorna! O código ficaria assim:

    SELECT * FROM artists AS a
    LEFT JOIN albums AS al
    ON a.artist_id = al.artist_id

  Legal né? agora esta na hora de colocar a mão no teclado e praticar um pouco mais.

  #### Exercícios de fixação
  * Faça uma query que busque todos os dados da tabela 'users' e busque os dados correspondentes 
    da tabela 'followers' pelo campo 'user_id'.  

  ### Entendendo o RIGTH JOIN
  Agora você vai estudar o RIGTH JOIN, o RIGTH JOIN faz exatamente a mesma coisa
  que o LEFT JOIN, a unica mudança e o foco ele busca todos os valores da tabela a direita
  e busca apenas os valores correspondentes da tabela a esquerda, ao contrario do que faz 
  o LEFT JOIN. Veja essa representação abaixo:

  <img height="210px" width="320px" src="https://cdn.pixabay.com/photo/2022/08/13/01/10/sql-7382703_960_720.jpg" alt="">

  #### Sintaxe
  Perceba, a sintaxe do RIGTH JOIN e a mesma do LEFT JOIN:
  
    SELECT * FROM tabela1 AS t1
    LEFT JOIN tabela2 AS t2
    ON t1.coluna = t2.coluna;

  Na query acima, estamos buscando todos os valores da 'tabela1' que e a tabela a direita,
  e estamos buscando apenas os valores correspondentes da 'tabela2' que e a tabela a esquerda.

  #### Exemplo
  No exemplo a seguir nos faremos a mesma query que fizemos no exemplo de LEFT JOIN,
  dessa vez usaremos RIGHT JOIN, faremos uma query que busca todos os valores da tabela 'albums'
  e busca apenas os valores correspondentes na tabela 'artistas'. Copie e cole o codigo abaixo no 
  seu Worckench e veja o que essa query te retorna! O código ficaria assim:

    SELECT * FROM artists AS a
    RIGHT JOIN albums AS al
    ON a.artist_id = al.artist_id

  #### Exercícios de fixação
  * Faça uma query que busque todos os dados da tabela 'followers' e busque os dados correspondentes 
    da tabela 'users' pelo campo 'user_id'. 

## Vamos praticar!
Agora vamos colocar a mão na massa :rocket::rocket:, chegou a hora de você colocar em pratica 
todos os conteudos aprendidos no dia de hoje.

<img src="https://media2.giphy.com/media/13HBDT4QSTpveU/200.webp?cid=ecf05e47tzetoapbkifyfkvikjflg7shnbpl6b2spwnv2g7o&rid=200.webp&ct=g" alt="">

Para os exercicios a seguir, nos vamos utilizar a base de dados Sakila, para isso click no link a seguir
para fazer o download do arquivo sql, e cria uma base de dados a partir dele. ['CLIQUE AQUI'](https://docs.google.com/uc?export=download&id=1W0ASx1b20AV57dm2wmyFzx4oDFDsgKI2)

## Recursos Adicionais (opcional)
* [SQL JOIN(INNER, LEFT, RIGHT e FULL) combinando tabelas! por Trybe.](https://blog.betrybe.com/sql/sql-join/)
* [SQL JOIN: Entenda como funciona o retorno dos dados, por DevMedia.](https://www.devmedia.com.br/sql-join-entenda-como-funciona-o-retorno-dos-dados/31006)
* [SQL JOIN: Aprenda INNER, LEFT, RIGHT, FULL e CROSS, por Alura.](https://www.alura.com.br/artigos/join-em-sql)
