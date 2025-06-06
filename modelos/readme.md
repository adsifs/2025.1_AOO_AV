# 📊 Diagramas UML do Sistema

## Visão Geral do Sistema

> Diagrama de caso de uso

```puml
@startuml
left to right direction
skinparam packageStyle rectangle
skinparam usecase {
  BackgroundColor LightSkyBlue
  BorderColor DarkSlateGray
}

actor Usuario
actor Motorista
actor Proprietario
actor Robo

rectangle "Sistema REVISAÍ" {

 rectangle "Sistema de autenticação" {
    usecase "login" as UC1
}
  
    usecase "Cadastrar Usuário" as UC2
    usecase "Registrar Documentação" as UC3
    usecase "Cadastrar Veículos" as UC4
    usecase "Compartilhar Veículos" as UC5
    usecase "Registrar Manutenções" as UC6
    usecase "Emitir Históricos e Relatórios" as UC7
    usecase "Atualizar Quilometragem" as UC8
    usecase "Registrar Despesas Gerais" as UC9
    usecase "Fazer Checklist de Viagem" as UC10
  
  usecase "Alertar" as UC11
}

Usuario --> UC1
Usuario --> UC2
Usuario --> UC4
Usuario --> UC6
Usuario --> UC7
Usuario --> UC8
Usuario --> UC9
Usuario --> UC10
Proprietario --> UC5

Motorista --|> Usuario
Proprietario --|> Usuario
Robo --> UC11

UC2 ..> UC3 : <<include>>
UC4 ..> UC3 : <<include>>

@enduml
```

## Casos de Uso

| Nome                               | Descrição breve             | Observações |
| ---------------------------------- | --------------------------- | ----------- |
| [Realizar Login](./UC_login.md) | Permite o acesso ao sistema | -           |
| [Cadastrar Usuário](./UC_Cadastro_Usuário.md) | Permite o cadastro de usuário | -           |
| [Cadastrar Veiculo](./UC_Cadastro_Veículo.md) | Permite o cadastro de veiculo | -           |
| Registrar Documentação | Registra a documentação dos cadastros | É necessario para a conclusão dos cadastros |
| [Compartilhar Veículos](./UC_Compartilhar_Veículo.md) | Permite o compartilhamento de veiculo | -           |
| [Registrar Manutenções](./UC_Manutenção.md) | Permite o registro de manutenção do veiculo | -           |
| [Emitir Históricos e Relatórios](./UC_Emitir_Relatório.md) | Permite a emição de relatórios e o histórico do veiculo | -           |
| [Atualizar Quilometragem](./UC_Quilometragem.md) | Permite a atualização manual da quilometragem do veiculo | -           |
| [Registrar Despesas Gerais](./UC_Registro_Despesas.md) | Permite o registro e emição das despesas do veiculo | -           |
| [Fazer Checklist de Viagem](./UC_Checklist.md) | Permite a criação de uma checklist com base na distância da viagem | -           |


## 🔹 Diagrama de Classes

| Nome                                     | Descrição breve                                               | Observações |
|------------------------------------------|----------------------------------------------------------------|-------------|
| [Usuario](./CL_Usuario.md)               | Representa o usuário da aplicação, com permissões e métodos de conta. | -           |
| [Veiculo](./CL_Veiculo.md)              | Representa um veículo cadastrado pelo usuário.                 | -           |
| [Manutencao](./CL_Manutencao.md)        | Armazena informações de serviços realizados no veículo.       | -           |
| [Alerta](./CL_Alerta.md)                | Permite a criação de alertas de manutenção por tempo ou quilometragem. | -           |
| [Despesa](./CL_Despesa.md)              | Registra despesas gerais associadas ao veículo.               | -           |
| [Historico](./CL_Historico.md)          | Mantém um log de ações realizadas sobre o veículo.            | -           |
| [Compartilhamento](./CL_Compartilhamento.md) | Gerencia o compartilhamento de veículos com outros usuários.   | -           |
| [ChecklistViagem](./CL_Checklist.md) | Permite criar listas personalizadas para preparo de viagens.   | -           |



# 🔹 Diagrama de Estados

## Diagrama de Estado — Usuário

Estados:

Cadastrado: Usuário concluiu o processo de cadastro, mas ainda não está ativo.

Ativo: Usuário autenticado e utilizando o sistema normalmente.

Inativo: Conta desativada temporariamente.

Bloqueado: Conta impedida de acesso por razões administrativas.

Removido: Conta encerrada permanentemente.

```plantuml
@startuml
[*] --> Cadastrado

Cadastrado --> Ativo : Verificação concluída com sucesso
Ativo --> Inativo : Usuário desativa a conta
Inativo --> Ativo : Reativação da conta
Ativo --> Bloqueado : Violação de termos / Denúncias
Bloqueado --> Ativo : Recurso aceito ou reabilitação manual
Cadastrado --> Bloqueado : Detecção de fraude ou erro grave no cadastro
Bloqueado --> Removido : Conta encerrada definitivamente
Inativo --> Removido : Exclusão definitiva a pedido do usuário
Cadastrado --> Removido : Cadastro incompleto não confirmado após X dias

@enduml
```

## Diagrama de Estado — Histórico de Manutenção 

Estados:

Criado: Registro inicial criado automaticamente ou por usuário.

AguardandoConfirmacao: Pendência de validação.

Confirmado: Registro validado.

Editado: Sofreu alguma edição.

Arquivado: Não mais ativo, mas mantido como histórico.

Removido: Apagado do sistema.

```plantuml
@startuml
[*] --> Criado

Criado --> AguardandoConfirmacao : Dados aguardando validação do usuário ou sistema
AguardandoConfirmacao --> Confirmado : Validação concluída com sucesso
Confirmado --> Editado : Modificação feita manualmente
Editado --> Confirmado : Nova validação concluída
Confirmado --> Arquivado : Veículo vendido ou item não mais relevante
Criado --> Removido : Remoção antes da confirmação
AguardandoConfirmacao --> Removido : Dados inválidos ou inconsistentes

@enduml

```
