# JOINs o que são, o que comem, onde vivem?
## O que vamos aprender?
Hoje você irá aprender um conteúdo muito importante para avançar no seu
aprendizado de SQL, hoje aprenderemos sobre SQL JOINs, JOIN e uma cláusula muito
importante dentro da linguagem sql, essa cláusula é usada para operações
cujo objetivo é juntar colunas de diferentes tabelas, possibilitando que vocè
escreva querys mais sofisticadas e complexas que atendam melhor a um determinado
objetivo. Existem diferentes tipos de JOINs sendo eles os mais comuns:

* INNER JOIN: faz uma junção retornando valores de diferentes tabelas 
  correspondente a condição

* RIGHT JOIN: faz uma junção retornado os valores da tabela à esquerda e retornando
  os valores correspondentes a condição da tabela à direita

* LEFT JOIN: faz uma junção retornado os valores da tabela à direita e retornando
  os valores correspondentes a condição da tabela à esquerda

* FULL JOIN: faz uma junção retornando todos os valores entre diferentes tabelas
  quando a relação entre os valores

* CROSS JOIN: faz uma junção e retorna para cada linha na tabela a direita 
  todas as linhas na tabela a esquerda ou vice-versa

Não se preocupe, pode parecer complicado mas é mais simples do que parece :stuck_out_tongue_winking_eye:, e no
dia de hoje vamos estudar a fundo esse assunto para que você possa aperfeçoar seu conhecimento
em SQL, vamos nessa? :rocket::rocket:

#### Você será capaz de:
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
  Antes de começarmos a ver o conteudo de hoje nos vamos cirar um banco de dados,
  nos usaremos esse banco durante o dia de hoje em momentos onde você colocara a mão 
  no codigo, por isso vamos colocar a mão na massa 

  <img height="200px" width="200px" src="https://media0.giphy.com/media/o0vwzuFwCGAFO/200w.webp?cid=ecf05e47o5dmmlcgmouwv0vyvxnai024lw3y4in5ugkoccqg&rid=200w.webp&ct=g" alt="">

  O codigo SQL abaixo cria uma base de dados, copie o codigo abaixo e cole no seu
  Workbench, execute o codigo para cirar a base de dados.

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

    Agora com a nossa base de dados que sera usa em exemplos criada podemos 
    prosseguir com o conteudo

  ### Entendendo o INNER JOIN
  Dentro dos metodos de junção o INNER JOIN talvez seja um dos mais utilizados,
  o que INNER JOIN faz e juntar os valores de diferentes tabelas se esses valores estiverem
  relacionados, veja essa representação abaixo:

  <img height="210px" width="300px" src="https://cdn.pixabay.com/photo/2022/08/12/17/14/sql-7382120_960_720.jpg" alt="">

  #### Sintaxe
  Agora nos veremos a sintaxe. No exemplo a seguir, nos vemos um codigo, uma query SQL 
  que utiliza o INNER JOIN

    SELECT * FROM tabela-a AS a
    INNER JOIN tabela-b AS b
    ON a.coluna = b.coluna;

  Esse codigo SQL utiliza o INNER JOIN e faz uma query em um banco ficticio, ele
  busca todas as colunas da tabela 'a' e busca tambem todas as colunas da tabela 'b', 
  desde que essas colunas satisfação a condição estebelecida pela cláusula ON, satisfeita
  a condição da clausula ON a query retorna uma representação das tebelas 'a' e 'b' unidas.

  #### Exemplo 
  No exemplo a seguir nos vamos usar a base de dados criado enteriormente, nos vamos
  fazer uma query, que vai buscar os nomes dos artistas na tabela artistas e vai buscar
  tambem o nome dos albuns que esse artista possui, na tabela albuns. O codigo ficaria assim:

    SELECT a.artist, al.album FROM artists AS a
    INNER JOIN albums AS al
    ON a.artist_id = al.artist_id

  Tambem e possivel acrecentar um outro join em nossa query, para buscarmos tambem
  as musicas pertencentes a cada album. O codigo ficaria assim:

    SELECT a.artist, al.album, s.song FROM artists AS a
    INNER JOIN albums AS al
    ON a.artist_id = al.artist_id
    INNER JOIN songs AS s
    ON al.album_id = s.album_id;

  #### O que e esse AS no codigo?
  O comando AS e um acronimo para aliases, uma palvra em ingles que pode ser trduzida 
  para apelido em portugues, e exatamente isso que esse comando faz em nossa query, ele da
  um apelido para a tabela, o comando AS renomeia temporariamente uma tabela, 
  isso existe como uma forma organizar melhor a query e prevenir erros. Um codigo sem
  o comando AS ficaria assim:

    SELECT artist, album, song FROM artists
    INNER JOIN albums
    ON artist_id = artist_id
    INNER JOIN songs
    ON album_id = album_id;

  Esse codigo falharia e retornaria o seguinte erro:

    Column 'album_id' in on clause is ambiguous

  Esse erro ocorre por que na utima linha, no comando ON ele encontra duas vezes 
  'album_id' e não consegue diferenciar de qual tabela eles enstão vindo.

  
  ### Entendendo o LEFT JOIN

  ### Entendendo o RIGTH JOIN

  ### Entendendo o LEFT JOIN

  ### Entendendo o FULL JOIN

  ### Entendendo o CROSS JOIN

## Vamos praticar!

## Recursos Adicionais

