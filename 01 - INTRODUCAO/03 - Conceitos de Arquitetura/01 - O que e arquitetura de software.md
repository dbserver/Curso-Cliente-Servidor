# O que é arquitetura de software?

Conceito: 
> A arquitetura de software de um sistema consiste na definição dos componentes de software, suas propriedades externas, e seus relacionamentos com outros softwares. 
O termo também se refere à documentação da arquitetura de software do sistema. A documentação da arquitetura do software facilita: a comunicação entre os stakeholders, registra as decisões iniciais acerca do projeto de alto-nível, e permite o reuso do projeto dos componentes e padrões entre projetos.

Fonte: https://pt.wikipedia.org/wiki/Arquitetura_de_software

Primeiramente vamos entender sobre tipos de arquiteturas, temos arquitetura de software, arquitetura de solução, arquitetura tecnológica e corporativa.
Nosso foco é na arquitetura de software, que nos leva mais próximo ao código, tem a intenção de fazer um software sobreviver por mais tempo.
A arquitetura de solução ajuda a gente a desenhar a solução para entregar mais valor. Com uma visão mais holística na solução dos produtos da empresa, tem uma visão de tecnologia mas não uma visão que alcance código ou implementação.

Entre arquitetura de software e de solução teremos uma área cinzenta que ambas irão trabalhar, em solução você precisa prever o armazenamento dos dados, e na de software você precisa definir e detalhar o banco de dados, e não tem problema algum o importante é que as pessoas e as soluções conversem no mesmo sentido.

Academicamente falando a definição de arquitetura de software é a seguinte: A arquitetura de software de um sistema consiste na definição dos componentes de software, suas propriedades externas, e seus relacionamentos com outros softwares. O termo também se refere à documentação da arquitetura de software do sistema. A documentação da arquitetura do software facilita: a comunicação entre os stakeholders, registra as decisões iniciais acerca do projeto de alto-nível, e permite o reuso do projeto dos componentes e padrões entre projetos.

# Arquitetura e Design

### Qual é a diferença? Existe diferença entre arquitetura e design?

Sim e não, toda arquitetura vai ter algum design de código, todo design de código está inserido em uma arquitetura de software, e um código mal escrito, ou seja, sem design também está inserido em uma arquitetura. 

Então novamente, qual a diferença?

Quando falamos de arquitetura, estamos falando em um escopo global, orientado a funcionalidades, infraestrutura, custos, etc.
Então, dado nosso modelo de negócio vamos decidir que a comunicação de A para B se dará via HTTP, já de B para C é assíncrono, então usaremos filas com persistência eventual. Isso está em um nível de arquitetura.

Quando falamos que a fila utilizada será do produto X, aplicando o pattern Y, daí estamos entrando no design, no detalhe da implementação.

Mas assim como nos tipos de arquitetura temos uma linha muito fina separando ambos, e eventualmente arquitetura e design precisarão sentar na mesma mesa para discutir implementações.

### Mas e o Clean Architecture?

Clean architecture é sobre design para arquitetura!

Não ajudou muito né?
Enfim, clean architecture é muito mais sobre o design de aplicações do que sobre arquitetura, porém, quando falamos especificamente do arquiteto de software, é neste ponto que se aplica.

Uma vez definida a arquitetura da solução, comunicação entre produtos, etc, o clean arquitecture vem para  nos ajudar a entender onde cada coisa está no software, como organizar as caixinhas, como fazer a comunicação entre as caixinhas usando design patterns e patterns para arquitetura.



