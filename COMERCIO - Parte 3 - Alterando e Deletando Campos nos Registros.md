# ⚠ **NOTA 1: ALTERANDO REGISTROS COM O `UPDATE`**

- **PASSO 1:** INSERINDO UM REGISTRO COM O `SEXO` ERRADO;
```SQL
/*INPUT*/
INSERT INTO CLIENTE VALUES(NULL,'PAULA','M',NULL,'77437493');
INSERT INTO ENDERECO VALUES(NULL,'RUA JOAQUIM SILVA','ALVORADA','NITEROI','RJ',7);

/*OUTPUT*/
mysql> INSERT INTO CLIENTE VALUES(NULL,'PAULA','M',NULL,'77437493');
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO ENDERECO VALUES(NULL,'RUA JOAQUIM SILVA','ALVORADA','NITEROI','RJ',7);
Query OK, 1 row affected (0.00 sec)
```


- **PASSO 2:** FILTRANDO PELO `SEXO` INSERIDO INCORRETAMENTE;
```SQL
/*INPUT*/
SELECT * FROM CLIENTE
WHERE SEXO = 'M';

/*OUTPUT*/
mysql> SELECT * FROM CLIENTE
    -> WHERE SEXO = 'M';
+-----------+--------+------+----------------+-------------+
| IDCLIENTE | NOME   | SEXO | EMAIL          | CPF         |
+-----------+--------+------+----------------+-------------+
|         1 | JOAO   | M    | JOAOA@IG.COM   | 76567587887 |
|         2 | CARLOS | M    | CARLOSA@IG.COM | 5464553466  |
|         5 | JORGE  | M    | JORGE@IG.COM   | 8756547688  |
|         6 | CELIA  | M    | JCELIA@IG.COM  | 5767876889  |
|         7 | PAULA  | M    | NULL           | 77437493    |
+-----------+--------+------+----------------+-------------+
5 rows in set (0.00 sec)
```


- **PASSO 3:** PROJETANDO O `SEXO` INSERIDO INCORRETAMENTE INDICANDO O `ID` DO REGISTRO;
```SQL
/*INPUT*/
SELECT * FROM CLIENTE
WHERE IDCLIENTE = 7;

/*OUTPUT*/
mysql> SELECT * FROM CLIENTE
    -> WHERE IDCLIENTE = 7;
+-----------+-------+------+-------+----------+
| IDCLIENTE | NOME  | SEXO | EMAIL | CPF      |
+-----------+-------+------+-------+----------+
|         7 | PAULA | M    | NULL  | 77437493 |
+-----------+-------+------+-------+----------+
1 row in set (0.00 sec)
```


- **PASSO 4:** ATUALIZANDO O `SEXO` INSERIDO INCORRETAMENTE INDICANDO O `ID` DO REGISTRO;
```SQL
/*INPUT*/
UPDATE CLIENTE
SET SEXO = 'F'
WHERE IDCLIENTE = 7;

/*OUTPUT*/
mysql> UPDATE CLIENTE
    -> SET SEXO = 'F'
    -> WHERE IDCLIENTE = 7;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```


- **PASSO 5:** CONFIRMANDO A ALTERAÇÃO NO `SEXO` INSERIDO INCORRETAMENTE INDICANDO O `ID` DO REGISTRO;
```SQL
/*INPUT*/
SELECT * FROM CLIENTE
WHERE IDCLIENTE = 7;

/*OUTPUT*/
mysql> SELECT * FROM CLIENTE
    -> WHERE IDCLIENTE = 7;
+-----------+-------+------+-------+----------+
| IDCLIENTE | NOME  | SEXO | EMAIL | CPF      |
+-----------+-------+------+-------+----------+
|         7 | PAULA | F    | NULL  | 77437493 |
+-----------+-------+------+-------+----------+
1 row in set (0.00 sec)
```


# ⚠ **NOTA 2: DELETANDO REGISTROS COM O `DELETE`**

- **PASSO 1:** INSERINDO UM REGISTRO A SER DELETEDADO NA `TABELA CLIENTE`;
```SQL
/*INPUT*/
INSERT INTO CLIENTE VALUES(NULL,'XXX','M',NULL,'XXX');

/*OUTPUT*/
mysql> INSERT INTO CLIENTE VALUES(NULL,'XXX','M',NULL,'XXX');
Query OK, 1 row affected (0.02 sec)
```


- **PASSO 2:** FILTRANDO A `TABELA CLIENTE` PARA CONFIRMAR A ENTRADA DO NOVO DADO;
```SQL
/*INPUT*/
SELECT * FROM CLIENTE
WHERE IDCLIENTE = 8;

/*OUTPUT*/
mysql> SELECT * FROM CLIENTE;
WHERE IDCLIENTE = 8;
+-----------+--------+------+----------------+-------------+
| IDCLIENTE | NOME   | SEXO | EMAIL          | CPF         |
+-----------+--------+------+----------------+-------------+
|         8 | XXX    | M    | NULL           | XXX         |
+-----------+--------+------+----------------+-------------+
1 rows in set (0.00 sec)
```


- **PASSO 3:** DELETANDO O REGISTRO DESEJADO DA `TABELA CLIENTE`;
```SQL
/*INPUT*/
DELETE FROM CLIENTE WHERE IDCLIENTE = 8;

/*OUTPUT*/
mysql> DELETE FROM CLIENTE WHERE IDCLIENTE = 8;
Query OK, 1 row affected (0.02 sec)
```


- **PASSO 4:** CONFIRMANDO A REMOÇÃO DO REGISTRO DESEJADO DA `TABELA CLIENTE`;
```SQL
/*INPUT*/
SELECT * FROM CLIENTE;

/*OUTPUT*/
mysql> SELECT * FROM CLIENTE;
+-----------+--------+------+----------------+-------------+
| IDCLIENTE | NOME   | SEXO | EMAIL          | CPF         |
+-----------+--------+------+----------------+-------------+
|         1 | JOAO   | M    | JOAOA@IG.COM   | 76567587887 |
|         2 | CARLOS | M    | CARLOSA@IG.COM | 5464553466  |
|         3 | ANA    | F    | ANA@IG.COM     | 456545678   |
|         4 | CLARA  | F    | NULL           | 5687766856  |
|         5 | JORGE  | M    | JORGE@IG.COM   | 8756547688  |
|         6 | CELIA  | M    | JCELIA@IG.COM  | 5767876889  |
|         7 | PAULA  | F    | NULL           | 77437493    |
+-----------+--------+------+----------------+-------------+
7 rows in set (0.00 sec)
```


# ⚠ **NOTA 2: ALTERANDO A TIPAGEM DE TABELAS COM O `ALTER`**

- **PASSO 1:** PROJETANDO A DESCRIÇÃO DA `TABELA PRODUTO`;
```SQL
/*INPUT*/
DESC PRODUTO;

/*OUTPUT*/
mysql> DESC PRODUTO;
+--------------+-------------+------+-----+---------+----------------+
| Field        | Type        | Null | Key | Default | Extra          |
+--------------+-------------+------+-----+---------+----------------+
| IDPRODUTO    | int(11)     | NO   | PRI | NULL    | auto_increment |
| NOME_PRODUTO | varchar(30) | NO   |     | NULL    |                |
| PRECO        | int(11)     | YES  |     | NULL    |                |
| FRETE        | float(10,2) | NO   |     | NULL    |                |
+--------------+-------------+------+-----+---------+----------------+
4 rows in set (0.01 sec)
```


- **PASSO 2:** ALTERANDO A TIPAGEM DA COLUNA `NOME_PRODUTO` PARA `VALOR_UNITARIO` COM O NOVO TIPO `INT NOT NULL`;
```SQL
/*INPUT*/
ALTER TABLE PRODUTO
CHANGE PRECO VALOR_UNITARIO INT NOT NULL;

/*OUTPUT*/
mysql> ALTER TABLE PRODUTO
    -> CHANGE PRECO VALOR_UNITARIO INT NOT NULL;
Query OK, 0 rows affected (0.05 sec)
Records: 0  Duplicates: 0  Warnings: 0
```


- **PASSO 3:** CONFIRMANDO A ALTERAÇÃO NA `TABELA PRODUTO`;
```SQL
/*INPUT*/
DESC PRODUTO;

/*OUTPUT*/
mysql> DESC PRODUTO;
+----------------+-------------+------+-----+---------+----------------+
| Field          | Type        | Null | Key | Default | Extra          |
+----------------+-------------+------+-----+---------+----------------+
| IDPRODUTO      | int(11)     | NO   | PRI | NULL    | auto_increment |
| NOME_PRODUTO   | varchar(30) | NO   |     | NULL    |                |
| VALOR_UNITARIO | int(11)     | NO   |     | NULL    |                |
| FRETE          | float(10,2) | NO   |     | NULL    |                |
+----------------+-------------+------+-----+---------+----------------+
4 rows in set (0.00 sec)
```


- **PASSO 4:** ALTERANDO NOVAMENTE A TIPAGEM DA COLUNA `VALOR_UNITARIO` PARA `INT`, REMOVENDO O `NOT NULL`;
```SQL
/*INPUT*/
ALTER TABLE PRODUTO
CHANGE VALOR_UNITARIO VALOR_UNITARIO INT;

/*OUTPUT*/
mysql> ALTER TABLE PRODUTO
    -> CHANGE VALOR_UNITARIO VALOR_UNITARIO INT;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0
```


- **PASSO 3:** CONFIRMANDO A ALTERAÇÃO NA TIPAGEM DA COLUNA `VALOR_UNITARIO`;
```SQL
/*INPUT*/
DESC PRODUTO;

/*OUTPUT*/
mysql> DESC PRODUTO;
+----------------+-------------+------+-----+---------+----------------+
| Field          | Type        | Null | Key | Default | Extra          |
+----------------+-------------+------+-----+---------+----------------+
| IDPRODUTO      | int(11)     | NO   | PRI | NULL    | auto_increment |
| NOME_PRODUTO   | varchar(30) | NO   |     | NULL    |                |
| VALOR_UNITARIO | int(11)     | YES  |     | NULL    |                |
| FRETE          | float(10,2) | NO   |     | NULL    |                |
+----------------+-------------+------+-----+---------+----------------+
4 rows in set (0.03 sec)
```


# ⚠ **NOTA 3: ALTERANDO A TIPAGEM DE TABELAS COM O `MODIFY`**

- **PASSO 1:** ALTERANDO NOVAMENTE A TIPAGEM DA COLUNA `VALOR_UNITARIO` PARA `VARCHAR(50) NOT NULL`;

    - Usando a cláusula `MODIFY` para alterar a tipagem de uma coluna, na query, não é necessário repetir o nome da coluna a ser alterada.

```SQL
/*INPUT*/
ALTER TABLE PRODUTO
MODIFY VALOR_UNITARIO VARCHAR(50) NOT NULL;

/*OUTPUT*/
mysql> ALTER TABLE PRODUTO
    -> MODIFY VALOR_UNITARIO VARCHAR(50) NOT NULL;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0
```


- **PASSO 2:** CONFIRMANDO A ALTERAÇÃO NA TIPAGEM DA COLUNA `VALOR_UNITARIO` COM O `MODIFY`;
```SQL
/*INPUT*/
DESC PRODUTO;

/*OUTPUT*/
mysql> DESC PRODUTO;
+----------------+-------------+------+-----+---------+----------------+
| Field          | Type        | Null | Key | Default | Extra          |
+----------------+-------------+------+-----+---------+----------------+
| IDPRODUTO      | int(11)     | NO   | PRI | NULL    | auto_increment |
| NOME_PRODUTO   | varchar(30) | NO   |     | NULL    |                |
| VALOR_UNITARIO | varchar(50) | NO   |     | NULL    |                |
| FRETE          | float(10,2) | NO   |     | NULL    |                |
+----------------+-------------+------+-----+---------+----------------+
4 rows in set (0.02 sec)
```


# ⚠ **NOTA 4: QUANDO ESCOLHER ENTRE O `MODIFY` O `ALTER`**

- **MUDAR O `NOME DA COLUNA` = USE O `ALTER`**

    - O `ALTER` é mais aconselhável para mudar o `NOME` de uma coluna para outro, pois a troca fica implítica na Query.

    - O `MODIFY` é mais aconselhável para o `TIPO` de uma coluna, pois no corpo da query não é necessário repetir o nome da coluna que se desjar modificar.


# ⚠ **NOTA 5: ADICIONANDO UMA COLUNA NA TABELA DESEJADA COM O `ADD`**

- **PASSO 1:** ADICIONANDO A COLUNA `PESO` NA TABELA `PRODUTO`;
```SQL
/*INPUT*/
ALTER TABLE PRODUTO
ADD PESO FLOAT(10,2) NOT NULL;

/*OUTPUT*/
mysql> ALTER TABLE PRODUTO
    -> ADD PESO FLOAT(10,2) NOT NULL;
Query OK, 0 rows affected (0.03 sec)
Records: 0  Duplicates: 0  Warnings: 0
```


- **PASSO 2:** CONFIRMANDO A INCLUSÃO DA COLUNA `PESO` NA `TABELA PRODUTO`;
```SQL
/*INPUT*/
DESC PRODUTO;

/*OUTPUT*/
mysql> DESC PRODUTO;
+----------------+-------------+------+-----+---------+----------------+
| Field          | Type        | Null | Key | Default | Extra          |
+----------------+-------------+------+-----+---------+----------------+
| IDPRODUTO      | int(11)     | NO   | PRI | NULL    | auto_increment |
| NOME_PRODUTO   | varchar(30) | NO   |     | NULL    |                |
| VALOR_UNITARIO | varchar(50) | NO   |     | NULL    |                |
| FRETE          | float(10,2) | NO   |     | NULL    |                |
| PESO           | float(10,2) | NO   |     | NULL    |                |
+----------------+-------------+------+-----+---------+----------------+
5 rows in set (0.01 sec)
```


# ⚠ **NOTA 6: ADICIONANDO UMA COLUNA NA ORDEM ESPECIFICA COM `AFTER`**

- **PASSO 1:** APAGAR A COLUNA `PESO`;
```SQL
/*INPUT*/
ALTER TABLE PRODUTO
DROP COLUMN PESO;

/*OUTPUT*/
mysql> ALTER TABLE PRODUTO
    -> DROP COLUMN PESO;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0
```


- **PASSO 2:** CONFIRMANDO A EXCLUSÃO DA COLUNA `PESO` DA `TABELA PRODUTO`;
```SQL
/*INPUT*/
DESC PRODUTO;

/*OUTPUT*/
mysql> DESC PRODUTO;
+----------------+-------------+------+-----+---------+----------------+
| Field          | Type        | Null | Key | Default | Extra          |
+----------------+-------------+------+-----+---------+----------------+
| IDPRODUTO      | int(11)     | NO   | PRI | NULL    | auto_increment |
| NOME_PRODUTO   | varchar(30) | NO   |     | NULL    |                |
| VALOR_UNITARIO | varchar(50) | NO   |     | NULL    |                |
| FRETE          | float(10,2) | NO   |     | NULL    |                |
+----------------+-------------+------+-----+---------+----------------+
4 rows in set (0.00 sec)
```


- **PASSO 3:** ADICIONANDO A COLUNA `PESO` NA ORDEM ESPECIFICADA, DEPOIS DA COLUNA `NOME_PRODUTO`;
```SQL
/*INPUT*/
ALTER TABLE PRODUTO
ADD COLUMN PESO FLOAT(10,2) NOT NULL
AFTER NOME_PRODUTO;

/*OUTPUT*/
mysql> ALTER TABLE PRODUTO
    -> ADD COLUMN PESO FLOAT(10,2) NOT NULL
    -> AFTER NOME_PRODUTO;
Query OK, 0 rows affected (0.03 sec)
Records: 0  Duplicates: 0  Warnings: 0
```


- **PASSO 2:** CONFIRMANDO A INCLUSÃO DA COLUNA `PESO` NA ORDEM ESPECIFICADA, DEPOIS DA COLUNA `NOME_PRODUTO`;
```SQL
/*INPUT*/
DESC PRODUTO;

/*OUTPUT*/
mysql> DESC PRODUTO;
+----------------+-------------+------+-----+---------+----------------+
| Field          | Type        | Null | Key | Default | Extra          |
+----------------+-------------+------+-----+---------+----------------+
| IDPRODUTO      | int(11)     | NO   | PRI | NULL    | auto_increment |
| NOME_PRODUTO   | varchar(30) | NO   |     | NULL    |                |
| PESO           | float(10,2) | NO   |     | NULL    |                |
| VALOR_UNITARIO | varchar(50) | NO   |     | NULL    |                |
| FRETE          | float(10,2) | NO   |     | NULL    |                |
+----------------+-------------+------+-----+---------+----------------+
5 rows in set (0.00 sec)
```


# ⚠ **NOTA 7: ADICIONANDO UMA COLUNA COMO PRIMEIRA DA TABELA, COM `FIRST`**

- **PASSO 1:** APAGAR A COLUNA `PESO`;
```SQL
/*INPUT*/
ALTER TABLE PRODUTO
DROP COLUMN PESO;

/*OUTPUT*/
mysql> ALTER TABLE PRODUTO
    -> DROP COLUMN PESO;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0
```


- **PASSO 2:** CONFIRMANDO A EXCLUSÃO DA COLUNA `PESO` DA `TABELA PRODUTO`;
```SQL
/*INPUT*/
DESC PRODUTO;

/*OUTPUT*/
mysql> DESC PRODUTO;
+----------------+-------------+------+-----+---------+----------------+
| Field          | Type        | Null | Key | Default | Extra          |
+----------------+-------------+------+-----+---------+----------------+
| IDPRODUTO      | int(11)     | NO   | PRI | NULL    | auto_increment |
| NOME_PRODUTO   | varchar(30) | NO   |     | NULL    |                |
| VALOR_UNITARIO | varchar(50) | NO   |     | NULL    |                |
| FRETE          | float(10,2) | NO   |     | NULL    |                |
+----------------+-------------+------+-----+---------+----------------+
4 rows in set (0.01 sec)
```


- **PASSO 3:** ADICIONANDO A COLUNA `PESO` COMO PRIMEIRA DA TABELA `PRODUTO`;
```SQL
/*INPUT*/
ALTER TABLE PRODUTO
ADD COLUMN PESO FLOAT(10,2) NOT NULL
FIRST;

/*OUTPUT*/
mysql> ALTER TABLE PRODUTO
    -> ADD COLUMN PESO FLOAT(10,2) NOT NULL
    -> FIRST;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0
```


- **PASSO 2:** CONFIRMANDO A INCLUSÃO DA COLUNA `PESO` COMO PRIMEIRA NA `TABELA PRODUTO`;
```SQL
/*INPUT*/
DESC PRODUTO;

/*OUTPUT*/
mysql> DESC PRODUTO;
+----------------+-------------+------+-----+---------+----------------+
| Field          | Type        | Null | Key | Default | Extra          |
+----------------+-------------+------+-----+---------+----------------+
| PESO           | float(10,2) | NO   |     | NULL    |                |
| IDPRODUTO      | int(11)     | NO   | PRI | NULL    | auto_increment |
| NOME_PRODUTO   | varchar(30) | NO   |     | NULL    |                |
| VALOR_UNITARIO | varchar(50) | NO   |     | NULL    |                |
| FRETE          | float(10,2) | NO   |     | NULL    |                |
+----------------+-------------+------+-----+---------+----------------+
5 rows in set (0.00 sec)
```
