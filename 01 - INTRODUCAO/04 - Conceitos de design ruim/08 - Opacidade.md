# Opacidade

## Conceito de Opacidade

A opacidade no código refere-se à dificuldade de compreensão ou leitura, quando o comportamento ou a lógica do sistema não é claro para outros desenvolvedores. Um código opaco não é intuitivo e requer um esforço excessivo para ser entendido. Isso pode acontecer devido a nomes de variáveis confusos, estrutura de controle complexa ou lógica não evidente, tornando o código difícil de ler, manter ou expandir.

## Principais Sintomas

Aqui estão alguns sinais de que o código pode estar opaco:

- Variáveis e funções com nomes pouco descritivos: Nomes que não refletem o propósito ou uso.
- Lógica complicada e não intuitiva: Estruturas de controle como loops ou condicionais aninhadas e longas que dificultam o entendimento.
- Abstrações excessivas ou mal planejadas: Uso de classes, interfaces e padrões de design que complicam a leitura do código.
- Comentários excessivos ou confusos: Quando há necessidade de muitos comentários para explicar o código, é um sinal de que o código não está claro.
- Métodos longos e sobrecarregados: Funções que realizam muitas tarefas diferentes, dificultando sua compreensão.

## Causas de Código com Opacidade

Algumas das causas comuns de código opaco incluem:

- Nomenclatura inadequada: Variáveis e métodos com nomes que não refletem seu uso ou propósito.
- Falta de consistência: Uso inconsistente de convenções de código, dificultando a compreensão por outros desenvolvedores.
- Design pouco intuitivo: Decisões de design que priorizam a complexidade em vez da simplicidade.
- Lógica inadequadamente segmentada: Falta de modularidade, com funções ou classes que fazem muito ou têm responsabilidade ambígua.
- Falta de documentação: Ausência de documentação básica, como descrições de métodos ou de sua finalidade.

## Impactos Negativos da Opacidade

Os principais impactos negativos do código opaco são:

- Dificuldade de manutenção: Um código difícil de entender é também difícil de manter, resultando em aumento do tempo para corrigir bugs ou adicionar funcionalidades.
- Maior propensão a erros: A falta de clareza aumenta as chances de erros quando outros desenvolvedores fazem mudanças ou adições ao código.
- Baixa colaboração: A opacidade no código pode desencorajar a colaboração, já que desenvolvedores podem hesitar em modificar um código que não entendem completamente.
- Perda de produtividade: O tempo gasto para entender o código aumenta, impactando negativamente a produtividade da equipe.
- Dívida técnica: O código opaco tende a acumular problemas, já que é mais difícil refatorá-lo ou melhorar sua qualidade.

## Como Evitar a Opacidade no Código

Aqui estão algumas práticas que ajudam a evitar a opacidade no código:

- Nomes descritivos: Use nomes de variáveis e métodos que descrevam claramente seu propósito.
- Funções pequenas e coesas: Escreva funções pequenas com responsabilidades claras e uma única tarefa bem definida.
- Refatoração contínua: Sempre que possível, refatore o código para simplificar a lógica e melhorar a legibilidade.
- Aplicação do princípio Clean Code: Mantenha o código simples, claro e com pouca dependência de comentários extensivos.
- Documentação mínima necessária: Inclua documentação clara e concisa para métodos e classes, especialmente para lógica complexa ou não intuitiva.

---

Exemplo de Código Opaco (Antes)
Este código tem lógica confusa e mal nomeada, o que torna difícil entender seu propósito:

```csharp
public class P
{
    public void M(List<int> a)
    {
        var b = 0;
        for (int i = 0; i < a.Count; i++)
        {
            if (a[i] > 10)
            {
                b += a[i] * 2;
            }
            else
            {
                b += a[i];
            }
        }
        if (b > 100)
        {
            Console.WriteLine("High");
        }
        else
        {
            Console.WriteLine("Low");
        }
    }
}
```

Problemas:

Nomenclatura opaca: O nome da classe P, do método M, e das variáveis a e b não indicam claramente o que fazem.
Lógica dispersa: O código mistura a lógica de processamento com a lógica de impressão, tornando mais difícil entender o propósito geral.

---

Exemplo Corrigido com Clareza Melhorada (Depois)
Aqui está uma versão refatorada que melhora a legibilidade:


```csharp
public class OrderProcessor
{
    public void ProcessOrders(List<int> orderAmounts)
    {
        int totalAmount = CalculateTotalAmount(orderAmounts);
        DisplayOrderCategory(totalAmount);
    }

    private int CalculateTotalAmount(List<int> orderAmounts)
    {
        int total = 0;
        foreach (var amount in orderAmounts)
        {
            if (amount > 10)
            {
                total += amount * 2;
            }
            else
            {
                total += amount;
            }
        }
        return total;
    }

    private void DisplayOrderCategory(int totalAmount)
    {
        if (totalAmount > 100)
        {
            Console.WriteLine("High");
        }
        else
        {
            Console.WriteLine("Low");
        }
    }
}
```

**Melhorias**:

- Nomes mais descritivos: A classe OrderProcessor, o método ProcessOrders e as variáveis orderAmounts e totalAmount refletem melhor o propósito do código.
- Separação de responsabilidades: O cálculo do total e a exibição da categoria de pedido foram separados em métodos distintos, facilitando o entendimento.
