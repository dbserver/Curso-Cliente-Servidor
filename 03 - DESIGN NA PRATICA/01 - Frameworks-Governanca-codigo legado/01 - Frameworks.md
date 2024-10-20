# Frameworks


## Introdução aos Frameworks

O que é um framework?

- Definição: Um framework é uma estrutura de código reutilizável que fornece uma base padrão sobre a qual aplicações podem ser desenvolvidas. Ele inclui bibliotecas, regras e convenções para organizar e estruturar o código.

Exemplos populares: .NET, Spring (Java), Django (Python), Angular (JavaScript).

Como um framework difere de uma biblioteca?

Uma biblioteca oferece funções que você pode chamar, mas você controla o fluxo de execução.
Um framework controla o fluxo e você "preenche as lacunas" com seu código.

## Importância dos Frameworks

- Facilitam o Desenvolvimento

Proporcionam uma estrutura bem definida, reduzindo o tempo de desenvolvimento, pois muito código já está implementado.

Exemplo: O uso de frameworks MVC (Model-View-Controller) facilita a separação de responsabilidades no código.

- Padronização

Um framework promove consistência entre projetos e equipes, padronizando a maneira de resolver problemas. Isso melhora a legibilidade e manutenção do código.

Exemplo: Um time de engenheiros pode usar o ASP.NET para garantir que todas as APIs sigam o mesmo padrão de desenvolvimento.

- Boas Práticas Incorporadas

Os frameworks geralmente incorporam boas práticas de arquitetura e design, como injeção de dependências, gestão de erros, e segurança.

Exemplo: Spring Boot ajuda a aplicar o conceito de Inversão de Controle e Dependency Injection de forma simplificada, assim como no .NET Framework também temos um motor para fazer a gestão da injeção de dependência via configuração simplificada.

- Ecossistema e Comunidade

A maioria dos frameworks populares tem um grande ecossistema, com ferramentas e plugins que facilitam o desenvolvimento, e uma comunidade ativa que contribui com soluções para problemas comuns.

Exemplo: Angular tem uma comunidade enorme que contribui com bibliotecas e extensões.


## Trade-offs de Frameworks

### Vantagens:

- Produtividade Elevada: Por fornecer uma base sólida e componentes prontos, os frameworks aceleram o desenvolvimento.
- Segurança: A maioria dos frameworks lida com preocupações de segurança como validação de dados, autenticação e criptografia de forma integrada.
- Facilidade de Manutenção: Como os frameworks seguem convenções e padrões, eles facilitam a manutenção e a transferência de projetos entre equipes.

### Desvantagens e Desafios

- Curva de Aprendizado: Embora ajudem a reduzir o tempo de desenvolvimento no longo prazo, pode haver uma curva de aprendizado inicial significativa, especialmente com frameworks complexos.

Exemplo: Spring tem uma curva de aprendizado mais íngreme em comparação a outras ferramentas de desenvolvimento.

- Rigidez: Um framework impõe sua estrutura, o que pode limitar a flexibilidade no desenvolvimento.

Exemplo: Desenvolvedores podem sentir-se "engessados" ao usar Ruby on Rails, que impõe uma estrutura rígida.

- Sobrecarga de Recursos: Alguns frameworks podem ser pesados, exigindo mais recursos de hardware e software, o que pode não ser ideal para projetos menores ou que precisam de desempenho otimizado.

Exemplo: O uso de frameworks complexos pode adicionar camadas extras de abstração, impactando o desempenho.

- Dependência: Um framework cria uma dependência forte do seu ecossistema. Se o framework se tornar obsoleto ou mudar drasticamente, o projeto pode enfrentar dificuldades de migração.

Exemplo: AngularJS foi descontinuado e muitos projetos tiveram que migrar para Angular 2+, o que gerou bastante esforço de reescrita.

## Porque criar um framework próprio dentro de casa?

## Segurança Customizada

Frameworks criados dentro da empresa permitem que as políticas de segurança específicas sejam implementadas diretamente no código, garantindo que as necessidades exclusivas do negócio sejam atendidas. Isso inclui a integração de práticas como criptografia de dados, autenticação, autorização e controle de acesso de maneira padronizada em todas as aplicações desenvolvidas.

Exemplo: Um framework interno pode garantir que todas as requisições façam uso de autenticação multifatorial (MFA) e políticas de controle de acesso baseadas em função (RBAC), alinhadas aos requisitos da empresa.

## Controle Total sobre o Código

Um framework criado internamente oferece controle total sobre o código-fonte, permitindo uma maior adaptabilidade e a implementação de atualizações e correções de vulnerabilidades rapidamente, sem depender de terceiros.

Exemplo: Se um componente de segurança externo apresenta uma vulnerabilidade crítica, a equipe pode demorar a receber uma correção. Com um framework interno, as vulnerabilidades são corrigidas imediatamente, como um componente customizado de gerenciamento de sessão que pode ser atualizado instantaneamente quando uma vulnerabilidade de session hijacking é descoberta.

## Padrões Consistentes de Desenvolvimento

Com um framework interno, é possível definir padrões de segurança que garantem que todos os desenvolvedores estejam seguindo as mesmas práticas, reduzindo a chance de falhas de segurança.

Exemplo: Um framework de autenticação e autorização pode garantir que todas as APIs implementem corretamente as verificações de permissões, evitando que endpoints críticos sejam acessados sem a devida validação.

## Integração de Conformidade e Regulamentações

Empresas que operam em setores altamente regulados, como financeiro ou saúde, precisam atender a regulamentos específicos (como GDPR, HIPAA, PCI-DSS). Frameworks internos podem incorporar esses requisitos diretamente no ciclo de desenvolvimento, facilitando a conformidade.

Exemplo: Um framework interno de manipulação de dados pessoais pode garantir que todas as operações de processamento de dados sensíveis estejam em conformidade com o GDPR/LGPD, aplicando regras de anonimização ou pseudonimização por padrão.

## Escalabilidade e Otimização para o Negócio

Um framework interno pode ser adaptado e otimizado para o cenário de negócio específico da empresa. Em termos de segurança, isso significa que a solução pode ser projetada para lidar com os volumes e tipos de dados mais críticos, sem sobrecarregar o sistema com funcionalidades genéricas ou desnecessárias.

Exemplo: Uma empresa de comércio eletrônico pode desenvolver um framework interno de segurança para lidar com transações financeiras, focando em otimizar o desempenho da validação de pagamentos e fraudes, sem as camadas extras que um framework genérico poderia trazer.

## Facilidade de Auditoria e Testes de Segurança

Como o framework é desenvolvido internamente, ele pode ser facilmente integrado com ferramentas de monitoramento e auditoria específicas da empresa. Isso torna mais simples rastrear e analisar possíveis tentativas de ataque, além de facilitar os testes regulares de segurança.

Exemplo: Um framework interno pode ter logs de segurança detalhados para cada evento crítico (como falhas de autenticação ou tentativas de acesso não autorizadas), integrados a um sistema centralizado de monitoramento de eventos de segurança (SIEM).

## Agilidade em Adaptações Tecnológicas

A evolução rápida de ameaças e novas técnicas de segurança exige agilidade nas respostas. Um framework interno pode ser facilmente adaptado para incorporar novas técnicas de segurança, sem a necessidade de esperar por atualizações de terceiros.

Exemplo: A implementação de tokenization para proteger informações de cartão de crédito em um framework de pagamentos pode ser rapidamente adaptada para novos padrões de segurança da indústria, sem depender de atualizações externas.

## Redução de Dependências de Terceiros

O uso de frameworks de terceiros pode trazer o risco de dependência excessiva de fornecedores externos, que podem introduzir vulnerabilidades ou problemas de compatibilidade. Um framework interno elimina essa dependência.

Exemplo: Em vez de depender de bibliotecas de autenticação de terceiros, a empresa pode desenvolver seu próprio framework de autenticação centralizado, que se integra perfeitamente com todos os sistemas da empresa, garantindo compatibilidade e controle.

## Aprimoramento Contínuo Baseado em Experiência Real

Como o framework é utilizado em diferentes projetos dentro da empresa, ele pode evoluir continuamente, incorporando lições aprendidas e aprimoramentos baseados em ataques reais ou problemas de segurança que surgem ao longo do tempo.

Exemplo: Um framework de segurança para APIs pode ser melhorado para incluir proteções contra ataques de brute-force após um evento de segurança que revelou essa vulnerabilidade em um serviço específico.

## História

Um ponto importante também é que alguns frameworks, linguagens que utilizamos só existem porque algum grupo de engenheiros precisou resolver algum problema para o seu negócio e isto acabou virando um framework, linguagem, IDE de mercado em algum momento.


## Resumo dos Pontos Abordados

O que são frameworks e como diferem de bibliotecas.
A importância dos frameworks para produtividade, padronização e manutenção.
Os trade-offs entre produtividade, rigidez e sobrecarga de recursos.