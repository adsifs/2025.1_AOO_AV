#### 🛠 Manutenção de Veículo
Reflete o ciclo de vida de uma manutenção veicular, desde o agendamento até sua conclusão ou cancelamento.

Estados:

Pendente: Manutenção registrada, mas ainda não iniciada.

Em Andamento: Manutenção atualmente sendo realizada.

Concluída: Serviço finalizado com sucesso.

Cancelada: Manutenção cancelada antes ou durante a execução.

```plantuml
@startuml
title Diagrama de Estados - Manutenção

[*] --> Pendente : novaManutencao()

Pendente --> Em_Andamento : iniciarServico()
Pendente --> Cancelada : cancelarManutencao()

Em_Andamento --> Concluida : finalizarServico()
Em_Andamento --> Cancelada : cancelarManutencao()

Concluida --> [*]
Cancelada --> [*]
@enduml
```
