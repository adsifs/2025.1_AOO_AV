# 📃 Requisitos do Sistema

## 🧑‍💼 Regras de Negócio (RN)

## 1. Regras de Usuários

### 1.1. Tipos de Usuário

A plataforma terá três tipos de usuários principais:

- **Cliente (Comprador):** Pessoa física ou jurídica que busca e compra produtos.
- **Vendedor (Lojista):** Pessoa física ou jurídica que anuncia e vende produtos.
- **Administrador:** Equipe interna da Nexus responsável pela gestão da plataforma.

### 1.2. Cadastro de Cliente

- O cadastro é gratuito e obrigatório para realizar compras.
- Campos obrigatórios: Nome completo, CPF/CNPJ, e-mail válido, senha, endereço principal e telefone de contato.
- O e-mail será o login do usuário e deve ser único na plataforma.
- O cliente deve ter no mínimo 18 anos ou ser emancipado legalmente.
- O cliente pode cadastrar múltiplos endereços de entrega.

### 1.3. Cadastro de Vendedor

- O cadastro de Vendedor passa por um processo de aprovação pela equipe de Administradores.
- Campos obrigatórios adicionais: Razão Social (se PJ), CNPJ/CPF, endereço comercial, dados bancários para repasse e definição do nome da loja virtual dentro da Nexus.
- O Vendedor deve aceitar os "Termos de Serviço do Vendedor", que incluem políticas de comissão, repasse e qualidade.
- A Nexus se reserva o direito de suspender ou banir vendedores com base em avaliações negativas recorrentes, violação dos termos ou práticas fraudulentas.

---

## 2. Regras de Produtos e Catálogo

### 2.1. Anúncio de Produtos

- Apenas Vendedores podem cadastrar produtos.
- Campos obrigatórios para o anúncio: Título do produto, descrição detalhada, categoria, imagens de alta qualidade (mínimo de 3), preço, peso e dimensões (para cálculo de frete), e quantidade em estoque.
- É proibido anunciar produtos ilegais, falsificados, perigosos ou que infrinjam direitos autorais e propriedade intelectual, conforme a lista de "Produtos Proibidos".
- Todos os anúncios estarão sujeitos à moderação e podem ser removidos pelos Administradores.

### 3.2. Preços e Estoque

- O preço é definido exclusivamente pelo Vendedor.
- Promoções e descontos são de responsabilidade do Vendedor, mas a Nexus pode criar eventos promocionais em toda a plataforma (ex: "Semana Nexus").
- O estoque deve ser gerenciado pelo Vendedor. O sistema deve abater automaticamente a quantidade do estoque após uma compra ser confirmada.
- Um produto com estoque zerado deve ser exibido como "Indisponível", não permitindo a compra.

### 3.3. Avaliações (Reviews)

- Apenas Clientes que compraram e receberam o produto podem avaliá-lo.
- A avaliação consistirá em uma nota de 1 a 5 estrelas e um comentário opcional.
- O Cliente também avaliará a experiência de compra com o Vendedor (atendimento, prazo de postagem, etc.).
- Avaliações que contenham discurso de ódio, spam ou informações pessoais serão removidas. A nota, no entanto, será mantida se for uma crítica construtiva.

---

## 4. Regras de Pedidos e Vendas

### 4.1. Carrinho de Compras

- O Cliente pode adicionar produtos de diferentes Vendedores no mesmo carrinho.
- O frete será calculado separadamente para cada Vendedor, com base na origem do produto e no CEP de entrega do cliente.
- O sistema deve consolidar o pagamento, mas gerar pedidos separados para cada Vendedor.

### 4.2. Ciclo de Vida do Pedido

O pedido terá os seguintes status:

1.  **Pagamento Pendente:** Aguardando confirmação do pagamento.
2.  **Pagamento Aprovado:** O Vendedor é notificado para preparar o envio.
3.  **Em Preparação:** O Vendedor está embalando o produto.
4.  **Enviado:** O Vendedor postou o produto e inseriu o código de rastreio. O cliente recebe o código.
5.  **Entregue:** Confirmado pela transportadora ou pelo cliente.
6.  **Cancelado:** O pedido foi cancelado pelo cliente ou pelo sistema (falha no pagamento).
7.  **Devolvido:** O cliente solicitou a devolução do produto.

### 4.3. Envio e Frete

- O cálculo do frete é automático, baseado em tabelas de transportadoras parceiras (Correios, etc.) e nas dimensões/peso do produto.
- O custo do frete é pago pelo Cliente no momento da compra.
- O Vendedor tem um prazo de **48 horas úteis** após a confirmação do pagamento para postar o produto e informar o código de rastreio. O descumprimento deste prazo impactará negativamente sua reputação.

### 4.4. Política de Devolução e Cancelamento

- O Cliente pode cancelar a compra a qualquer momento antes do envio.
- O Cliente tem o direito de arrependimento, podendo devolver o produto em até **7 dias corridos** após o recebimento, conforme o Código de Defesa do Consumidor. O produto deve ser devolvido em sua embalagem original e sem sinais de uso.
- Em caso de defeito, o prazo para reclamação é de **30 dias** para produtos não duráveis e **90 dias** para produtos duráveis. A troca ou reparo é de responsabilidade do Vendedor.

---

## 5. Regras Financeiras

### 5.1. Pagamentos

- A Nexus processará todos os pagamentos através de um gateway de pagamento seguro.
- Meios de pagamento aceitos: Cartão de Crédito (com parcelamento), Pix e Boleto Bancário.
- A confirmação de pagamento via Pix e Cartão de Crédito deve ser quase instantânea. Boletos podem levar até 3 dias úteis.

### 5.2. Comissionamento e Repasse

- A Nexus cobrará uma comissão sobre o valor total de cada venda (produto + frete). A taxa de comissão padrão é de **12%**, podendo variar conforme a categoria do produto ou o plano do Vendedor.
- O valor da venda (descontada a comissão) será repassado para a conta bancária do Vendedor em um prazo de **14 dias** após a confirmação de entrega do produto ao cliente. Esse prazo serve como uma garantia para casos de devolução ou disputas.

### 5.3. Disputas

- Caso um cliente não receba o produto ou receba algo diferente do anunciado, ele pode abrir uma "disputa".
- A equipe de Administradores da Nexus mediará a disputa entre Cliente e Vendedor.
- Se a disputa for favorável ao cliente, o pagamento será estornado integralmente. Se for favorável ao vendedor, o valor será liberado para repasse.

## ✅ Requisitos Funcionais (RF)

## 1. Módulo de Gestão de Contas de Usuário

### 1.1. Cadastro

- **RF-001:** O sistema deve permitir que um novo usuário se cadastre utilizando nome completo, CPF/CNPJ, e-mail e senha.
- **RF-002:** O sistema deve validar se o e-mail e o CPF/CNPJ informados já existem na base de dados para garantir a unicidade.
- **RF-003:** O sistema deve enviar um e-mail de confirmação para o endereço cadastrado para verificar a sua autenticidade.
- **RF-004:** O sistema deve permitir que um usuário (Cliente) inicie o processo de "Tornar-se Vendedor" a partir do seu painel de conta.
- **RF-005:** O formulário para "Tornar-se Vendedor" deve solicitar os dados adicionais obrigatórios (Nome da Loja, Dados Bancários, Endereço Comercial).
- **RF-006:** O sistema deve submeter os cadastros de novos vendedores para aprovação do Administrador.

### 1.2. Autenticação

- **RF-007:** O sistema deve permitir que o usuário faça login usando seu e-mail e senha.
- **RF-008:** O sistema deve fornecer uma funcionalidade de "Esqueci minha senha" que envie um link de redefinição para o e-mail do usuário.

### 1.3. Gerenciamento de Perfil

- **RF-009:** O sistema deve permitir que o Cliente edite suas informações pessoais (nome, telefone).
- **RF-010:** O sistema deve permitir que o Cliente adicione, edite e remova múltiplos endereços de entrega.
- **RF-011:** O sistema deve permitir que o Vendedor acesse um "Painel do Vendedor" para gerenciar suas vendas e produtos.
- **RF-012:** O sistema deve permitir que o Vendedor edite as informações da sua loja (nome da loja, descrição, etc.).

## 2. Módulo de Catálogo e Produtos

### 2.1. Gestão de Produtos (Vendedor)

- **RF-013:** O sistema deve permitir que o Vendedor cadastre um novo produto com título, descrição, categoria, preço, quantidade em estoque, peso e dimensões.
- **RF-014:** O sistema deve permitir que o Vendedor faça upload de múltiplas imagens para cada produto.
- **RF-015:** O sistema deve permitir que o Vendedor edite todas as informações de um produto já cadastrado.
- **RF-016:** O sistema deve permitir que o Vendedor visualize uma lista com todos os seus produtos cadastrados, incluindo status (ativo, pendente, indisponível).
- **RF-017:** O sistema deve atualizar automaticamente o status de um produto para "Indisponível" quando seu estoque chegar a zero.

### 2.2. Visualização de Produtos (Cliente)

- **RF-018:** O sistema deve exibir as páginas de produtos com todas as suas informações: imagens, título, descrição, preço, nome do vendedor e avaliações.
- **RF-019:** O sistema deve exibir o valor do frete calculado na página do produto, com base no CEP inserido pelo cliente.
- **RF-020:** O sistema deve exibir produtos relacionados ou da mesma categoria na página de um produto.

## 3. Módulo de Busca e Navegação

- **RF-021:** O sistema deve fornecer uma barra de busca que permita ao cliente pesquisar produtos por palavras-chave.
- **RF-022:** O sistema deve permitir a navegação por categorias e subcategorias de produtos.
- **RF-023:** A página de resultados de busca deve permitir a aplicação de filtros (faixa de preço, avaliação do vendedor, marca, etc.).

## 4. Módulo de Processo de Compra (Checkout)

- **RF-024:** O sistema deve permitir que o cliente adicione e remova produtos de um carrinho de compras.
- **RF-025:** O carrinho de compras deve exibir todos os produtos, quantidades, preços unitários e subtotais, agrupados por vendedor.
- **RF-026:** O sistema deve calcular os custos de frete separadamente para cada vendedor dentro do mesmo carrinho.
- **RF-027:** O sistema deve apresentar um resumo do pedido (produtos, endereço de entrega, valor total com frete) antes da confirmação do pagamento.
- **RF-028:** O sistema deve permitir que o cliente selecione o método de pagamento (Cartão de Crédito, Pix, Boleto).
- **RF-029:** O sistema deve gerar um pedido único para o cliente, mas internamente criar sub-pedidos para cada vendedor envolvido na compra.

## 5. Módulo de Gestão de Pedidos

### 5.1. Visão do Cliente

- **RF-030:** O sistema deve permitir que o cliente visualize seu histórico de compras.
- **RF-031:** Para cada compra, o sistema deve exibir o status atualizado do pedido (Pagamento Aprovado, Enviado, Entregue, etc.).
- **RF-032:** O sistema deve exibir o código de rastreio quando o pedido for despachado pelo vendedor.
- **RF-033:** O sistema deve permitir que o cliente inicie um processo de cancelamento ou devolução a partir do seu histórico de compras, respeitando as regras de negócio.

### 5.2. Visão do Vendedor

- **RF-034:** O sistema deve notificar o vendedor sobre novos pedidos recebidos.
- **RF-035:** O painel do vendedor deve exibir uma lista de pedidos com seus respectivos status.
- **RF-036:** O sistema deve permitir que o vendedor atualize o status de um pedido (ex: de "Pagamento Aprovado" para "Enviado").
- **RF-037:** O sistema deve exigir que o vendedor insira um código de rastreio válido para alterar o status para "Enviado".

## 6. Módulo de Avaliações (Reviews)

- **RF-038:** O sistema deve permitir que apenas clientes que compraram um determinado produto possam avaliá-lo.
- **RF-039:** A funcionalidade de avaliação deve permitir a atribuição de uma nota (1 a 5 estrelas) e um comentário em texto.
- **RF-040:** O sistema deve calcular e exibir a média de avaliações na página do produto e na página do vendedor.

## 7. Módulo Administrativo

- **RF-041:** O painel administrativo deve permitir a visualização e gestão de todos os usuários (Clientes e Vendedores).
- **RF-042:** O sistema deve permitir que o Administrador aprove ou rejeite novos cadastros de vendedores.
- **RF-043:** O sistema deve permitir que o Administrador modere e remova anúncios de produtos que violem as políticas da plataforma.
- **RF-044:** O sistema deve permitir que o Administrador visualize todos os pedidos da plataforma.
- **RF-045:** O sistema deve fornecer uma ferramenta para o Administrador mediar disputas abertas entre clientes e vendedores.
- **RF-046:** O painel administrativo deve exibir relatórios financeiros básicos (total de vendas, comissão arrecadada, etc.).

## :ballot_box_with_check: Requisitos Não Funcionais (RNF)

## 1. Desempenho

- **RNF-001 (Tempo de Resposta):** As páginas principais da plataforma (Home, página de produto, resultados de busca) devem carregar completamente em no máximo 3 segundos em uma conexão de banda larga padrão.
- **RNF-002 (Tempo de Resposta do Servidor):** O tempo de resposta do servidor (Time to First Byte - TTFB) para qualquer requisição não deve exceder 500 milissegundos.
- **RNF-003 (Carga Concorrente):** O sistema deve suportar, no mínimo, 1.000 usuários simultâneos realizando transações (navegação, busca, adição ao carrinho) sem degradação perceptível no desempenho.
- **RNF-004 (Processamento de Checkout):** O processo de finalização de compra, desde o clique em "Pagar" até a página de confirmação, deve ser concluído em menos de 5 segundos, excluindo o tempo de processamento externo do gateway de pagamento.

## 2. Segurança

- **RNF-005 (Proteção de Dados):** Todos os dados sensíveis dos usuários (senhas, dados pessoais, informações financeiras) devem ser armazenados de forma criptografada no banco de dados.
- **RNF-006 (Comunicação Segura):** Toda a comunicação entre o cliente (browser) e o servidor deve ser obrigatoriamente realizada via protocolo HTTPS (com certificado SSL/TLS válido).
- **RNF-007 (Conformidade com a LGPD):** O sistema deve estar em total conformidade com a Lei Geral de Proteção de Dados (Lei nº 13.709/2018), garantindo os direitos dos titulares de dados, como acesso, correção e exclusão de suas informações.
- **RNF-008 (Segurança de Pagamentos):** A plataforma deve utilizar um gateway de pagamento que possua a certificação PCI-DSS (Payment Card Industry Data Security Standard). O sistema Nexus não deve armazenar dados completos de cartões de crédito.
- **RNF-009 (Proteção contra Ameaças):** O sistema deve possuir mecanismos de proteção contra as principais vulnerabilidades da web, como SQL Injection, Cross-Site Scripting (XSS) e Cross-Site Request Forgery (CSRF), seguindo as recomendações do OWASP Top 10.
- **RNF-010 (Controle de Acesso):** O acesso às funcionalidades do sistema deve ser rigorosamente controlado por papéis (Cliente, Vendedor, Administrador), garantindo que um usuário só possa visualizar e executar ações permitidas para o seu nível de permissão.

## 3. Confiabilidade e Disponibilidade

- **RNF-011 (Disponibilidade):** O sistema deve ter uma disponibilidade mínima de **99.8%** (uptime), o que equivale a um tempo máximo de inatividade de aproximadamente 1 hora e 45 minutos por mês.
- **RNF-012 (Backups):** Devem ser realizados backups diários e automáticos do banco de dados. Os backups devem ser armazenados em um local geograficamente distinto do servidor principal.
- **RNF-013 (Recuperação de Desastres):** O sistema deve possuir um plano de recuperação de desastres que permita a restauração completa da plataforma em até 24 horas em caso de falha catastrófica.

## 4. Usabilidade

- **RNF-014 (Responsividade):** A interface do usuário deve ser totalmente responsiva, adaptando-se e proporcionando uma boa experiência em diferentes tamanhos de tela (desktops, tablets e smartphones).
- **RNF-015 (Consistência Visual):** A plataforma deve manter uma identidade visual e um padrão de navegação consistentes em todas as suas páginas.
- **RNF-016 (Acessibilidade):** O sistema deve seguir as principais diretrizes de acessibilidade da Web (WCAG) 2.1, nível AA, para garantir que pessoas com deficiência possam navegar e utilizar a plataforma.
- **RNF-017 (Intuitividade):** Um novo usuário deve ser capaz de encontrar um produto, adicioná-lo ao carrinho e finalizar uma compra sem a necessidade de um manual ou tutorial.

## 5. Escalabilidade

- **RNF-018 (Escalabilidade Horizontal):** A arquitetura do sistema deve permitir a adição de mais servidores (escalabilidade horizontal) para lidar com o aumento de tráfego e de volume de dados sem a necessidade de reescrever a aplicação.
- **RNF-019 (Crescimento de Dados):** O sistema deve ser capaz de suportar um crescimento de 100% no número de usuários e produtos cadastrados ao longo de um ano sem perda de desempenho.

## 6. Manutenibilidade

- **RNF-020 (Código Documentado):** O código-fonte deve ser bem documentado, seguindo padrões de desenvolvimento (Style Guide) para facilitar a compreensão e a manutenção por novos desenvolvedores.
- **RNF-021 (Modularidade):** A arquitetura do sistema deve ser modular (ex: microsserviços ou módulos bem definidos), permitindo que alterações ou correções em uma parte do sistema não afetem as outras.
- **RNF-022 (Logs):** O sistema deve gerar logs detalhados de erros e de atividades críticas para facilitar a depuração (debugging) e a auditoria.

## 7. Compatibilidade

- **RNF-023 (Compatibilidade com Navegadores):** A plataforma deve ser compatível com as duas últimas versões estáveis dos principais navegadores do mercado: Google Chrome, Mozilla Firefox, Microsoft Edge e Safari.
