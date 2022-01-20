# Pandas Basic Wiki

Trata-se de uma Wiki que apresentará as funcionalidades básicas da biblioteca *Pandas*.

<br>

**Sumário**
1. [Importando a biblioteca](#importando-a-biblioteca)
1. [Lendo arquivo .csv](#lendo-arquivo-.csv)
1. [Lendo o título de todas as colunas](#lendo-o-título-de-todas-as-colunas)
1. [Lendo uma coluna específica](#lendo-uma-coluna-específica)
1. [Lendo uma linha específica](#Lendo-uma-linha-específica)
1. [Lendo todas as linhas de valores iguais](#lendo-todas-as-linhas-de-valores-iguais)
1. [Organizando os dados à partir de colunas](#organizando-os-dados-à-partir-de-colunas)
1. [Retirando colunas](#retirando-colunas)
1. [Reorganizando colunas](#reorganizando-colunas)
1. [Criando arquivos .csv](#criando-arquivos-.csv)
1. [Criando arquivos .xlsx](#criando-arquivos-.xlsx)
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

## Lendo o título de todas as colunas

```py
titulo_colunas = data.columns
```

<br>

## Lendo uma coluna específica

```py
coluna_especifica = data['Coluna 2']
```

<br>

## Lendo uma linha específica

```py
linha_especifica = data.iloc[5]
```

<br>

## Lendo todas as linhas de valores iguais

```py
linhas_mesma_info = data.loc[data['Nome'] == 'Judite']
```

<br>

## Organizando os dados à partir de colunas

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

## Criando arquivos .csv

```py
data_alterada.to_csv('nova-data.csv', index=False)
```

<br>

## Criando arquivos .xlsx

```py
data_alterada.to_excel('nova-data.xlsx', index=False)
```

<br>

## Lendo colunas a partir de um parâmetro

```py
data.loc[
    (data.School == 'Transmutation') &
    (data['Damage/Effect'] == 'Control') & (data.Level >= 3)
    ])
```

<br>


## Resetar index e retirar coluna da index antiga

```py
new_data = data.loc[(data['Damage/Effect'] == 'Creation')]
new_data.reset_index(drop=True, inplace=True)
```

<br>

## Lendo todas as linhas com mesmo trechos de str em uma coluna

```py
print(data.loc[data.Name.str.contains('Fire|Flame')])
```

<br>

## Alterando nomes de uma coluna

```py
data.loc[data.Source == 'Tasha\'s Cauldron of Everything', 'Source'] = \
    'Tasha\'s Cauldron'
```

<br>
