# Aulinhas de banco

## O que é

- São vários bancos de dados (databases)
- Databases tem várias tabelas - definição de um esquema e suas características (colunas)
- Tabelas tem vários registros/linhas

## Tipos de comandos SQL

- DDL - Criação de databases e tabelas - cria apenas a parte lógica, não os dados em sí
- DML - Manipula os dados - insere, atualiza e deleta dados das tabelas
- DQL - Consulta os dados das tabelas - pode consultar dados de mais de uma tabela ao mesmo tempo

## Tipo de dados

Comparação com Python

| python   | sql      |
| -------- | -------- |
| int      | integer  |
| str      | varchar  |
| float    | float    |
| bool     | bool     |
| date     | date     |
| datetime | datetime |

## Criando Tabela (sem dados)

Colunas

- id - int
- cliente_name - varchar
- course_id - int
- mensalidade - float

Exemplo

```sql
CREATE TABLE [IF NOT EXISTS] table_name (
   column1 datatype(length) column_contraint,
   column2 datatype(length) column_contraint,
   column3 datatype(length) column_contraint,
   table_constraints
);
```

Criacao - DDL

```sql
CREATE TABLE compras (
    id int,
    cliente_name varchar,
    course_id int,
    mensalidade decimal(5, 2)
)
```

Deletar tabela - DDL

```sql
DROP TABLE compras
```

## Inserir dados - DML

Precisa escrever qual tabela queremos inserir e quais colunas

Exemplo

```sql
INSERT INTO table_name (Colunas, [separado por virgula]) VALUES (Valores, [separado por virgula])
```

Insercao

```sql
INSERT INTO compras (id, cliente_name, course_id, mensalidade) VALUES (24, 'Felipe Gomes', 13, 99.9)

INSERT INTO compras VALUES (24, 'Felipe Gomes', 13, 99.9)

INSERT INTO compras VALUES
(25, 'Roger Guedes', 10, 119.90),
(26, 'Carla Amorim', 12, 250.00),
(27, 'Eduardo Queiroz', 10, 119.90)
```

## Consultar dados - DQL

### Operadores condicionais

| python                        | sql                           |
| :---------------------------: | :--------------------------:  |
| >                             | >                             |
| <                             | <                             |
| <=                            | <=                            |
| >=                            | >=                            |
| ==                            | =                             |
| != ou not                     | != ou <>                      |

Selecionar todas as colunas da tabela compras

```sql
select * from compras
```

Selecionar o nome e a mensalidade da tabela compras

```sql
select cliente_name, mensalidade from compras
```

### Com filtros

Selecionar o nome e a mensalidade das compras que sao maiores que `100`

```sql
select cliente_name, mensalidade
from compras
where mensalidade > 100
```

Selecionar o nome e a mensalidade das compras que sao maiores que `900`

```sql
select cliente_name, mensalidade
from compras
where mensalidade > 900
```

Selecionar o nome e a mensalidade das compras que sao iguais a `250`

```sql
select cliente_name, mensalidade
from compras
where mensalidade = 250
```

Selecionar o nome e a mensalidade das compras que sao diferentes de `250`

```sql
select cliente_name, mensalidade
from compras
where mensalidade != 250
```

### Consultar com ordenação

Ordenar pelo id do curso

```sql
Select * FROM cursos
ORDER BY id asc(ou desc)
```

## Atualizar linhas

Atualizar a mensalidade de todos para `1000`

```sql
UPDATE compras SET mensalidade = 1000
```

Atualizar a mensalidade de todos para `1000`

### Atualizar com filtros

Atualizar o nome do cliente para `Clebinho` quando o nome dele for igual a `Carla Amorim`

```sql
UPDATE compras SET cliente_name = 'Clebinho'
where cliente_name = 'Carla Amorim'
```

Atualizar a mensalidade para `100` de quem tem o curso com o id `10`

```sql
UPDATE compras SET mensalidade = 100
where course_id = 10
```

## Deletar registros

## Tomar muito cuidado com DELETE SEM WHERE

Deletar todos os registros da tabela compras

```sql
DELETE FROM compras
```

### Deletar com filtro

Deletar os registros de quem tem o id do curso igual a `10`

```sql
DELETE FROM compras
where course_id = 10
```

## Consultar com múltiplos filtros

Consultar o nome de quem tem o curso igual `10` e a mensalidade eh maior que `100`

```sql
select cliente_name
from compras
where course_id = 10 and mensalidade > 100
```

Consultar o nome e a mensalidade de quem tem o curso igual `10` ou a mensalidade eh igual a `250`

```sql
select cliente_name,mensalidade
from compras
where course_id = 10 or mensalidade = 250
```

## Joins

Adicionando condicionais (match de chaves) nos joins

```sql
[INNER|LEFT|RIGHT|FULL] JOIN ON
    tabela_a.id = tabela_b.id
```

Adicionando condicionais (match de chaves compostas) nos joins

```sql
[INNER|LEFT|RIGHT|FULL] JOIN ON
    users.id = compras.user_id AND
    users.cpf = compras.user_cpf
```

### (INNER) JOIN

Retorna registros que existem estritamente nas duas tabelas

| A   | B   | Retorna    |
| --- | --- | ---------- |
| 1   | -   | Falso      |
| 2   | 2   | Verdadeiro |
| -   | 3   | Falso      |
| -   | -   | Falso      |

### LEFT JOIN

Retorna todos os registros da tabela da esquerda (a primeira que aparece na query) e os registros que derem match na tabela da direita (que aparece depois)

| A   | B   | Retorna    |
| --- | --- | ---------- |
| 1   | -   | Verdadeiro |
| 2   | 2   | Verdadeiro |
| -   | 3   | Falso      |
| -   | -   | Falso      |

### RIGHT JOIN

Retorna todos os registros da tabela da direita (que aparece depois na query) e os registros que derem match na tabela da esquerda (que aparece antes)

| A   | B   | Retorna    |
| --- | --- | ---------- |
| 1   | -   | Falso      |
| 2   | 2   | Verdadeiro |
| -   | 3   | Verdadeiro |
| -   | -   | Falso      |

### FULL JOIN - O pior de todos

Retorna todos os registros das duas tabelas

| A   | B   | Retorna    | Colunas Tab. A NOT NULL | Colunas Tab. B NOT NULL |
| --- | --- | ---------- | ----------------------- | ----------------------- |
| 1   | -   | Verdadeiro | SIM                     | NÃO                     |
| 2   | 2   | Verdadeiro | SIM                     | SIM                     |
| -   | 3   | Verdadeiro | NÃO                     | SIM                     |
| -   | -   | Falso      | NÃO                     | NÃO                     |

Tabela Users

| id  | nome    | cpf |
| --- | ------- | --- |
| 1   | jason   | 444 |
| 2   | larissa | 333 |
| 10  | maggie  | 555 |

Tabela Compras

| id  | user_id | mensalidade |
| --- | ------- | ----------- |
| 1   | 1       | 100         |
| 2   | 2       | 299         |
| 3   | 1       | 300         |
| 4   | 4       | 400         |
| 5   | 5       | 500         |

Resultado FULL JOIN

| compras_id | compras_user_id | compras_mensalidade | users_id | users_nome | users_cpf |
| ---------- | --------------- | ------------------- | -------- | ---------- | --------- |
| 1          | 1               | 100                 | 1        | jason      | 444       |
| 2          | 2               | 299                 | 2        | larissa    | 333       |
| 3          | 1               | 300                 | 1        | jason      | 444       |
| 4          | 4               | 400                 | NULO     | NULO       | NULO      |
| 5          | 5               | 500                 | NULO     | NULO       | NULO      |
| -          | -               | -                   | 10       | maggie     | 555       |

## JOINS ENCADEADOS

Sintaxe

```sql
SELECT coluna_1, coluna_2, coluna_3
FROM tabela_A INNER JOIN tabela_B ON
    tabela_A.id = tabela_B.a_id
INNER JOIN tabela_C ON
    tabela_B.id = tabela_C.b_id
LEFT JOIN tabela_D ON
    tabela_C.id = tabela_D.c_id
```

## ORDER BY

Ordena os registros, NÃO A ORDEM DAS COLUNAS

- Número: ordena de forma crescente ou decrescente
- Palavras: ordena de forma alfabética (de A a Z) ou de Z a A

### Exemplo

Listar o nome da cidade, nome do estado e a população da cidade. Ordenar primeiro pelo nome do estado e depois pela maior população (decrescente)

```sql
SELECT cidade, estado, cidade_população
FROM cidades
INNER JOIN estados ON
    cidades.id_estado = estados.id
ORDER BY
    estado, cidade_população DESC
```

| cidade         | estado | população |
| -------------- | ------ | --------- |
| Curitiba       | PR     | 1000      |
| Caçapava       | SP     | 10        |
| SJC            | SP     | 100       |
| Belo Horizonte | MG     | 500       |
| São Paulo      | SP     | 1000      |

Resultado ordenado

| cidade         | estado | população |
| -------------- | ------ | --------- |
| Belo Horizonte | MG     | 500       |
| Curitiba       | PR     | 1000      |
| São Paulo      | SP     | 1000      |
| SJC            | SP     | 100       |
| Caçapava       | SP     | 10        |

Resultado se `ORDER BY população DESC, estado`

| cidade         | estado | população |
| -------------- | ------ | --------- |
| Curitiba       | PR     | 1000      |
| São Paulo      | SP     | 1000      |
| Belo Horizonte | MG     | 500       |
| SJC            | SP     | 100       |
| Caçapava       | SP     | 10        |
