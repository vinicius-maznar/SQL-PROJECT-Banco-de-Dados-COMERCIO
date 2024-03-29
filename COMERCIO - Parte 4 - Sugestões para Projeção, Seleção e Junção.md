# 🛠 **DATABASE SIMPLES PARA COMERCIO**

* 🔎 Sugestões para Seleção, Projeção e Junção

## 🏗 **PARTE 3 - CONSTRUÇÕES DE QUERIES**


- **REQUISITO 1:** TRAGA O `NOME`, `SEXO` E `EMAIL` DOS CLIENTES DO `SEXO FEMININO`;
```SQL
/*INPUT*/
SELECT NOME, SEXO, EMAIL		/*PROJEÇÃO*/
FROM CLIENTE					/*ORIGEM*/
WHERE SEXO ='F';				/*SELEÇÃO*/

/*OUTPUT*/
mysql> SELECT NOME, SEXO, EMAIL
    -> FROM CLIENTE
    -> WHERE SEXO ='F';
+-------+------+------------+
| NOME  | SEXO | EMAIL      |
+-------+------+------------+
| ANA   | F    | ANA@IG.COM |
| CLARA | F    | NULL       |
+-------+------+------------+
2 rows in set (0.00 sec)
```


- **REQUISITO 2:** TRAGA TODOS OS CELULARES DA `TABELA TELEFONE`;
```SQL
/*INPUT*/
SELECT NUMERO AS CELULARES
FROM TELEFONE
WHERE TIPO ='CEL';

/*OUTPUT*/
mysql> SELECT NUMERO AS CELULARES
    -> FROM TELEFONE
    -> WHERE TIPO ='CEL';
+-----------+
| CELULARES |
+-----------+
| 78458743  |
| 87866896  |
| 78989765  |
| 99766676  |
| 88687909  |
+-----------+
5 rows in set (0.00 sec)
```


- **REQUISITO 3:** TRAGA O `NOME`, `SEXO`, O `BAIRRO` A `CIDADE` E OS `NUMEROS` DE TELEFONE E SEUS RESPECTIVOS `TIPOS`;
```SQL
/*INPUT*/
SELECT CLIENTE.NOME, CLIENTE.SEXO, ENDERECO.BAIRRO, ENDERECO.CIDADE, TELEFONE.TIPO, TELEFONE.NUMERO
FROM CLIENTE
  INNER JOIN ENDERECO
ON CLIENTE.IDCLIENTE = ENDERECO.ID_CLIENTE
  INNER JOIN TELEFONE
ON CLIENTE.IDCLIENTE = TELEFONE.ID_CLIENTE;

/*OUTPUT*/
mysql> SELECT CLIENTE.NOME, CLIENTE.SEXO, ENDERECO.BAIRRO, ENDERECO.CIDADE, TELEFONE.TIPO, TELEFONE.NUMERO
    -> FROM CLIENTE
    ->   INNER JOIN ENDERECO
    -> ON CLIENTE.IDCLIENTE = ENDERECO.ID_CLIENTE
    ->   INNER JOIN TELEFONE
    -> ON CLIENTE.IDCLIENTE = TELEFONE.ID_CLIENTE;
+--------+------+---------+----------------+------+----------+
| NOME   | SEXO | BAIRRO  | CIDADE         | TIPO | NUMERO   |
+--------+------+---------+----------------+------+----------+
| JOAO   | M    | CENTRO  | RIO DE JANEIRO | CEL  | 87866896 |
| JOAO   | M    | CENTRO  | RIO DE JANEIRO | RES  | 99667587 |
| JOAO   | M    | CENTRO  | RIO DE JANEIRO | COM  | 66687899 |
| ANA    | F    | JARDINS | SAO PAULO      | CEL  | 78989765 |
| ANA    | F    | JARDINS | SAO PAULO      | CEL  | 99766676 |
| CARLOS | M    | ESTACIO | RIO DE JANEIRO | COM  | 54768899 |
| CARLOS | M    | ESTACIO | RIO DE JANEIRO | CEL  | 88687909 |
| JORGE  | M    | CENTRO  | VITORIA        | CEL  | 78458743 |
| JORGE  | M    | CENTRO  | VITORIA        | RES  | 56576876 |
| JORGE  | M    | CENTRO  | VITORIA        | RES  | 89986668 |
+--------+------+---------+----------------+------+----------+
10 rows in set (0.00 sec)
```


# ⚠ **NOTA 1: DML: QUERIES AVANÇADAS**

## 🔨 **TAREFA 1:** FAÇA UM RELATÓRIO DE TODOS OS `CLIENTES` COM `TELEFONE` E `ENDERECO` ;

- **PASSO 1:** PROJETE A DESCRIÇÃO DE TODAS AS TABELAS SOLICITADAS COMO `CLIENTE`, `TELEFONE` E `ENDERECO` ;
```SQL
/*INPUT*/
DESC CLIENTE;
DESC TELEFONE;
DESC ENDERECO;

/*OUTPUT*/
mysql> DESC CLIENTE;
+-----------+---------------+------+-----+---------+----------------+
| Field     | Type          | Null | Key | Default | Extra          |
+-----------+---------------+------+-----+---------+----------------+
| IDCLIENTE | int(11)       | NO   | PRI | NULL    | auto_increment |
| NOME      | varchar(30)   | NO   |     | NULL    |                |
| SEXO      | enum('M','F') | NO   |     | NULL    |                |
| EMAIL     | varchar(50)   | YES  | UNI | NULL    |                |
| CPF       | varchar(15)   | YES  | UNI | NULL    |                |
+-----------+---------------+------+-----+---------+----------------+
5 rows in set (0.03 sec)

mysql> DESC TELEFONE;
+------------+-------------------------+------+-----+---------+----------------+
| Field      | Type                    | Null | Key | Default | Extra          |
+------------+-------------------------+------+-----+---------+----------------+
| IDTELEFONE | int(11)                 | NO   | PRI | NULL    | auto_increment |
| TIPO       | enum('RES','COM','CEL') | NO   |     | NULL    |                |
| NUMERO     | varchar(30)             | NO   |     | NULL    |                |
| ID_CLIENTE | int(11)                 | YES  | MUL | NULL    |                |
+------------+-------------------------+------+-----+---------+----------------+
4 rows in set (0.00 sec)

mysql> DESC ENDERECO;
+------------+-------------+------+-----+---------+----------------+
| Field      | Type        | Null | Key | Default | Extra          |
+------------+-------------+------+-----+---------+----------------+
| IDENDERECO | int(11)     | NO   | PRI | NULL    | auto_increment |
| LOGRADOURO | varchar(30) | NO   |     | NULL    |                |
| BAIRRO     | varchar(30) | NO   |     | NULL    |                |
| CIDADE     | varchar(30) | NO   |     | NULL    |                |
| ESTADO     | char(2)     | NO   |     | NULL    |                |
| ID_CLIENTE | int(11)     | YES  | UNI | NULL    |                |
+------------+-------------+------+-----+---------+----------------+
6 rows in set (0.00 sec)
```


- **PASSO 2:** CONSTRUINDO A QUERY PARA TRAZER O RELATÓRIO GERAL DE TODOS `CLIENTES` COM `TELEFONE` E `ENDERECO`;
```SQL
/*INPUT*/
SELECT C.IDCLIENTE,C.NOME,C.SEXO,C.EMAIL,C.CPF,E.LOGRADOURO,E.BAIRRO,E.CIDADE,E.ESTADO,T.TIPO,T.NUMERO
FROM CLIENTE C
INNER JOIN ENDERECO E
ON C.IDCLIENTE = E.ID_CLIENTE
INNER JOIN TELEFONE T
ON C.IDCLIENTE = T.ID_CLIENTE;

/*OUTPUT*/
mysql> SELECT C.IDCLIENTE,C.NOME,C.SEXO,C.EMAIL,C.CPF,E.LOGRADOURO,E.BAIRRO,E.CIDADE,E.ESTADO,T.TIPO,T.NUMERO
    -> FROM CLIENTE C
    -> INNER JOIN ENDERECO E
    -> ON C.IDCLIENTE = E.ID_CLIENTE
    -> INNER JOIN TELEFONE T
    -> ON C.IDCLIENTE = T.ID_CLIENTE;
+-----------+---------+------+-------------------+-------------+--------------------+------------+----------------+--------+------+----------+
| IDCLIENTE | NOME    | SEXO | EMAIL             | CPF         | LOGRADOURO         | BAIRRO     | CIDADE         | ESTADO | TIPO | NUMERO   |
+-----------+---------+------+-------------------+-------------+--------------------+------------+----------------+--------+------+----------+
|         1 | JOAO    | M    | JOAOA@IG.COM      | 76567587887 | RUA CAPITAO HERMES | CENTRO     | RIO DE JANEIRO | RJ     | CEL  | 87866896 |
|         1 | JOAO    | M    | JOAOA@IG.COM      | 76567587887 | RUA CAPITAO HERMES | CENTRO     | RIO DE JANEIRO | RJ     | RES  | 99667587 |
|         1 | JOAO    | M    | JOAOA@IG.COM      | 76567587887 | RUA CAPITAO HERMES | CENTRO     | RIO DE JANEIRO | RJ     | COM  | 66687899 |
|         3 | ANA     | F    | ANA@IG.COM        | 456545678   | RUA PRES VARGAS    | JARDINS    | SAO PAULO      | SP     | CEL  | 78989765 |
|         3 | ANA     | F    | ANA@IG.COM        | 456545678   | RUA PRES VARGAS    | JARDINS    | SAO PAULO      | SP     | CEL  | 99766676 |
|         2 | CARLOS  | M    | CARLOSA@IG.COM    | 5464553466  | RUA ALFANDEGA      | ESTACIO    | RIO DE JANEIRO | RJ     | COM  | 54768899 |
|         2 | CARLOS  | M    | CARLOSA@IG.COM    | 5464553466  | RUA ALFANDEGA      | ESTACIO    | RIO DE JANEIRO | RJ     | CEL  | 88687909 |
|         5 | JORGE   | M    | JORGE@IG.COM      | 8756547688  | RUA URUGUAIANA     | CENTRO     | VITORIA        | ES     | CEL  | 78458743 |
|         5 | JORGE   | M    | JORGE@IG.COM      | 8756547688  | RUA URUGUAIANA     | CENTRO     | VITORIA        | ES     | RES  | 56576876 |
|         5 | JORGE   | M    | JORGE@IG.COM      | 8756547688  | RUA URUGUAIANA     | CENTRO     | VITORIA        | ES     | RES  | 89986668 |
|         9 | FLAVIO  | M    | FLAVIO@IG.COM     | 4657765     | RUA GUEDES         | CASCADURA  | B. HORIZONTE   | MG     | RES  | 68976565 |
|         9 | FLAVIO  | M    | FLAVIO@IG.COM     | 4657765     | RUA GUEDES         | CASCADURA  | B. HORIZONTE   | MG     | CEL  | 99656675 |
|        11 | GIOVANA | F    | NULL              | 0876655     | RUA VISCONDESSA    | CENTRO     | RIO DE JANEIRO | RJ     | CEL  | 33567765 |
|        11 | GIOVANA | F    | NULL              | 0876655     | RUA VISCONDESSA    | CENTRO     | RIO DE JANEIRO | RJ     | CEL  | 88668786 |
|        11 | GIOVANA | F    | NULL              | 0876655     | RUA VISCONDESSA    | CENTRO     | RIO DE JANEIRO | RJ     | COM  | 55689654 |
|        12 | KARLA   | M    | KARLA@GMAIL.COM   | 545676778   | RUA NELSON MANDELA | COPACABANA | RIO DE JANEIRO | RJ     | COM  | 88687979 |
|        13 | DANIELE | M    | DANIELE@GMAIL.COM | 43536789    | RUA ARAUJO LIMA    | CENTRO     | VITORIA        | ES     | COM  | 88965676 |
|        15 | EDUARDO | M    | NULL              | 54376457    | AV CAPITAO ANTUNES | CENTRO     | CURITIBA       | PR     | CEL  | 89966809 |
|        16 | ANTONIO | F    | ANTONIO@IG.COM    | 12436767    | AV CARLOS BARROSO  | JARDINS    | SAO PAULO      | SP     | COM  | 88679978 |
|        17 | ANTONIO | M    | ANTONIO@UOL.COM   | 3423565     | ALAMEDA SAMPAIO    | BOM RETIRO | CURITIBA       | PR     | CEL  | 99655768 |
|        18 | ELAINE  | M    | ELAINE@GLOBO.COM  | 32567763    | RUA DA LAPA        | LAPA       | SAO PAULO      | SP     | RES  | 89955665 |
|        19 | CARMEM  | M    | CARMEM@IG.COM     | 787832213   | RUA GERONIMO       | CENTRO     | RIO DE JANEIRO | RJ     | RES  | 77455786 |
|        19 | CARMEM  | M    | CARMEM@IG.COM     | 787832213   | RUA GERONIMO       | CENTRO     | RIO DE JANEIRO | RJ     | RES  | 89766554 |
|        20 | ADRIANA | F    | ADRIANA@GMAIL.COM | 88556942    | RUA GOMES FREIRE   | CENTRO     | RIO DE JANEIRO | RJ     | RES  | 77755785 |
|        20 | ADRIANA | F    | ADRIANA@GMAIL.COM | 88556942    | RUA GOMES FREIRE   | CENTRO     | RIO DE JANEIRO | RJ     | COM  | 44522578 |
|        21 | JOICE   | F    | JOICE@GMAIL.COM   | 55412256    | RUA GOMES FREIRE   | CENTRO     | RIO DE JANEIRO | RJ     | CEL  | 44522578 |
+-----------+---------+------+-------------------+-------------+--------------------+------------+----------------+--------+------+----------+
26 rows in set (0.00 sec)
```


## 🔨 **TAREFA 2:** FAÇA UM RELATÓRIO DE TODOS OS `CLIENTES`  DO SEXO `M` COM `TELEFONE` E `ENDERECO`;

- **PASSO 1:** CRIANDO A DB `BIBLIOTECA`;

- INPUT: 

```SQL
SELECT C.IDCLIENTE,C.NOME,C.SEXO,C.EMAIL,C.CPF,E.LOGRADOURO,E.BAIRRO,E.CIDADE,E.ESTADO,T.TIPO,T.NUMERO
FROM CLIENTE C
INNER JOIN ENDERECO E
ON C.IDCLIENTE = E.ID_CLIENTE
INNER JOIN TELEFONE T
ON C.IDCLIENTE = T.ID_CLIENTE
WHERE SEXO = 'M';
```

- OUTPUT:

```SQL
mysql> SELECT C.IDCLIENTE,C.NOME,C.SEXO,C.EMAIL,C.CPF,E.LOGRADOURO,E.BAIRRO,E.CIDADE,E.ESTADO,T.TIPO,T.NUMERO
    -> FROM CLIENTE C
    -> INNER JOIN ENDERECO E
    -> ON C.IDCLIENTE = E.ID_CLIENTE
    -> INNER JOIN TELEFONE T
    -> ON C.IDCLIENTE = T.ID_CLIENTE
    -> WHERE SEXO = 'M';
+-----------+---------+------+-------------------+-------------+--------------------+------------+----------------+--------+------+----------+
| IDCLIENTE | NOME    | SEXO | EMAIL             | CPF         | LOGRADOURO         | BAIRRO     | CIDADE         | ESTADO | TIPO | NUMERO   |
+-----------+---------+------+-------------------+-------------+--------------------+------------+----------------+--------+------+----------+
|         1 | JOAO    | M    | JOAOA@IG.COM      | 76567587887 | RUA CAPITAO HERMES | CENTRO     | RIO DE JANEIRO | RJ     | CEL  | 87866896 |
|         1 | JOAO    | M    | JOAOA@IG.COM      | 76567587887 | RUA CAPITAO HERMES | CENTRO     | RIO DE JANEIRO | RJ     | RES  | 99667587 |
|         1 | JOAO    | M    | JOAOA@IG.COM      | 76567587887 | RUA CAPITAO HERMES | CENTRO     | RIO DE JANEIRO | RJ     | COM  | 66687899 |
|         2 | CARLOS  | M    | CARLOSA@IG.COM    | 5464553466  | RUA ALFANDEGA      | ESTACIO    | RIO DE JANEIRO | RJ     | COM  | 54768899 |
|         2 | CARLOS  | M    | CARLOSA@IG.COM    | 5464553466  | RUA ALFANDEGA      | ESTACIO    | RIO DE JANEIRO | RJ     | CEL  | 88687909 |
|         5 | JORGE   | M    | JORGE@IG.COM      | 8756547688  | RUA URUGUAIANA     | CENTRO     | VITORIA        | ES     | CEL  | 78458743 |
|         5 | JORGE   | M    | JORGE@IG.COM      | 8756547688  | RUA URUGUAIANA     | CENTRO     | VITORIA        | ES     | RES  | 56576876 |
|         5 | JORGE   | M    | JORGE@IG.COM      | 8756547688  | RUA URUGUAIANA     | CENTRO     | VITORIA        | ES     | RES  | 89986668 |
|         9 | FLAVIO  | M    | FLAVIO@IG.COM     | 4657765     | RUA GUEDES         | CASCADURA  | B. HORIZONTE   | MG     | RES  | 68976565 |
|         9 | FLAVIO  | M    | FLAVIO@IG.COM     | 4657765     | RUA GUEDES         | CASCADURA  | B. HORIZONTE   | MG     | CEL  | 99656675 |
|        12 | KARLA   | M    | KARLA@GMAIL.COM   | 545676778   | RUA NELSON MANDELA | COPACABANA | RIO DE JANEIRO | RJ     | COM  | 88687979 |
|        13 | DANIELE | M    | DANIELE@GMAIL.COM | 43536789    | RUA ARAUJO LIMA    | CENTRO     | VITORIA        | ES     | COM  | 88965676 |
|        15 | EDUARDO | M    | NULL              | 54376457    | AV CAPITAO ANTUNES | CENTRO     | CURITIBA       | PR     | CEL  | 89966809 |
|        17 | ANTONIO | M    | ANTONIO@UOL.COM   | 3423565     | ALAMEDA SAMPAIO    | BOM RETIRO | CURITIBA       | PR     | CEL  | 99655768 |
|        18 | ELAINE  | M    | ELAINE@GLOBO.COM  | 32567763    | RUA DA LAPA        | LAPA       | SAO PAULO      | SP     | RES  | 89955665 |
|        19 | CARMEM  | M    | CARMEM@IG.COM     | 787832213   | RUA GERONIMO       | CENTRO     | RIO DE JANEIRO | RJ     | RES  | 77455786 |
|        19 | CARMEM  | M    | CARMEM@IG.COM     | 787832213   | RUA GERONIMO       | CENTRO     | RIO DE JANEIRO | RJ     | RES  | 89766554 |
+-----------+---------+------+-------------------+-------------+--------------------+------------+----------------+--------+------+----------+
17 rows in set (0.00 sec)
```


- **PASSO 2:** CORRIGINDO OS DADOS INCORRETOS DOS `IDs` SELECIONADOS (`12`, `13`, `18`, `19`);

    - Anota-se os `IDs` dos registros a serem alterados. Após, faz-se uma projeção dos `IDs` selecionados para a confirmação prévia a alteração.
```SQL
/*INPUT*/
SELECT * FROM CLIENTE
WHERE IDCLIENTE IN (12,13,18,19);

/*OUTPUT*/
mysql> SELECT * FROM CLIENTE
    -> WHERE IDCLIENTE IN (12,13,18,19);
+-----------+---------+------+-------------------+-----------+
| IDCLIENTE | NOME    | SEXO | EMAIL             | CPF       |
+-----------+---------+------+-------------------+-----------+
|        12 | KARLA   | M    | KARLA@GMAIL.COM   | 545676778 |
|        13 | DANIELE | M    | DANIELE@GMAIL.COM | 43536789  |
|        18 | ELAINE  | M    | ELAINE@GLOBO.COM  | 32567763  |
|        19 | CARMEM  | M    | CARMEM@IG.COM     | 787832213 |
+-----------+---------+------+-------------------+-----------+
4 rows in set (0.00 sec)
```


- **PASSO 3:** FAZENDO UM `UPDATE` PARA ALTERAR OS DADOS INCORRETOS DOS `IDs` SELECIONADOS (`12`, `13`, `18`, `19`);
```SQL
/*INPUT*/
UPDATE CLIENTE SET SEXO = 'F'
WHERE IDCLIENTE IN (12,13,18,19);

/*OUTPUT*/
mysql> UPDATE CLIENTE SET SEXO = 'F'
    -> WHERE IDCLIENTE IN (12,13,18,19);
Query OK, 4 rows affected (0.00 sec)
Rows matched: 4  Changed: 4  Warnings: 0
```

- **PASSO 4:** VERIFICANDO OS DADOS ATUALIZADOS DE ACORDO COM OS `IDs` SELECIONADOS (`12`, `13`, `18`, `19`);
```SQL
/*INPUT*/
SELECT * FROM CLIENTE
WHERE IDCLIENTE IN (12,13,18,19);

/*OUTPUT*/
mysql> SELECT * FROM CLIENTE
    -> WHERE IDCLIENTE IN (12,13,18,19);
+-----------+---------+------+-------------------+-----------+
| IDCLIENTE | NOME    | SEXO | EMAIL             | CPF       |
+-----------+---------+------+-------------------+-----------+
|        12 | KARLA   | F    | KARLA@GMAIL.COM   | 545676778 |
|        13 | DANIELE | F    | DANIELE@GMAIL.COM | 43536789  |
|        18 | ELAINE  | F    | ELAINE@GLOBO.COM  | 32567763  |
|        19 | CARMEM  | F    | CARMEM@IG.COM     | 787832213 |
+-----------+---------+------+-------------------+-----------+
4 rows in set (0.00 sec)
```

- **PASSO 5:** TRAZENDO O RELATÓRIO CORRETO DE TODOS OS `CLIENTES`  DO SEXO `M` COM `TELEFONE` E `ENDERECO`;
```SQL
/*INPUT*/
SELECT C.IDCLIENTE,C.NOME,C.SEXO,C.EMAIL,C.CPF,E.LOGRADOURO,E.BAIRRO,E.CIDADE,E.ESTADO,T.TIPO,T.NUMERO
FROM CLIENTE C
INNER JOIN ENDERECO E
ON C.IDCLIENTE = E.ID_CLIENTE
INNER JOIN TELEFONE T
ON C.IDCLIENTE = T.ID_CLIENTE
WHERE SEXO = 'M';

/*OUTPUT*/
mysql> SELECT C.IDCLIENTE,C.NOME,C.SEXO,C.EMAIL,C.CPF,E.LOGRADOURO,E.BAIRRO,E.CIDADE,E.ESTADO,T.TIPO,T.NUMERO
    -> FROM CLIENTE C
    -> INNER JOIN ENDERECO E
    -> ON C.IDCLIENTE = E.ID_CLIENTE
    -> INNER JOIN TELEFONE T
    -> ON C.IDCLIENTE = T.ID_CLIENTE
    -> WHERE SEXO = 'M';
+-----------+---------+------+-----------------+-------------+--------------------+------------+----------------+--------+------+----------+
| IDCLIENTE | NOME    | SEXO | EMAIL           | CPF         | LOGRADOURO         | BAIRRO     | CIDADE         | ESTADO | TIPO | NUMERO   |
+-----------+---------+------+-----------------+-------------+--------------------+------------+----------------+--------+------+----------+
|         1 | JOAO    | M    | JOAOA@IG.COM    | 76567587887 | RUA CAPITAO HERMES | CENTRO     | RIO DE JANEIRO | RJ     | CEL  | 87866896 |
|         1 | JOAO    | M    | JOAOA@IG.COM    | 76567587887 | RUA CAPITAO HERMES | CENTRO     | RIO DE JANEIRO | RJ     | RES  | 99667587 |
|         1 | JOAO    | M    | JOAOA@IG.COM    | 76567587887 | RUA CAPITAO HERMES | CENTRO     | RIO DE JANEIRO | RJ     | COM  | 66687899 |
|         2 | CARLOS  | M    | CARLOSA@IG.COM  | 5464553466  | RUA ALFANDEGA      | ESTACIO    | RIO DE JANEIRO | RJ     | COM  | 54768899 |
|         2 | CARLOS  | M    | CARLOSA@IG.COM  | 5464553466  | RUA ALFANDEGA      | ESTACIO    | RIO DE JANEIRO | RJ     | CEL  | 88687909 |
|         5 | JORGE   | M    | JORGE@IG.COM    | 8756547688  | RUA URUGUAIANA     | CENTRO     | VITORIA        | ES     | CEL  | 78458743 |
|         5 | JORGE   | M    | JORGE@IG.COM    | 8756547688  | RUA URUGUAIANA     | CENTRO     | VITORIA        | ES     | RES  | 56576876 |
|         5 | JORGE   | M    | JORGE@IG.COM    | 8756547688  | RUA URUGUAIANA     | CENTRO     | VITORIA        | ES     | RES  | 89986668 |
|         9 | FLAVIO  | M    | FLAVIO@IG.COM   | 4657765     | RUA GUEDES         | CASCADURA  | B. HORIZONTE   | MG     | RES  | 68976565 |
|         9 | FLAVIO  | M    | FLAVIO@IG.COM   | 4657765     | RUA GUEDES         | CASCADURA  | B. HORIZONTE   | MG     | CEL  | 99656675 |
|        15 | EDUARDO | M    | NULL            | 54376457    | AV CAPITAO ANTUNES | CENTRO     | CURITIBA       | PR     | CEL  | 89966809 |
|        17 | ANTONIO | M    | ANTONIO@UOL.COM | 3423565     | ALAMEDA SAMPAIO    | BOM RETIRO | CURITIBA       | PR     | CEL  | 99655768 |
+-----------+---------+------+-----------------+-------------+--------------------+------------+----------------+--------+------+----------+
12 rows in set (0.00 sec)
```


## 🔨 **TAREFA 3:** FAÇA UM RELATÓRIO DE TODOS OS `CLIENTES`  DO SEXO `F` COM `TELEFONE` E `ENDERECO`;

```SQL
/*INPUT*/
SELECT C.IDCLIENTE,C.NOME,C.SEXO,C.EMAIL,C.CPF,E.LOGRADOURO,E.BAIRRO,E.CIDADE,E.ESTADO,T.TIPO,T.NUMERO
FROM CLIENTE C
INNER JOIN ENDERECO E
ON C.IDCLIENTE = E.ID_CLIENTE
INNER JOIN TELEFONE T
ON C.IDCLIENTE = T.ID_CLIENTE
WHERE SEXO = 'F';

/*OUTPUT*/
mysql> SELECT C.IDCLIENTE,C.NOME,C.SEXO,C.EMAIL,C.CPF,E.LOGRADOURO,E.BAIRRO,E.CIDADE,E.ESTADO,T.TIPO,T.NUMERO
    -> FROM CLIENTE C
    -> INNER JOIN ENDERECO E
    -> ON C.IDCLIENTE = E.ID_CLIENTE
    -> INNER JOIN TELEFONE T
    -> ON C.IDCLIENTE = T.ID_CLIENTE
    -> WHERE SEXO = 'F';
+-----------+---------+------+-------------------+-----------+--------------------+------------+----------------+--------+------+----------+
| IDCLIENTE | NOME    | SEXO | EMAIL             | CPF       | LOGRADOURO         | BAIRRO     | CIDADE         | ESTADO | TIPO | NUMERO   |
+-----------+---------+------+-------------------+-----------+--------------------+------------+----------------+--------+------+----------+
|         3 | ANA     | F    | ANA@IG.COM        | 456545678 | RUA PRES VARGAS    | JARDINS    | SAO PAULO      | SP     | CEL  | 78989765 |
|         3 | ANA     | F    | ANA@IG.COM        | 456545678 | RUA PRES VARGAS    | JARDINS    | SAO PAULO      | SP     | CEL  | 99766676 |
|        11 | GIOVANA | F    | NULL              | 0876655   | RUA VISCONDESSA    | CENTRO     | RIO DE JANEIRO | RJ     | CEL  | 33567765 |
|        11 | GIOVANA | F    | NULL              | 0876655   | RUA VISCONDESSA    | CENTRO     | RIO DE JANEIRO | RJ     | CEL  | 88668786 |
|        11 | GIOVANA | F    | NULL              | 0876655   | RUA VISCONDESSA    | CENTRO     | RIO DE JANEIRO | RJ     | COM  | 55689654 |
|        12 | KARLA   | F    | KARLA@GMAIL.COM   | 545676778 | RUA NELSON MANDELA | COPACABANA | RIO DE JANEIRO | RJ     | COM  | 88687979 |
|        13 | DANIELE | F    | DANIELE@GMAIL.COM | 43536789  | RUA ARAUJO LIMA    | CENTRO     | VITORIA        | ES     | COM  | 88965676 |
|        16 | ANTONIO | F    | ANTONIO@IG.COM    | 12436767  | AV CARLOS BARROSO  | JARDINS    | SAO PAULO      | SP     | COM  | 88679978 |
|        18 | ELAINE  | F    | ELAINE@GLOBO.COM  | 32567763  | RUA DA LAPA        | LAPA       | SAO PAULO      | SP     | RES  | 89955665 |
|        19 | CARMEM  | F    | CARMEM@IG.COM     | 787832213 | RUA GERONIMO       | CENTRO     | RIO DE JANEIRO | RJ     | RES  | 77455786 |
|        19 | CARMEM  | F    | CARMEM@IG.COM     | 787832213 | RUA GERONIMO       | CENTRO     | RIO DE JANEIRO | RJ     | RES  | 89766554 |
|        20 | ADRIANA | F    | ADRIANA@GMAIL.COM | 88556942  | RUA GOMES FREIRE   | CENTRO     | RIO DE JANEIRO | RJ     | RES  | 77755785 |
|        20 | ADRIANA | F    | ADRIANA@GMAIL.COM | 88556942  | RUA GOMES FREIRE   | CENTRO     | RIO DE JANEIRO | RJ     | COM  | 44522578 |
|        21 | JOICE   | F    | JOICE@GMAIL.COM   | 55412256  | RUA GOMES FREIRE   | CENTRO     | RIO DE JANEIRO | RJ     | CEL  | 44522578 |
+-----------+---------+------+-------------------+-----------+--------------------+------------+----------------+--------+------+----------+
14 rows in set (0.00 sec)
```


- **PASSO 1:** CORRIGINDO OS DADOS INCORRETOS DOS `IDs` SELECIONADOS (`16`);

    - Anota-se os `IDs` dos registros a serem alterados. Após, faz-se uma projeção dos `IDs` selecionados para a confirmação prévia a alteração.
```SQL
/*INPUT*/
SELECT * FROM CLIENTE
WHERE IDCLIENTE IN (16);

/*OUTPUT*/
mysql> SELECT * FROM CLIENTE
    -> WHERE IDCLIENTE IN (16);
+-----------+---------+------+----------------+----------+
| IDCLIENTE | NOME    | SEXO | EMAIL          | CPF      |
+-----------+---------+------+----------------+----------+
|        16 | ANTONIO | F    | ANTONIO@IG.COM | 12436767 |
+-----------+---------+------+----------------+----------+
1 row in set (0.00 sec)
```


- **PASSO 2:** FAZENDO UM `UPDATE` PARA ALTERAR OS DADOS INCORRETOS DOS `IDs` SELECIONADOS (`16`);
```SQL
/*INPUT*/
UPDATE CLIENTE SET SEXO = 'M'
WHERE IDCLIENTE IN (16);

/*OUTPUT*/
mysql> UPDATE CLIENTE SET SEXO = 'M'
    -> WHERE IDCLIENTE IN (16);
Query OK, 1 row affected (0.03 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```

- **PASSO 3:** VERIFICANDO OS DADOS ATUALIZADOS DE ACORDO COM OS `IDs` SELECIONADOS (`12`, `13`, `18`, `19`);
```SQL
/*INPUT*/
SELECT * FROM CLIENTE
WHERE IDCLIENTE IN (16);

/*OUTPUT*/
mysql> SELECT * FROM CLIENTE
    -> WHERE IDCLIENTE IN (16);
+-----------+---------+------+----------------+----------+
| IDCLIENTE | NOME    | SEXO | EMAIL          | CPF      |
+-----------+---------+------+----------------+----------+
|        16 | ANTONIO | M    | ANTONIO@IG.COM | 12436767 |
+-----------+---------+------+----------------+----------+
1 row in set (0.00 sec)
```

- **PASSO 4:** TRAZENDO O RELATÓRIO CORRETO DE TODOS OS `CLIENTES`  DO SEXO `M` COM `TELEFONE` E `ENDERECO`;
```SQL
/*INPUT*/
SELECT C.IDCLIENTE,C.NOME,C.SEXO,C.EMAIL,C.CPF,E.LOGRADOURO,E.BAIRRO,E.CIDADE,E.ESTADO,T.TIPO,T.NUMERO
FROM CLIENTE C
INNER JOIN ENDERECO E
ON C.IDCLIENTE = E.ID_CLIENTE
INNER JOIN TELEFONE T
ON C.IDCLIENTE = T.ID_CLIENTE
WHERE SEXO = 'F';

/*OUTPUT*/
mysql> SELECT C.IDCLIENTE,C.NOME,C.SEXO,C.EMAIL,C.CPF,E.LOGRADOURO,E.BAIRRO,E.CIDADE,E.ESTADO,T.TIPO,T.NUMERO
    -> FROM CLIENTE C
    -> INNER JOIN ENDERECO E
    -> ON C.IDCLIENTE = E.ID_CLIENTE
    -> INNER JOIN TELEFONE T
    -> ON C.IDCLIENTE = T.ID_CLIENTE
    -> WHERE SEXO = 'F';
+-----------+---------+------+-------------------+-----------+--------------------+------------+----------------+--------+------+----------+
| IDCLIENTE | NOME    | SEXO | EMAIL             | CPF       | LOGRADOURO         | BAIRRO     | CIDADE         | ESTADO | TIPO | NUMERO   |
+-----------+---------+------+-------------------+-----------+--------------------+------------+----------------+--------+------+----------+
|         3 | ANA     | F    | ANA@IG.COM        | 456545678 | RUA PRES VARGAS    | JARDINS    | SAO PAULO      | SP     | CEL  | 78989765 |
|         3 | ANA     | F    | ANA@IG.COM        | 456545678 | RUA PRES VARGAS    | JARDINS    | SAO PAULO      | SP     | CEL  | 99766676 |
|        11 | GIOVANA | F    | NULL              | 0876655   | RUA VISCONDESSA    | CENTRO     | RIO DE JANEIRO | RJ     | CEL  | 33567765 |
|        11 | GIOVANA | F    | NULL              | 0876655   | RUA VISCONDESSA    | CENTRO     | RIO DE JANEIRO | RJ     | CEL  | 88668786 |
|        11 | GIOVANA | F    | NULL              | 0876655   | RUA VISCONDESSA    | CENTRO     | RIO DE JANEIRO | RJ     | COM  | 55689654 |
|        12 | KARLA   | F    | KARLA@GMAIL.COM   | 545676778 | RUA NELSON MANDELA | COPACABANA | RIO DE JANEIRO | RJ     | COM  | 88687979 |
|        13 | DANIELE | F    | DANIELE@GMAIL.COM | 43536789  | RUA ARAUJO LIMA    | CENTRO     | VITORIA        | ES     | COM  | 88965676 |
|        18 | ELAINE  | F    | ELAINE@GLOBO.COM  | 32567763  | RUA DA LAPA        | LAPA       | SAO PAULO      | SP     | RES  | 89955665 |
|        19 | CARMEM  | F    | CARMEM@IG.COM     | 787832213 | RUA GERONIMO       | CENTRO     | RIO DE JANEIRO | RJ     | RES  | 77455786 |
|        19 | CARMEM  | F    | CARMEM@IG.COM     | 787832213 | RUA GERONIMO       | CENTRO     | RIO DE JANEIRO | RJ     | RES  | 89766554 |
|        20 | ADRIANA | F    | ADRIANA@GMAIL.COM | 88556942  | RUA GOMES FREIRE   | CENTRO     | RIO DE JANEIRO | RJ     | RES  | 77755785 |
|        20 | ADRIANA | F    | ADRIANA@GMAIL.COM | 88556942  | RUA GOMES FREIRE   | CENTRO     | RIO DE JANEIRO | RJ     | COM  | 44522578 |
|        21 | JOICE   | F    | JOICE@GMAIL.COM   | 55412256  | RUA GOMES FREIRE   | CENTRO     | RIO DE JANEIRO | RJ     | CEL  | 44522578 |
+-----------+---------+------+-------------------+-----------+--------------------+------------+----------------+--------+------+----------+
13 rows in set (0.00 sec)
```

## 🔨 **TAREFA 5:** PROJETE QUANTIDADE DE TODOS OS `HOMENS` E `MULHERES`;

```SQL
/*INPUT*/
SELECT COUNT(*) AS QUANTIDADE, SEXO
FROM CLIENTE
GROUP BY SEXO;

/*OUTPUT*/
mysql> SELECT COUNT(*) AS QUANTIDADE, SEXO
    -> FROM CLIENTE
    -> GROUP BY SEXO;
+------------+------+
| QUANTIDADE | SEXO |
+------------+------+
|         10 | M    |
|         10 | F    |
+------------+------+
2 rows in set (0.00 sec)
```


## 🔨 **TAREFA 6:** TRAGA OS `IDs` E `EMAILs` DAS `MULHERES` QUE MOREM NO `CENTRO DO RIO DE JANEIRO` E `NÃO TENHAM CELULAR`;

- **PASSO 1:** PARA A CONSTRUÇÃO DA QUERY, PROJETE TODAS AS INFORMAÇÕES NECESSÁRIAS, MESMO QUE ALGUMAS NÃO IRÃO APARECER MA QUERY FINAL.

    - Usa-se essa primeira projeçao como referência para organizar a query principal;

    - Aqui, será projetado um relatório completo, até com os clientes do sexo masculino, primeiramente.

```SQL
/*INPUT*/
SELECT C.IDCLIENTE, C.EMAIL, C.NOME, C.SEXO
FROM CLIENTE C
INNER JOIN ENDERECO E
ON C.IDCLIENTE = E.ID_CLIENTE
INNER JOIN TELEFONE T
ON C.IDCLIENTE = T.ID_CLIENTE;

/*OUTPUT*/
mysql> SELECT C.IDCLIENTE, C.EMAIL, C.NOME, C.SEXO
    -> FROM CLIENTE C
    -> INNER JOIN ENDERECO E
    -> ON C.IDCLIENTE = E.ID_CLIENTE
    -> INNER JOIN TELEFONE T
    -> ON C.IDCLIENTE = T.ID_CLIENTE;
+-----------+-------------------+---------+------+
| IDCLIENTE | EMAIL             | NOME    | SEXO |
+-----------+-------------------+---------+------+
|         1 | JOAOA@IG.COM      | JOAO    | M    |
|         1 | JOAOA@IG.COM      | JOAO    | M    |
|         1 | JOAOA@IG.COM      | JOAO    | M    |
|         2 | CARLOSA@IG.COM    | CARLOS  | M    |
|         2 | CARLOSA@IG.COM    | CARLOS  | M    |
|         3 | ANA@IG.COM        | ANA     | F    |
|         3 | ANA@IG.COM        | ANA     | F    |
|         5 | JORGE@IG.COM      | JORGE   | M    |
|         5 | JORGE@IG.COM      | JORGE   | M    |
|         5 | JORGE@IG.COM      | JORGE   | M    |
|         9 | FLAVIO@IG.COM     | FLAVIO  | M    |
|         9 | FLAVIO@IG.COM     | FLAVIO  | M    |
|        11 | NULL              | GIOVANA | F    |
|        11 | NULL              | GIOVANA | F    |
|        11 | NULL              | GIOVANA | F    |
|        12 | KARLA@GMAIL.COM   | KARLA   | F    |
|        13 | DANIELE@GMAIL.COM | DANIELE | F    |
|        15 | NULL              | EDUARDO | M    |
|        16 | ANTONIO@IG.COM    | ANTONIO | M    |
|        17 | ANTONIO@UOL.COM   | ANTONIO | M    |
|        18 | ELAINE@GLOBO.COM  | ELAINE  | F    |
|        19 | CARMEM@IG.COM     | CARMEM  | F    |
|        19 | CARMEM@IG.COM     | CARMEM  | F    |
|        20 | ADRIANA@GMAIL.COM | ADRIANA | F    |
|        20 | ADRIANA@GMAIL.COM | ADRIANA | F    |
|        21 | JOICE@GMAIL.COM   | JOICE   | F    |
+-----------+-------------------+---------+------+
26 rows in set (0.00 sec)
```


- **PASSO 2:** PROJETANDO AS INFORMAÇÕES SOLICITADAS FILTRANDO PELO `SEXO FEMININO`;
```SQL
/*INPUT*/
SELECT C.IDCLIENTE, C.EMAIL, C.NOME, C.SEXO
FROM CLIENTE C
INNER JOIN ENDERECO E
ON C.IDCLIENTE = E.ID_CLIENTE
INNER JOIN TELEFONE T
ON C.IDCLIENTE = T.ID_CLIENTE
WHERE SEXO = 'F';

/*OUTPUT*/
mysql> SELECT C.IDCLIENTE, C.EMAIL, C.NOME, C.SEXO
    -> FROM CLIENTE C
    -> INNER JOIN ENDERECO E
    -> ON C.IDCLIENTE = E.ID_CLIENTE
    -> INNER JOIN TELEFONE T
    -> ON C.IDCLIENTE = T.ID_CLIENTE
    -> WHERE SEXO = 'F';
+-----------+-------------------+---------+------+
| IDCLIENTE | EMAIL             | NOME    | SEXO |
+-----------+-------------------+---------+------+
|         3 | ANA@IG.COM        | ANA     | F    |
|         3 | ANA@IG.COM        | ANA     | F    |
|        11 | NULL              | GIOVANA | F    |
|        11 | NULL              | GIOVANA | F    |
|        11 | NULL              | GIOVANA | F    |
|        12 | KARLA@GMAIL.COM   | KARLA   | F    |
|        13 | DANIELE@GMAIL.COM | DANIELE | F    |
|        18 | ELAINE@GLOBO.COM  | ELAINE  | F    |
|        19 | CARMEM@IG.COM     | CARMEM  | F    |
|        19 | CARMEM@IG.COM     | CARMEM  | F    |
|        20 | ADRIANA@GMAIL.COM | ADRIANA | F    |
|        20 | ADRIANA@GMAIL.COM | ADRIANA | F    |
|        21 | JOICE@GMAIL.COM   | JOICE   | F    |
+-----------+-------------------+---------+------+
13 rows in set (0.00 sec)
```


# ⚠ **NOTA 1: A IMPORTÂNCIA DE PROJETAR AS 'COLUNAS DE REFERÊNCIAS' DURANTE A CONSTRUÇÃO DE UMA QUERY**

- No exemplo anterior, na coluna `EMAIL` aparecem alguns resultados nulo `NULL` que podem confundir sobre a veracidade dos dados projetados.

- Com a projeção das outras colunas, mesmo que não solicitadas para a Query principal, a confirmação dos dados é facilitada, pois garantidos as informações que fazem referência ao que foi solicitado no requisito.


- **PASSO 3:** ACRESCENTANDO MAIS FILTROS(`SEXO` = 'F', `BAIRRO` = 'CENTRO', `CIDADE` = 'RIO DE JANEIRO') E MAIS COLUNAS(`TIPO`, `BAIRRO`, `CIDADE`) PARA UMA BUSCA MAIS REFINADA;
```SQL
/*INPUT*/
SELECT C.IDCLIENTE, C.EMAIL, C.NOME, C.SEXO, T.TIPO, E.BAIRRO,E.CIDADE
FROM CLIENTE C
INNER JOIN ENDERECO E
ON C.IDCLIENTE = E.ID_CLIENTE
INNER JOIN TELEFONE T
ON C.IDCLIENTE = T.ID_CLIENTE
WHERE SEXO = 'F'
AND BAIRRO = 'CENTRO' AND CIDADE = 'RIO DE JANEIRO'
AND TIPO = 'RES' OR TIPO = 'COM';

/*OUTPUT*/
mysql> SELECT C.IDCLIENTE, C.EMAIL, C.NOME, C.SEXO, T.TIPO, E.BAIRRO,E.CIDADE
    -> FROM CLIENTE C
    -> INNER JOIN ENDERECO E
    -> ON C.IDCLIENTE = E.ID_CLIENTE
    -> INNER JOIN TELEFONE T
    -> ON C.IDCLIENTE = T.ID_CLIENTE
    -> WHERE SEXO = 'F'
    -> AND BAIRRO = 'CENTRO' AND CIDADE = 'RIO DE JANEIRO'
    -> AND TIPO = 'RES' OR TIPO = 'COM';
+-----------+-------------------+---------+------+------+------------+----------------+
| IDCLIENTE | EMAIL             | NOME    | SEXO | TIPO | BAIRRO     | CIDADE         |
+-----------+-------------------+---------+------+------+------------+----------------+
|         1 | JOAOA@IG.COM      | JOAO    | M    | COM  | CENTRO     | RIO DE JANEIRO |
|         2 | CARLOSA@IG.COM    | CARLOS  | M    | COM  | ESTACIO    | RIO DE JANEIRO |
|        11 | NULL              | GIOVANA | F    | COM  | CENTRO     | RIO DE JANEIRO |
|        12 | KARLA@GMAIL.COM   | KARLA   | F    | COM  | COPACABANA | RIO DE JANEIRO |
|        13 | DANIELE@GMAIL.COM | DANIELE | F    | COM  | CENTRO     | VITORIA        |
|        16 | ANTONIO@IG.COM    | ANTONIO | M    | COM  | JARDINS    | SAO PAULO      |
|        19 | CARMEM@IG.COM     | CARMEM  | F    | RES  | CENTRO     | RIO DE JANEIRO |
|        19 | CARMEM@IG.COM     | CARMEM  | F    | RES  | CENTRO     | RIO DE JANEIRO |
|        20 | ADRIANA@GMAIL.COM | ADRIANA | F    | RES  | CENTRO     | RIO DE JANEIRO |
|        20 | ADRIANA@GMAIL.COM | ADRIANA | F    | COM  | CENTRO     | RIO DE JANEIRO |
+-----------+-------------------+---------+------+------+------------+----------------+
10 rows in set (0.00 sec)
```

# ⚠ **NOTA 2: SUBQUERY: CORRIJINDO O ERRO DE ANÁLISE DO EXEMPLO ACIMA**

- 

- 


## 🔨 **TAREFA 7:** O SETOR SOLICITOU UM RELATÓRIO COM O `NOME`, `EMAIL` E `TELEFONE CELULAR` DOS CLIENTES QUE MORAM NO `ESTADO DO RIO DE JANEIRO`;

```SQL
/*INPUT*/
SELECT C.NOME, C.EMAIL, T.NUMERO AS CELULAR
FROM CLIENTE C
INNER JOIN ENDERECO E
ON C.IDCLIENTE = E.ID_CLIENTE
INNER JOIN TELEFONE T
ON C.IDCLIENTE = T.ID_CLIENTE
WHERE TIPO = 'CEL' AND ESTADO = 'RJ';

/*OUTPUT*/
mysql> SELECT C.NOME, C.EMAIL, T.NUMERO AS CELULAR
    -> FROM CLIENTE C
    -> INNER JOIN ENDERECO E
    -> ON C.IDCLIENTE = E.ID_CLIENTE
    -> INNER JOIN TELEFONE T
    -> ON C.IDCLIENTE = T.ID_CLIENTE
    -> WHERE TIPO = 'CEL' AND ESTADO = 'RJ';
+---------+-----------------+----------+
| NOME    | EMAIL           | CELULAR  |
+---------+-----------------+----------+
| JOAO    | JOAOA@IG.COM    | 87866896 |
| CARLOS  | CARLOSA@IG.COM  | 88687909 |
| GIOVANA | NULL            | 33567765 |
| GIOVANA | NULL            | 88668786 |
| JOICE   | JOICE@GMAIL.COM | 44522578 |
+---------+-----------------+----------+
5 rows in set (0.00 sec)
```

# ⚠ **NOTA 3: REGRAS PARA A PARTE `ORIGEM`(`FROM`) E `CONDIÇÃO`(`ON`)**

- Na parte `ORIGEM`(`FROM`) da Query, sempre usa-se de refência a tabela que tiver mais ligações de dados entre as outras tabelas.

- Na parte `CONDIÇÃO`(`ON`) as chaves iniciais na comparação (antes do sinal de `=`) devem ser da tabela que é usada na `ORIGEM`


## 🔨 **TAREFA 8:** TRAGA UM RELATÓRIO COM O `NOME`, `EMAIL` E `TELEFONE CELULAR` DOS CLIENTES QUE MORAM NO `ESTADO DO RIO DE JANEIRO`;

```SQL
/*INPUT*/
SELECT C.NOME, C.EMAIL, T.NUMERO AS CELULAR
FROM CLIENTE C
INNER JOIN ENDERECO E
ON C.IDCLIENTE = E.ID_CLIENTE
INNER JOIN TELEFONE T
ON C.IDCLIENTE = T.ID_CLIENTE
WHERE TIPO = 'CEL' AND ESTADO = 'RJ';

/*OUTPUT*/
mysql> SELECT C.NOME, C.EMAIL, T.NUMERO AS CELULAR
    -> FROM CLIENTE C
    -> INNER JOIN ENDERECO E
    -> ON C.IDCLIENTE = E.ID_CLIENTE
    -> INNER JOIN TELEFONE T
    -> ON C.IDCLIENTE = T.ID_CLIENTE
    -> WHERE TIPO = 'CEL' AND ESTADO = 'RJ';
+---------+-----------------+----------+
| NOME    | EMAIL           | CELULAR  |
+---------+-----------------+----------+
| JOAO    | JOAOA@IG.COM    | 87866896 |
| CARLOS  | CARLOSA@IG.COM  | 88687909 |
| GIOVANA | NULL            | 33567765 |
| GIOVANA | NULL            | 88668786 |
| JOICE   | JOICE@GMAIL.COM | 44522578 |
+---------+-----------------+----------+
5 rows in set (0.00 sec)
```


## 🔨 **TAREFA 7:** TRAGA UM RELATÓRIO COM O `NOME`, `EMAIL` E `TELEFONE CELULAR` DAS `MULHERES` QUE MORAM NO `ESTADO DE SÃO PAULO`; 

- **PASSO 1:** Faça uma projeção de referência;
```SQL
/*INPUT*/
SELECT C.NOME, C.EMAIL, C.SEXO, E.ESTADO, T.NUMERO AS CELULAR
FROM CLIENTE C
INNER JOIN ENDERECO E
ON C.IDCLIENTE = E.ID_CLIENTE
INNER JOIN TELEFONE T
ON C.IDCLIENTE = T.ID_CLIENTE
WHERE SEXO = 'F' AND ESTADO = 'SP';

/*OUTPUT*/
mysql> SELECT C.NOME, C.EMAIL, C.SEXO, E.ESTADO, T.NUMERO AS CELULAR
    -> FROM CLIENTE C
    -> INNER JOIN ENDERECO E
    -> ON C.IDCLIENTE = E.ID_CLIENTE
    -> INNER JOIN TELEFONE T
    -> ON C.IDCLIENTE = T.ID_CLIENTE
    -> WHERE SEXO = 'F' AND ESTADO = 'SP';
+--------+------------------+------+--------+----------+
| NOME   | EMAIL            | SEXO | ESTADO | CELULAR  |
+--------+------------------+------+--------+----------+
| ANA    | ANA@IG.COM       | F    | SP     | 78989765 |
| ANA    | ANA@IG.COM       | F    | SP     | 99766676 |
| ELAINE | ELAINE@GLOBO.COM | F    | SP     | 89955665 |
+--------+------------------+------+--------+----------+
3 rows in set (0.00 sec)
```

