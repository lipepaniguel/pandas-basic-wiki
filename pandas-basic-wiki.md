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
1. [Triagem por index e título de coluna]
    1. [Lendo colunas específicas](#lendo-colunas-específicas)
    1. [Lendo linhas específicas](#lendo-linhas-específicas)
1. [Triagem por conteúdo](#triagem-por-conteúdo)
    1. [Lendo linhas pelos valores de colunas](#lendo-linhas-pelos-valores-de-colunas)
    1. [Lendo linhas por trechos de str do conteúdo](#lendo-linhas-por-trechos-de-str-do-conteúdo)
1. [Organizando os dados à partir de colunas](#organizando-os-dados-à-partir-de-colunas)
1. [Retirando colunas](#retirando-colunas)
1. [Reorganizando colunas](#reorganizando-colunas)
1. [Criando arquivos .csv](#criando-arquivos-csv)
1. [Criando arquivos .xlsx](#criando-arquivos-xlsx)
1. [Resetar index e retirar coluna index antigo](#resetar-index-e-retirar-coluna-index-antigo)
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

O comando `print(data)` exibirá as cinco primeiras e cinco últimas linhas do nosso conjunto de dados. As colunas podem ser apresentadas em sua totalidade ou não, variando conforme o espaço disponível para apresenta-las. Os dados das linhas e colunas ocultadas são representados por reticências `...`.  
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

sequencia_de_linhas = data.loc[2:6]
sequencia_de_linhas = data.iloc[4:7]

mais_de_uma_linha = data.loc[[2, 4, 6]]
mais_de_uma_linha = data.iloc[[4, 7, 12]]
```
Para selecionar uma sequência de linhas é possível ainda omitir ambos os tributos, utilizando diretamente colchetes e indicando o intervalo do index por meio de dois pontos, assim como no atributo `.iloc`, a linha representada pelo ultimo index inserido é deixada de fora.
```py
sequencia_de_linhas = data[4:15]
```

<br>

# Triagem por conteúdo

## Lendo linhas pelo conteúdo das colunas 
O atributo `.loc` nos permite ainda selecionar linhas à partir do conteúdo de uma determinada coluna, retornando todas as linhas que apresentarem esse mesmo valor. É possível utilizar todos os operadores de comparação.
```py
linhas_mesma_info = data.loc[data['Nome'] == 'Judite']
```
Além disso, é possível selecionar linhas à partir do conteúdo de mais de uma coluna, estabelencendo relação entre elas. Para isso é possível utilizar operadores lógicos como "and" ou "or", entretanto nessa biblioteca eles são representados por `&` significando o mesmo que `and` e `|` significando o mesmo que `or`.
```py
data.loc[(data['Nome'] == 'Joao') & (data['Idade'] >= '30')]
```

<br>

## Lendo linhas por trechos de str do conteúdo

```py
print(data.loc[data.Name.str.contains('Joao|Judite')])
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

## Resetar index e retirar coluna index antigo

```py
new_data = data.loc[(data['Damage/Effect'] == 'Creation')]
new_data.reset_index(drop=True, inplace=True)
```

<br>

## Alterando nomes de uma coluna

```py
data.loc[data.Source == 'Joao maria', 'Name'] = 'Joao Maria'
```

<br>
