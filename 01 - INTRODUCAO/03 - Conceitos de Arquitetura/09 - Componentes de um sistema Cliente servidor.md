# Componentes de um sistema Cliente servidor

## Cliente:

O  cliente é responsável pela apresentação do negocio para o cliente / usuário, ela é composta por 3 elementos fundamentais:

- Interface do Usuário: Responsável por fornecer uma interface gráfica ou de linha de comando para interação com o usuário.

- Lógica de Apresentação: Responsável por processar a entrada do usuário e exibir informações relevantes na interface.

- Gerenciador de Estado: Responsável por manter o estado da aplicação no lado do cliente, como dados do usuário, preferências e histórico de navegação.


## Servidor

Servidor é o que chamamos de backend, ou seja, tudo que esta do lado da infra estrutura do fornecedor do serviço, ele pode ser composto por vários elementos:

- Serviços ou APIs: Conjunto de interfaces de programação de aplicativos (APIs) que definem os serviços disponíveis para os clientes. Isso inclui operações como autenticação, autorização, processamento de dados e acesso a recursos.

- Lógica de Negócios: Responsável por implementar a lógica de negócios da aplicação, incluindo regras de negócios, processamento de dados e manipulação de eventos.

- Acesso a Dados: Responsável por acessar e manipular os dados armazenados pelo sistema. Isso pode envolver consultas a um banco de dados, integração com sistemas externos ou acesso a serviços de armazenamento em nuvem.

- Gerenciador de Estado: Responsável por manter o estado da aplicação no lado do servidor, como sessões de usuários, caches de dados e estado da aplicação.

## Comunicação

Quando falamos de comunicação, estamos falando normalmente de 2 elementos:

- Protocolo de Comunicação: Define as regras e formatos de comunicação entre o cliente e o servidor. Exemplos incluem HTTP, TCP/IP, WebSocket.

- Bibliotecas ou Frameworks de Comunicação: Conjuntos de ferramentas ou bibliotecas que simplificam a implementação da comunicação entre o cliente e o servidor, facilitando a troca de dados e mensagens.

## Segurança

Quando falamos de segurança, estamos querendo atender a pelo menos 3 necessidades:

- Autenticação: Processo de verificação da identidade do usuário ou cliente que acessa o sistema.

- Autorização: Processo de determinar quais recursos ou funcionalidades um usuário autenticado tem permissão para acessar.

- Criptografia: Técnica de proteção dos dados durante a transmissão entre o cliente e o servidor, garantindo sua confidencialidade e integridade.


## Tratamento de exceções e  logs.

Quando tratamos os erros da aplicação temos pelo menos 2 tipos de erros e 2 tipos de preocupações:
Erros tratados e erros não tratados, isso significa que temos os erros de negocio e os erros de infra estrutura.

Preocupações:

- Devolução para o cliente: Quando temos um erro precisamos apresentar para o cliente o erro gerado pela aplicação, por questões de segurança não podemos vazar dados de infra estrutura. Mas precisamo informar que o erro ocorreu,

- Logging: Registro de eventos e atividades relevantes do sistema para análise, monitoramento e auditoria.

Cada um desses componentes desempenha um papel fundamental na construção e operação de um sistema cliente/servidor eficiente e robusto. 

