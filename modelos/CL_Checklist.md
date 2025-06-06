#Checklist de Viagem
- 

```puml
@startuml
!theme mars

class ChecklistViagem {
    -id: UUID
    -tipoViagem: String
    -dataGeracao: Date
    -itens: List<String>
    -status: Enum (PENDENTE, CONCLUIDO)
    -veiculoId: UUID
    -autorId: UUID
    +gerarSugestao()
    +personalizar()
    +exportarPDF()
    +marcarItemVerificado()
    +registrarConclusao()
}

@enduml
```
