@startuml
title Diagrama de Classes - Diagrama De Classes - Nexus Marketplace

package "Modelo de Usuários" {
    class Usuario {
        -id: int
        -nome: String
        -razaoSocial: String
        -tipoPessoa: TipoPessoa
        -documento: String
        -email: String
        -senhaHash: String
        -dataCadastro: Date
        -isVendedor: boolean
        +login(): boolean
        +logout(): void
        +habilitarVendedor(): void
        +validarDocumento(): boolean
    }

    enum TipoPessoa {
        FISICA
        JURIDICA
    }

    class Cliente {
        +verHistoricoPedidos(): Pedido[]
        +abrirDisputa(pedido: Pedido): Disputa
        +solicitarDevolucao(pedido: Pedido): Devolucao
        +avaliarProduto(produto: Produto, nota: int): Avaliacao
    }

    class Vendedor {
        -nomeLoja: String
        -reputacao: float
        -dataHabilitacao: Date
        +cadastrarProduto(produto: Produto): void
        +gerenciarEstoque(produto: Produto, qtde: int): void
        +responderDisputa(disputa: Disputa): void
        +gerenciarPedidos(): Pedido[]
    }

    class Administrador {
        -nivelAcesso: int
        +mediarDisputa(disputa: Disputa, decisao: String): void
        +aprovarVendedor(vendedor: Vendedor): void
        +processarDevolucao(devolucao: Devolucao): void
    }

    Usuario <|-- Cliente
    Usuario <|-- Vendedor
    Usuario <|-- Administrador
    Usuario --> TipoPessoa
}

package "Modelo de Produtos e Pedidos" {
    class Produto {
        -id: int
        -nome: String
        -descricao: String
        -preco: double
        -estoque: int
        +atualizarEstoque(quantidade: int): void
    }

    class Categoria {
        -id: int
        -nome: String
    }

    class Pedido {
        -id: int
        -data: Date
        -valorTotal: double
        -valorFrete: double
        -status: StatusPedido
        +calcularTotal(): double
    }

    class ItemDePedido {
        -id: int
        -quantidade: int
        -precoUnitario: double
        -PedidoId: int
        -ProdutoId: int
        +calcularSubtotal(): double
    }

    class Endereco {
        -id: int
        -logradouro: String
        -cidade: String
        -cep: String
    }

    enum StatusPedido {
        PENDENTE
        PAGO
        ENVIADO
        ENTREGUE
        CANCELADO
        EM_DISPUTA
        DEVOLVIDO
    }

    Vendedor "1" --> "0..*" Produto : vende >
    Produto "0..*" --> "1" Categoria : pertence >
    Cliente "1" --> "0..*" Pedido : faz >
    Pedido "1" --> "1..*" ItemDePedido : contém >
    ItemDePedido "1" --> "1" Produto : refere-se a >
    Pedido --> StatusPedido
    Cliente "1" --> "0..*" Endereco : possui >
    Pedido "1" --> "1" Endereco : enviado para >
}

package "Modelo de Pagamentos" {
    class Pagamento {
        -id: int
        -valor: double
        -status: StatusPagamento
        -metodo: MetodoPagamento
        +processarPagamento(): boolean
    }

    enum StatusPagamento {
        PENDENTE
        APROVADO
        RECUSADO
    }

    enum MetodoPagamento {
        CARTAO_CREDITO
        PIX
        BOLETO
    }

    Pedido "1" --> "1" Pagamento : processado via >
    Pagamento --> StatusPagamento
    Pagamento --> MetodoPagamento
}

package "Modelo de Disputas" {
    class Disputa {
        -id: int
        -motivo: String
        -dataAbertura: Date
        -status: StatusDisputa
        -pedidoId: int {FK}
        -clienteId: int {FK}
        +adicionarMensagem(msg: MensagemDisputa): void
        +resolverDisputa(decisao: String): void
    }

    class MensagemDisputa {
        -id: int
        -texto: String
        -data: Date
        -disputaId: int {FK}
        -autorId: int {FK}
    }

    enum StatusDisputa {
        ABERTA
        AGUARDANDO_MEDIACAO
        RESOLVIDA
        REJEITADA
    }

    Usuario ||--o{ Disputa : "clienteId (FK)"
    Pedido ||--o{ Disputa : "pedidoId (FK)"
    Disputa ||--|{ MensagemDisputa : "disputaId (FK)"
    Usuario ||--o{ MensagemDisputa : "autorId (FK)"
    Administrador ||--o{ Disputa : "processa"
    Disputa --> StatusDisputa
}

package "Modelo de Devoluções" {
    class Devolucao {
        -id: int
        -motivo: String
        -dataSolicitacao: Date
        -dataProcessamento: Date
        -valorReembolso: double
        -status: StatusDevolucao
        -observacoes: String
        -pedidoId: int {FK}
        -clienteId: int {FK}
        +adicionarMensagem(msg: String): void
        +atualizarStatus(status: StatusDevolucao): void
        +calcularReembolso(): double
        +processarReembolso(): boolean
    }

    class MensagemDevolucao {
        -id: int
        -texto: String
        -data: Date
        -devolucaoId: int {FK}
        -autorId: int {FK}
    }

    enum StatusDevolucao {
        PENDENTE
        EM_ANALISE
        APROVADO
        RECUSADO
        PROCESSANDO
        CONCLUIDO
        CANCELADO
    }

    Usuario ||--o{ Devolucao : "clienteId (FK)"
    Pedido ||--o{ Devolucao : "pedidoId (FK)"
    Devolucao ||--|{ MensagemDevolucao : "devolucaoId (FK)"
    Usuario ||--o{ MensagemDevolucao : "autorId (FK)"
    Administrador ||--o{ Devolucao : "processa"
    Devolucao --> StatusDevolucao
}

package "Modelo de Avaliações" {
    class Avaliacao {
        -id: int
        -nota: int
        -comentario: String
        -data: Date
        -clienteId: int {FK}
        -produtoId: int {FK}
        +validarNota(): boolean
    }

    Usuario ||--o{ Avaliacao : "clienteId (FK)"
    Produto ||--o{ Avaliacao : "produtoId (FK)"
}

note right of Usuario : Modelo unificado com TipoPessoa\ne campo documento único.\nPermite habilitar vendedor\na partir de cliente existente

note right of Produto : Adicionadas chaves estrangeiras\ncategoriaId e vendedorId\npara relacionamentos corretos

note bottom of ItemDePedido : Nova classe com FKs para\nPedido e Produto, resolvendo\no relacionamento many-to-many

note left of StatusDevolucao : Novo enum com status\nespecíficos para o processo\nde devolução

note bottom of Administrador : Administrador agora pode\nprocessar devoluções além\nde mediar disputas

@enduml