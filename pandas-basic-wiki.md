# Pandas Basic Wiki

Trata-se de uma Wiki que apresenta os recursos básicos da biblioteca *Pandas*.  

<br>

**Sumário**
1. [Armazenando os dados](#armazenando-os-dados)
    1. [Importando a biblioteca](#importando-a-biblioteca)
    1. [Lendo arquivos .csv](#lendo-arquivo-csv)
    1. [DataFrame](#dataframe)
1. [Vizualizando os dados](#vizualizando-os-dados)
    1. [Formato de exibição do dataframe](#Formato-de-exibição-do-dataframe)
    1. [Exibindo as informações gerais](#exibindo-as-informações-gerais)
    1. [Lendo o título de todas as colunas](#lendo-o-título-de-todas-as-colunas)
    1. [Lendo colunas específicas](#lendo-colunas-específicas)
    1. [Lendo linhas específicas](#Lendo-linhas-específicas)
1. [Lendo todas as linhas de valores iguais](#lendo-todas-as-linhas-de-valores-iguais)
1. [Organizando os dados à partir de colunas](#organizando-os-dados-à-partir-de-colunas)
1. [Retirando colunas](#retirando-colunas)
1. [Reorganizando colunas](#reorganizando-colunas)
1. [Criando arquivos .csv](#criando-arquivos-csv)
1. [Criando arquivos .xlsx](#criando-arquivos-xlsx)
1. [Lendo colunas a partir de um parâmetro](#lendo-colunas-a-partir-de-um-parâmetro)
1. [Resetar index e retirar coluna index antigo](#resetar-index-e-retirar-coluna-index-antigo)
1. [Lendo todas as linhas com mesmo trechos de str de uma coluna](#lendo-todas-as-linhas-com-mesmo-trechos-de-str-de-uma-coluna)
1. [Alterando nomes de uma coluna](#alterando-nomes-de-uma-coluna)

<br>

# Armazenando os dados

## Importando a biblioteca

Para se utilizar qualquer biblioteca em python é necessário primeiro importa-la. Nessa Wiki a utilizaremos por meio de sua forma abreviada `pd`. 

```py
import pandas as pd
```

<br>

## Lendo arquivo .csv
Para trabalhar com um arquivo tipo CSV (valores separados por vírgulas) basta utilizar o método `read_csv()` e inserir entre parênteses o caminho do arquivo. No exemplo abaixo armazenamos o conteúdo na variável `data`.
```py
data = pd.read_csv('data.csv')
```

<br>

## DataFrame
O conteúdo é armazenado em uma variável do tipo objeto chamada *DataFrame*.
Se utilizarmos o comando `print(type(data))` receberemos o seguinte output:
```
<class 'pandas.core.frame.DataFrame'>
```

<br>

# Vizualizando os dados

## Formato de exibição do dataframe

O comando `print(data)` exibirá as cinco primeiras e cinco últimas linhas do nosso conjunto de dados. As colunas podem ser apresentadas em sua totalidade ou não, variando conforme o espaço disponível para apresenta-las. Os dados das linhas e colunas ocultadas são representados por reticências "`...`".  
No topo de cada coluna é possível ler seus respectivos títulos, no canto esquerdo é exibido uma coluna "extra" correspondente ao index de cada linha - em que 0 equivale a primeira linha e assim por diante - e ao fim, entre colchetes, é exibido o número total de linhas e colunas do dataframe.

<br>

## Exibindo as informações gerais

Para se obter as informações gerais do dataframe é possível utilizar o método `info()`.
```py
info_gerais = data.info()
```

<br>

## Lendo o título de todas as colunas
Para obter todos os títulos presentes no dataframe basta utilizar o atributo `.columns`.

```py
titulo_colunas = data.columns
```

<br>

## Lendo colunas específicas
O modo para selecionar colunas específicas dentro do dataframe varia conforme o número de colunas que se deseja obter. 
Para uma única coluna, é possível utilizar o nome do dataframe seguido de um ponto e o nome da coluna, ou utilizar o nome da coluna entre aspas simples ou duplas e colchetes.  
Para selecionar mais de uma coluna, deve-se utilizar o nome de cada coluna entre aspas, separadas por vírgula e todas elas inseridas entre **dois** colchetes.
```py
coluna_especifica = data.Coluna1
coluna_especifica = data['Coluna1']

mais_de_uma_coluna = data[['Coluna1', 'Coluna2']]
```

<br>

## Lendo linhas específicas
À partir do index gerado pelo dataframe podemos obter linhas específicas do conjunto de dados. Para isso podemos utilizar tanto o atributo `.loc` quanto o atributo `.iloc`. Basta inserir o index da linha entre colchetes.  
Para selecionar mais de uma linha é possível utilizar vírgulas entre cada index que se deseja obter e utilizar dois colchetes ao invés de um. Ou ainda utilizar dois pontos como se fossem listas entre o primeiro e último index, deve-se ressaltar que assim como as listas, o atributo `.iloc` deixará de fora o último elemento, o mesmo não ocorrendo com `.loc`, que exibirá inclusive a última linha do index inserido.

```py
linha_especifica = data.loc[5]
linha_especifica = data.iloc[2]

mais_de_uma_linha = data.loc[2:6]
mais_de_uma_linha = data.iloc[4:7]

mais_de_uma_linha = data.loc[[2, 4, 6]]
mais_de_uma_linha = data.iloc[[4, 7, 12]]
```

<br>

## Lendo células específicas
À partir do index e utilizando ainda os atributos `.iloc` e `.loc` é possível obter os valores de células específicas dentro do dataframe. Para isso deve-se compreender a "estrutura" desses atributos.  
Ambos podem ser retratados da seguinte maneira:
```
data.loc[<linha>, <coluna>]
```
Mas há uma diferença importante entre ambos, `.iloc` trata as colunas como index, ou seja, aceita apenas os valores de 0 até o último index correspondente às colunas, enquanto `.loc` aceita apenas os respectivos títulos das colunas. Observe no exemplo abaixo.
```py
data.iloc[0, 0]

data.loc[0, 'Coluna1']
```
Ambos os comandos apontam para a mesma célula, isto é, para o conteúdo da primeira linha na primeira coluna.

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
    (data.Name == 'Joao') &
    (data['Idade'] >= '30')
    ]
```

<br>


## Resetar index e retirar coluna index antigo

```py
new_data = data.loc[(data['Damage/Effect'] == 'Creation')]
new_data.reset_index(drop=True, inplace=True)
```

<br>

## Lendo todas as linhas com mesmo trechos de str de uma coluna

```py
print(data.loc[data.Name.str.contains('Joao|Judite')])
```

<br>

## Alterando nomes de uma coluna

```py
data.loc[data.Source == 'Joao maria', 'Name'] = 'Joao Maria'
```

<br>
