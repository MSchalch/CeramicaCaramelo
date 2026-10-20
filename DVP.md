# Documento de Visão do Projeto (DVP) - Caramelo Cerâmicas

## 1. Introdução
O projeto consiste no desenvolvimento de uma plataforma de comércio eletrônico B2C (Business to Consumer) focada na venda de peças utilitárias de cerâmica artesanal. O objetivo é criar um ambiente digital que valorize o trabalho manual, oferecendo uma experiência de compra fluida e intuitiva. 
O catálogo do e-commerce será composto exclusivamente por utensílios de cerâmica voltados para a mesa posta e o uso diário.

## 2. Estado Atual e Tecnologias
O software possui design para aplicação web e, por enquanto, só foi desenvolvido o protótipo de frontend, englobando as visões do Cliente e do Administrador.

As tecnologias e ferramentas escolhidas e aplicadas para o projeto são:
- **Front-end:** React, Bootstrap 5 e Axios.
- **Back-end:** Java 21, Spring Boot 3.x, Flyway, Lombok e Swagger.
- **Banco de Dados e Infraestrutura:** PostgreSQL, Docker e Docker Compose.
- **APIs e Integrações:** Google AI Studio API (chatbot inteligente) e ViaCEP API.
- **Ferramentas:** Google Gemini Pro 3.1, Antigravity, Git/GitHub/GitLab, DBeaver, Postman e Cypress.
- **Arquitetura:** Padrão MVC, Design Patterns (Facade e Strategy).

## 3. Requisitos do Sistema
Os requisitos a seguir descrevem as funcionalidades e características que o sistema deverá contemplar.

### 3.1. Requisitos Funcionais
**Cadastro de Peças de Cerâmica:**
- O sistema deve manter um cadastro único para peças de cerâmica.
- O sistema deve possibilitar que utensílios sejam inativados de forma manual ou automática (quando sem estoque e com venda inferior ao parâmetro predefinido).
- O sistema deve possibilitar a alteração e consulta (com filtros) do cadastro dos utensílios.
- O sistema deve permitir ativar o cadastro de um utensílio.

**Cadastro de Clientes:**
- O sistema deve possibilitar o cadastro, alteração e inativação de clientes.
- O sistema deve permitir que um cliente seja consultado com base em um filtro definido pelo usuário.
- O sistema deve disponibilizar a consulta de todas as transações realizadas pelo cliente.
- O sistema deve permitir associar diversos endereços de entrega e cartões de crédito ao cadastro.
- O sistema deve possibilitar a alteração da senha sem necessidade de alterar outros dados cadastrais.

**Gerenciar Vendas Eletrônicas:**
- O sistema deve permitir adicionar, editar a quantidade, excluir e visualizar peças em um carrinho de compra temporário.
- O sistema deve calcular o frete com base nos itens (peso/dimensões) e o endereço apontado.
- O sistema deve permitir o uso de cupons de troca/promocionais combinados com pagamento via cartão de crédito.
- O sistema deve processar e gerenciar o fluxo da compra: processamento, transporte, entrega e solicitações de troca.
- O sistema deve gerar cupons de troca após a confirmação do recebimento da peça devolvida.

**Controle de Estoque:**
- O sistema deve permitir a entrada de itens, registrando a quantidade e calculando o valor de venda com base no custo e grupo de precificação.
- O sistema deve dar baixa no total de itens para cada venda realizada e permitir a reentrada de itens a partir da devolução/troca.

**Análise & Recomendação:**
- O sistema deve permitir a consulta do histórico de vendas em gráficos (filtrados por período e categoria).
- O sistema deve permitir a exportação dos dados dos gráficos em formato de planilha.
- O sistema deve utilizar Inteligência Artificial Generativa para recomendar peças através de um chatbot com base no estilo de compra e feedback do cliente.

### 3.2. Requisitos Não Funcionais
- O sistema deve garantir que toda consulta tenha resposta em no máximo 1 segundo.
- O sistema deve registrar data, hora, usuário e dados alterados nas operações de escrita (Log de transação).
- O sistema deve atribuir um código único (SKU) para todo utensílio e um código único para todo cliente cadastrado.
- O sistema deve exigir senhas fortes e digitação dupla no registro, e as mesmas devem ser criptografadas.
- O sistema deve exibir gráficos interativos (tooltips) com formatação monetária e legendas apropriadas.

### 3.3. Regras de Negócio
- O sistema deve exigir a presença de dados obrigatórios no cadastro de peças (artesão, categoria, material, dimensões, grupo de precificação, SKU) e de clientes (CPF, endereço completo, dados do cartão, etc.).
- O sistema deve exigir autorização de um gerente caso o valor da peça sofra alteração para um patamar abaixo da margem de lucro estabelecida.
- O sistema não deve permitir a entrada de estoque com quantidade zero, e não deve permitir a adição de peças sem estoque ao carrinho.
- O sistema deve reter a baixa no estoque apenas quando a compra sair do status EM PROCESSAMENTO.
- O sistema deve consolidar as vendas por mês na análise gerencial considerando somente as compras com status APROVADA, EM TRANSPORTE ou ENTREGUE.

## 4. Fases do Projeto
As fases de desenvolvimento foram mapeadas e estruturadas conforme as etapas do Kanban do projeto:

### 4.1. Feito (Concluído)
- Escolha do tema e tecnologias.
- Protótipo.

### 4.2. Fazendo (Sprint da Semana)
- DVP (Documento de Visão do Projeto).

### 4.3. Backlog / A Fazer
- CRUD de cliente.
- Funcionalidades de compra (Catálogo, Carrinho).
- Funcionalidades de compra (Cupons).
- Chatbot (Integração Google Gemini API Java).
- Dashboard de análise.
- Testes E2E com Cypress.
- Refatorações, validações finais de segurança.
- Documentação final, Build da Aplicação.
- Apresentação Final do Projeto.

## 5. Artefatos e Detalhamentos Futuros
Os seguintes elementos serão mapeados, documentados e preenchidos posteriormente no decorrer do projeto:
- 5.1. Diagrama de entidade: pendente
- 5.2. Diagrama de classes: pendente
- 5.3. Modelo lógico e físico de dados: pendente
- 5.4. Mapeamento de casos de uso: pendente
