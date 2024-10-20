# Principio da Inversão de Dependência

## Introdução ao DIP
O Princípio de Inversão de Dependência afirma que módulos de alto nível não devem depender de módulos de baixo nível; ambos devem depender de abstrações. Além disso, abstrações não devem depender de detalhes, os detalhes devem depender de abstrações.

Pensando em um contexto financeiro, pode haver dependência direta entre serviços de pagamento, transações ou processamento de contas. Quando quebramos o DIP, essas dependências diretas tornam o código rígido e difícil de alterar. O DIP nos ajuda a evitar essas dependências explícitas e fortalecer a flexibilidade do código.

## Principais Sintomas de Quebras do DIP

- O código de alto nível depende diretamente de classes de implementação de baixo nível.
- Alterações em implementações de baixo nível forçam mudanças nas classes de alto nível.
- Dificuldade em testar componentes isolados porque não há abstrações ou interfaces sendo usadas.


## Impactos Negativos de Quebrar o DIP

- Alto acoplamento: Classes de alto nível tornam-se fortemente acopladas a classes de baixo nível, dificultando a modificação ou substituição de implementações.
- Testabilidade reduzida: Como o código de alto nível depende diretamente de implementações concretas, torna-se difícil introduzir mocks ou stubs em testes unitários.
- Dificuldade em expandir: Adicionar novas funcionalidades pode exigir alterações no código de alto nível, mesmo que a alteração se refira apenas ao comportamento de baixo nível.

## Como Aplicar o DIP

Para aplicar o DIP, devemos criar abstrações (como interfaces ou classes abstratas) que tanto o código de alto nível quanto o de baixo nível possam depender. O código de alto nível não deveria conhecer as implementações concretas de baixo nível, apenas as abstrações.

Vamos a um exemplo com código, pense em um "Sistema de Processamento de Pagamento"
Aqui, o serviço de pagamento (PaymentService) depende diretamente de uma classe concreta CreditCardProcessor.

```csharp
public class CreditCardProcessor
{
    public void Process()
    {
        Console.WriteLine("Processing credit card payment...");
    }
}

public class PaymentService
{
    private CreditCardProcessor _creditCardProcessor;

    public PaymentService()
    {
        _creditCardProcessor = new CreditCardProcessor();
    }

    public void ProcessPayment()
    {
        _creditCardProcessor.Process();
    }
}
```

O problema aqui é que a classe PaymentService depende diretamente de CreditCardProcessor, o que viola o DIP, pois qualquer mudança no CreditCardProcessor pode impactar o PaymentService.

Vamos refatorar e tentar resolver aplicando DIP
Para aplicarmos o DIP introduzimos uma abstração (IPaymentProcessor), permitindo que o PaymentService dependa de uma interface, e não de uma implementação concreta.

```csharp
public interface IPaymentProcessor
{
    void Process();
}

public class CreditCardProcessor : IPaymentProcessor
{
    public void Process()
    {
        Console.WriteLine("Processing credit card payment...");
    }
}

public class BankTransferProcessor : IPaymentProcessor
{
    public void Process()
    {
        Console.WriteLine("Processing bank transfer...");
    }
}

public class PaymentService
{
    private readonly IPaymentProcessor _paymentProcessor;

    public PaymentService(IPaymentProcessor paymentProcessor)
    {
        _paymentProcessor = paymentProcessor;
    }

    public void ProcessPayment()
    {
        _paymentProcessor.Process();
    }
}
```

Com esta melhoria aplicada, PaymentService depende da abstração IPaymentProcessor, e não da implementação concreta CreditCardProcessor. Isso torna o código flexível e fácil de expandir para outros tipos de processadores de pagamento.