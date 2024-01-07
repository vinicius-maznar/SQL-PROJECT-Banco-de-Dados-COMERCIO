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