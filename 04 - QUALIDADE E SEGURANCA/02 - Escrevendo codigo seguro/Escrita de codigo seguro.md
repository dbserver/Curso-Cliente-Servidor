# Escrevendo código seguro

## Introdução à Importância do Código Seguro

Por que escrever código seguro?

Código seguro protege dados sensíveis, previne vulnerabilidades e protege contra ataques, como injeção de código, acesso não autorizado e exploração de falhas.
Requisitos legais, regulamentações de conformidade e a confiança do cliente demandam que o código seja desenvolvido com segurança em mente.

Impacto de falhas de segurança:
- Perda de dados, comprometimento de sistemas, danos à reputação da empresa e, potencialmente, altos custos financeiros.

## Princípios Gerais de Código Seguro

### Princípio do Mínimo Privilégio:

- Atribua o nível mais baixo de permissões possível para executar tarefas. Um módulo ou método deve apenas ter acesso aos recursos e dados estritamente necessários para sua operação.

### Princípio da Defensividade:

- Sempre escreva código que espera o pior cenário: entradas malformadas, tentativas de invasão, exceções inesperadas. Trate erros de forma robusta.

### Manter a simplicidade:

- Código complexo é mais difícil de auditar e tem maior probabilidade de esconder vulnerabilidades. Prefira simplicidade e clareza.

### Boas Práticas na Escrita de Métodos e Módulos

#### Validação de Entradas (Toda entrada é, por definição, mal intencionada):

- Sanitização: Nunca confie em entradas externas. Utilize métodos que garantam que os dados inseridos sejam seguros.
- Tipos de dados fortes: Use tipos de dados adequados para validar o formato das entradas (ex: usar int ou Guid para IDs, DateTime para datas).
- White-listing: Em vez de tentar bloquear valores inválidos (badlisting), prefira aceitar apenas o que é explicitamente permitido (whitelisting).

#### Tratamento de Exceções:

- Sempre trate exceções adequadamente. Evite expor detalhes internos do sistema em mensagens de erro.

#### Log seguro: 
- Registre erros de forma que possam ser rastreados, mas evite registrar dados sensíveis (senhas, números de cartão de crédito, etc.).

#### Uso de Dependências Externas:

- Tenha cuidado com bibliotecas de terceiros. Verifique se não possuem vulnerabilidades conhecidas e mantenha-as atualizadas.
Verifique a integridade do código de bibliotecas externas (use assinaturas digitais ou gerenciadores de pacotes que garantam segurança).

#### Controle de Acesso e Gerenciamento de Permissões (ACL)

Autenticação e Autorização:

- Autenticação: Certifique-se de que o usuário ou sistema é quem diz ser (use autenticação forte, como autenticação multifator).
- Autorização: Uma vez autenticado, verifique se o usuário tem permissão para executar a ação solicitada.

Boas práticas com ACL:

- Roles e Grupos: Defina permissões de acesso com base em papéis, e não diretamente para cada usuário. Isso facilita a administração e a auditoria.
- Verificação frequente de permissões: Verifique permissões durante todas as operações críticas, não apenas no login.

#### Least Privilege Application:

Atribua permissões mínimas necessárias para execução de tarefas específicas, reduzindo a superfície de ataque no sistema.

#### Segurança na Comunicação e Criptografia

Protocolo Seguro (HTTPS):

Utilize HTTPS para garantir que os dados transmitidos entre cliente e servidor estejam criptografados.

Hashing e Salting de Senhas:

Não armazene senhas em texto plano. Use algoritmos seguros de hashing, como bcrypt ou PBKDF2, com um salt forte.

Segurança em APIs:

Para APIs públicas, use tokens de autenticação (como JWT) e proteja endpoints sensíveis com verificação de permissões adequada.

### Exemplo de Código Seguro 

Antes: Um exemplo de código inseguro, que não faz validação de entradas ou trata exceções corretamente:

```csharp
public void ProcessarDados(string userInput)
{
    // Entradas não validadas
    string query = $"SELECT * FROM Usuarios WHERE Nome = '{userInput}'";
    var resultado = ExecutarQuery(query);
}
```

Depois: Código corrigido com validação de entrada e tratamento de exceções:

```csharp

public void ProcessarDados(string userInput)
{
    if (string.IsNullOrWhiteSpace(userInput))
    {
        throw new ArgumentException("Nome de usuário inválido");
    }

    // Parâmetro com segurança contra SQL Injection
    string query = "SELECT * FROM Usuarios WHERE Nome = @Nome";
    var resultado = ExecutarQueryComParametro(query, new { Nome = userInput });
}
```

7. Conclusão e Perguntas
Resumo:

Código seguro começa com práticas simples como validação de entrada, tratamento de exceções e controle de acesso.
Seguir princípios de segurança ao projetar e escrever código aumenta a resiliência do software contra ataques.
