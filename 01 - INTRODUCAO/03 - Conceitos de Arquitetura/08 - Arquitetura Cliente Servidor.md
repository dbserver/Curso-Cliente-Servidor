# Arquitetura Cliente Servidor

A arquitetura cliente-servidor é essencial na construção de sistemas de software distribuídos. Nesse modelo, as responsabilidades são divididas entre dois tipos de entidades: o cliente, que solicita serviços ou recursos, e o servidor, que fornece esses serviços em resposta às solicitações dos clientes. Essa abordagem permite uma melhor organização e distribuição das funcionalidades do sistema, promovendo modularidade, escalabilidade e eficiência na comunicação entre as partes envolvidas. Em um sistema cliente-servidor, o cliente interage com a interface do usuário e envia solicitações ao servidor, que processa essas solicitações e fornece os resultados de volta ao cliente. Essa divisão de responsabilidades facilita a manutenção, escalabilidade e evolução dos sistemas de software distribuídos, tornando a arquitetura cliente-servidor uma boa escolha para muitas aplicações atuais.

## Papeis na arquitetura Cliente / Servidor

Cliente é uma entidade que solicita serviços ou recursos do servidor. Ele geralmente é responsável por interagir diretamente com o usuário final, fornecendo uma interface para acessar os recursos disponíveis no sistema ou pensando em integrações entre sistemas o cliente pode ser um consumidor de serviço que recebe um contrato de informações.

Servidor: Servidor é a entidade que fornece serviços ou recursos em resposta às solicitações do cliente. Ele geralmente é responsável por processar as solicitações dos clientes, realizar operações de negócios, executar as persistências e mudanças de estado e fornecer os resultados de volta aos clientes.

## Comunicação

A comunicação entre o cliente e o servidor geralmente ocorre por meio de protocolos de comunicação, como HTTP, TCP/IP ou WebSocket.

1. TCP/IP

- O que é: O TCP/IP é um conjunto de protocolos usados para comunicação na internet. Ele define como os dados são transmitidos de um dispositivo para outro em uma rede. A camada TCP (Transmission Control Protocol) garante a entrega confiável de dados, enquanto a camada IP (Internet Protocol) cuida do roteamento dos pacotes de dados.

Características:

- Confiável: TCP garante que os pacotes de dados cheguem completos e na ordem correta.
- Conexão orientada: Uma conexão é estabelecida entre o cliente e o servidor antes da troca de dados.
- Uso comum: Qualquer comunicação de rede, incluindo navegação na web, email e transferência de arquivos.
- Quando usar: Quando você precisa de uma comunicação confiável e com entrega garantida de dados.

2. HTTP (Hypertext Transfer Protocol)

- O que é: HTTP é um protocolo de aplicação baseado em TCP/IP usado para comunicação entre clientes (navegadores) e servidores. Ele é o protocolo mais utilizado na web.

Características:

- Orientado a requisição/resposta: Cada interação no HTTP começa com uma requisição (do cliente) e termina com uma resposta (do servidor). Exemplo: carregar uma página web.
- Stateless (sem estado): Cada requisição é independente. Não guarda informações sobre requisições anteriores (a menos que se use cookies ou sessões).
- Confiável: Por ser baseado em TCP, a entrega dos dados é garantida.
- Uso comum: Principalmente para a web, ao acessar e enviar informações de sites e APIs RESTful.
- Quando usar: Quando você precisa de uma comunicação simples e baseada em requisições, como na navegação em sites ou chamadas a APIs.

3. WebSocket

- O que é: WebSocket é um protocolo que permite comunicação bidirecional entre cliente e servidor em tempo real. Diferente do HTTP, após a conexão inicial, ele permanece aberto, permitindo a troca contínua de mensagens.

Características:

- Bidirecional: Tanto o cliente quanto o servidor podem enviar e receber mensagens sem que um precise esperar pelo outro.
- Baixa latência: Por ser uma conexão contínua, há menos sobrecarga na troca de dados, tornando-o ideal para aplicações em tempo real.
- Mantém o estado da conexão: A conexão persiste, ao contrário do HTTP.
- Uso comum: Ideal para aplicações que requerem atualizações constantes e em tempo real, como chats, sistemas de notificação e jogos online.
- Quando usar: Quando você precisa de comunicação em tempo real, como em chats ou dashboards de mercado financeiro.


