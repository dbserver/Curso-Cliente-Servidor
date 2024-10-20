# Data Gateway

Vamos falar de duas formas comuns de acesso a dados para orientação a objetos, não são únicos como veremos em outros patterns, mas são duas principais que você provavelmente utiliza no dia a dia.

Mas antes, vamos olhar a definição de localização no clean architecture. Banco de dados é um driver, que fica do lado de fora da aplicação, ou seja, ele serve à aplicação para nutrir entidades dos casos de uso.
Entre os casos de uso e o banco de dados, temos os Gateways como adapters para tornar possível a conversão de dados em aplicação e o inverso também em caso de persistência. 

![clean architecture](./../../assets/clean-arch.png)


## Row Data Gateway

Uma instância para cada linha retornada por uma consulta.
Ou seja, quando eu faço uma consulta em uma tabela, para cada linha que retorna eu tenho um objeto.

![row data image](./../../assets/row-data.png)

## Table Data Gateway

Estrutura genérica de tabelas e linhas que imitam / copiam a estrutura tabular de um banco de dados, ou seja, o RecordSet.
Neste caso você terá uma classe por tabela, que na consulta retorna uma tabela em memória.

![row data image](./../../assets/table-data.png)

## Padrões de domínio

Olhando novamente para clean architecture, quando estamos falando de gateways, estamos falando da porta para fora do nosso software, vamos falar de alguns padrões que tratam da porta para dentro, ou seja, que resolvem a parte lógica do coração da nossa aplicação.

## Table Module

Muito comum sistemas serem iniciados orientados a banco de dados, ou seja, a aplicação começa na modelagem do banco de dados.
Neste caso talvez faça muito sentido utilizar Row data gateway ou table data gateway, onde para dentro da aplicação você terá uma classe anêmica que representa uma tabela e seus relacionamentos no banco de dados.
Neste caso a sua aplicação esta orientada a estrutura de dados do banco de dados.

## Domain Module

Quando pensamos nossa aplicação a partir do domínio, ou seja, dos nossos casos de uso e das relações entre as entidades dele.
Ou seja, você cria uma conta, automaticamente você irá criar ou adicionar uma ou mais pessoa, vai adicionar os dados destas pessoas como endereço, telefone.

Quando você trabalha desta forma, e o sistema cresce, mais você ira notar que a modelagem da aplicação fica mais distante da modelagem do banco de dados.

## Active Record

Active record é um pattern onde o seu objeto encapsula uma linha, tabela ou view e permite a adição de lógica de domínio nos seus dados.
Assim toda vez que estiver trabalhando com um objeto de conta corrente você pode adicionar um dependente à esta conta, ou adicionar dados de contato da pessoa desta conta, ou alterar o numero da agenda que é proprietária desta conta. Tudo isso na mesma classe, trazendo muita facilidade da hora de trabalhar.

Então quando falamos de active record estamos falando de uma classe que carrega os dados do banco de dados e na mesma classe aplica lógica de negócios nela.

Ponto negativo, gera um acoplamento gigante entre a lógica da aplicação e o banco de dados.

## Data Mapper

Data mapper é uma camada de abstração que gerencia e transforma os dados do banco de dados na aplicação, e o domínio da aplicação em estrutura para o banco de dados.
Quando trabalhamos com ORM, estamos fazendo um mapeamento objeto relacional, ou seja, relacionando o nosso modelo de domínio em modelo de banco de dados, não necessariamente 1:1 como no Table Module.

Quando eu tenho um domínio muito complexo usar data mapper pode ser uma boa alternativa, pois o domínio da aplicação vai crescer independente do banco de dados.

## Identity Map

O que é um Identity Map? 
O Identity Map garante que cada objeto é carregado apenas uma vez e o mantém em um mapa de controle.

Pensa que estamos usando o Data Mapper, então eu carrego uma entidade ou lista, quando eu busco novamente esta entidade o idendity map primeiramente busca no mapa a entidade que está em memória e desta forma não gerando uma nova consulta no banco de dados.

Identity Map é uma estrutura de dados que carrega o que está em uso na memória melhorando a performance e reduzindo as inconsistências.

## Repository

Repository é um pattern para trabalhar com agregações.
Quando você tem um domínio rico e trabalha com agregações na lógica da aplicação, a persistência e consulta de dados pode ser feita por este padrão.

Uma agregação é um conjunto de classes que se relacionam entre si para que um pedaço da lógica e suas dependências andem juntas.
Uma agregação tem uma raiz, ou seja, uma classe principal que gerencia a agregação. 

Em um exemplo de uma Agregação de conta você pode ter algumas classes, como a classe que representa a conta, uma classe que representa os dados de contado da pessoa, outra classe que mantenha a informação de risco desta pessoa nesta conta para fazer a gestão de limites.

Neste caso a raiz tende a ser a classe conta, logo se você pretende editar o limite desta conta, você não busca a classe de gestão de risco e edita o limite, você busca a raiz da agregação e ela é que deve conhecer os detalhes da gestão de limites, e quando você vai persistir no banco de dados via repositório, você envia apenas a classe que é a raiz de agregação, e o repositório deve saber o que fazer com as alterações recebidas.
