# Rigidez de código

## Definição de Rigidez: 

A rigidez refere-se à dificuldade em modificar ou estender um sistema de software devido à sua estrutura. Quando um código é rígido, alterações pequenas e aparentemente simples podem exigir uma série de modificações em diferentes partes do sistema. Isso acontece por várias razões:

- Acoplamento Forte: Quando classes ou módulos estão fortemente interligados, a alteração de um deles pode afetar outros, exigindo mudanças em vários lugares.

- Código Monolítico: Sistemas que não foram divididos em componentes ou serviços menores tendem a ser mais rígidos, pois mudanças em um módulo podem impactar o funcionamento de outros.

- Falta de Abstração: A ausência de interfaces ou classes base torna o código menos flexível. Sem abstrações, as mudanças em um tipo de objeto podem exigir mudanças em todas as partes do código que interagem com esse objeto.

- Dependências Rígidas: Quando as dependências são codificadas de forma rígida, em vez de serem injetadas ou abstraídas, a capacidade de modificar ou substituir partes do sistema se torna limitada.

## Porque rigidez é impactante?

A rigidez de código impacta nos seguintes pontos:


- Agilidade no Desenvolvimento: Em ambientes ágeis, a capacidade de adaptar-se rapidamente a novas demandas é crucial. Um código rígido dificulta essa adaptação, aumentando o tempo necessário para implementar mudanças.

- Aumento da Dívida Técnica: A rigidez muitas vezes resulta em dívida técnica, onde a equipe procrastina a refatoração ou a melhoria do código, levando a problemas maiores no futuro. Com o tempo, a dívida técnica pode se acumular, tornando o código ainda mais difícil de gerenciar.

- Custo de Manutenção: O custo associado à manutenção de um sistema rígido pode ser significativo. À medida que o sistema cresce e evolui, o tempo e o esforço necessários para implementar novas funcionalidades aumentam, impactando a produtividade da equipe.

- Qualidade do Software: Sistemas rígidos são mais propensos a conter bugs, pois mudanças em uma parte do código podem ter efeitos colaterais inesperados em outras partes. Isso compromete a confiança da equipe no sistema e na capacidade de entregar software de qualidade.

- Satisfação da Equipe: Desenvolvedores que trabalham em sistemas rígidos frequentemente experimentam frustração e desmotivação. A dificuldade em implementar mudanças pode levar a um ambiente de trabalho negativo, afetando a moral e a produtividade.

## Vamos tentar detalhar um pouco mais os pontos que definem rigidez.


### Acoplamento Forte

Podemos dizer que uma classe com baixo acoplamento ou acoplamento fraco não depende de muitas outras classes para fazer o que precisa fazer.
Já uma classe com acoplamento forte depende muito de muitas outras classes, o que torna difícil de manter, difícil de entender e quase impossível de ser reutilizada.

```csharp
public class CarrinhoCompra
{
    public float Preco;
    public int Quantidade;
}

public class CarrinhoItens
{
    public CarrinhoCompra[] items;
}
public class Pedido
{
    private CarrinhoItens carrinho;
    private float imposto;
    public Pedido(CarrinhoItens carrinho, float imposto)
    {
        this.carrinho = carrinho;
        this.imposto = imposto;
    }
    public float PedidoTotal()
    {
        float carrinhoTotal = 0;
        for (int i = 0; i < carrinho.items.Length; i++)
        {
            carrinhoTotal += carrinho.items[i].Preco * 
                                             carrinho.items[i].Quantidade;
        }
        carrinhoTotal += carrinhoTotal * imposto;
        return carrinhoTotal;
    }
}
```

Neste código temos um exemplo de acoplamento forte, onde a classe pedido executa todo o código com dependências das demais classes, dificultando qualquer alteração ou extensão de código.

Se refatorarmos para:

```csharp
public class CarrinhoCompra
{
    public float Preco;
    public int Quantidade;
    public float GetTotalItem()
    {
        return Preco * Quantidade;
    }
}

public class CarrinhoItens
{
    public CarrinhoCompra[] items;
    public float GetCarrinhoItensTotal()
    {
        float carrinhoTotal = 0;
        foreach (CarrinhoCompra item in items)
        {
            carrinhoTotal += item.GetTotalItem();
        }
        return carrinhoTotal;
    }
}
public class Pedido
{
    private CarrinhoItens carrinho;
    private float imposto;
    public Pedido(CarrinhoItens carrinho, float imposto)
    {
        this.carrinho = carrinho;
        this.imposto = imposto;
    }
    public float PedidoTotal()
    {
        return carrinho.GetCarrinhoItensTotal() * (2.0f + imposto);
    }
}
```

O que mudamos aqui foi dar maior responsabilidade para cada classe, possibilitando que novas implementações sejam possíveis sem que o impacto de uma nova funcionalidade necessite alterar todo ecossistema daquela lógica de negócio.

Com por exemplo, adicionar uma uma lógica de desconto:

```csharp
public class CarrinhoCompra
{
    public float Preco;
    public int Quantidade;

    public float Desconto

    public float GetTotalItem()
    {
        return Preco * Quantidade - Desconto;
    }
}
```

No primeiro código precisaríamos adicionar esta lógica na classe pedido, gerando maior acoplamento, maior necessidade de duplicação de código, maior custo de desenvolvimento.

<a href="https://macoratti.net/23/01/c_acoplafrafort1.htm">Fonte: Macoratti</a>

### Falta de Abstração

Mais para frente retomaremos o conceito de abstração em orientação a objetos, sendo assim vou tratar neste momento como conhecimento já adquirido.

Vou utilizar como base o mesmo exemplo acima do pedido e carrinho de compras, focando apenas no pedido, alterando a função para pagamento e acrescentando um pouco mais de código.

```csharp
public class PagamentoPedido
{
    private CarrinhoItens carrinho;
    private float imposto;
    public Pedido(CarrinhoItens carrinho, float imposto)
    {
        this.carrinho = carrinho;
        this.imposto = imposto;
    }
    public float PedidoTotal()
    {
        return carrinho.GetCarrinhoItensTotal() * (2.0f + imposto);
    }

    public void PagamentoExecutado(){
        // Grava em banco de dados que o pagamento foi executado
        // Envia email de confirmacao para o cliente
        EmailConfirmacao();
        // Avisa infra estrutura que o processo foi concluido
        LogPagamentoConfirmadoEmailEnviado();
    }

    public void EmailConfirmacao(){
        // implementação do envio do email
    }

    public void LogPagamentoConfirmadoEmailEnviado(){
        // grava o log do processo como finalizado na infra estrutura
    }
}

public class ExemploUsoPagamentoPedido
{
    private PagamentoPedido _pagamentoPedido;

    public ExemploUsoPagamentoPedido(PagamentoPedido pagamentoPedido)
    {
        this._pagamentoPedido = pagamentoPedido;
    }

    public void MetodoQueUsaPagamentoPedido()
    {
        _pagamentoPedido.PagamentoExecutado();
        _pagamentoPedido.EmailConfirmacao();
        _pagamentoPedido.LogPagamentoConfirmadoEmailEnviado();
    }
}
```

Bom, no código acima temos diversos problemas, mas vamos focar na falta de abstração, primeiramente temos um classe concreta que faz todo processo de pagamento do pedido.
O problema não esta apenas em ela ser concreta, mas sim que ela abre para fora dela todo processo executado, ou seja, tanto a base do que ela deve fazer como todos os detalhes estão expostos.

Vamos tentar corrigir apenas o problema da abstração?

```csharp

public Interface IPagamentoPedido
{
    void PagamentoExecutado();
}

public class PagamentoPedido : IPagamentoPedido
{
    private CarrinhoItens carrinho;
    private float imposto;
    public Pedido(CarrinhoItens carrinho, float imposto)
    {
        this.carrinho = carrinho;
        this.imposto = imposto;
    }
    public float PedidoTotal()
    {
        return carrinho.GetCarrinhoItensTotal() * (2.0f + imposto);
    }

    public void PagamentoExecutado(){
        // Grava em banco de dados que o pagamento foi executado
        // Envia email de confirmacao para o cliente
        EmailConfirmacao();
        // Avisa infra estrutura que o processo foi concluido
        LogPagamentoConfirmadoEmailEnviado();
    }

    public void EmailConfirmacao(){
        // implementação do envio do email
    }

    public void LogPagamentoConfirmadoEmailEnviado(){
        // grava o log do processo como finalizado na infra estrutura
    }
}

public class ExemploUsoPagamentoPedido
{
    private IPagamentoPedido _pagamentoPedido;

    public ExemploUsoPagamentoPedido(IPagamentoPedido pagamentoPedido)
    {
        this._pagamentoPedido = pagamentoPedido;
    }

    public void MetodoQueUsaPagamentoPedido()
    {
        _pagamentoPedido.PagamentoExecutado();
    }
}
```

Vamos entender o que mudou do ponto de vista de abstração.

Primeiramente criamos uma interface para abstrair apenas o necessário que o negocio precisa conhecer, ou seja, quem chamar a classe de pagamento pedido terá acesso apenas ao máximo necessário de informações, sem conhecimento dos detalhes de implementação.

Desta forma, minha classe PagamentoPedido implementa a interface IPagamentoPedido, e a minha classe concreta não mais será utilizada para quem precisa efetuar o pagamento, sempre a interface, desta forma encapsulamos os detalhes e expomos o que precisa ser exposto.

Como visto no exemplo acima, quem utiliza a classe agora só enxerga o método de pagamento executado, não sabe mais email é enviado, que a infra grava os logs de execução.

### Código monolítico e dependências rígidas

Código monolítico não é necessariamente sinônimo de rigidez, mas dado o forma que ele é construído ele tem a tendencia a facilitar o alto acoplamento e outras más praticas, mas o bom design de código faz com que mesmo monólitos não tenham tanta rigidez em código.
O que vem muito de encontro as dependências rígidas que podem ser vistas de duas formas, uma é o código acoplado, onde a mesma funcionalidade não consegue ser utilizada em mais de um sistema.

Por exemplo, a autenticação / autorização, quando você à constrói dentro da aplicação se outra aplicação precisar utilizar a mesma rotina, então ou se refatora tudo na aplicação atual ou se replica código, ambas soluções são ruins neste ponto.

Outro ponto relacionado a design de código mesmo.

Vamos pegar como exemplo o código de carrinho de compras e fazer o caminho contrário, vamos explicar a boa solução e na sequencia mostrar a forma mais rígida de fazer a mesma coisa:

```csharp
public class CarrinhoCompra
{
    public float Preco;
    public int Quantidade;
    public float GetTotalItem()
    {
        return Preco * Quantidade;
    }
}

public class CarrinhoItens
{
    public CarrinhoCompra[] items;
    public float GetCarrinhoItensTotal()
    {
        float carrinhoTotal = 0;
        foreach (CarrinhoCompra item in items)
        {
            carrinhoTotal += item.GetTotalItem();
        }
        return carrinhoTotal;
    }
}

public class Pedido
{
    private CarrinhoItens carrinho;
    private float imposto;
    public Pedido(CarrinhoItens carrinho, float imposto)
    {
        this.carrinho = carrinho;
        this.imposto = imposto;
    }
    public float PedidoTotal()
    {
        return carrinho.GetCarrinhoItensTotal() * (2.0f + imposto);
    }
}
```

Quando você inicializa o Pedido, no construtor você recebe uma instancia da classe CarrinhoItens, o nome disso é injeção de dependência, onde a classe recebe as dependências da sua execução injetadas no seu construtor, desconhecendo os detalhes de sua implementação ou inicialização.

Vamos alterar a classe Pedido para mostrar como ficaria com uma implementação rígida:

```csharp
public class CarrinhoCompra
{
    public float Preco;
    public int Quantidade;
    public float GetTotalItem()
    {
        return Preco * Quantidade;
    }
}

public class CarrinhoItens
{
    public CarrinhoCompra[] items;
    public float GetCarrinhoItensTotal()
    {
        float carrinhoTotal = 0;
        foreach (CarrinhoCompra item in items)
        {
            carrinhoTotal += item.GetTotalItem();
        }
        return carrinhoTotal;
    }
}

public class Pedido
{
    private CarrinhoItens carrinho;
    private float imposto;

    public Pedido(List<CarrinhoCompra> _items, float imposto)
    {
        var carrinho = new CarrinhoItens();
        carrinho.items = _items.ToArray();

        this.carrinho = carrinho;
        this.imposto = imposto;
    }
    public float PedidoTotal()
    {
        return carrinho.GetCarrinhoItensTotal() * (2.0f + imposto);
    }
}
```

Nesta alteração, a classe Pedido recebe uma lista de CarrinhoCompra que contem um preço e uma quantidade, e no construtor você instancia uma classe CarrinhoItens com new, ou seja, você cria um nível de acoplamento onde a classe Pedido conhece o detalhe de implementação da classe CarrinhoItems.

Agora vamos conversar um pouco sobre como Rigidez atrapalha o dia a dia do desenvolvimento.
Pensem em uma mudança pequena, onde CarrinhoItens passa a ser uma classe Abstrata porque no nível de negócio você pode ter 2 ou mais tipos de calculo de valor total do carrinho.
Como por exemplo, um carrinho de um produto promocional e um carrinho com preço padrão.

Em ambas implementações, você precisaria tornar a classe CarrinhoItens abstrata e criar uma implementação padrão e outra com desconto.
Uma vez feito isso, nada precisaria mudar no código de Pedido, ele continuaria recebendo CarrinhoItens, mas sem se importar se a implementação é padrão ou com desconto.

Já na segunda implementação, não seria possível manter o código sem reescrever ele para outra solução. Uma vez que você tem um código que esta em produção, qualquer alteração que impacte vai eventualmente gerar bugs, retrabalho, vai aumentar o custo de produção, vai impactar o processo Ágil da equipe, caso utilizem métricas de qualidade.

## Como evitar Rigidez no código?

PrincÍpios S.O.L.I.D., veremos detalhadamente mais para frente, mas são eles:

S: Single Responsibility Principle
O: Open/Closed Principle
L: Liskov Substitution Principle
I: Interface Segregation Principle
D: Dependency Inversion Principle

Refatoração:

Todo código legado tende a precisar de refatoração, a melhor forma de fazer isso é de forma planejada, existem muitas formas de refatorar código dependendo do objetivo a ser alcançado, como melhoria de código ou substituição.
Então se identificou alguns destes elementos citados para rigidez em algum código que você tenha construído ou mantido, verifique junto ao time o porque esta assim, como refatorar, etc.

Testes automatizados:

Você não deve, pode mas não deve, desenvolver sem testes, pensando em refatoração eles são mais necessários ainda.