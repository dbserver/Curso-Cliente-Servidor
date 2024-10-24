# Arquitetura orientada a domínio

## Padrões Arquiteturais Antes do das arquiteturas orientadas a domínio

### Arquitetura Monolítica 

O que é:

Nas primeiras décadas de desenvolvimento de software, a arquitetura monolítica era o padrão predominante. Todo o sistema era implementado em uma única base de código, com camadas bem definidas (UI, lógica de negócio, banco de dados) mas sem separação clara de domínios.

Benefícios:
- Simplicidade Inicial: Ideal para projetos pequenos ou startups, onde a implementação rápida é prioritária.
- Desempenho: Como tudo reside em um único ambiente, a comunicação interna é rápida.
- Fácil Deploy: Um único deploy pode atualizar o sistema inteiro.

Malefícios:
- Dificuldade de Escalabilidade: À medida que o sistema cresce, a manutenção e adição de funcionalidades se tornam complexas.
- Interdependências: Alterações em uma parte do sistema podem afetar outras partes, criando instabilidade.
- Monolito da Complexidade: A falta de divisão clara entre os domínios da aplicação resulta em "Big Balls of Mud", onde o código se torna ininteligível.

### Evolução, Arquitetura em camadas (Layered Architecture) 

A arquitetura em camadas introduziu a ideia de separar responsabilidades por camadas (UI, Lógica de Negócio, Persistência de Dados, etc.). Ela busca uma melhor organização e modularização do código.

Benefícios:
- Clareza de Responsabilidades: Cada camada tem um propósito específico, facilitando a manutenção.
- Facilita Testes: Como as camadas são independentes, testes unitários e de integração são mais fáceis de implementar.

Malefícios:
- Rigidez: A comunicação excessivamente dependente de camadas pode gerar rigidez, dificultando mudanças e adaptações.
- Acoplamento entre Camadas: Apesar de a arquitetura em camadas sugerir independência, na prática, camadas podem se tornar altamente acopladas.

### Evolução, Arquitetura Orientada a Serviços (SOA) 

O SOA surgiu como uma resposta aos problemas de escalabilidade das arquiteturas monolíticas. Ele promove a criação de serviços independentes que se comunicam por meio de interfaces bem definidas.

Benefícios:
- Escalabilidade: Serviços podem ser escalados independentemente.
- Reutilização: Serviços podem ser reutilizados em diferentes contextos e projetos.

Malefícios:
- Complexidade Operacional: A coordenação entre serviços, especialmente com muitas dependências, pode se tornar complexa.
- Problemas de Performance: A comunicação entre serviços por meio de redes pode introduzir latência.

## O Surgimento da Arquitetura Orientada a Domínio (DDD)

### Desafios na Era Pré-DDD:

À medida que sistemas cresciam em tamanho e complexidade, os padrões arquiteturais tradicionais se mostravam insuficientes para lidar com problemas como:
- Domínios de negócios complexos.
- Dificuldade de comunicação entre times de negócios e técnicos.
- Falta de flexibilidade e clareza nas mudanças de requisitos.

### O surgimento do DDD:
Em 2003, Eric Evans publicou o livro Domain-Driven Design: Tackling Complexity in the Heart of Software, introduzindo uma abordagem centrada no domínio de negócio, focada em alinhar o código com as regras e processos do negócio.

### Conceitos Chave do DDD

Modelo de Domínio:
Representa o núcleo do negócio dentro do software, refletindo as regras e operações específicas do domínio.

Ubiquitous Language:
Linguagem compartilhada entre todos os envolvidos no projeto (desenvolvedores, stakeholders, especialistas de negócio) para evitar ambiguidades.

Bounded Contexts:
Divisão de grandes sistemas em domínios menores e independentes, com fronteiras bem definidas, permitindo maior modularidade e clareza no código.

### Benefícios do DDD 

- Alinhamento com o Negócio: O DDD força uma compreensão mais profunda do domínio de negócio, resultando em sistemas mais alinhados com as necessidades reais da organização.
- Modularidade e Flexibilidade: A separação de domínios em bounded contexts facilita a manutenção e evolução do sistema.
- Redução de Complexidade: Ao focar nas partes importantes do sistema e isolá-las, o DDD ajuda a evitar que a complexidade se espalhe.

### Malefícios e Desafios do DDD

- Curva de Aprendizado: Requer um entendimento profundo do domínio do negócio, o que pode ser desafiador em sistemas muito complexos ou em setores desconhecidos.
- Sobrecarga de Modelagem: Para sistemas pequenos ou menos complexos, o DDD pode parecer um excesso de formalização.


## Além do DDD

Arquitetura Orientada a Domínio:

Arquiteturas que colocam o domínio de negócio no centro, separando as regras de negócio dos detalhes técnicos, como infraestrutura, bancos de dados ou interfaces de usuário.

Então, após o DDD tivemos algumas evoluções dos patterns conceituais como Arquitetura Hexagonal e Clean Architecture

### Arquitetura Hexagonal 

#### O que é a Arquitetura Hexagonal

Conceito:

Introduzida por Alistair Cockburn nos anos 2000, a Arquitetura Hexagonal também é conhecida como Arquitetura de Ports and Adapters.

O principal objetivo da Arquitetura Hexagonal é permitir que o núcleo de negócio (o domínio) seja independente de detalhes externos, como banco de dados ou interfaces. Ela organiza o software em torno de um modelo de domínio e permite a fácil substituição de componentes periféricos.

####  Estrutura e Componentes

Núcleo (Domínio):
No centro, está a lógica de negócio pura e isolada de dependências externas.

Portas (Interfaces):
As portas são pontos de entrada e saída que conectam o núcleo a componentes externos (interfaces de usuário, sistemas de persistência, APIs).

Adaptadores:
Adaptadores são implementações específicas que conectam as portas ao mundo externo, como banco de dados, APIs externas, ou interfaces gráficas.

Exemplo: Um adaptador de banco de dados pode implementar uma interface de repositório, enquanto uma API pode ser conectada por meio de outro adaptador.

#### Benefícios da Arquitetura Hexagonal

Isolamento do Domínio:
- A lógica de negócio é protegida de mudanças externas. Isso significa que o domínio pode ser testado isoladamente, sem precisar simular a infraestrutura.

Facilidade de Teste:
- Com o isolamento claro entre domínios e tecnologias externas, testes unitários e de integração podem ser implementados sem se preocupar com detalhes técnicos, como banco de dados ou interfaces gráficas.

Flexibilidade e Substituição de Componentes:
- Tecnologias periféricas podem ser trocadas sem afetar o núcleo. Por exemplo, você pode trocar de um banco de dados relacional para um NoSQL sem modificar a lógica central.

### Desafios da Arquitetura Hexagonal

Complexidade Inicial:
Para pequenos projetos, o overhead da separação entre portas e adaptadores pode parecer exagerado.
Curva de Aprendizado:
Desenvolvedores que estão acostumados com padrões mais tradicionais podem levar algum tempo para entender e aplicar corretamente a Arquitetura Hexagonal.

### Clean Architecture

#### O que é Clean Architecture

Conceito:

Criada por Robert C. Martin (Uncle Bob), a Clean Architecture foi introduzida como um aprimoramento das arquiteturas orientadas a domínio, inspirada na Arquitetura Hexagonal e em outras abordagens, como o Onion Architecture.

A Clean Architecture propõe um modelo onde as regras de negócio são completamente independentes de frameworks, interfaces de usuário e detalhes de infraestrutura, seguindo a ideia de que o software deve ser fácil de modificar e manter.

#### Camadas da Clean Architecture

Núcleo do Domínio:
- Como na Arquitetura Hexagonal, o domínio representa o coração do software, contendo as regras de negócio mais puras, sem dependências externas.

Use Cases (Aplicação):
- Os casos de uso são responsáveis por orquestrar as interações entre o domínio e o mundo externo. Eles descrevem o comportamento do sistema sem se preocupar com como os dados são armazenados ou exibidos.

- Interface de Interface (Interface Adapters):
Esta camada contém adaptadores que convertem dados do mundo externo em um formato que o núcleo pode entender. Isso inclui a implementação de controladores de UI, mapeamento de dados, etc.

- Infraestrutura e Frameworks:
A camada externa contém detalhes de infraestrutura, como frameworks, bancos de dados e bibliotecas de terceiros. Esses detalhes podem ser facilmente substituídos sem afetar o núcleo.

### Benefícios da Clean Architecture

Independência de Frameworks:
- A Clean Architecture permite que você substitua frameworks com facilidade, porque eles não afetam o núcleo de seu sistema.

Testabilidade:
- Assim como a Arquitetura Hexagonal, a Clean Architecture isola as regras de negócio, facilitando a criação de testes sem dependências de infraestrutura.

Flexibilidade de Evolução:
- A estrutura modular da Clean Architecture permite que o sistema evolua de maneira controlada, substituindo ou expandindo camadas de infraestrutura com facilidade.

### Desafios da Clean Architecture

Complexidade Inicial:
- A Clean Architecture pode parecer complexa para desenvolvedores que estão acostumados com abordagens mais lineares ou orientadas a frameworks.

Overhead para Projetos Simples:
- Para projetos pequenos, a aplicação de Clean Architecture pode parecer um esforço desnecessário.

### Comparação: Arquitetura Hexagonal vs. Clean Architecture

Semelhanças:

Ambas as arquiteturas compartilham a ideia de isolar o domínio e as regras de negócio do resto do sistema.
Ambas utilizam interfaces e adaptadores para conectar o núcleo a sistemas externos, mantendo flexibilidade e testabilidade.

Diferenças:
- Camadas: A Clean Architecture tem uma divisão de camadas mais explícita e um foco maior em use cases do que a Arquitetura Hexagonal.
- Abstração: A Clean Architecture é mais rigorosa em garantir que o domínio não tenha conhecimento das camadas externas, enquanto a Arquitetura Hexagonal permite maior flexibilidade nesse aspecto.

## Conclusão 
Resumo:

A Arquitetura Hexagonal e a Clean Architecture são abordagens poderosas para criar sistemas modulares, flexíveis e orientados ao domínio. Embora possam parecer excessivas para projetos pequenos, oferecem enormes benefícios para sistemas de grande escala e alta complexidade.

