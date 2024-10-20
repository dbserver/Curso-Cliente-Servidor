# Desenvolvimento em camadas

Falando rapidamente em “estilos” ou formas de avaliar algumas arquiteturas de sistemas de informação.

Camadas são separações lógicas e ou físicas de código por função executada. Ou seja, você pode ter um sistema pequeno que resolve tudo em um bloco de código estruturado. Por outro lado, em programação orientada a objetos você começa a naturalmente tentar separar responsabilidades do código. Por exemplo, começa a não fazer sentido uma entidade de serviços fazer tudo internamente, acumular muitas responsabilidades e gerar acoplamento demais.
Ou seja, com uma arquitetura em camadas você consegue separar as responsabilidades, trabalhar melhor com abstrações.

# Layer e Tier

É importante separar os conceitos de layer e de tier.

Quando falamos em camadas usando “Layer” como representação, estamos falando que logicamente a responsabilidade de receber a requisição é da camada de controllers, e que a persistência esta na camada de infraestrutura.

Quando falamos em camadas usando “Tier” estamos nos referindo a uma separação física, ou seja, a camada de controllers esta na pasta física do SO chamada controller, ou no pacote da api, assim como a camada de infraestrutura esta na pasta infrastructure ou no projeto, pacote chamada infrastructure.

Em resumo, você pode ter uma aplicação onde todas as classes estejam juntas, mas com suas responsabilidades lógicas separadas em classes diferentes, ou podemos ter uma aplicação para receber as requisições, uma aplicação para processar o negócio e outra aplicação para resolver persistência de dados.

Em ambos os casos estamos falando de arquitetura em camadas.
Lembrando que quando falamos de arquitetura podemos ter patterns de implementação e patterns conceituais.

