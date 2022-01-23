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
    1. [Exibindo as n primeiras linhas](#exibindo-as-n-primeiras-linhas)
    1. [Exibindo as informações gerais](#exibindo-as-informações-gerais)
    1. [Lendo o título de todas as colunas](#lendo-o-título-de-todas-as-colunas)
    1. [Lendo linhas e colunas em formato de lista](#lendo-linhas-e-colunas-em-formato-de-lista)
1. [Triagem por index e título de coluna](#triagem-por-index-e-título-de-coluna)
    1. [Lendo colunas específicas](#lendo-colunas-específicas)
    1. [Lendo linhas específicas](#lendo-linhas-específicas)
    1. [Lendo células específicas](#lendo-células-específicas)
1. [Triagem por conteúdo de célula](#triagem-por-conteúdo-de-célula)
    1. [Lendo linhas pelo conteúdo das colunas](#lendo-linhas-pelo-conteúdo-das-colunas)
    1. [Lendo linhas por trechos de str do conteúdo](#lendo-linhas-por-trechos-de-str-do-conteúdo)
1. [Editando o dataframe](#editando-o-dataframe)
    1. [Parâmetros de organização](#parâmetros-de-organização)
    1. [Reorganizando linhas à partir de colunas](#reorganizando-linhas-à-partir-de-colunas)
    1. [Retirando linhas e colunas](#retirando-linhas-e-colunas)
    1. [Reorganizando linhas e colunas](#reorganizando-linhas-colunas)
    1. [Alterando valores de uma coluna](#alterando-valores-de-uma-coluna)
    1. [Corrigindo a coluna index](#corrigindo-a-coluna-index)
1. [Escrevendo arquivos](#escrevendo-arquivos)    
    1. [Criando arquivos .csv](#criando-arquivos-csv)
    1. [Criando arquivos .xlsx](#criando-arquivos-xlsx)

<br>

# Armazenando os dados

## Importando a biblioteca

Para se utilizar qualquer biblioteca em python é necessário primeiro importa-la. Nessa Wiki a utilizaremos por meio de sua forma abreviada `pd`. 

```py
import pandas as pd
```

<br>

## Lendo arquivos .csv
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

## Exibindo as n primeiras linhas
Por meio do método `.head()` é possível obter, por padrão, as cinco primeiras linhas do dataframe. Além disso, é possível inserir um valor n entre os parêntes, sendo retornado as n primeiras linhas do dataframe. Mas dependendo da quantidade de linhas, será retornado apenas as cinco primeiras e cinco últimas, e o intervalo ocultado será representado por `...`.
```py
print(data.head(25))
```

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

## Lendo linhas e colunas em formato de lista
O método `.tolist()` pode se mostrar muito útil conforme for sendo necessário visualizar e manipular os dados do dataframe. Basta inseri-lo após a seleção de uma linha ou coluna e ele retornará uma lista com todos os valores selecionados.
```
lista_titulo_colunas = data.columns.tolist()
```

<br>

# Triagem por index e título de coluna

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

# Triagem por conteúdo de célula

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
O método str.contains() é capaz de checar se uma determinada coluna apresenta um determinado trecho de `string`, retornando um valor booleano.
```py
data['nome'].str.contains('João')
```
À partir desse método é possível, juntamente com o atributo `.loc`, obter determinadas linhas que apresentem tal trecho de string. Por meio de operadores lógicos, é possível utilizar, inclusive, mais de um trecho de string.
```py
print(data.loc[data.Name.str.contains('Joao|Judite')])
```

<br>

# Editando o dataframe
## Parâmetros de organização
Existem alguns parâmetros úteis para serem utilizados quando se deseja reorganizar o dataframe. Talvez o principal deles seja `ascending`. Ele é responsável por representar os valores de forma ascendente (do menor para o maior) quando seu valor for `True`, ou por ordem decrescente (do maior para o menor) quando seu valor for `False`. Se esse parâmetro não for informado, por padrão ele sempre será `True`.  
Um outro parâmetro que pode ser útil é o `ignore_index`. Quando se reorganiza a ordem das linhas de um dataframe, o index permanece permanece com os valores originais de quando foi gerado, ou seja o atributo possui o valor `False` por padrão. Para que o index corresponda a disposição da nova ordem de linhas deve-se alterar o parâmetro `ignore_index` para `True`.

<br>

## Reorganizando linhas à partir de colunas
Uma forma de reorganizar as linhas de um dataframe é utilizar os valores de uma ou mais colunas como critério de organização por meio do método `.sort_values()`.  
Abaixo vemos um dataframe reorganizado pelos valores da "Idade", à partir dos maiores valores, no caso, dos mais velhos, aos de menores valores, ou seja, aos mais novos.

```py
data_reorganizada = data.sort_values('Idade', ascending=False)
```
É possível utilizar os valores de mais de uma coluna para organizar as linhas, a prioridade para organiza-las segue a ordem em que foram dispostas.  
No exemplo abaixo, os dados foram organizados conforme a "Idade" e em seguida o "Nome", ou seja, a ordem é dos mais novos aos mais velhos e entre os de mesma idade, a ordem segue àquela do alfabeto. Ainda nesse mesmo exemplo o index antigo é ignorado, e a nova disposição passa a receber um novo index próprio, organizado à partir de 0.
```py
data_reorganizada = data.sort_values(['Idade', 'Nome'], ignore_index=True)
```

<br>

## Retirando linhas e colunas
Com o método `.drop()` é possível remover do dataframe qualquer linha ou coluna, basta inserir o parâmetro `index` dentro do parênteses atribuindo o número do index da linha que se deseja retirar ou inserindo o parâmetro `columns`, também atribuindo o nome da coluna entre aspas que se deseja retirar.
```py
data_sem_a_linha = data.drop(index=3)

data_sem_a_coluna = data.drop(columns='Coluna Indesejada')
```

<br>

## Reorganizando linhas e colunas
À partir do atributo `.values`, que retorna uma lista com valores ordenados, é possível reorganizar o dataframe, optando por quais linhas ou colunas serão obtidas, podendo alterar dessa forma também as suas respectivas ordens.  
O primeiro passo é armazenar o valor obtido pelo atributo `.values` em uma variável do tipo lista. Assim podemos tratar cada uma das linhas ou colunas como um index.  
No caso das linhas, deve utilizar o atributo `.iloc` para podermos indicar as linhas que dejemos obter.
```py
linhas = list(data.index.values)
nova_data = data.iloc[linhas[0:3] + [linhas[5]]]
```
Já para colunas o processo é mais simples, basta apenas indicar o index das colunas por meio da lista criada.
```py
colunas = list(data.columns.values)
nova_data = data[colunas[0:3] + [colunas[7]]
```

<br>

## Alterando valores de uma coluna
É possível alterar valores de uma coluna no dataframe à partir de um determinado filtro. Dependendo do tipo de filtro é possível alterar apenas um valor ou todos os valores correspondentes ao grupo filtrado.  
Para se criar o filtro é utilizado o atributo `.loc` com o nome da coluna e o valor correspondente a ser filtrado. Em seguida utiliza-se o nome da coluna a ser alterada, por fim é atribuído o novo valor a ser substituído. Ou seja, será alterado cada um dos elementos presentes na coluna selecionada, de acordo com o filtro estipulado. A estrutura do código pode ser observada abaixo.
```py
data.loc[data['coluna_filtrada'] == 'valor_filtrado', 'coluna_a_ser_alterada'] = 'novo_valor'
```
Se quisermos, por exemplo, alterar a idade de todo os Josés presentes em um dataframe para 31 anos.
```py
data.loc[data['Nome'] == 'José', 'Idade'] = '31'
```

<br>

## Corrigindo a coluna index
Após editar o conjunto de dados pode-se querer atribuir um novo index ao dataframe, para isso é possível utilizar o método `.reset_index`.  Ele pode ser utilizado sem parâmetro nenhum, como no exemplo abaixo,
à partir da criação de um novo dataframe que apresentará o novo index bem como uma tabela "extra" contendo o index antigo.
```py
new_data = data.reset_index()
```
Ou então, de forma mais prática e gerando um dataframe sem o index antigo podemos utilizar os parâmetros `inplace` e `drop`, como no exemplo abaixo. Ambos tem o valor de `False` por padrão, mudando para `True`, o `inplace` passa a gerar um novo index no próprio dataframe e `drop` irá retirar a tabela index antiga.
```py
data.reset_index(drop=True, inplace=True)
```

<br>

# Escrevendo arquivos
## Criando arquivos .csv
Para criar um novo arquivo do tipo csv basta utilizar o método `.to_csv()` incluindo entre parêntes o nome do arquivo. Um parâmetro que pode ser utilizado ao se criar novos arquivos é o `index`. Por padrão ele é `True`, gerando assim um index para o novo dataframe. Se o dataframe em questão já apresentar um index, basta atribuir a ele o valor de `False`, dessa forma o index não sairá duplicado.
```py
data_alterada.to_csv('nova-data.csv', index=False)
```

<br>

## Criando arquivos .xlsx
O mesmo é válido para criar arquivos xlsx, bastando utilizar o método `.to_excel`.
```py
data_alterada.to_excel('nova-data.xlsx', index=False)
```

<br>

