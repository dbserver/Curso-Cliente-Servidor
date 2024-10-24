# Ports and Adapters

## Introdução

A Arquitetura Hexagonal foi proposta por Alistair Cockburn em 2005 como uma forma de estruturar sistemas de software que sejam independentes de frameworks, permitindo maior flexibilidade e facilidade de manutenção. O objetivo é criar um design de software que seja mais adaptável a mudanças e mais fácil de testar.

## Conceito Central

A Arquitetura Hexagonal separa o sistema em três áreas principais:

- Domínio Central (ou núcleo): Contém a lógica de negócios pura e regras essenciais que não dependem de tecnologia externa.
- Portas (Ports): Interfaces que permitem a comunicação com o domínio central, conectando-o com o mundo externo.
- Adaptadores (Adapters): Implementações técnicas que interagem com portas, adaptando as interfaces para que o domínio central possa se comunicar com fontes externas como bancos de dados, APIs ou interfaces de usuário.

Esse design promove uma forte separação entre a lógica de negócios e os detalhes de infraestrutura, garantindo que as regras do domínio sejam independentes de frameworks ou bibliotecas externas.

## Motivação e Benefícios

- Independência de Frameworks: O núcleo da aplicação não depende de bibliotecas externas ou frameworks, o que permite que você mude ou substitua a infraestrutura sem afetar o domínio central.

- Facilidade de Teste: Como o núcleo da aplicação está isolado, ele pode ser testado de forma independente. Testes unitários não precisam de infraestrutura real, pois os adaptadores podem ser simulados.

- Manutenibilidade e Extensibilidade: Como as dependências externas são isoladas em adaptadores, a aplicação se torna mais fácil de manter e modificar, já que alterações de infraestrutura ou tecnologia não afetam o núcleo do sistema.

## Componentes da Arquitetura Hexagonal

**Núcleo (Domínio Central)**

O núcleo da aplicação contém as regras de negócio e as entidades do domínio. Ele não conhece os detalhes de como os dados são persistidos, de como a comunicação com sistemas externos é feita ou de como as informações são apresentadas ao usuário. O núcleo se comunica com o mundo externo através de portas.

**Portas (Ports)**
As portas são as interfaces através das quais o núcleo se comunica com o mundo exterior. Existem dois tipos principais:

Portas de Entrada (Driving Ports): Interfaces que permitem que o mundo exterior envie comandos para o núcleo. Exemplo: APIs que controlam a lógica de negócios.

Portas de Saída (Driven Ports): Interfaces que o núcleo usa para solicitar dados ou serviços de fora. Exemplo: A interface que o domínio usa para buscar dados de um banco de dados.

**Adaptadores (Adapters)**
Os adaptadores são implementações concretas que fazem a ponte entre as portas e o mundo externo, como bancos de dados, APIs, sistemas de arquivos, etc. Eles "adaptam" as interfaces fornecidas pelas portas para uma tecnologia específica.

Exemplo de Adaptador de Entrada: Um controlador de API REST que traduz uma requisição HTTP para uma chamada a um caso de uso do domínio.

Exemplo de Adaptador de Saída: Um repositório que traduz chamadas do núcleo para operações no banco de dados.

## Fluxo de Comunicação

Na Arquitetura Hexagonal, o fluxo de comunicação sempre começa pelos adaptadores de entrada, que traduzem a interação do usuário ou de sistemas externos em uma ação no núcleo da aplicação. O núcleo processa a ação e, se necessário, utiliza os adaptadores de saída para interagir com serviços externos, como bancos de dados ou APIs.