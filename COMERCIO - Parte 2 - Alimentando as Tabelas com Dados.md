# 🛠 **DATABASE SIMPLES PARA COMERCIO**

* 🧗‍♀️ ETAPAS PARA A CRIAÇÃO, ALIMENTAÇÃO E MANUTENÇÃO DE UM BANCO DE DADO SIMPLES PARA COMÉRCIO

## 🍜 **PARTE 2 - ALIMENTANDO AS TABELAS COM DADOS**


- **PASSO 1:** INSIRA OS DADOS DESEJADOS NA `TABELA CLIENTE`. INICIE COM APENAS UMA INSERÇÃO PARA CONFIRMARMOS A SINTAXE DA QUERY;
```SQL
/*INPUT*/
INSERT INTO CLIENTE VALUES(NULL,'JOAO','M','76567587887');

/*OUTPUT*/
mysql> INSERT INTO CLIENTE VALUES(NULL,'JOAO','M','76567587887');
/* ERROR 1136 (21S01): Column count doesn't match value count at row 1 */
```

- O `Error 1136 (21S01)` aponta que a quantidade de dados a ser inserida não corresponde com a quantidade de colunas para receber esses dados.
Nota-se que está faltando o dado do `EMAIL`.



- **PASSO 2:** CORRIJINDO A QUANTIDADE DE DADOS A SER INSERIDA NA QUERY. ACRESCENTA-SE O DADO DO `EMAIL`;
```SQL
/*INPUT*/
INSERT INTO CLIENTE VALUES(NULL,'JOAO','M','JOAOA@IG.COM','76567587887');

/*OUTPUT*/
mysql> INSERT INTO CLIENTE VALUES(NULL,'JOAO','M','JOAOA@IG.COM','76567587887');
Query OK, 1 row affected (0.00 sec)
```


- **PASSO 3:** INSERINDO OS RESTANTE DOS DADOS NA `TABELA CLIENTE`;
```SQL
/*INPUT*/
INSERT INTO CLIENTE VALUES(NULL,'CARLOS','M','CARLOSA@IG.COM','5464553466');
INSERT INTO CLIENTE VALUES(NULL,'ANA','F','ANA@IG.COM','456545678');
INSERT INTO CLIENTE VALUES(NULL,'CLARA','F',NULL,'5687766856');
INSERT INTO CLIENTE VALUES(NULL,'JORGE','M','JORGE@IG.COM','8756547688');
INSERT INTO CLIENTE VALUES(NULL,'CELIA','M','JCELIA@IG.COM','5767876889');

/*OUTPUT*/
mysql> INSERT INTO CLIENTE VALUES(NULL,'CARLOS','M','CARLOSA@IG.COM','5464553466');
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO CLIENTE VALUES(NULL,'ANA','F','ANA@IG.COM','456545678');
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO CLIENTE VALUES(NULL,'CLARA','F',NULL,'5687766856');
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO CLIENTE VALUES(NULL,'JORGE','M','JORGE@IG.COM','8756547688');
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO CLIENTE VALUES(NULL,'CELIA','M','JCELIA@IG.COM','5767876889');
Query OK, 1 row affected (0.01 sec)
```


- **PASSO 4:** VERIFICANDO OS DADOS INSERIDOS NA `TABELA CLIENTE`;
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
+-----------+--------+------+----------------+-------------+
6 rows in set (0.00 sec)
```

- ⚠ **NOTA 1: INTEGRIDADE REFERENCIAL** - UTILIZANDO O A QUERY A SEGUIR:
```SQL
/*INPUT*/
INSERT INTO ENDERECO VALUES(NULL,'RUA ANTONIO SA','CENTRO','B. HORIZONTE','MG',45);

/*OUTPUT*/
mysql> INSERT INTO ENDERECO VALUES(NULL,'RUA ANTONIO SA','CENTRO','B. HORIZONTE','MG',45);
ERROR 1452 (23000): Cannot add or update a child row: a foreign key constraint fails (`comercio`.`endereco`, CONSTRAINT `endereco_ibfk_1` FOREIGN KEY (`ID_CLIENTE`) REFERENCES `cliente` (`IDCLIENTE`))
```

- O `Error 1452 (23000)` aponta que a chave estrangeira da query `...45);` não tem nenhuma referência na tabela relacioanda de origem.
Nesse caso a `TABELA CLIENTE`. Não há, na coluna `IDCLIENTE`, localizada na `TABELA CLIENTE` onde a `FOREIGN KEY` usa como referência para se ligar ao registro correto, uma `ID` de número `45`.

- O Banco de Dados de tabelas relacionadas exige e garante a integridade referencial.


- **PASSO 5:** INSIRA OS DADOS DESEJADOS NA `TABELA ENDERECO`. INICIE COM APENAS UMA INSERÇÃO PARA CONFIRMARMOS A SINTAXE DA QUERY;
```SQL
/*INPUT*/
INSERT INTO ENDERECO VALUES(NULL,'RUA ANTONIO SA','CENTRO','B. HORIZONTE','MG',4);

/*OUTPUT*/
mysql> INSERT INTO ENDERECO VALUES(NULL,'RUA ANTONIO SA','CENTRO','B. HORIZONTE','MG',4);
Query OK, 1 row affected (0.00 sec)
```


- **PASSO 7:** VERIFICANDO OS DADOS INSERIDOS NA `TABELA ENDERECO`;
```SQL
/*INPUT*/
SELECT * FROM ENDERECO;

/*OUTPUT*/
mysql> SELECT * FROM ENDERECO;
+------------+----------------+--------+--------------+--------+------------+
| IDENDERECO | LOGRADOURO     | BAIRRO | CIDADE       | ESTADO | ID_CLIENTE |
+------------+----------------+--------+--------------+--------+------------+
|          2 | RUA ANTONIO SA | CENTRO | B. HORIZONTE | MG     |          4 |
+------------+----------------+--------+--------------+--------+------------+
1 row in set (0.00 sec)
```

- No caso do `IDENDERECO` iniciar com a posição `2` mesmo sendo o primeiro dado da `TABELA ENDERECO` é que:
Quando o comando de uma query bate em uma checagem de integridade referêncial e o banco de dados rejeita e apaga esses dados,
a posição do `ID` é descartada, utilizando-se a próxima posição.

- Isso não causa nenhum problema de performance ou estrutura no Banco de Dados. Sendo um comportamento normal.

- Nunca se deve bater `PRIMARY KEY` com `PRIMARY KEY`. Isso não existe.

- O correto é comparar `PRIMARY KEY` com `FOREIGN KEY`.


- **PASSO 8:** INSERINDO DADOS NA `TABELA ENDERECO`;
```SQL
/*INPUT*/
INSERT INTO ENDERECO VALUES(NULL,'RUA CAPITAO HERMES','CENTRO','RIO DE JANEIRO','RJ',1);
INSERT INTO ENDERECO VALUES(NULL,'RUA PRES VARGAS','JARDINS','SAO PAULO','SP',3);
INSERT INTO ENDERECO VALUES(NULL,'RUA ALFANDEGA','ESTACIO','RIO DE JANEIRO','RJ',2);
INSERT INTO ENDERECO VALUES(NULL,'RUA DO OUVIDOR','FLAMENGO','RIO DE JANEIRO','RJ',6);
INSERT INTO ENDERECO VALUES(NULL,'RUA URUGUAIANA','CENTRO','VITORIA','ES',5);

/*OUTPUT*/
mysql> INSERT INTO ENDERECO VALUES(NULL,'RUA CAPITAO HERMES','CENTRO','RIO DE JANEIRO','RJ',1);
Query OK, 1 row affected (0.03 sec)

mysql> INSERT INTO ENDERECO VALUES(NULL,'RUA PRES VARGAS','JARDINS','SAO PAULO','SP',3);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO ENDERECO VALUES(NULL,'RUA ALFANDEGA','ESTACIO','RIO DE JANEIRO','RJ',2);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO ENDERECO VALUES(NULL,'RUA DO OUVIDOR','FLAMENGO','RIO DE JANEIRO','RJ',6);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO ENDERECO VALUES(NULL,'RUA URUGUAIANA','CENTRO','VITORIA','ES',5);
Query OK, 1 row affected (0.00 sec)
```


- **PASSO 9:** VERIFICANDO OS DADOS INSERIDOS NA `TABELA ENDERECO`;
```SQL
/*INPUT*/
SELECT * FROM ENDERECO;

/*OUTPUT*/
mysql> SELECT * FROM ENDERECO;
+------------+--------------------+----------+----------------+--------+------------+
| IDENDERECO | LOGRADOURO         | BAIRRO   | CIDADE         | ESTADO | ID_CLIENTE |
+------------+--------------------+----------+----------------+--------+------------+
|          2 | RUA ANTONIO SA     | CENTRO   | B. HORIZONTE   | MG     |          4 |
|          3 | RUA CAPITAO HERMES | CENTRO   | RIO DE JANEIRO | RJ     |          1 |
|          4 | RUA PRES VARGAS    | JARDINS  | SAO PAULO      | SP     |          3 |
|          5 | RUA ALFANDEGA      | ESTACIO  | RIO DE JANEIRO | RJ     |          2 |
|          6 | RUA DO OUVIDOR     | FLAMENGO | RIO DE JANEIRO | RJ     |          6 |
|          7 | RUA URUGUAIANA     | CENTRO   | VITORIA        | ES     |          5 |
+------------+--------------------+----------+----------------+--------+------------+
6 rows in set (0.00 sec)
```


- ⚠ **NOTA 2: INTEGRIDADE REFERENCIAL** - UTILIZANDO O A QUERY A SEGUIR:
```SQL
/*INPUT*/
INSERT INTO ENDERECO VALUES(NULL,'RUA ALFANDEGA','CENTRO','SÃO PAULO','SP',5);

/*OUTPUT*/
mysql> INSERT INTO ENDERECO VALUES(NULL,'RUA ALFANDEGA','CENTRO','SÃO PAULO','SP',5);
ERROR 1062 (23000): Duplicate entry '5' for key 'ID_CLIENTE'
```

- O `Error 1062 (23000)` aponta que a chave estrangeira da query `...5);` já existe. Nesse caso a condição da chave estrangeira `ID_CLIENTE` está sob a cláusula `UNIQUE`.

- A cláusula `UNIQUE`  informa ao Bando de Dados que o `ID_CLIENTE`, que é uma chave estrangeira, deve ser único e não poderá se repetir.



- **PASSO 10:** INSIRA OS DADOS DESEJADOS NA `TABELA TELEFONE`. INICIE COM APENAS UMA INSERÇÃO PARA CONFIRMARMOS A SINTAXE DA QUERY;
```SQL
/*INPUT*/
INSERT INTO TELEFONE VALUES(NULL,'CEL','78458743',5);

/*OUTPUT*/
mysql> INSERT INTO TELEFONE VALUES(NULL,'CEL','78458743',5);
Query OK, 1 row affected (0.01 sec)
```


- **PASSO 11:** VERIFICANDO OS DADOS INSERIDOS NA `TABELA TELEFONE`;
```SQL
/*INPUT*/
SELECT * FROM TELEFONE;

/*OUTPUT*/
mysql> SELECT * FROM TELEFONE;
+------------+------+----------+------------+
| IDTELEFONE | TIPO | NUMERO   | ID_CLIENTE |
+------------+------+----------+------------+
|          1 | CEL  | 78458743 |          5 |
+------------+------+----------+------------+
1 row in set (0.00 sec)
```


- **PASSO 12:** INSERINDO DADOS NA `TABELA TELEFONE`;
```SQL
/*INPUT*/
INSERT INTO TELEFONE VALUES(NULL,'RES','56576876',5);
INSERT INTO TELEFONE VALUES(NULL,'CEL','87866896',1);
INSERT INTO TELEFONE VALUES(NULL,'COM','54768899',2);
INSERT INTO TELEFONE VALUES(NULL,'RES','99667587',1);
INSERT INTO TELEFONE VALUES(NULL,'CEL','78989765',3);
INSERT INTO TELEFONE VALUES(NULL,'CEL','99766676',3);
INSERT INTO TELEFONE VALUES(NULL,'COM','66687899',1);
INSERT INTO TELEFONE VALUES(NULL,'RES','89986668',5);
INSERT INTO TELEFONE VALUES(NULL,'CEL','88687909',2);

/*OUTPUT*/
mysql> INSERT INTO TELEFONE VALUES(NULL,'RES','56576876',5);
Query OK, 1 row affected (0.02 sec)

mysql> INSERT INTO TELEFONE VALUES(NULL,'CEL','87866896',1);
Query OK, 1 row affected (0.01 sec)

mysql> INSERT INTO TELEFONE VALUES(NULL,'COM','54768899',2);
Query OK, 1 row affected (0.02 sec)

mysql> INSERT INTO TELEFONE VALUES(NULL,'RES','99667587',1);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO TELEFONE VALUES(NULL,'CEL','78989765',3);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO TELEFONE VALUES(NULL,'CEL','99766676',3);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO TELEFONE VALUES(NULL,'COM','66687899',1);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO TELEFONE VALUES(NULL,'RES','89986668',5);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO TELEFONE VALUES(NULL,'CEL','88687909',2);
Query OK, 1 row affected (0.00 sec)
```


- **PASSO 13:** VERIFICANDO OS DADOS INSERIDOS NA `TABELA TELEFONE`;
```SQL
/*INPUT*/
SELECT * FROM TELEFONE;

/*OUTPUT*/
mysql> SELECT * FROM TELEFONE;
+------------+------+----------+------------+
| IDTELEFONE | TIPO | NUMERO   | ID_CLIENTE |
+------------+------+----------+------------+
|          1 | CEL  | 78458743 |          5 |
|          2 | RES  | 56576876 |          5 |
|          3 | CEL  | 87866896 |          1 |
|          4 | COM  | 54768899 |          2 |
|          5 | RES  | 99667587 |          1 |
|          6 | CEL  | 78989765 |          3 |
|          7 | CEL  | 99766676 |          3 |
|          8 | COM  | 66687899 |          1 |
|          9 | RES  | 89986668 |          5 |
|         10 | CEL  | 88687909 |          2 |
+------------+------+----------+------------+
10 rows in set (0.00 sec)
```