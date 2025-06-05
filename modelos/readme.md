# 📊 Diagramas UML do Sistema

## Visão Geral do Sistema

> Adicionar o diagrama de caso de uso que mostra a visão geral do sistema

```puml
@startuml
left to right direction
skinparam packageStyle rectangle
skinparam usecase {
  BackgroundColor LightSkyBlue
  BorderColor DarkSlateGray
}

actor Usuario
actor Proprietario
actor Motorista
actor Robo

rectangle "Sistema REVISAÍ" {
  
    usecase "Cadastrar Usuário" as UC1
    usecase "Registrar Documentação" as UC2
    usecase "Cadastrar Veículos" as UC3
    usecase "Compartilhar Veículos" as UC4
    usecase "Registrar Manutenções" as UC5
    usecase "Emitir Históricos e Relatórios" as UC6
    usecase "Atualizar Quilometragem" as UC7
    usecase "Registrar Despesas Gerais" as UC8
    usecase "Fazer Checklist de Viagem" as UC9
  
  usecase "Alertar" as UC10
}

Usuario --> UC1
Usuario --> UC3
Usuario --> UC5
Usuario --> UC6
Usuario --> UC7
Usuario --> UC8
Usuario --> UC9
Proprietario --> UC4

Motorista --|> Usuario
Proprietario --|> Usuario
Robo --> UC10

UC1 ..> UC2 : <<include>>
UC3 ..> UC2 : <<include>>

@enduml


```

## Casos de Uso

>  Para cada item, apresentar: Nome, Atores, Fluxo principal, Fluxo alternativo, Pré-condições e Pós-condições, etc. 


| Nome                               | Descrição breve             | Observações |
| ---------------------------------- | --------------------------- | ----------- |
| [Realizar Login](./UC_01_login.md) | Permite o acesso ao sistema | -           |
| [Cadastrar Usuário](./DA_Cadastro_Usuário.md) | Permite o cadastro de usuário | -           |
| A2                                 | B2                          | C2          |
| A3                                 | B3                          | C3          |

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

