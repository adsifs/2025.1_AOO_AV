@startuml
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Context.puml

LAYOUT_WITH_LEGEND()

Person(cliente, "Cliente", "Pessoa que compra produtos")
Person(vendedor, "Vendedor", "Pessoa que vende produtos")
Person(admin, "Administrador", "Pessoa que gerencia o sistema")

System_Ext(gateway_pagamento, "Gateway de Pagamento", "Sistema externo para processar transações financeiras.")
System_Ext(sistema_entrega, "Sistema de Entrega", "Serviço de logística externo para envio de produtos.")
System_Ext(servico_email, "Serviço de E-mail", "Serviço externo para envio de notificações por e-mail.")

System_Boundary(c1, "Nexus Marketplace") {
    System(app_web, "Aplicativo Web/Mobile", "Frontend para clientes, vendedores e administradores.")
    System(api_gateway, "API Gateway", "Ponto de entrada único para os microsserviços.")
    
    Boundary(b1, "Microsserviços") {
        System(microsservico_usuarios, "Microsserviço de Usuários", "Gerencia perfis, autenticação e autorização.")
        System(microsservico_produtos, "Microsserviço de Produtos", "Gerencia produtos, categorias e avaliações.")
        System(microsservico_pedidos, "Microsserviço de Pedidos", "Gerencia pedidos, itens e status.")
        System(microsservico_pagamentos, "Microsserviço de Pagamentos", "Gerencia transações e comunicação com o gateway.")
        System(microsservico_moderacao, "Microsserviço de Moderação", "Gerencia a moderação de conteúdo e disputas.")
        System(microsservico_notificacoes, "Microsserviço de Notificações", "Gerencia o envio de e-mails, SMS e notificações.")
    }
}

Rel(cliente, app_web, "Usa o")
Rel(vendedor, app_web, "Usa o")
Rel(admin, app_web, "Usa o")

Rel(app_web, api_gateway, "Acessa a API")
Rel(api_gateway, microsservico_usuarios, "Roteia requisições")
Rel(api_gateway, microsservico_produtos, "Roteia requisições")
Rel(api_gateway, microsservico_pedidos, "Roteia requisições")
Rel(api_gateway, microsservico_moderacao, "Roteia requisições")

Rel(microsservico_pedidos, gateway_pagamento, "Processa pagamentos")
Rel(microsservico_pedidos, sistema_entrega, "Informa dados de entrega")
Rel(microsservico_pedidos, microsservico_notificacoes, "Solicita notificação", "Evento de Pedido Criado")
Rel(microsservico_pagamentos, gateway_pagamento, "Gerencia transação")
Rel(microsservico_pagamentos, microsservico_notificacoes, "Solicita notificação", "Evento de Pagamento Aprovado")
Rel(microsservico_moderacao, microsservico_notificacoes, "Solicita notificação", "Evento de Produto Aprovado")
Rel(microsservico_notificacoes, servico_email, "Envia e-mails")
@enduml