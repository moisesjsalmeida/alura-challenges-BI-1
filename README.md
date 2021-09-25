# Alura Log

![Logo](https://github.com/moisesjsalmeida/alura-challenges-BI-1/blob/main/alura%20log%20preto.png)

https://app.powerbi.com/groups/me/reports/4e337623-356c-4040-b461-677f1a931bf6?ctid=1eeced09-952f-4080-adfa-f57ed5f7d002&pbi_source=linkShare

## 🚚 Sobre o projeto

Este projeto foi desenvolvido como parte do Alura Challenge BI, com o objetivo de aprofundar o estudo em Business Intelligence, utilizando a ferramenta Power BI.

O caso se baseia nas bases de dados da empresa fictícia de logística Alura Log, que desejava visualizar métricas importantes para o acompanhamento gerencial de sua operação.

## 🛠 Ferramentas

O projeto foi desenvolvido exclusivamente no Power BI, utilizando as linguagens M para tratamento de dados e DAX para cálculos e medidas.

## 🗃 Bases de Dados

As bases de dados estão em formato CSV.

### Tabela Pedidos

- Total de registros: 147.934
- Colunas:
	- ID Pedido
	- ID Produto
	- Quantidade
	- ID Veículo
	- Status do pedido
	- Data da compra
	- Data de entrega
	- Data previsão
	- Latitude
	- Longitude
	- UF da entrega

### Tabela Estoque

- Total de registros:
- Colunas:
  - ID Produto
  - Data atualização
  - Quantidade

### Tabela Produtos

- Total de registros:
- Colunas:
  - categoria_produto
  - preço

### Tabela Veículos

- Total de registros:
- Colunas:
  - ID veículos
  - Tipo
  - Status



## 🔍 Tratamento dos Dados

Tal qual em situações reais, os dados não estavam prontos para a criação de dashboards, sendo necessário realizar o ETL (Extract, Transform, Load) para que a criação dos gráficos e os relacionamentos entre estes fosse possível.

### Tabela Pedidos

Certamente, a tabela que mais precisou de transformações.

Primeiramente, precisávamos alterar o tipo dos dados para *DateTime*, atentando-nos que existiam colunas com o padrão brasileiro (*dd/mm/aaaa hh:mm*) e colunas em formato estadunidense (*mm/dd/aa hh:mm*).

Feito isso, precisávamos encontrar valores inválidos nestas colunas. Para os pedidos com status *"Em Trânsito"*, o valor da data de entrega era *"Não disponível"*. Pelo seu formato *DateTime*, a coluna não poderia receber valores do tipo *String*. Assim, realizamos a substituição por valores *null*, deixando, assim, aquela coluna com dados vazios.

Feito isso, bastou-nos alterar os tipos das colunas restantes para os mais adequados (*Latitude* e *Longitude* para decimal, *Quantidade* para numérico).

### Tabela Estoque

Para esta tabela, existia um problema para o campo *Data atualização*, que contava com um formato de data *1-jan.-2019*. Após retirarmos o caracter 'ponto' após o mês, realizamos a substituição dos hífens por barras e sua devida tipagem para formato *Date*.

### Tabela Produtos

Nesta tabela, o grande problema foi na coluna *categoria_produto*, que englobava os IDs de cada produto juntamente com o nome da categoria, em formato *[snake_case](https://en.wikipedia.org/wiki/Snake_case)*. Assim, Foi necessária a extração dos dados, separando-os em colunas diferentes, bem como a formatação para a substituição de *underscores* por espaços. Por fim, foi necessária a tipagem para *Decimal* na coluna *Preço*.

### Tabela Veículos

Nesta tabela, bastou-nos remover os prefixos acrescentados aos IDs dos veículos, facilitando o relacionamento com a tabela Pedidos.

### Relacionamentos

![Modelagem](https://github.com/moisesjsalmeida/alura-challenges-BI-1/blob/main/Modelagem.jpg)

Como podemos perceber na figura, a modelagem foi feita de forma simples. As tabelas *Pedidos*, *Produtos* e *Estoque* se relacionam através da coluna *ID Produto*; As tabelas *Pedidos* e *Veículos* se relacionam através da coluna *ID Veículo*.

## 📊 Métricas

### Dashboard Principal

- Quantidade de entregas no prazo;
- Quantidade de entregas atrasadas;
- Média de estoque disponível por ano;
- S2D* por Mês;
- Quantidade de pedidos por estado;

* *S2D (Shipping to Door): Tempo da expedição até a chegada do produto para o cliente*

### Controle de veículos

- Quantidade total de veículos
- Veículos ocupados
- Veículos disponíveis
- Total de veículos por tipo
- Veículos disponíveis por tipo
- Quantidade de entregas por tipo de veículo

### Financeiro

- Faturamento Total
- Estados com maior faturamento
- Faturamento por ano e mês
- Faturamento por categoria de produto

## 🖼 Screenshots

![Principal](https://github.com/moisesjsalmeida/alura-challenges-BI-1/blob/main/Screenshot1.jpg)

![Veiculos](https://github.com/moisesjsalmeida/alura-challenges-BI-1/blob/main/Screenshot2.jpg)

![Financeiro](https://github.com/moisesjsalmeida/alura-challenges-BI-1/blob/main/Screenshot3.jpg)
