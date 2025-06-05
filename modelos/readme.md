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
| [Registrar Documentação]() | Registra a documentação dos cadastros | É necessario para a conclusão dos cadastros |
| [Cadastrar Veiculo](./UC_Cadastro_Veiculo.md) | Permite o cadastro de veiculo | -           |
| [Compartilhar Veículos](./UC_Compartilhar_Veiculo.md) | Permite o compartilhamento de veiculo | -           |
| [Registrar Manutenções](./UC_Manutenção.md) | Permite o registro de manutenção do veiculo | -           |
| [Emitir Históricos e Relatórios](./UC_Relatório.md) | Permite a emição de relatórios e o histórico do veiculo | -           |
| [Emitir Históricos e Relatórios](./UC_Relatório.md) | Permite a emição de relatórios e o histórico do veiculo | -           |


## 🔹 Diagrama de Classes

### Módulo de Usuário

```plantuml
@startuml
skinparam groupInheritance 2
abstract class Usuario {
  + id: Integer <<PK>>
  + nome: String
  + email: String
  + senhaHash: String
  + dataCadastro: DateTime
  + ultimoAcesso: DateTime
  --
  + autenticar(): Boolean
  + solicitarTrocaSenha(): void
}

class Administrador {
  + nivelAcesso: Integer
  + desbloquearUsuario(): void
  + excluirUsuario(): void
}

class UsuarioComum {
  + preferencias: String
}

class StatusLogin{
  + id: Integer <<PK>>
  + tipo: Status
  + dataAlteracao: DateTime
  + motivo: String
  --
  + atualizarStatus(novoStatus: Status): void
}

class TentativaLogin {
  + id: Integer <<PK>>
  + dataHora: DateTime
  + ip: String
  + sucesso: Boolean
}

Usuario "1" *-- "1" StatusLogin
Usuario "1" *-- "0..*" TentativaLogin

Administrador --|> Usuario
UsuarioComum --|> Usuario

enum Status {
  AGUARDANDO_CONFIRMACAO
  ATIVO
  BLOQUEADO
  CANCELADO
  EXCLUIDO
}

Usuario "1" --> "1..*" Status

@enduml
```


## 🔹 Diagrama de Estados

> Mostra os estados possíveis de cada entidade [ex: login] e as transições entre eles.

| Nome                            | Finalidade / Obs  |
| ------------------------------- | ----------------- |
| [Status Usuário](./DE_login.md) | Status do usuário |
| A2                              | B2                |
| A3                              | B3                |

