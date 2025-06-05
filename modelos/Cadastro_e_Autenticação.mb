# 📃 Requisitos do Sistema

## 🧑‍💼 Regras de Negócio (RN)

1. O sistema deve aceitar placas nos formatos ABC-1234 e AAA1A11, com máscara e validação automática, prevenindo duplicidade.  
2. Deve oferecer controle de manutenção para evitar prejuízos e prolongar a vida útil dos veículos.  
3. Haverá uma versão gratuita com funções básicas e uma versão premium com recursos adicionais.  
4. Possibilidade de parcerias com oficinas, seguradoras e autopeças.  
5. Indicadores de desempenho (KPIs), como:  
   - Número de usuários ativos  
   - Taxa de engajamento com alertas  
   - Manutenções preventivas registradas por mês  
   - Retenção de usuários após 30 dias  
6. O sistema deve receber atualizações trimestrais e oferecer suporte via e-mail ou formulário.  
7. Disponibilização de plano corporativo para gestão de frotas de pequenas e médias empresas.  
8. Sistema de recompensas baseado em uso contínuo e boas práticas de manutenção.  
9. Loja de serviços integrada (futuramente), com catálogo, agendamento e promoções.  
10. Sistema de avaliação e aprovação de escritórios de manutenção.  
11. Disponibilização de API pública para integração com serviços terceiros.

---

## ✅ Requisitos Funcionais (RF)

### 1. Cadastro e Autenticação
- Cadastro com nome completo, e-mail e senha.  
- Login via conta Google.  
- Recuperação de senha por e-mail.  
- Senhas armazenadas com hash seguro.  
- Edição e exclusão de conta.  

### 2. Cadastro de Veículos
- Cadastro de múltiplos veículos por usuário.  
- Campos obrigatórios: marca, modelo, ano, combustível, quilometragem atual, placa.  
- Validação de placa (formatos Mercosul e antigo).  
- Prevenção de placas duplicadas.  
- Indicação de proprietário e motoristas autorizados.  
- Edição e exclusão com controle de permissões.  

### 3. Compartilhamento de Veículos
- Compartilhamento via e-mail ou código de convite.  
- Controle de permissões (visualização ou edição).  
- Remoção de acesso a qualquer momento.  
- Notificações de alterações feitas por convidados.  
- Transferência de propriedade do veículo.  

### 4. Registro de Manutenções
- Registro de tipo de serviço, data, quilometragem, oficina, valor e observações.  
- Upload de nota fiscal com leitura automática (OCR).  
- Edição e exclusão com rastreamento do autor.  

### 5. Alertas Inteligentes
- Geração de alertas por tempo e quilometragem.  
- Notificações para todos os motoristas vinculados.  
- Sugestões automáticas com base no histórico de manutenções.  
- Cálculo dinâmico de alertas.  

### 6. Histórico e Relatórios
- Histórico completo por veículo.  
- Filtros por motorista, serviço, oficina e datas.  
- Relatórios promocionais e exportação em PDF.  
- Geração de relatório de entrega de veículo.  

### 7. Atualização de Quilometragem
- Atualização manual da quilometragem.  
- Histórico das atualizações por usuário.  

### 8. Módulo de Despesas Gerais
- Registro de despesas como IPVA, seguro, multas, lavagens, etc.  
- Categorização das despesas.  
- Relatórios por mês, categoria e veículo.  

### 9. Checklist de Viagem
- Lista sugerida com base no tipo de viagem e revisões.  
- Exportação em PDF.  

---

## :ballot_box_with_check: Requisitos Não Funcionais (RNF)

### 1. Segurança e Permissões
- Controle de permissões por usuário.  
- Criptografia de dados.  
- Autenticação via JWT.  
- Confirmações para ações críticas.  

### 2. Compatibilidade e Acessibilidade
- Compatível com Android 8.0 ou superior.  
- Suporte a modo escuro.  
- Interface responsiva e acessível.  

### 3. Desempenho e Escalabilidade
- Tela inicial carregando em até 2 segundos.  
- Backend desacoplado e escalável (Node.js + PostgreSQL).  

### 4. Funcionalidade Offline
- Salvamento e notificações locais.  
- Sincronização segura quando online.  

### 5. Backup e Confiabilidade
- Backups diários com criptografia.  
- Sistema de logs e testes ajustáveis.  

### 6. Suporte Multilíngue e Integração
- Interface inicialmente em português com suporte a multilíngue.  
- Integração com calendário do celular.  
