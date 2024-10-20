# Testes de Unidade

## Introdução ao Teste de Unidade

- O que é um Teste de Unidade?

Um teste de unidade verifica o comportamento de uma unidade individual de código (normalmente um método ou função) de maneira isolada, garantindo que funcione conforme o esperado.
Exemplo: Imagine um método que soma dois números. O teste de unidade vai garantir que ele sempre retorna a soma correta, independentemente de outros fatores externos.

- Por que Testar Unidades?
    - Detecção precoce de falhas: Testes de unidade permitem identificar bugs logo no início do desenvolvimento, antes de afetarem outras partes do sistema.
    - Segurança para refatoração: Com testes de unidade, é possível refatorar código sem medo de quebrar funcionalidades, desde que os testes continuem a passar.
    - Feedback rápido: Eles são rápidos para executar, proporcionando um ciclo de feedback imediato durante o desenvolvimento.

- Vantagens do Teste de Unidade:
    - Isolamento: Testes de unidade são isolados, ou seja, não dependem de outras partes do sistema, como bancos de dados ou APIs externas.
    - Manutenibilidade: Eles ajudam a manter o código organizado e verificável, facilitando futuras mudanças.

## Estrutura de um Teste de Unidade

AAA: Arrange, Act, Assert

Testes de unidade geralmente seguem o padrão triple A "AAA":

- Arrange (Configurar): Prepara o ambiente, inicializando as variáveis necessárias.
- Act (Executar): Executa o método ou função que está sendo testado.
- Assert (Verificar): Verifica se o resultado do método é o esperado.

Exemplo em C#:

```csharp
[Test]
public void Sum_TwoPositiveNumbers_ReturnsCorrectResult()
{
    // Arrange
    var calculator = new Calculator();
    int num1 = 5;
    int num2 = 10;

    // Act
    int result = calculator.Sum(num1, num2);

    // Assert
    Assert.AreEqual(15, result);
}
```

O código prepara os dados (5 e 10), executa o método Sum e verifica se o resultado é 15. Esse é um exemplo típico de um teste simples e claro.

### Verificando Condições Limites:

Testes de unidade também são usados para testar condições extremas (edge cases), como:
Valores nulos (null).
Zeros.
Limites máximos ou mínimos de variáveis (ex.: int.MaxValue).

Exemplo:
```csharp
[Test]
public void Sum_NullValues_ThrowsArgumentNullException()
{
    // Arrange
    var calculator = new Calculator();

    // Act & Assert
    Assert.Throws<ArgumentNullException>(() => calculator.Sum(null, null));
}
```

## Boas Práticas para Testes de Unidade

- Escreva Testes Simples e Objetivos

Um bom teste de unidade deve focar em uma única funcionalidade. Se um teste faz muitas verificações, fica mais difícil identificar a causa de uma falha.
Exemplo errado: Testar diversas funcionalidades em um único teste, como somar e dividir ao mesmo tempo. Isso torna o teste menos legível e mais complexo.

- Isolamento e Dependências

Para garantir que o teste de unidade não dependa de fatores externos, como bancos de dados ou serviços, você pode usar técnicas como mocking para simular dependências.
Exemplo: Se um método depende de um serviço externo, como uma API de terceiros, você pode usar uma biblioteca como Moq (C#) para criar um substituto que simula a resposta esperada da API.

- Testes Determinísticos

Um teste de unidade deve ser determinístico, ou seja, ele deve sempre produzir o mesmo resultado quando rodado em diferentes condições. Testes que dependem de data, hora ou fatores externos podem resultar em falhas intermitentes.
Exemplo: Se um método depende da data atual, passe a data como um parâmetro em vez de chamá-la diretamente no método.

- Nomeação de Testes

O nome do teste deve ser descritivo e indicar claramente o comportamento que está sendo verificado. Isso ajuda a entender rapidamente o que o teste faz sem ter que ler seu conteúdo.
Exemplo:
    Nome claro: Sum_TwoPositiveNumbers_ReturnsCorrectResult.
    Nome ruim: TestMethod1.

- Cobertura de Testes

A cobertura de testes é importante, mas não deve ser um objetivo absoluto. Priorize testes para as partes mais críticas do sistema, em vez de tentar cobrir 100% do código.
Foco na qualidade: É melhor ter menos testes de alta qualidade do que uma grande quantidade de testes frágeis e de baixa manutenção.

## Ferramentas e Frameworks para Teste de Unidade

Frameworks Populares

C#: NUnit, xUnit, MSTest.
Java: JUnit, TestNG.
JavaScript: Jest, Mocha, Jasmine.
Bibliotecas de Mocking

Bibliotecas de mocking permitem simular dependências e focar no teste da unidade de código em si.
C#: Moq, NSubstitute.
Java: Mockito.
JavaScript: Sinon.
Integração com CI/CD

Integrar os testes de unidade com sistemas de Integração Contínua (CI) garante que os testes sejam executados automaticamente a cada mudança no código, proporcionando um feedback rápido.
Ferramentas: Jenkins, GitHub Actions, Azure Pipelines.

## Conclusão e Perguntas
Resumo

Testes de unidade são a base de uma boa estratégia de testes, permitindo detectar erros de forma rápida e eficaz.
Seguindo boas práticas, como isolamento, clareza e testes determinísticos, você pode garantir que seu código seja testado de maneira confiável.
Discussão

Abra espaço para perguntas da equipe e compartilhe exemplos práticos de como eles podem melhorar seus testes atuais.
Esse roteiro oferece uma explicação detalhada sobre testes de unidade, cobrindo conceitos-chave e boas práticas, sem mergulhar em TDD.

## Exercício









