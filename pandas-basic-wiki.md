# Pandas Basic Wiki

Trata-se de uma Wiki que apresentará as funcionalidades básicas da biblioteca *Pandas*.

<br>

**Sumário**
1. [Importando a biblioteca](#importando-a-biblioteca)
1. [Lendo arquivo .csv](#lendo-arquivo-.csv)
1. [](#)
1. [](#)
1. [](#)
1. [](#)
1. [](#)
1. [](#)
1. [](#)
1. [](#)
1. [](#)
1. [](#)
1. [](#)
1. [](#)

<br>

## Importando a biblioteca

```py
import pandas as pd
```
<br>

## Lendo arquivo .csv

```py
data = pd.read_csv('data.csv')
```

<br>

## Lendos os títulos das colunas

```py
titulo_coluna = data.columns
```

<br>

## Lendo uma coluna específica

```py
coluna_especifica = data['Coluna 2']
```

<br>

## Lendo uma linha específica

```py
linha_especifica = data.iloc[341]
```

<br>

## Lendo todas as linhas que possuem a mesma informação em uma dada coluna

```py
linhas_mesma_info = data.loc[data['Nome'] == 'Judite']
```

<br>

## Organizar os dados por um valor de coluna específico

```py
data_organizada = data.sort_values(['Coluna 3', 'Name'])
```

<br>

## Retirando colunas

```py
data_sem_uma_coluna = data.drop(columns=['Coluna Indesejada'])
```

<br>

## Reorganizando colunas

```py
colunas = list(data.columns.values)
data_alterada = data[
    colunas[0:3] + [colunas[-2]] + [colunas[9]] + colunas[-4:-6] +
    colunas[3:9] + colunas[10:14:] + [colunas[-3]] + [colunas[-1]]
    ]
```

<br>

## Escrevendo/Criando arquivos .csv

```py
data_alterada.to_csv('nova-data.csv', index=False)
```

<br>

## Escrevendo/Criando arquivos .xlsx

```py
data_alterada.to_excel('nova-data.xlsx', index=False)
```

<br>
