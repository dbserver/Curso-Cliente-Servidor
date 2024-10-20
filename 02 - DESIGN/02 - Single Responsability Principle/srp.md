# Conceito

Responsabilidade única diz o seguinte: 

"Uma classe ou um módulo deve ter um, e somente um, motivo para mudar."

Uncle Bob adiciona:

"Apenas um ator deve ser a origem da mudança."

## Principio difícil

O Principio da Responsabilidade única é um dos mais difíceis de entender, talvez porque o significado abra precedente para mais de uma interpretação (inclusive no gepeto 10\/2024 esta errado).
Vamos tentar entender da forma correta, segundo Uncle Bob.

O que significa um motivo para mudar, significa que o software só deve ter um único motivo para receber alterações, ok, mas ai parece obvio né? Vamos seguir então com uma pergunta;
Quem muda um software?

Quem muda um software é uma pessoa, concordam?
Mas uma pessoa, quando em um software significa um grupo com características especificas, então vamos renomear esta pessoa para uma pessoa do software, logo, quem muda um software é um ator ou uma persona.


## Entendendo melhor:

Vamos considerar uma classe chamada LinhaExtrato, que serviria para imprimir uma linha do extrato.
Esta classe tem três métodos, uma para impressão da data, outro para impressão da ocorrência, outro para impressão do valor.
Esta classe é utilizada pelo cliente do banco, para imprimir o extrato da sua conta, é utilizado pelo setor de auditoria para verificação contábil.

Com estas informações, o que podemos inferir que esta errado nesta classe? 

```csharp

public class LinhaExtrato{

    public string ImprimirDataFormatada(){ return "dd/mm/aaaa hh:MM:ss"; }

    public string ImprimirDescricaoOcorrencia(){ return "Depósito na boca do caixa."}

    public string ImprimirValorFormatado(){ return "R$100,00"; }
}
```

## Resolvendo o problema

Bom, primeiro problema é que tem 2 atores solicitando alterações para esta classe.
Para o primeiro ator, chamado cliente, tudo bem o retorno com 2 casas decimais, porém para auditoria não, para auditoria contábil precisamos de 4 casas decimais.

Então pensando em uma situação real de desenvolvimento de software, um bug é aberto para relatório de extrato auditoria, na descrição do bug esta escrito: "Para correção do relatório auditoria deve imprimir com 4 casas decimais."

O desenvolvedor pega o ticket aberto para correção de bug e altera de "R$100,00" para "R$100,0000", e temos um problema já levantado em aulas anteriores.

Poderíamos explorar coisas como criar um método diferente, quem chamar usar um if para identificar quem é o autor, mas como a ideia aqui são melhores práticas não vamos nem explorar ideias ruins de solução, então vamos para o código explorar o que seria uma boa possível solução:

```csharp
public abstract class AbstractLinhaExtrato{

    public string ImprimirDataFormatada(){ return "dd/mm/aaaa hh:MM:ss"; }

    public string ImprimirDescricaoOcorrencia(){ return "Depósito na boca do caixa."; }

    public abstract string ImprimirValorFormatado();
}

public class LinhaExtratoCliente : AbstractLinhaExtrato{

    public override string ImprimirValorFormatado(){ return "R$100,00"; }
}

public class LinhaExtratoAuditoria : AbstractLinhaExtrato{

    public override string ImprimirValorFormatado(){ return "R$100,0000"; }
}
```

## Porque o SRP é o princípio mais difícil de entender

Segundo o gepeto, em 10/2024, o SRP tem a seguinte definição:

"O Princípio da Responsabilidade Única, ou SRP, é um dos pilares fundamentais do SOLID. Ele afirma que uma classe deve ter apenas uma razão para mudar, ou seja, ela deve ser responsável por uma única parte da funcionalidade do software. Quando uma classe faz mais do que o necessário, ela se torna difícil de manter, testar e modificar."

Lembrando que IA aprende com o que esta disponível, neste caso, por mais que seja conhecimento gerado por ele, a base de conhecimento é a base que esta espalhada. Logo, podemos inferir que o entendimento errado do conceito é mais difundido que o entendimento real.

Isto significa que tudo esta errado nesta definição? Não, o que esta definição aborda, nós abordamos em más práticas ou design de código ruins, e podem ser corrigidas e contornadas por design patterns de mercado.