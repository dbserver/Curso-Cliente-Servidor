# Repetição Desnecessária

## Conceito de Repetição Desnecessária

Repetição desnecessária, ou code duplication, ocorre quando blocos de código semelhantes ou idênticos são repetidos em múltiplas partes do sistema. Isso viola o princípio DRY (Don't Repeat Yourself), que diz que a lógica não deve ser duplicada. A repetição de código leva à inconsistência e à dificuldade de manutenção, uma vez que qualquer alteração futura precisará ser feita em todos os lugares onde o código foi duplicado.

## Principais Sintomas

Aqui estão os principais sintomas de repetição desnecessária:

- Código idêntico em diferentes métodos ou classes: O mesmo bloco de código, como uma validação ou cálculo, aparece em várias partes do sistema.
- Funções similares com pequenas variações: Funções que realizam tarefas quase idênticas, mas com pequenas diferenças, como diferentes parâmetros.
- Uso excessivo de Copy-Paste: Código duplicado por cópia e colagem ao adicionar novas funcionalidades ou corrigir bugs.
- Repetição de lógica comum: Algoritmos, como cálculos matemáticos ou validação de entrada, são replicados em diferentes partes do código.

## Causas de Código com Repetição Desnecessária

As principais causas da repetição desnecessária incluem:

- Falta de refatoração: Desenvolvedores podem não perceber que estão duplicando código, ou optam por uma solução rápida sem reorganizar o código existente.
- Copiar e colar soluções: A abordagem de copiar e colar código de uma parte do sistema para outra sem abstrair a lógica comum.
- Desconhecimento de padrões de design: Falta de compreensão ou aplicação de boas práticas de engenharia, como o uso de funções reutilizáveis, classes e herança.
- Pressão por prazos: Em cenários com prazos apertados, pode ser mais fácil e rápido duplicar o código do que refatorar para remover a repetição.

## Impactos Negativos da Repetição Desnecessária

Os impactos negativos de código com repetição desnecessária são:

- Aumento da complexidade: Com múltiplas cópias de código, qualquer mudança precisa ser replicada em vários lugares, aumentando a probabilidade de erros.
- Maior custo de manutenção: Corrigir bugs ou modificar funcionalidades exige identificar todas as instâncias do código duplicado.
- Inconsistência: O mesmo comportamento pode ser alterado de maneira diferente em partes duplicadas, levando a inconsistências no sistema.
- Dificuldade de leitura: O código se torna mais difícil de entender e seguir, especialmente se várias partes realizam essencialmente a mesma coisa de formas ligeiramente diferentes.

## Como Evitar Repetição Desnecessária

Algumas formas de evitar a repetição de código são:

- Aplicar o princípio DRY: Centralizar lógicas comuns em funções ou classes reutilizáveis.
- Refatoração frequente: Ao detectar duplicação de código, sempre refatore para abstrair a lógica duplicada.
- Utilizar herança e composição: Aproveitar herança e composição de classes para compartilhar comportamentos entre diferentes partes do sistema.
- Padrões de design apropriados: Implementar padrões como Factory, Strategy ou Template Method para lidar com variações na lógica sem duplicar código.

--- 

Exemplo de Código com Repetição Desnecessária (Antes)
Aqui está um exemplo onde o código de cálculo de desconto está duplicado em dois métodos diferentes:

```csharp
public class Order
{
    public decimal CalculateRegularDiscount(decimal totalPrice)
    {
        if (totalPrice > 100)
        {
            return totalPrice * 0.1m;
        }
        return 0;
    }

    public decimal CalculateSpecialDiscount(decimal totalPrice)
    {
        if (totalPrice > 100)
        {
            return totalPrice * 0.15m;
        }
        return 0;
    }
}
```

**Problema**: Há uma duplicação no código de cálculo de descontos, o que aumenta o risco de inconsistência caso as regras mudem.

---

Exemplo Corrigido com Repetição Eliminada (Depois)
Agora, vamos refatorar o código para eliminar a duplicação, centralizando a lógica em um método auxiliar:


```csharp
public class Order
{
    private decimal CalculateDiscount(decimal totalPrice, decimal discountRate)
    {
        if (totalPrice > 100)
        {
            return totalPrice * discountRate;
        }
        return 0;
    }

    public decimal CalculateRegularDiscount(decimal totalPrice)
    {
        return CalculateDiscount(totalPrice, 0.1m);
    }

    public decimal CalculateSpecialDiscount(decimal totalPrice)
    {
        return CalculateDiscount(totalPrice, 0.15m);
    }
}
```

Vantagens da Versão Corrigida:

- Menos duplicação: A lógica comum foi centralizada no método CalculateDiscount, reduzindo a duplicação.
- Fácil manutenção: Se a lógica de desconto mudar, precisaremos atualizar apenas um lugar.
- Código mais legível: O código agora está mais fácil de entender e segue melhor o princípio DRY.