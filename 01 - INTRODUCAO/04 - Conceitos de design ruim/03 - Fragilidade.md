# Fragilidade

## Conceito de Fragilidade

Definição: Código frágil é aquele que, ao fazer pequenas modificações ou adicionar funcionalidades, tende a quebrar em partes não relacionadas ou inesperadas do sistema.

Imagine um sistema onde, ao adicionar uma nova funcionalidade, outras áreas que não foram diretamente alteradas começam a apresentar erros. Isso é um sinal de que o código é frágil.

Da mesma forma que a rigidez exige muita alteração de código, fragilidade também, mas neste caso não estamos falando que um código quebra, mas sim que uma implementação de negocio quebra. Ou seja, a quebra não ocorre em módulos de código relacionados, mas sim conceitualmente divergentes.

Pense em uma classe que imprime os valores da movimentação de um extrato bancário.
A responsabilidade dela é pegar o valor em decimal e converter para texto adicionando R$ na frente.
Simples, recebe 10.1010 e devolve R$10,10 arredondados, correto?

Esta classe e método são chamados na impressão do extrato para o usuário, na impressão do extrato para o gerente e na impressão do extrato para validação na área contábil.

O problema é que a área contábil precisa de uma precisão de 4 casas, e o requisito chega na mesa de um desenvolvedor.
O que ele faz, altera o código para devolver 4 casas decimais.

Neste momento, todo o código funciona, mas os valores para extrato tanto do cliente quando do gerente estão erradas em nível de negócio.
Então vejam só, o código não esta quebrando, mas uma alteração gerou impacto em outra funcionalidade de outro usuário.


## Principais Sintomas de Código Frágil
Sintomas mais comuns de fragilidade no código:

Impacto colateral em mudanças: Toda vez que uma parte do sistema é alterada, outras partes inesperadamente falham.
Dificuldade em isolar e corrigir bugs: Corrigir um bug pode introduzir novos problemas em áreas aparentemente não relacionadas.
Testes quebram com frequência: Mudanças mínimas requerem reescrever ou ajustar muitos testes, indicando que o design não é robusto.
Exemplos de como um sistema onde o código não está modularizado e pequenas alterações exigem grandes refatorações.

## Causas de Fragilidade no Código
Causas mais comuns de fragilidade:

Acoplamento forte: Componentes dependem fortemente uns dos outros, então uma mudança em um lugar afeta muitos outros.
Baixa coesão: Classes e métodos fazem muitas coisas diferentes, violando o princípio da responsabilidade única (SRP).
Falta de testes automatizados: Isso dificulta a detecção rápida de erros e leva a introduzir mais fragilidade com o tempo.
Design que não segue princípios SOLID: Ao ignorar boas práticas de design de software, o código se torna difícil de adaptar a novas exigências sem quebrar o que já funciona.

## Como Evitar Código Frágil
Práticas para evitar fragilidade:

Seguir princípios SOLID: Garantir que o código seja modular, com responsabilidade bem definida.
Investir em testes automatizados: Para detectar rapidamente qualquer impacto colateral causado por alterações.
Refatoração constante: Identificar e corrigir fragilidades à medida que o código evolui.
Encapsulamento adequado: Minimizar dependências diretas entre classes, utilizando interfaces e abstrações.