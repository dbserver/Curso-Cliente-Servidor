# Liskov Substitution Principle

O Princípio da Substituição de Liskov (LSP) é o terceiro princípio do S.O.L.I.D.. Ele afirma que objetos de uma classe derivada devem poder substituir objetos da classe base sem alterar as propriedades corretas do programa. Em outras palavras, uma classe filha deve ser **completamente** substituível por sua classe base, sem quebrar o comportamento do sistema. Isso assegura a integridade do sistema quando lidamos com hierarquias de herança.

O Princípio da Substituição de Liskov foca em garantir que classes derivadas possam ser usadas no lugar das classes base sem alterar a lógica do programa. Esse princípio é essencial para garantir que as hierarquias de herança façam sentido e que o polimorfismo funcione corretamente.

Por exemplo, uma classe base chamada Emprestimo e uma classe derivada de Emprestimo chamada EmprestimoConsignado o LSP garante que qualquer código que funcione com Emprestimo também funcione com EmprestimoConsignado, sem precisar de modificações.

##  Sintomas de Violação do LSP

- Sobrecarga desnecessária: Se a classe derivada precisa alterar o comportamento da classe base para funcionar, isso é um sinal de que o LSP está sendo violado.
- Uso de verificações de tipo: Quando o código usa if ou switch para tratar classes derivadas de forma diferente, isso indica que a substituição não é adequada.
- Erros inesperados: Substituir uma classe base por uma derivada resulta em comportamentos incorretos ou erros, o que revela a violação do princípio.

Vamos a um exemplo:

Violando o LSP
Neste exemplo, temos uma classe base Emprestimo que possui o método EmprestarSemValidarModalidade. A classe derivada EmprestimoConsignado não deve EmprestarSemValidarModalidade sem validar, mas ainda é obrigada a implementar o método EmprestarSemValidarModalidade.

```csharp
public class Emprestimo
{
    public virtual void EmprestarSemValidarModalidade()
    {
        Console.WriteLine("Emprestimo executado com sucesso");
    }
}

public class EmprestimoConsignado : Emprestimo
{
    public override void EmprestarSemValidarModalidade()
    {
        throw new InvalidOperationException("Emprestimo não pode ser executado nesta modalidade");
    }
}
```

Problemas:

- A classe Emprestimo não deve herdar o método EmprestarSemValidarModalidade, pois EmprestimoConsignado não devem emprestar sem validar a modalidade. No entanto, como Emprestimo herda de Emprestimo, a substituição de EmprestarSemValidarModalidade com uma exceção viola o LSP.
- Qualquer código que espera que todos os empréstimos possam emprestar sem validar modalidade pode falhar ao lidar com a classe Emprestimo.

Vamos tentar corrigir refatorando o código atual:

```csharp
public abstract class AbstractEmprestimo
{
    // Propriedades e métodos comuns a todos os emprestimos.
}

public interface IEmprestimoSemValidacaoDeModadlidade
{
    void EmprestarSemValidarModalidade();
}

public class Emprestimo : AbstractEmprestimo, IEmprestimoSemValidacaoDeModadlidade
{
    public void EmprestarSemValidarModalidade()
    {
        Console.WriteLine("Emprestimo executado com sucesso");
    }
}

public class EmprestimoConsignado : AbstractEmprestimo
{
    // Nenhum método EmprestarSemValidarModalidade se faz necessário
}

```

Melhorias aplicadas na refatoração:

Agora, temos uma distinção clara entre empréstimos que não validam modalidade  (Emprestimo) e aqueles que validam (EmprestimoConsignado), respeitando o LSP.
A classe EmprestimoConsignado pode ser usada sem violar o comportamento esperado de outros empréstimos.
O código ficou mais limpo e alinhado ao princípio, evitando exceções desnecessárias.

## Impactos Negativos da Violação do LSP

- Inconsistência no comportamento: Ao violar o LSP, você cria inconsistências no comportamento esperado das classes derivadas, o que pode levar a bugs difíceis de detectar.
- Polimorfismo quebrado: O polimorfismo perde seu propósito, pois as classes derivadas não podem ser substituídas de maneira transparente.
- Código frágil: O código se torna mais suscetível a erros, especialmente em sistemas grandes e complexos, onde as classes derivadas são usadas em várias partes do sistema.

## Como Evitar a Violação do LSP

- Evite herança desnecessária: Utilize herança apenas quando as classes derivadas realmente forem especializações da classe base.
- Utilize interfaces adequadas: Separe comportamentos distintos em interfaces, como no exemplo IEmprestimoSemValidacaoDeModadlidade, para que as classes implementem apenas o que precisam.
- Respeite o comportamento esperado: Se uma classe derivada não pode substituir a base sem alterar seu comportamento, isso indica que a herança não foi bem aplicada.

