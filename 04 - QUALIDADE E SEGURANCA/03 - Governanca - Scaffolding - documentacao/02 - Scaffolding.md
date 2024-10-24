# 02 - Scaffolding

## O que é Scaffolding?

Definição:

Scaffolding é uma técnica que gera automaticamente código básico ou padrão para acelerar o desenvolvimento de aplicações. Muito utilizado em frameworks como ASP.NET Core, ele cria estruturas de código como controllers, views e models.

### Objetivo:
Acelerar o processo inicial de desenvolvimento ao automatizar a criação de código padrão, evitando o trabalho repetitivo e manual de codificação das camadas básicas de uma aplicação.

## Benefícios de Scaffolding na Aceleração do Desenvolvimento

### Redução do Trabalho Manual:

Scaffolding gera automaticamente código que segue padrões do framework utilizado, economizando tempo na criação de rotinas como CRUD (Create, Read, Update, Delete).

### Melhoria na Produtividade:

Acelera o desenvolvimento ao permitir que os engenheiros se concentrem em funcionalidades específicas do negócio, já que a infraestrutura básica já foi criada.

### Padronização do Código:

O código gerado segue convenções e padrões do framework, o que facilita a manutenção e garante consistência entre as partes da aplicação.

### Facilidade de Uso para Novos Desenvolvedores:

Para engenheiros novos em um projeto, scaffolding oferece uma base clara e estruturada, reduzindo a curva de aprendizado.

## Implicações de Segurança no Uso de Scaffolding

### Atenção às Vulnerabilidades:

Embora scaffolding acelere o desenvolvimento, o código gerado nem sempre leva em consideração as nuances de segurança do projeto. É importante sempre validar a segurança após o uso de scaffolding.

### Validação de Entradas e Autenticação:

O código gerado pode não incluir implementações robustas de segurança, como a validação adequada de entradas, controles de autenticação e autorização. É importante revisar o código gerado para aplicar medidas de segurança adequadas.

### Dependência de Bibliotecas de Terceiros:

Em alguns casos, o scaffolding pode gerar dependências externas ou integrar pacotes de terceiros. Essas dependências devem ser revisadas regularmente para garantir que não existam vulnerabilidades conhecidas.

### Scaffolding e Governança de Código 

#### Padronização e Governança:

Scaffolding promove governança ao garantir que o código gerado siga padrões e boas práticas de codificação predefinidos. No entanto, é necessário definir padrões personalizados para adaptar o código gerado às necessidades do projeto.

#### Revisões de Código e Automação:

Mesmo com o uso de scaffolding, a revisão de código permanece essencial para garantir que as regras de governança sejam respeitadas, especialmente para questões de segurança e conformidade.

#### Documentação e Transparência:

Ao gerar código automaticamente, scaffolding ajuda a documentar as partes estruturais da aplicação de maneira consistente, contribuindo para a governança do projeto e facilitando auditorias.

## Conclusão e Perguntas

Resumo:

Scaffolding é uma ferramenta poderosa para acelerar o desenvolvimento, mas seu uso exige atenção especial à segurança e governança. A integração de controles adicionais, como validações e revisões, é fundamental para garantir a qualidade e a segurança do código.
