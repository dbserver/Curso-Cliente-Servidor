# Imobilidade

## Conceito de Imobilidade 

Imobilidade é um dos problemas clássicos de design de software e refere-se à dificuldade de reutilizar partes de um sistema porque o código está fortemente acoplado. Isso significa que, ao tentar mover um pedaço de código para outro lugar ou reutilizá-lo em outro projeto, o desenvolvedor é forçado a levar consigo uma série de dependências desnecessárias, criando uma cadeia complexa de vínculos entre módulos que deveriam ser independentes.

## Principais Sintomas de Imobilidade

- Definição rápida: Imobilidade ocorre quando o código não pode ser facilmente movido ou reutilizado sem trazer consigo partes desnecessárias do sistema.
- Consequência: A reutilização de código se torna difícil ou impossível, forçando o retrabalho e a duplicação de código, o que leva a aumento de manutenção e fragilidade.

**Exemplo**: Imagine um módulo de cálculo financeiro que, ao tentar reutilizar, você percebe que ele depende de várias outras partes do sistema, como autenticação, logging, e controle de acesso. Mover ou isolar essa funcionalidade se torna complexo.

## Causas de código com Imobilidade

- Acoplamento Forte:
    - Excesso de dependências: Quando uma classe ou método depende de muitos outros, você precisa mover tudo junto, o que gera imobilidade.
    - Módulos grandes e monolíticos: Sistemas com módulos enormes em que cada parte depende de outra. Mexer em uma parte significa ter que ajustar várias outras.

- Falta de Coesão:
    - Responsabilidades misturadas: Quando uma classe ou módulo faz muitas coisas diferentes, torna-se difícil reutilizar apenas uma parte dele. O código não é modular o suficiente para ser extraído facilmente.

- Dependências circulares:
    - Quando módulos dependem diretamente ou indiretamente uns dos outros em um ciclo, mover qualquer parte resulta na quebra do ciclo e requer um esforço significativo para isolar dependências.

## Impactos Negativos da Imobilidade

- Dificuldade de Reutilização: O código não pode ser aproveitado em outros projetos ou áreas do sistema sem esforço adicional.
- Complexidade no Refatoração: Alterar ou melhorar uma parte do código sem quebrar as dependências existentes é difícil.
- Aumento no Custo de Manutenção: Desenvolvedores acabam duplicando funcionalidades em vez de reutilizá-las, o que leva a uma manutenção mais cara e complexa.
- Maior Chance de Erros: Como muitos módulos estão interconectados, mexer em uma parte pode inadvertidamente introduzir bugs em outra.

## Como Evitar Código com Imobilidade

- Desacoplamento:
    - Aplicar princípios de design SOLID: Em especial o princípio da Inversão de Dependência (DIP), que reduz o acoplamento direto entre classes.
    - Uso de Injeção de Dependências (DI): Facilita a substituição de dependências e promove a criação de componentes mais modulares.

- Segregação de Responsabilidades:
    - Seguir o Princípio da Responsabilidade Única (SRP): Cada classe ou módulo deve ter uma única responsabilidade, permitindo que sejam movidos ou reutilizados com facilidade.

- Modularidade:
    - Criação de Bibliotecas ou Pacotes Reutilizáveis: Extrair componentes específicos e transformá-los em pacotes ou bibliotecas que possam ser reutilizados sem dependências do sistema completo.
- Uso de Interfaces e Abstrações:
    - Definir interfaces claras: Isso permite que diferentes implementações possam ser substituídas sem impactar outras partes do código.

# Exemplo de código com Imobilidade:

```csharp
public class RelatorioFinanceiro
{
    private ServicoAutenticacao _autenticacao;
    private Logger _logger;
    private BancoDeDados _db;

    public RelatorioFinanceiro()
    {
        _autenticacao = new ServicoAutenticacao();
        _logger = new Logger();
        _db = new BancoDeDados();
    }

    public void GerarRelatorio()
    {
        if (_autenticacao.VerificarUsuario())
        {
            _logger.Log("Relatório gerado.");
            _db.SalvarRelatorio();
        }
    }
}
```

Problema: A classe RelatorioFinanceiro está diretamente acoplada ao sistema de autenticação, logging e banco de dados, tornando impossível reutilizar o método GerarRelatorio em outro contexto sem levar esses componentes juntos.

# Exemplo da correção de código com Imobilidade:

```csharp
public interface IAutenticacao { bool VerificarUsuario(); }
public interface ILogger { void Log(string mensagem); }
public interface IBancoDeDados { void SalvarRelatorio(); }

public class RelatorioFinanceiro
{
    private readonly IAutenticacao _autenticacao;
    private readonly ILogger _logger;
    private readonly IBancoDeDados _db;

    public RelatorioFinanceiro(IAutenticacao autenticacao, ILogger logger, IBancoDeDados db)
    {
        _autenticacao = autenticacao;
        _logger = logger;
        _db = db;
    }

    public void GerarRelatorio()
    {
        if (_autenticacao.VerificarUsuario())
        {
            _logger.Log("Relatório gerado.");
            _db.SalvarRelatorio();
        }
    }
}
```

**Melhoria**: Ao usar interfaces e injeção de dependências, a classe RelatorioFinanceiro agora pode ser reutilizada em diferentes contextos, substituindo as implementações de autenticação, logging ou banco de dados conforme necessário, tornando o código mais flexível e móvel.