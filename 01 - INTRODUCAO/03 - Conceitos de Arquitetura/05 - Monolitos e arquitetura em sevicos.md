# Monólitos e arquiteturas em serviços

Vamos iniciar por exemplos de arquiteturas monolíticas.

**Wordpress**: O WordPress é um sistema de gerenciamento de conteúdo (CMS) popular que é construído em uma arquitetura monolítica. Ele apresenta uma única base de código que inclui todas as funcionalidades, como gerenciamento de conteúdo, temas e plugins. Essa abordagem é adequada para aplicativos que não exigem escalabilidade extrema e podem se beneficiar da simplicidade e facilidade de manutenção de uma arquitetura monolítica.

**Magento**: Uma plataforma de comércio eletrônico como o Magento também é um exemplo de uma aplicação monolítica. Ele oferece uma ampla gama de recursos, incluindo gerenciamento de catálogo, processamento de pedidos, carrinho de compras, entre outros, tudo dentro de uma única aplicação. Isso facilita o desenvolvimento e a integração, mas pode apresentar desafios de escalabilidade em casos de grandes volumes de tráfego.

E por último, mas não menos importante nem desconhecido, Stackoverflow, dispensa apresentações, porém vamos falar dele um pouco. Ele roda muitos sites em um único IIS, utiliza apenas um banco de dados por aplicação desenvolvido com foco em performance.

Embora olhando diretamente pareça não ter uma relação com produtos financeiros, com as constantes atualizações do que é marketing digital, cada vez mais qualquer empresa tem uma área de compras de produtos, precisa fazer gestão de conteúdo e isto está inserido dentro dos produtos vendidos.

E é claro, ter a velocidade de resposta do stackoverflow sem perder o foco na segurança.

# Arquitetura em microsserviços

**Netflix**: Um dos exemplos mais citados de arquitetura em serviços é o da Netflix. A Netflix é construída em uma arquitetura de microservices que permite escalabilidade, flexibilidade e tolerância a falhas. Cada funcionalidade, como recomendações, reprodução de vídeo e gerenciamento de usuários, é implementada como um serviço independente, permitindo atualizações e implantações contínuas sem afetar o sistema como um todo.

**Uber**: A Uber é outro exemplo de uma aplicação que utiliza arquitetura de microservices para lidar com a complexidade de suas operações. Diferentes aspectos do aplicativo, como gerenciamento de corridas, pagamentos, geolocalização e notificações, são tratados por serviços independentes, permitindo escalabilidade e desenvolvimento ágil.

Netflix tem um grande poder de gestão de recomendações, esta inteligência aplicada a recomendações de produtos financeiros seria possível com análise de bigdata, dados não integrados em uma base única, a tolerância a falhas que microsserviços proporciona e etc.

Já no exemplo do uber, em um nível técnico temos um sistema orientado a integrações.

