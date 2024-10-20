# Principio da segregação de interfaces

O Princípio de Segregação de Interfaces afirma que os clientes não devem ser forçados a depender de interfaces que não utilizam. Em outras palavras, as interfaces devem ser pequenas e específicas para não obrigar classes a implementar métodos desnecessários.

## Principais Sintomas de Quebras do ISP

- Interfaces que obrigam classes a implementar métodos que não fazem sentido para elas.
- Mudanças em uma interface grande causam modificações em várias classes desnecessariamente.
- Implementação de métodos vazios ou com "throw new NotImplementedException()" porque a classe não precisa daquele comportamento.

## Impactos Negativos de Interfaces Grandes

- Alta acoplamento: Classes ficam dependentes de muitas funcionalidades que não utilizam.
- Dificuldade de manutenção: Alterar uma interface grande afeta várias classes, mesmo as que não usam os métodos modificados.
- Reduz a flexibilidade: Classes podem acabar se tornando mais complexas porque precisam lidar com comportamentos irrelevantes para elas.

# Como Aplicar o ISP

O objetivo é dividir interfaces grandes em interfaces menores e mais específicas, onde cada cliente (classe) implementa apenas o que realmente precisa. Isso leva a um design mais flexível, fácil de manter e de entender.

Vamos a um exemplo prático para um Sistema de Pagamento
Aqui, temos uma interface IPaymentService com muitos métodos. Algumas classes podem ser obrigadas a implementar métodos que não utilizam.

```csharp
public interface IPaymentService
{
    void ProcessCreditCardPayment();
    void ProcessBankTransfer();
    void ProcessPayPalPayment();
}

public class CreditCardPaymentService : IPaymentService
{
    public void ProcessCreditCardPayment()
    {
        Console.WriteLine("Processing credit card payment...");
    }

    public void ProcessBankTransfer()
    {
        throw new NotImplementedException();
    }

    public void ProcessPayPalPayment()
    {
        throw new NotImplementedException();
    }
}

```

Qual o problema identificado?

Problema: A classe CreditCardPaymentService é obrigada a implementar métodos que não utiliza, violando o ISP.

Vamos refatorar para corrigir o problema da quebra do ISP.

```csharp
public interface ICreditCardPayment
{
    void ProcessCreditCardPayment();
}

public interface IBankTransferPayment
{
    void ProcessBankTransfer();
}

public interface IPayPalPayment
{
    void ProcessPayPalPayment();
}

public class CreditCardPaymentService : ICreditCardPayment
{
    public void ProcessCreditCardPayment()
    {
        Console.WriteLine("Processing credit card payment...");
    }
}

public class BankTransferPaymentService : IBankTransferPayment
{
    public void ProcessBankTransfer()
    {
        Console.WriteLine("Processing bank transfer...");
    }
}

```

Aplicando ISP, separamos a interface em interfaces menores e mais específicas para cada tipo de pagamento.
Com esta melhoria aplicada cada serviço de pagamento implementa apenas os métodos necessários. Não há mais implementações de métodos irrelevantes ou exceções lançadas.


