@startuml
autonumber
actor Administrador
participant PainelAdmin as "Painel do Administrador"
participant RelatorioService as "Microsserviço de Relatórios"
participant NotificacaoService as "Microsserviço de Notificações"

Administrador -> PainelAdmin: Solicitar Relatório de Vendas
PainelAdmin -> RelatorioService: gerarRelatorioVendas(dadosFiltros)
RelatorioService -> RelatorioService: processarDadosVendas(filtros)
RelatorioService --> PainelAdmin: relatorioVendas(gerado)
PainelAdmin --> Administrador: exibir relatório de vendas
RelatorioService -> NotificacaoService: enviarNotificacao('relatorio_disponivel')
NotificacaoService --> Administrador: notificar disponibilidade de relatório
@enduml