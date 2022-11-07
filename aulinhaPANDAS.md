# IMPORTANDO PANDAS

```python
import pandas as pd
```

# Criando um Dataframe

## Se os dados já estiverem dentro do arquivo em uma variável(um dict por exemplo):

```python
df = pd.DataFrame(variavel)
```

## Se os dados estiverem dentro de um arquivo `.csv`:

Usando de exemplo o arquivo `users.txt` da api do primeiro semestre. Nesse caso, todas as linhas do arquivo são de dados, incluindo a primeira linha, que deveria ter os nomes das colunas.

- `sep`: separador que está sendo usado no arquivo entre aspas duplas, o padrão da função é a vírgula ","

- `header`: quantas linhas do arquivo ele vai ignorar:
    1. `None` = nenhuma
    2. `[0,1,...,n]` = da primeira em diante

- `names`: nomes que serão usados para as colunas. Caso as colunas não estejam nomeadas no arquivo, elas serão criadas apenas. Caso estejam nomeadas no arquivo, esses nomes serão substituidos pelos novos; nesse caso, o ideal é usar o `header` diferente de `None`

- `usecols`: colunas que serão mostradas. Elas serão mostradas na ordem do arquivo, independente da ordem que colocar dentro do parâmetro

- `index_col`: usa uma das colunas do arquivo como a coluna de índice (coluna principal) no df. Permite especificar mais de uma coluna de índice

```python
df = pd.read_csv("~/users.txt", 
    sep=";", 
    header=None, 
    names=["id", "category", "name", "email", "password"],
    usecols=["id", "category", "name", "email"],
    index_col="id"
    )
```

## Funções

`.shape`: mostra o número de linhas e colunas no formato de tupla `(linhas,colunas)`

`.groupby`: agrupa os valores das colunas