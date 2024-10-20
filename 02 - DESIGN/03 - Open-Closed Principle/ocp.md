# Princípio aberto e fechado.

O Princípio do Aberto/Fechado, o segundo dos princípios do S.O.L.I.D., afirma que:
"uma classe deve estar aberta para extensão, mas fechada para modificação" 

Isso significa que devemos ser capazes de adicionar novas funcionalidades ao sistema sem modificar o código existente. Este princípio é essencial para promover a flexibilidade e minimizar o risco de introduzir novos erros ao alterar o sistema.

O OCP tem como objetivo garantir que sistemas sejam fáceis de estender sem a necessidade de alterar o código existente, evitando assim a introdução de novos erros. Isso é particularmente importante em sistemas grandes e em constante evolução, onde modificações frequentes no código existente podem causar efeitos colaterais indesejados.

O princípio incentiva o uso de polimorfismo e herança para alcançar flexibilidade, mantendo o código base intacto.

##  Sintomas da Violação do OCP

- Modificação de código existente para implementar novas funcionalidades.
- Alta propensão a bugs: cada vez que uma nova funcionalidade é adicionada, é necessário modificar várias classes, o que pode introduzir erros.
- Código que quebra com frequência devido à introdução de novas funcionalidades.
- Muitos if ou switch para verificar diferentes tipos ou condições, ao invés de utilizar herança ou interfaces.

Vamos a um exemplo, temos uma classe que calcula o preço de diferentes tipos de produtos. Cada vez que adicionamos um novo tipo de produto, precisamos modificar a classe CalculadoraDePrecos.

```csharp
public class CalculadoraDePrecos
{
    public decimal CalcularPreco(Product product)
    {
        if (product.Type == "Physical")
        {
            return product.BasePrice + 10; // Custo de envio
        }
        else if (product.Type == "Digital")
        {
            return product.BasePrice; // Sem custo de envio
        }
        else if (product.Type == "Subscription")
        {
            return product.BasePrice * 0.9m; // Desconto de 10%
        }
        
        throw new ArgumentException("Tipo de produto desconhecido.");
    }
}
```

Quais são os problemas deste código?

Cada vez que um novo tipo de produto é adicionado, precisamos modificar a classe CalculadoraDePrecos, o que viola o OCP.
Além disso, toda mudança neste código esta propenso a erros.
O método CalcularPreco cresce de forma descontrolada com a adição de mais tipos de produtos.

---

Agora, vamos refatorar o código para seguir o OCP. Vamos procurar uma forma que a classe CalculadoraDePrecos possa ser estendida sem ser modificada.

```csharp
public interface IPrecificacaoStrategy
{
    decimal CalcularPreco(Product product);
}

public class PhysicalProductPricingStrategy : IPrecificacaoStrategy
{
    public decimal CalcularPreco(Product product)
    {
        return product.BasePrice + 10; // Custo de envio
    }
}

public class DigitalProductPricingStrategy : IPrecificacaoStrategy
{
    public decimal CalcularPreco(Product product)
    {
        return product.BasePrice; // Sem custo de envio
    }
}

public class SubscriptionProductPricingStrategy : IPrecificacaoStrategy
{
    public decimal CalcularPreco(Product product)
    {
        return product.BasePrice * 0.9m; // Desconto de 10%
    }
}

public class CalculadoraDePrecos
{
    private readonly IPrecificacaoStrategy _pricingStrategy;

    public CalculadoraDePrecos(IPrecificacaoStrategy pricingStrategy)
    {
        _pricingStrategy = pricingStrategy;
    }

    public decimal CalcularPreco(Product product)
    {
        return _pricingStrategy.CalcularPreco(product);
    }
}

```

Melhorias aplicadas ao código:

Criamos uma interface IPricingStrategy e implementamos estratégias específicas para cada tipo de produto.
A classe CalculadoraDePrecos está agora fechada para modificação e aberta para extensão. Podemos adicionar novos tipos de produtos simplesmente criando novas implementações de IPrecificacaoStrategy, sem alterar o código da classe.
O código está mais limpo, organizado e menos propenso a erros.

## Benefícios e Impacto do OCP

- Extensibilidade: O sistema pode ser facilmente estendido com novas funcionalidades sem alterar o código existente, o que minimiza o risco de introduzir bugs.
- Manutenibilidade: Como não há necessidade de modificar o código existente para adicionar novas funcionalidades, o sistema se torna mais fácil de manter ao longo do tempo.
- Organização: O código é dividido de forma modular, onde cada responsabilidade está bem definida e encapsulada.
- Testabilidade: Cada parte do sistema pode ser testada independentemente, uma vez que as novas funcionalidades são adicionadas por meio de novas classes.