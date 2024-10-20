# Viscosidade

## Conceito de Viscosidade no Código

A viscosidade em código refere-se à resistência que ele oferece a mudanças. Quando o código tem alta viscosidade, é difícil ou demorado realizar alterações corretamente. Em vez disso, o caminho mais fácil para mudanças tende a ser "quebrar" o design ou as boas práticas.

Existem dois tipos principais de viscosidade:

- Viscosidade do Design: Alterações feitas de forma correta exigem muito esforço, enquanto fazer a alteração errada é mais fácil.
- Viscosidade do Ambiente: O processo de configuração do ambiente de desenvolvimento ou teste é tão complicado que desincentiva mudanças adequadas.

## Principais Sintomas

Alguns dos sintomas mais comuns que indicam que o código tem alta viscosidade incluem:

- Duplicação de Código: Quando novas funcionalidades são adicionadas copiando e colando código existente em vez de reaproveitar lógica existente.
- Excesso de Condicionais: Grande número de estruturas condicionais (if/else ou switch), principalmente quando o número de ramificações cresce à medida que novos recursos são adicionados.
- Refatorações Evitadas: Se a equipe opta por adicionar código "rapidamente" em vez de refatorar e melhorar a base existente.
- Dificuldade de Testes: Testes automatizados são difíceis de configurar, exigindo ajustes manuais frequentes no ambiente.

## Causas de Código com Viscosidade

Algumas das principais causas de viscosidade no código são:

- Design Monolítico: O sistema está muito interligado, de forma que qualquer mudança exige modificações em várias partes do código.
- Falta de Modularity ou Abstrações: O código não está organizado em módulos reutilizáveis ou não utiliza abstrações adequadas, forçando a repetição de lógica.
- Complexidade Acumulada: Muitas alterações pequenas feitas ao longo do tempo podem fazer o código crescer desorganizado e difícil de ajustar.
- Técnica de "Hotfix": Aplicar soluções rápidas e pontuais sem pensar em longo prazo ou nas consequências de design.

## Impactos Negativos da Viscosidade

Os principais impactos negativos de um código com alta viscosidade são:

- Manutenção Difícil: A cada nova alteração, fica cada vez mais difícil manter o design correto sem quebrar outras partes do código.
- Código Fragilizado: Pequenas alterações podem introduzir bugs inesperados, causando efeitos colaterais em outras áreas do sistema.
- Aumento do Custo de Desenvolvimento: O esforço necessário para realizar novas funcionalidades ou corrigir bugs aumenta consideravelmente.
- Desmotivação da Equipe: Quando o código é difícil de trabalhar, os desenvolvedores podem se sentir desmotivados ou frustrados, o que afeta a produtividade e a qualidade do trabalho.

## Como Evitar Viscosidade

Algumas práticas para evitar ou reduzir a viscosidade no código incluem:

- Aplicar Princípios SOLID: Especialmente o Princípio Aberto/Fechado (OCP), que incentiva a extensão do código sem modificação das partes já existentes.
- Refatoração Contínua: Refatorar o código regularmente para garantir que ele permaneça flexível e fácil de estender.
- Abstrações Adequadas: Use interfaces e abstrações para isolar mudanças e permitir fácil extensão do código.
- Modularização: Organize o código em pequenos módulos que sejam reutilizáveis e independentes, facilitando a evolução e manutenção.
- Automação do Ambiente: Facilite a configuração do ambiente de desenvolvimento e testes, evitando frustrações e economizando tempo.

---

Exemplo de Código com Alta Viscosidade (Antes)

Aqui está um exemplo de código onde adicionar novos métodos de pagamento é difícil e requer a modificação do código existente, o que vai contra o Princípio Aberto/Fechado:

```csharp
public class PaymentProcessor
{
    public void ProcessPayment(string paymentType)
    {
        if (paymentType == "CreditCard")
        {
            // Lógica para cartão de crédito
            Console.WriteLine("Processing credit card payment...");
        }
        else if (paymentType == "DebitCard")
        {
            // Lógica para cartão de débito
            Console.WriteLine("Processing debit card payment...");
        }
        else if (paymentType == "PayPal")
        {
            // Lógica para PayPal
            Console.WriteLine("Processing PayPal payment...");
        }
    }
}
```

Se precisarmos adicionar um novo método de pagamento, como Bitcoin, teríamos que modificar o método ProcessPayment, o que viola o princípio de design.

Exemplo Corrigido com Baixa Viscosidade (Depois)
Aqui está a versão corrigida, onde novos métodos de pagamento podem ser adicionados sem modificar o código existente. O código agora segue o Princípio Aberto/Fechado e utiliza Polimorfismo:

```csharp
public interface IPaymentMethod
{
    void ProcessPayment();
}

public class CreditCardPayment : IPaymentMethod
{
    public void ProcessPayment()
    {
        Console.WriteLine("Processing credit card payment...");
    }
}

public class DebitCardPayment : IPaymentMethod
{
    public void ProcessPayment()
    {
        Console.WriteLine("Processing debit card payment...");
    }
}

public class PayPalPayment : IPaymentMethod
{
    public void ProcessPayment()
    {
        Console.WriteLine("Processing PayPal payment...");
    }
}

public class PaymentProcessor
{
    public void ProcessPayment(IPaymentMethod paymentMethod)
    {
        paymentMethod.ProcessPayment();
    }
}
```

Agora, para adicionar um novo método de pagamento, como Bitcoin, podemos simplesmente criar uma nova classe que implemente IPaymentMethod, sem alterar o código existente:

```csharp
public class BitcoinPayment : IPaymentMethod
{
    public void ProcessPayment()
    {
        Console.WriteLine("Processing Bitcoin payment...");
    }
}
```