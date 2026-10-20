# Plano de Testes - Caramelo Cerâmicas

---

## Capa e Cabeçalho
- **Nome do Projeto:** Caramelo Cerâmicas
- **Subtítulo (Opcional):** Plataforma de E-commerce B2C de Cerâmicas Artesanais

---

## Histórico de Versões

| Data | Versão | Descrição | Autor | Revisor |
| :--- | :--- | :--- | :--- | :--- |
| 18/10/2026 | 1.0 | Elaboração inicial do Plano de Testes contemplando Gestão de Clientes, Carrinho, Checkout/Pagamentos e Dashboard Analítico | Matheus Schalch | Professor / Equipe |

---

## Identificação do Documento e Página de Assinaturas

- **Cliente:** FATEC Mogi das Cruzes — Disciplina de Laboratório de Engenharia de Software (LES)
- **Documento:** Plano de Testes: Caramelo Cerâmicas
- **Data:** 18 de outubro de 2026
- **Autor(es):** Matheus Schalch (preencher RA e demais integrantes, se aplicável)
- **Documento base:** `DRS_LES_2_2026` (Versão 1.0)

---

## 1. INTRODUÇÃO

### 1.1 Objetivo
Este Plano de Testes tem como propósito definir a estratégia, os critérios de aceitação, o ambiente e a especificação detalhada dos casos de teste para verificar o incremento atual do sistema de e-commerce **Caramelo Cerâmicas**, abrangendo os módulos de Gestão de Clientes (dados pessoais, endereços e cartões), Carrinho de Compras, Checkout com regras financeiras de múltiplos cartões e cupons, e o Painel Analítico de Vendas (Dashboard). Os resultados obtidos na execução deste plano apoiam a decisão técnica de homologação e liberação da entrega (sprint) para avaliação junto ao cliente/professor.

### 1.2 Escopo
O escopo deste plano compreende a verificação funcional, não funcional e de regressão ponta a ponta (E2E) das funcionalidades já implementadas na plataforma web (Front-end em React e Back-end em Spring Boot com PostgreSQL). Estão cobertos o ciclo completo do cadastro e manutenção de clientes, a montagem de carrinho por usuários autenticados e anônimos, a cotação de frete, o processamento de pedidos com cartões de crédito e cupons (promocionais e de troca) até o status inicial `EM PROCESSAMENTO`, e a visualização de métricas e gráficos gerenciais por período e categoria. O detalhamento completo dos itens cobertos e excluídos encontra-se nas seções 2 e 3.

### 1.3 Documentos de referência

| Documento | Versão | Observação |
| :--- | :--- | :--- |
| Documento de Requisitos de Software (`DRS_LES_2_2026`) | 1.0 | Fonte oficial dos requisitos funcionais (RF), regras de negócio (RN) e requisitos não funcionais (RNF) rastreados |
| Especificação de Casos de Uso (`Especificacao_Caso_de_Uso.md`) | 1.0 | Especificação detalhada do caso de uso `CDU01 - Gerenciar Vendas Eletrônicas` |
| Documento de Visão do Projeto (`DVP.md` / `Entrega_DVP_Word.md`) | 1.0 | Visão arquitetural, tecnológica, modelagem de dados e escopo macro do projeto Caramelo Cerâmicas |

### 1.4 Definições e siglas

| Termo | Definição |
| :--- | :--- |
| RF / RN / RNF | Requisito Funcional / Regra de Negócio / Requisito Não Funcional |
| CT | Caso de Teste |
| E2E | *End to End*: teste que percorre o fluxo completo pela interface do usuário integrando front-end, API REST e banco de dados |
| CDU / UC | Caso de Uso (*Use Case*) |
| SKU | *Stock Keeping Unit*: código identificador alfanumérico único atribuído a cada peça de cerâmica |
| SPA | *Single Page Application*: aplicação web em React que atualiza dinamicamente a interface sem recarregamento completo de página |
| PERT | *Program Evaluation and Review Technique*: técnica de estimativa de esforço ponderada entre cenários otimista (O), mais provável (M) e pessimista (P) |

---

## 2. ITENS A SEREM TESTADOS

| Funcionalidade | Requisitos (DRS) | Caso de uso | Prioridade |
| :--- | :--- | :--- | :--- |
| **F01 - Gestão de Clientes (Cadastro, Alteração, Consulta, Inativação, Histórico e Senha)** | `RF0021`, `RF0022`, `RF0023`, `RF0024`, `RF0025`, `RF0028`, `RN0021`, `RN0022`, `RN0026`, `RNF0012`, `RNF0031`, `RNF0032`, `RNF0035` | `UC01 - Gerenciar Clientes` | Alta |
| **F02 - Gestão de Endereços de Entrega e Cartões de Crédito do Cliente** | `RF0026`, `RF0027`, `RN0023`, `RN0024`, `RN0025`, `RNF0034` | `UC02 - Gerenciar Endereços e Cartões` | Alta |
| **F03 - Carrinho de Compras e Cálculo de Frete** | `RF0031`, `RF0032`, `RF0033`, `RF0034`, `RN0031`, `RN0032` | `CDU01 - Gerenciar Vendas Eletrônicas` | Alta |
| **F04 - Checkout, Pagamento (Múltiplos Cartões e Cupons) e Finalização de Pedido** | `RF0035`, `RF0036`, `RF0037`, `RF0038`, `RN0033`, `RN0034`, `RN0035`, `RN0036`, `RNF0012` | `CDU01 - Gerenciar Vendas Eletrônicas` | Alta |
| **F05 - Painel Analítico de Vendas (Dashboard)** | `RF0055`, `RF0056`, `RN0065`, `RNF0011`, `RNF0051` | `UC07 - Consultar Dashboard e Relatórios` | Média |

---

## 3. ITENS FORA DO ESCOPO

| Item | Motivo da exclusão |
| :--- | :--- |
| **Fluxos de Troca, Devolução e Reentrada em Estoque (`RF0041` a `RF0045`, `RF0054`, `RN0041` a `RN0046`)** | Fora do escopo desta entrega conforme diretrizes da atividade; a validação E2E do ciclo de vendas encerra-se na geração do pedido com status `EM PROCESSAMENTO`. |
| **Transições Administrativas de Status do Pedido e Baixa Definitiva de Estoque (`RF0039`, `RF0040`, `RF0053`, `RN0028`, `RN0038` a `RN0040`)** | Conforme registrado na arquitetura (`Fachada.java`) e no escopo da atividade, a tramitação logística pós-compra (`APROVADA`, `EM TRANSPORTE`, `ENTREGUE`) e a baixa definitiva não compõem esta bateria de testes. |
| **Expiração Automática de Bloqueio Temporário de Carrinho (`RN0044`, `RN0045`, `RNF0042`)** | Funcionalidade dependente de rotina temporal assíncrona não contemplada nesta fase de testes funcionais de interface. |
| **Recomendação de Peças via Chatbot com IA Generativa (Google Gemini API)** | Por envolver respostas generativas não determinísticas de uma API externa de LLM, a validação do Chatbot é conduzida de forma exploratória fora da suíte determinística do Cypress. |
| **Testes de Carga, Estresse e Infraestrutura em Nuvem** | O ambiente de homologação da disciplina é executado integralmente em infraestrutura local (`localhost`), sem requisito de estresse concorrente distribuído. |

---

## 4. ESTRATÉGIA DE TESTES

### 4.1 Níveis de teste

| Nível | Objetivo | Ferramenta | Responsável |
| :--- | :--- | :--- | :--- |
| **Unitário** | Verificar regras de negócio isoladas (Strategies de validação no back-end como CPF, força de senha, cálculo de preço/margem e funções utilitárias `formatters.ts` e `gerarCpfValido` no front-end) | JUnit 5 (Spring Boot Test) / TypeScript Utils | Matheus Schalch |
| **Integração** | Verificar a comunicação entre camadas (Controllers REST, `Fachada`, `Strategies`, `DAOs` e persistência no banco PostgreSQL com migrations Flyway) | Postman / `cy.request` (Cypress) | Matheus Schalch |
| **Sistema (E2E)** | Verificar os fluxos completos ponta a ponta pela interface gráfica do usuário no navegador interagindo com a API e banco reais | Cypress (v13+) | Matheus Schalch |
| **Aceitação** | Validar o atendimento integral aos requisitos do DRS e ao roteiro mínimo da apresentação junto ao cliente (professor) | Execução manual e assistida via Cypress | Matheus Schalch |

### 4.2 Tipos de teste
- **Funcional:** verifica se o sistema executa exatamente o que os Requisitos Funcionais (RF) e as Regras de Negócio (RN) do `DRS_LES_2_2026` determinam nos fluxos de clientes, carrinho, checkout e dashboard.
- **Regressão:** reexecuta a bateria automatizada de casos de teste no Cypress após cada alteração no código-fonte, restaurando automaticamente o estado dos cupons (`/api/cupons/reset-testes`) para garantir que nenhuma funcionalidade previamente aprovada tenha sofrido degradação.
- **Não funcional:** verifica políticas de segurança de senhas (`RNF0031` e `RNF0032`), geração de códigos únicos (`RNF0035`), modularidade na adição de endereços (`RNF0034`), auditoria em banco via Log de Transação (`RNF0012`), tempo de resposta de consultas (`RNF0011`) e usabilidade/interatividade dos gráficos (`RNF0051`).

### 4.3 Técnicas de projeto de casos de teste

| Técnica | Onde foi aplicada |
| :--- | :--- |
| **Partição de equivalência** | **1. Política de Senha (`RNF0031`):** Particionada em classe válida (mínimo 8 caracteres com maiúscula, minúscula e especial, ex.: `SenhaForte@123`) e classes inválidas (sem caractere especial `SenhaSemEspecial123`, tamanho insuficiente `Fraca@1`).<br>**2. Bandeiras de Cartão (`RN0025`):** Particionada em bandeiras permitidas (`VISA`, `MASTERCARD`, `ELO`) e bandeiras não homologadas.<br>**3. Cupons (`RF0037`):** Particionados em cupom promocional ativo (`CARAMELO20`), cupom de troca ativo (`TROCA-50`, `TROCA-200`), cupom inativo/inexistente e cupom excedente (`TROCA-15`). |
| **Análise de valor limite** | **1. Valor mínimo por Cartão (`RN0034` / `RN0035`):** Limite inferior de `R$ 10,00` por cartão em pagamentos com múltiplos cartões sem cupom (valores `< 10,00` como `R$ 9,99` são rejeitados; valores `>= 10,00` como `R$ 10,00` e `R$ 30,00` são aprovados) e abertura de exceção para valores `< R$ 10,00` exclusivamente quando corresponderem ao saldo residual após aplicação de cupons (`RN0035`).<br>**2. Comprimento da Senha (`RNF0031`):** Limite entre 7 caracteres (`Fraca@1` — inválido) e 8 caracteres (`Forte@12` — válido).<br>**3. Quantidade em Estoque (`RN0031` / `RN0032`):** Limite inferior `1` e limite superior igual ao estoque atual da peça (`peca.estoque`), bloqueando `estoque + 1`. |
| **Tabela de decisão** | **Processamento de Pagamento no Checkout (`RF0036`, `RF0037`, `RN0033` a `RN0036`):** Combinação das condições: *(C1)* Há cupom de troca aplicado? *(C2)* Soma dos cupons $\ge$ Valor Total do Pedido? *(C3)* Quantidade de cartões $> 1$? *(C4)* Todos os cartões possuem valor $\ge \text{R\$ } 10,00$? *(C5)* Soma dos cartões $=$ Saldo Restante? Derivando as regras de bloqueio de cupom desnecessário (`RN0036`), geração automática de cupom de troco (`RN0036`), permissão de cartão residual $< \text{R\$ } 10,00$ (`RN0035`) ou bloqueio por violação de valor mínimo/divergente (`RN0034`). |
| **Transição de estados** | **Persistência de Sessão do Carrinho Deslogado até o Pedido (`RF0031`, `RF0033`, `RF0038`):** Verifica a transição de estados do usuário anônimo que monta e edita o carrinho (`Estado: Visitante com Carrinho`), tenta acessar `/checkout` sendo interceptado para `/login` (`Estado: Autenticação Pendente`), realiza login e retorna automaticamente ao `/checkout` com os itens preservados (`Estado: Checkout Autenticado`) até a criação do pedido em `EM PROCESSAMENTO`. |

---

## 5. AMBIENTE DE TESTES

| Componente | Especificação |
| :--- | :--- |
| **Sistema operacional** | Windows 11 Pro / Home (64 bits) |
| **Navegadores e versões** | Google Chrome (v129+ / Electron Headless integrado ao Cypress em resolução `1280x720`) e Microsoft Edge |
| **Banco de dados** | PostgreSQL 16 (executando em contêiner Docker na porta `5432`, base dedicada `ceramica_caramelo` estruturada via Flyway Migrations `V1` a `V9`) |
| **Ferramentas** | Cypress v13+ (automação E2E no front-end), Postman (testes de integração REST), JUnit 5 (back-end), Git / GitHub Issues (versionamento e gestão de defeitos) |
| **URL / servidor** | Front-end React + Vite: `http://localhost:5173` \| Back-end API Spring Boot (Java 21): `http://localhost:8080` |
| **Massa de dados** | **1. Carga inicial automatizada (Flyway Seeds):** A migration `V5` insere 3 clientes ativos (`marina.silva@email.com`, `lucas.mendes@email.com`, `beatriz.rocha@email.com`, senha `123456`) com endereços e cartões, além de 20 peças em 5 categorias; a `V6` cria os cupons `TROCA-50`, `TROCA-15`, `TROCA-200` e `CARAMELO20`; a `V9` popula 9 pedidos históricos para o Dashboard.<br>**2. Restauração e geração dinâmica:** Antes de cada teste (`beforeEach`), o Cypress limpa o `localStorage` e aciona `POST http://localhost:8080/api/cupons/reset-testes` para reativar os cupons utilizados. Novos clientes utilizam `gerarCpfValido()` e carimbo de tempo (`Date.now()`). |

---

## 6. CRITÉRIOS

| Critério | Descrição Objetiva |
| :--- | :--- |
| **Critérios de entrada** | 1. Contêiner PostgreSQL em execução na porta `5432` com as 9 migrations do Flyway (`V1` a `V9`) aplicadas sem erros.<br>2. API Back-end Spring Boot respondendo na porta `8080` e servidor Front-end React respondendo em `http://localhost:5173`.<br>3. Endpoint utilitário `POST /api/cupons/reset-testes` disponível para restauração da massa de cupons. |
| **Critérios de saída** | 1. 100% dos casos de teste de prioridade **Alta** executados e com status **Aprovado**.<br>2. Pelo menos 90% dos casos de teste de prioridade **Média** executados e aprovados.<br>3. 100% dos requisitos listados no escopo (Seção 2) cobertos na Matriz de Rastreabilidade.<br>4. Nenhum defeito de severidade **Crítica** ou **Alta** aberto/pendente de correção. |
| **Critérios de suspensão** | 1. Indisponibilidade do banco PostgreSQL ou falha na API Spring Boot que impeça a execução das requisições REST.<br>2. Ocorrência de defeito de severidade **Crítica** nas rotas de autenticação (`/login`), catálogo (`/`) ou checkout (`/checkout`) que bloqueie mais de 30% dos casos de teste planejados. |
| **Critérios de retomada** | 1. Correção e validação do defeito bloqueante ou restabelecimento dos serviços Docker/Spring Boot/Vite.<br>2. Limpeza de sessão (`cy.clearLocalStorage()`) e reexecução do reset de massa (`/api/cupons/reset-testes`). |

---

## 7. CASOS DE TESTE

### 7.1 Resumo dos casos de teste

| ID | Título | Requisitos | Prioridade | Automatizado |
| :--- | :--- | :--- | :--- | :--- |
| **CT001** | Cadastrar novo cliente com todos os dados obrigatórios e geração de Código Único | `RF0021`, `RN0021`, `RN0022`, `RN0023`, `RN0026`, `RNF0012`, `RNF0035` | Alta | Sim (Cypress) |
| **CT002** | Impedir cadastro de cliente quando as senhas de confirmação não coincidirem | `RF0021`, `RNF0032` | Alta | Sim (Cypress) |
| **CT003** | Impedir cadastro de cliente com senha fraca (menos de 8 dígitos ou sem caractere especial) | `RF0021`, `RNF0031` | Alta | Sim (Cypress) |
| **CT004** | Impedir cadastro de cliente com campos obrigatórios vazios ou CPF inválido/duplicado | `RF0021`, `RN0021`, `RN0022`, `RN0026` | Alta | Não (Manual / API) |
| **CT005** | Consultar clientes por filtro (Nome, CPF e E-mail) e editar dados cadastrais | `RF0022`, `RF0024`, `RNF0012` | Alta | Sim (Cypress) |
| **CT006** | Alterar apenas a senha do cliente sem modificar outros dados cadastrais | `RF0028`, `RNF0031`, `RNF0032` | Alta | Sim (Cypress) |
| **CT007** | Inativar e reativar o cadastro de um cliente com sucesso | `RF0023`, `RNF0012` | Alta | Sim (Cypress) |
| **CT008** | Consultar histórico de transações/pedidos realizados pelo cliente | `RF0025` | Média | Sim (Cypress) |
| **CT009** | Adicionar novo endereço de entrega com frase curta sem alterar demais dados do cliente | `RF0026`, `RN0023`, `RNF0034` | Alta | Sim (Cypress) |
| **CT010** | Impedir cadastro de endereço com campos obrigatórios da composição vazios | `RF0026`, `RN0023` | Média | Não (Manual) |
| **CT011** | Associar novo cartão de crédito com bandeira permitida e definir como preferencial | `RF0027`, `RN0024`, `RN0025` | Alta | Sim (Cypress) |
| **CT012** | Impedir associação de cartão de crédito sem dados obrigatórios ou com bandeira inválida | `RF0027`, `RN0024`, `RN0025` | Média | Não (Manual / API) |
| **CT013** | Incluir mais de um item no carrinho, alterar quantidades e calcular frete por CEP | `RF0031`, `RF0032`, `RF0034`, `RN0031` | Alta | Sim (Cypress) |
| **CT014** | Impedir adição ou alteração de quantidade no carrinho superior ao estoque disponível | `RF0031`, `RF0032`, `RN0031`, `RN0032` | Alta | Não (Manual) |
| **CT015** | Exigir login ao finalizar carrinho montado deslogado, preservar itens e concluir compra | `RF0031`, `RF0033`, `RF0038` | Alta | Sim (Cypress) |
| **CT016** | Realizar compra com endereço e cartão pré-cadastrados e barrar valor divergente do total | `RF0033`, `RF0035`, `RF0036`, `RF0038` | Alta | Sim (Cypress) |
| **CT017** | Realizar compra cadastrando novo endereço e novo cartão no checkout e incorporá-los ao perfil | `RF0035`, `RF0036`, `RN0023`, `RN0024`, `RN0025` | Alta | Sim (Cypress) |
| **CT018** | Pagar com mais de um cartão de crédito respeitando o valor mínimo de R$ 10,00 por cartão | `RF0036`, `RN0034` | Alta | Sim (Cypress) |
| **CT019** | Pagar com cartão de crédito combinado a cupons com saldo residual inferior a R$ 10,00 | `RF0036`, `RF0037`, `RN0033`, `RN0035` | Alta | Sim (Cypress) |
| **CT020** | Utilizar cupom de troca superior ao total da compra (gerando troco) e bloquear cupom desnecessário | `RF0037`, `RF0038`, `RN0036`, `RNF0012` | Alta | Sim (Cypress) |
| **CT021** | Validar KPIs, gráfico de linhas e filtros por período e categorias no Dashboard Analítico | `RF0055`, `RF0056`, `RN0065`, `RNF0011`, `RNF0051` | Média | Sim (Cypress) |
| **CT022** | Impedir filtragem no Dashboard quando a data final for anterior à data inicial | `RF0056` | Média | Não (Manual) |

---

### 7.2 Especificação dos casos de teste

#### CT001 — Cadastrar novo cliente com todos os dados obrigatórios e geração de Código Único

| Campo | Descrição |
| :--- | :--- |
| **Requisitos rastreados** | `RF0021`, `RN0021`, `RN0022`, `RN0023`, `RN0026`, `RNF0012`, `RNF0035` |
| **Caso de uso relacionado** | `UC01 - Gerenciar Clientes` |
| **Nível / Tipo** | Sistema (E2E) / Funcional e Não funcional |
| **Técnica de projeto** | Partição de equivalência (classe válida de dados pessoais, senha e endereço completo) |
| **Prioridade** | Alta |
| **Pré-condições** | Usuário autenticado como Administrador (`cy.loginAdmin()`) e aplicação acessível em `http://localhost:5173`. |
| **Dados de teste** | Nome: `Cliente Requisitos <timestamp>`; E-mail: `requisitos.<timestamp>@caramelo.com`; CPF: gerado por `gerarCpfValido()`; Telefone: `(11) 98765-4321`; Nascimento: `1994-06-15`; Gênero: `Masculino`; Senha/Confirmação: `SenhaForte@123`; Endereço: Identificação `Residência Principal`, Tipo `Apartamento`, CEP `04538-133`, Logradouro `Avenida Brigadeiro Faria Lima`, Nº `3477`, Bairro `Itaim Bibi`, Cidade `São Paulo`, UF `SP`, Tipo de Endereço `AMBOS` (Cobrança e Entrega). |

| Passo | Ação | Resultado esperado |
| :---: | :--- | :--- |
| 1 | Acessar a rota `/customer/new`. | O sistema exibe o formulário "Novo Cliente". |
| 2 | Preencher todos os dados pessoais obrigatórios (`nome`, `email`, `cpf`, `telefone`, `dataNascimento`, `genero`, `senha` e `confirmarSenha`). | Os campos aceitam os valores formatados sem mensagens de erro. |
| 3 | Preencher os campos obrigatórios do endereço inicial selecionando a finalidade `AMBOS` (`RN0021` e `RN0022`). | Os dados de endereço ficam preenchidos corretamente. |
| 4 | Clicar no botão `Cadastrar Cliente`. | O sistema exibe alerta de sucesso (`.alert-success`) e redireciona para `/admin/customers`. |
| 5 | Verificar a linha correspondente ao cliente recém-cadastrado na tabela. | O cliente é listado como `Ativo` e possui um código único no formato `CLI-XXXXXXXX` (`RNF0035`). |

| Campo | Descrição |
| :--- | :--- |
| **Pós-condições** | Cliente persistido no PostgreSQL com endereço vinculado, senha criptografada e log de auditoria registrado (`RNF0012`). |
| **Automatizado?** | Sim; Cypress — `front-end/cypress/e2e/clientes.cy.ts` (teste 1) e `front-end/cypress/e2e/regras_negocio_cliente.cy.ts` (teste 3). |
| **Resultado da execução** | Aprovado; 18/10/2026; Responsável: Matheus Schalch; Sem defeitos. |

---

#### CT002 — Impedir cadastro de cliente quando as senhas de confirmação não coincidirem

| Campo | Descrição |
| :--- | :--- |
| **Requisitos rastreados** | `RF0021`, `RNF0032` |
| **Caso de uso relacionado** | `UC01 - Gerenciar Clientes` |
| **Nível / Tipo** | Sistema (E2E) / Não funcional (Segurança / Usabilidade) |
| **Técnica de projeto** | Partição de equivalência (classe inválida: `senha != confirmarSenha`) |
| **Prioridade** | Alta |
| **Pré-condições** | Usuário na tela de cadastro de cliente (`/customer/new`). |
| **Dados de teste** | Nome: `Cliente Teste Invalido`; CPF válido; Senha: `SenhaForte@123`; Confirmar Senha: `SenhaDiferente@999`. |

| Passo | Ação | Resultado esperado |
| :---: | :--- | :--- |
| 1 | Acessar `/customer/new` e preencher os dados pessoais básicos. | Campos preenchidos na tela. |
| 2 | Digitar `SenhaForte@123` no campo `senha` e `SenhaDiferente@999` no campo `confirmarSenha`. | O sistema exibe imediatamente o feedback visual `.invalid-feedback` com a mensagem `"As senhas não coincidem"`. |
| 3 | Clicar no botão `Cadastrar Cliente`. | O sistema dispara alerta bloqueando o envio e permanece na rota `/customer/new`. |

| Campo | Descrição |
| :--- | :--- |
| **Pós-condições** | Nenhum registro de cliente inválido é gravado no banco de dados. |
| **Automatizado?** | Sim; Cypress — `front-end/cypress/e2e/regras_negocio_cliente.cy.ts` (teste 1). |
| **Resultado da execução** | Aprovado; 18/10/2026; Responsável: Matheus Schalch; Sem defeitos. |

---

#### CT003 — Impedir cadastro de cliente com senha fraca (menos de 8 dígitos ou sem caractere especial)

| Campo | Descrição |
| :--- | :--- |
| **Requisitos rastreados** | `RF0021`, `RNF0031` |
| **Caso de uso relacionado** | `UC01 - Gerenciar Clientes` |
| **Nível / Tipo** | Sistema (E2E) / Não funcional (Segurança) |
| **Técnica de projeto** | Análise de valor limite (7 caracteres vs. mín. 8) e Partição de equivalência (ausência de caractere especial) |
| **Prioridade** | Alta |
| **Pré-condições** | Usuário na tela `/customer/new`. |
| **Dados de teste** | Tentativa 1 (7 caracteres): `Fraca@1`; Tentativa 2 (sem caractere especial): `SenhaSemEspecial123`. |

| Passo | Ação | Resultado esperado |
| :---: | :--- | :--- |
| 1 | Acessar `/customer/new` e preencher nome, e-mail, CPF, telefone, nascimento e gênero. | Dados básicos preenchidos. |
| 2 | Informar `Fraca@1` nos campos `senha` e `confirmarSenha`. | O sistema exibe `.invalid-feedback` informando que a senha deve conter no mínimo 8 caracteres, letras maiúsculas, minúsculas e caracteres especiais. |
| 3 | Substituir a senha por `SenhaSemEspecial123` em ambos os campos e clicar em `Cadastrar Cliente`. | O sistema exibe alerta de `"Senha fraca"`, impede a submissão e mantém o usuário em `/customer/new`. |

| Campo | Descrição |
| :--- | :--- |
| **Pós-condições** | Cadastro bloqueado na interface e na Strategy `ValidarDadosObrigatoriosClienteStrategy`. |
| **Automatizado?** | Sim; Cypress — `front-end/cypress/e2e/regras_negocio_cliente.cy.ts` (teste 2). |
| **Resultado da execução** | Aprovado; 18/10/2026; Responsável: Matheus Schalch; Sem defeitos. |

---

#### CT004 — Impedir cadastro de cliente com campos obrigatórios vazios ou CPF inválido/duplicado

| Campo | Descrição |
| :--- | :--- |
| **Requisitos rastreados** | `RF0021`, `RN0021`, `RN0022`, `RN0026` |
| **Caso de uso relacionado** | `UC01 - Gerenciar Clientes` |
| **Nível / Tipo** | Integração e Sistema / Funcional |
| **Técnica de projeto** | Partição de equivalência (campos obrigatórios nulos/vazios, CPF com dígitos verificadores inválidos e CPF já existente) |
| **Prioridade** | Alta |
| **Pré-condições** | Cliente `marina.silva@email.com` (`CPF 529.982.247-25`) previamente cadastrado na base via Migration V5. |
| **Dados de teste** | Cenário A: Nome vazio `""`; Cenário B: CPF inválido `111.111.111-11`; Cenário C: CPF duplicado `529.982.247-25`. |

| Passo | Ação | Resultado esperado |
| :---: | :--- | :--- |
| 1 | Tentar submeter o cadastro em `/customer/new` deixando o campo obrigatório `nome` ou `endereco` em branco. | O formulário/API bloqueia a operação exigindo o preenchimento de todos os dados obrigatórios (`RN0026`, `RN0021`, `RN0022`). |
| 2 | Preencher o formulário com o CPF inválido `111.111.111-11` e submeter. | A strategy `ValidarCpfValidoStrategy` rejeita o cadastro com mensagem de CPF inválido. |
| 3 | Preencher o formulário com o CPF já cadastrado `529.982.247-25` e submeter. | A strategy `ValidarCpfUnicoStrategy` impede a duplicidade retornando erro de CPF já cadastrado. |

| Campo | Descrição |
| :--- | :--- |
| **Pós-condições** | Base de clientes permanece íntegra sem registros incompletos ou duplicados. |
| **Automatizado?** | Não; execução manual / Postman (`POST /api/clientes`). |
| **Resultado da execução** | Aprovado; 18/10/2026; Responsável: Matheus Schalch; Sem defeitos. |

---

#### CT005 — Consultar clientes por filtro (Nome, CPF e E-mail) e editar dados cadastrais

| Campo | Descrição |
| :--- | :--- |
| **Requisitos rastreados** | `RF0022`, `RF0024`, `RNF0012` |
| **Caso de uso relacionado** | `UC01 - Gerenciar Clientes` |
| **Nível / Tipo** | Sistema (E2E) / Funcional |
| **Técnica de projeto** | Partição de equivalência (filtros de busca por Nome, CPF e E-mail) |
| **Prioridade** | Alta |
| **Pré-condições** | Administrador autenticado e cliente previamente cadastrado na base. |
| **Dados de teste** | Filtro por Nome, CPF e E-mail do cliente criado; Novo Nome: `Cliente Teste Cypress Atualizado <timestamp>`. |

| Passo | Ação | Resultado esperado |
| :---: | :--- | :--- |
| 1 | Acessar `/admin/customers`, digitar o CPF do cliente no campo de busca e clicar em `Buscar`. | A tabela filtra e exibe exatamente o registro do cliente correspondente (`RF0024`). |
| 2 | Realizar nova busca informando o e-mail e, em seguida, o nome do cliente. | Em ambas as consultas o cliente é localizado corretamente na listagem. |
| 3 | Clicar no botão `Ver Detalhes / Editar` na linha do cliente. | O modal `Gerenciar Perfil` é aberto com os dados carregados. |
| 4 | Alterar o campo `nome` para `Cliente Teste Cypress Atualizado <timestamp>` e clicar em `Salvar Alterações`. | O modal exibe `.alert-success` confirmando a atualização (`RF0022`). |
| 5 | Fechar o modal e pesquisar pelo novo nome na tabela. | A tabela exibe o cliente com o nome atualizado. |

| Campo | Descrição |
| :--- | :--- |
| **Pós-condições** | Nome do cliente atualizado no banco de dados e operação `ALTERAR` registrada em `logs_transacao` (`RNF0012`). |
| **Automatizado?** | Sim; Cypress — `front-end/cypress/e2e/clientes.cy.ts` (teste 2) e `front-end/cypress/e2e/regras_negocio_cliente.cy.ts` (teste 8). |
| **Resultado da execução** | Aprovado; 18/10/2026; Responsável: Matheus Schalch; Sem defeitos. |

---

#### CT006 — Alterar apenas a senha do cliente sem modificar outros dados cadastrais

| Campo | Descrição |
| :--- | :--- |
| **Requisitos rastreados** | `RF0028`, `RNF0031`, `RNF0032` |
| **Caso de uso relacionado** | `UC01 - Gerenciar Clientes` |
| **Nível / Tipo** | Sistema (E2E) / Funcional e Não funcional |
| **Técnica de projeto** | Partição de equivalência (atualização isolada de credencial com senha forte) |
| **Prioridade** | Alta |
| **Pré-condições** | Administrador autenticado em `/admin/customers` com cliente ativo localizado. |
| **Dados de teste** | Nova Senha: `NovaSenhaSegura@2026`; Confirmar Senha: `NovaSenhaSegura@2026`. |

| Passo | Ação | Resultado esperado |
| :---: | :--- | :--- |
| 1 | Localizar o cliente em `/admin/customers` e abrir o modal `Ver Detalhes / Editar`. | Modal aberto mantendo os dados pessoais atuais intactos. |
| 2 | Preencher apenas os campos `senha` e `confirmarSenha` com `NovaSenhaSegura@2026`. | Campos validam positivamente a regra de senha forte e coincidência. |
| 3 | Clicar em `Salvar Alterações`. | O sistema salva a nova senha criptografada sem exigir ou alterar outros dados e exibe `.alert-success`. |

| Campo | Descrição |
| :--- | :--- |
| **Pós-condições** | Senha atualizada e criptografada no banco de dados; demais atributos cadastrais permanecem inalterados. |
| **Automatizado?** | Sim; Cypress — `front-end/cypress/e2e/regras_negocio_cliente.cy.ts` (teste 6). |
| **Resultado da execução** | Aprovado; 18/10/2026; Responsável: Matheus Schalch; Sem defeitos. |

---

#### CT007 — Inativar e reativar o cadastro de um cliente com sucesso

| Campo | Descrição |
| :--- | :--- |
| **Requisitos rastreados** | `RF0023`, `RNF0012` |
| **Caso de uso relacionado** | `UC01 - Gerenciar Clientes` |
| **Nível / Tipo** | Sistema (E2E) / Funcional |
| **Técnica de projeto** | Transição de estados (`Ativo` $\rightarrow$ `Inativo` $\rightarrow$ `Ativo`) |
| **Prioridade** | Alta |
| **Pré-condições** | Administrador autenticado em `/admin/customers` e cliente com status `Ativo`. |
| **Dados de teste** | Cliente: `Cliente Teste Cypress Atualizado <timestamp>`. |

| Passo | Ação | Resultado esperado |
| :---: | :--- | :--- |
| 1 | Buscar o cliente na tabela de `/admin/customers` e verificar a coluna de status. | O badge exibe o estado `Ativo`. |
| 2 | Clicar no botão `Inativar Cliente` e confirmar na caixa de diálogo. | O status do cliente na tabela muda imediatamente para o badge `Inativo`. |
| 3 | Clicar no botão `Reativar Cliente` na mesma linha. | O status do cliente retorna para o badge `Ativo`. |

| Campo | Descrição |
| :--- | :--- |
| **Pós-condições** | Status do cliente atualizado no banco de dados e log de auditoria registrado. |
| **Automatizado?** | Sim; Cypress — `front-end/cypress/e2e/clientes.cy.ts` (teste 3) e `front-end/cypress/e2e/regras_negocio_cliente.cy.ts` (teste 9). |
| **Resultado da execução** | Aprovado; 18/10/2026; Responsável: Matheus Schalch; Sem defeitos. |

---

#### CT008 — Consultar histórico de transações/pedidos realizados pelo cliente

| Campo | Descrição |
| :--- | :--- |
| **Requisitos rastreados** | `RF0025` |
| **Caso de uso relacionado** | `UC01 - Gerenciar Clientes` |
| **Nível / Tipo** | Sistema (E2E) / Funcional |
| **Técnica de projeto** | Partição de equivalência (consulta de transações vinculadas ao cliente) |
| **Prioridade** | Média |
| **Pré-condições** | Administrador autenticado em `/admin/customers`. |
| **Dados de teste** | Cliente cadastrado na base. |

| Passo | Ação | Resultado esperado |
| :---: | :--- | :--- |
| 1 | Filtrar pelo cliente em `/admin/customers`. | Linha do cliente exibida na tabela. |
| 2 | Clicar no botão de ação `Histórico de Pedidos`. | O sistema abre o modal `Histórico de Pedidos` exibindo os dados do cliente e suas transações registradas. |
| 3 | Fechar o modal clicando em `.btn-close`. | O modal é encerrado retornando à listagem. |

| Campo | Descrição |
| :--- | :--- |
| **Pós-condições** | Nenhuma alteração de dados; consulta concluída com sucesso. |
| **Automatizado?** | Sim; Cypress — `front-end/cypress/e2e/regras_negocio_cliente.cy.ts` (teste 7). |
| **Resultado da execução** | Aprovado; 18/10/2026; Responsável: Matheus Schalch; Sem defeitos. |

---

#### CT009 — Adicionar novo endereço de entrega com frase curta sem alterar demais dados do cliente

| Campo | Descrição |
| :--- | :--- |
| **Requisitos rastreados** | `RF0026`, `RN0023`, `RNF0034` |
| **Caso de uso relacionado** | `UC02 - Gerenciar Endereços e Cartões` |
| **Nível / Tipo** | Sistema (E2E) / Funcional e Não funcional |
| **Técnica de projeto** | Partição de equivalência (composição completa de endereço de entrega) |
| **Prioridade** | Alta |
| **Pré-condições** | Administrador autenticado com modal de detalhes do cliente aberto. |
| **Dados de teste** | Identificação (frase curta): `Escritório Comercial`; Tipo de Residência: `Comercial`; CEP: `01310-100`; Logradouro: `Avenida Paulista`; Nº: `1000`; Bairro: `Bela Vista`; Cidade: `São Paulo`; UF: `SP`; Tipo: `ENTREGA`. |

| Passo | Ação | Resultado esperado |
| :---: | :--- | :--- |
| 1 | No modal do cliente, clicar na aba `Endereços` e depois no botão `Novo Endereço`. | O formulário de inclusão de endereço é exibido sem exigir edição dos dados pessoais (`RNF0034`). |
| 2 | Preencher a frase curta `Escritório Comercial` e todos os atributos obrigatórios da composição do endereço (`RN0023`). | Campos preenchidos corretamente. |
| 3 | Clicar em `Salvar Endereço`. | O endereço `Escritório Comercial - Avenida Paulista` passa a constar na lista de endereços do cliente (`RF0026`). |

| Campo | Descrição |
| :--- | :--- |
| **Pós-condições** | Novo endereço de entrega vinculado ao cliente no banco de dados. |
| **Automatizado?** | Sim; Cypress — `front-end/cypress/e2e/regras_negocio_cliente.cy.ts` (teste 4). |
| **Resultado da execução** | Aprovado; 18/10/2026; Responsável: Matheus Schalch; Sem defeitos. |

---

#### CT010 — Impedir cadastro de endereço com campos obrigatórios da composição vazios

| Campo | Descrição |
| :--- | :--- |
| **Requisitos rastreados** | `RF0026`, `RN0023` |
| **Caso de uso relacionado** | `UC02 - Gerenciar Endereços e Cartões` |
| **Nível / Tipo** | Sistema / Funcional |
| **Técnica de projeto** | Partição de equivalência (campos obrigatórios de `RN0023` omitidos) |
| **Prioridade** | Média |
| **Pré-condições** | Modal de cadastro de novo endereço aberto (no perfil ou durante o checkout). |
| **Dados de teste** | Identificação: `Casa Incompleta`; CEP: `""` (vazio); Logradouro: `""` (vazio); Número: `""` (vazio). |

| Passo | Ação | Resultado esperado |
| :---: | :--- | :--- |
| 1 | Abrir o modal de Novo Endereço e preencher apenas o campo `identificacao`. | Demais campos obrigatórios permanecem vazios. |
| 2 | Clicar em `Salvar Endereço`. | O sistema bloqueia o salvamento e exibe alerta exigindo o preenchimento de todos os campos obrigatórios (`RN0023`). |

| Campo | Descrição |
| :--- | :--- |
| **Pós-condições** | Endereço incompleto não é adicionado à lista do cliente. |
| **Automatizado?** | Não; execução manual. |
| **Resultado da execução** | Aprovado; 18/10/2026; Responsável: Matheus Schalch; Sem defeitos. |

---

#### CT011 — Associar novo cartão de crédito com bandeira permitida e definir como preferencial

| Campo | Descrição |
| :--- | :--- |
| **Requisitos rastreados** | `RF0027`, `RN0024`, `RN0025` |
| **Caso de uso relacionado** | `UC02 - Gerenciar Endereços e Cartões` |
| **Nível / Tipo** | Sistema (E2E) / Funcional |
| **Técnica de projeto** | Partição de equivalência (cartão válido com bandeira permitida) |
| **Prioridade** | Alta |
| **Pré-condições** | Modal de gerenciamento de perfil do cliente aberto. |
| **Dados de teste** | Número: `5412751234123456`; Nome Impresso: `CLIENTE REQUISITOS`; Bandeira: `MASTERCARD`; CVV: `321`; Preferencial: `Marcado (true)`. |

| Passo | Ação | Resultado esperado |
| :---: | :--- | :--- |
| 1 | Acessar a aba `Cartões` no modal do cliente e clicar em `Novo Cartão`. | Formulário de cartão de crédito é exibido. |
| 2 | Preencher número, nome impresso, selecionar a bandeira permitida `MASTERCARD` (`RN0025`), informar o CVV (`RN0024`) e marcar o checkbox `Preferencial` (`RF0027`). | Todos os campos são preenchidos. |
| 3 | Clicar em `Salvar Cartão`. | O cartão é listado na aba com a bandeira `MASTERCARD` e o badge `Preferencial` visível. |

| Campo | Descrição |
| :--- | :--- |
| **Pós-condições** | Cartão persistido e marcado como preferencial para seleção automática no checkout. |
| **Automatizado?** | Sim; Cypress — `front-end/cypress/e2e/regras_negocio_cliente.cy.ts` (teste 5). |
| **Resultado da execução** | Aprovado; 18/10/2026; Responsável: Matheus Schalch; Sem defeitos. |

---

#### CT012 — Impedir associação de cartão de crédito sem dados obrigatórios ou com bandeira inválida

| Campo | Descrição |
| :--- | :--- |
| **Requisitos rastreados** | `RF0027`, `RN0024`, `RN0025` |
| **Caso de uso relacionado** | `UC02 - Gerenciar Endereços e Cartões` |
| **Nível / Tipo** | Sistema / Funcional |
| **Técnica de projeto** | Partição de equivalência (CVV/número ausentes ou bandeira vazia) |
| **Prioridade** | Média |
| **Pré-condições** | Usuário na aba `Cartões` do perfil ou na seção de pagamento do `/checkout`. |
| **Dados de teste** | Número: `""` (vazio); Nome Impresso: `TESTE`; Bandeira: não selecionada; CVV: `""`. |

| Passo | Ação | Resultado esperado |
| :---: | :--- | :--- |
| 1 | Iniciar inclusão de novo cartão deixando o número do cartão, bandeira ou código de segurança (CVV) em branco. | Campos obrigatórios de `RN0024` e `RN0025` ausentes. |
| 2 | Tentar salvar o cartão ou confirmar o pedido no checkout. | O sistema impede a operação e exige o preenchimento completo dos atributos obrigatórios do cartão e bandeira válida. |

| Campo | Descrição |
| :--- | :--- |
| **Pós-condições** | Cartão inválido não é associado ao cliente nem processado. |
| **Automatizado?** | Não; execução manual. |
| **Resultado da execução** | Aprovado; 18/10/2026; Responsável: Matheus Schalch; Sem defeitos. |

---

#### CT013 — Incluir mais de um item no carrinho, alterar quantidades e calcular frete por CEP

| Campo | Descrição |
| :--- | :--- |
| **Requisitos rastreados** | `RF0031`, `RF0032`, `RF0034`, `RN0031` |
| **Caso de uso relacionado** | `CDU01 - Gerenciar Vendas Eletrônicas` |
| **Nível / Tipo** | Sistema (E2E) / Funcional |
| **Técnica de projeto** | Partição de equivalência e Análise de valor limite (quantidades válidas dentro do estoque) |
| **Prioridade** | Alta |
| **Pré-condições** | Catálogo carregado com as 20 peças ativas da Migration V5 em `http://localhost:5173/`. |
| **Dados de teste** | Produto 1: quantidade inicial `2`, depois alterada para `3`; Produto 2: quantidade `1`; CEP para cotação: `01310-100`. |

| Passo | Ação | Resultado esperado |
| :---: | :--- | :--- |
| 1 | Na página inicial (`/`), definir a quantidade `2` no primeiro card de produto e clicar em `Adicionar ao Carrinho` (`RF0032`). | O sistema redireciona para `/cart` exibindo 1 item com quantidade `2`. |
| 2 | Clicar em `Continuar Comprando`, selecionar quantidade `1` no segundo produto do catálogo e adicionar ao carrinho. | O carrinho (`/cart`) passa a listar 2 itens distintos (`RF0031`). |
| 3 | Alterar a quantidade do primeiro item diretamente no carrinho de `2` para `3`. | O subtotal dos itens e o peso acumulado são recalculados imediatamente. |
| 4 | Informar o CEP `01310-100` e clicar em `Calcular` (`RF0034`). | O sistema exibe o valor do frete calculado e atualiza o valor total do pedido. |

| Campo | Descrição |
| :--- | :--- |
| **Pós-condições** | Carrinho atualizado com 2 produtos distintos, quantidades ajustadas e frete cotado. |
| **Automatizado?** | Sim; Cypress — `front-end/cypress/e2e/compras_checkout.cy.ts` (teste 1) e `front-end/cypress/e2e/carrinho_deslogado_e_dashboard.cy.ts` (teste 1). |
| **Resultado da execução** | Aprovado; 18/10/2026; Responsável: Matheus Schalch; Sem defeitos. |

---

#### CT014 — Impedir adição ou alteração de quantidade no carrinho superior ao estoque disponível

| Campo | Descrição |
| :--- | :--- |
| **Requisitos rastreados** | `RF0031`, `RF0032`, `RN0031`, `RN0032` |
| **Caso de uso relacionado** | `CDU01 - Gerenciar Vendas Eletrônicas` (Fluxo de Exceção E2) |
| **Nível / Tipo** | Integração e Sistema / Funcional |
| **Técnica de projeto** | Análise de valor limite (quantidade solicitada $>$ `estoque` disponível da peça) |
| **Prioridade** | Alta |
| **Pré-condições** | Peça ativa no catálogo com estoque conhecido (ex.: `Bowl Terracota Rústico` com estoque de 15 unidades). |
| **Dados de teste** | Quantidade solicitada: `50` unidades (superior ao limite de 15 em estoque). |

| Passo | Ação | Resultado esperado |
| :---: | :--- | :--- |
| 1 | No catálogo (`/`) ou no carrinho (`/cart`), tentar informar a quantidade `50` para a peça cujo estoque é `15`. | O sistema exibe alerta informando que a quantidade solicitada supera o estoque disponível (`RN0031`, `RN0032`). |
| 2 | Tentar submeter um pedido via API (`POST /api/pedidos`) com quantidade maior que o estoque no banco. | A strategy `ValidarEstoquePedidoStrategy` rejeita a criação do pedido retornando `"Estoque insuficiente para a peça..."`. |

| Campo | Descrição |
| :--- | :--- |
| **Pós-condições** | Quantidade inválida é bloqueada e o estoque permanece íntegro. |
| **Automatizado?** | Não; execução manual / Postman. |
| **Resultado da execução** | Aprovado; 18/10/2026; Responsável: Matheus Schalch; Sem defeitos. |

---

#### CT015 — Exigir login ao finalizar carrinho montado deslogado, preservar itens e concluir compra

| Campo | Descrição |
| :--- | :--- |
| **Requisitos rastreados** | `RF0031`, `RF0033`, `RF0038` |
| **Caso de uso relacionado** | `CDU01 - Gerenciar Vendas Eletrônicas` |
| **Nível / Tipo** | Sistema (E2E) / Funcional |
| **Técnica de projeto** | Transição de estados (Visitante deslogado $\rightarrow$ Login obrigatório $\rightarrow$ Checkout com carrinho preservado) |
| **Prioridade** | Alta |
| **Pré-condições** | Usuário não autenticado (`localStorage` limpo). |
| **Dados de teste** | Produto 1 com quantidade `3`; CEP `01310-100`; Login: `marina.silva@email.com` / Senha: `123456`. |

| Passo | Ação | Resultado esperado |
| :---: | :--- | :--- |
| 1 | Sem estar logado, acessar `/`, adicionar um produto ao carrinho, alterar a quantidade para `3` e simular o frete em `/cart`. | O sistema permite gerenciar o carrinho e exibe o aviso `.aviso-login-carrinho`. |
| 2 | Clicar em `Finalizar Compra` (`.btn-iniciar-compra`) ou tentar acessar `/checkout` diretamente pela URL. | O sistema bloqueia o acesso anônimo ao checkout, redireciona para `/login` e exibe `"Faça login para finalizar a compra do seu pedido"`. |
| 3 | Autenticar-se com `marina.silva@email.com` e senha `123456`. | O sistema redireciona automaticamente de volta para `/checkout` preservando os 3 itens no resumo do pedido. |
| 4 | Clicar em `Confirmar Pedido`. | O pedido é concluído e listado em `/profile/orders` com status `EM PROCESSAMENTO`. |

| Campo | Descrição |
| :--- | :--- |
| **Pós-condições** | Pedido registrado para a cliente autenticada e carrinho esvaziado após a compra. |
| **Automatizado?** | Sim; Cypress — `front-end/cypress/e2e/carrinho_deslogado_e_dashboard.cy.ts` (teste 1). |
| **Resultado da execução** | Aprovado; 18/10/2026; Responsável: Matheus Schalch; Sem defeitos. |

---

#### CT016 — Realizar compra com endereço e cartão pré-cadastrados e barrar valor divergente do total

| Campo | Descrição |
| :--- | :--- |
| **Requisitos rastreados** | `RF0033`, `RF0035`, `RF0036`, `RF0038` |
| **Caso de uso relacionado** | `CDU01 - Gerenciar Vendas Eletrônicas` |
| **Nível / Tipo** | Sistema (E2E) / Funcional |
| **Técnica de projeto** | Partição de equivalência e Tabela de decisão (1 cartão com valor divergente vs. valor exato do pedido) |
| **Prioridade** | Alta |
| **Pré-condições** | Cliente `marina.silva@email.com` autenticada (possui endereços e cartões pré-cadastrados na Migration V5). |
| **Dados de teste** | Valor inválido no cartão único: `15.00` (apenas o frete); Valor válido: total exato do pedido (`R$ 80,00`). |

| Passo | Ação | Resultado esperado |
| :---: | :--- | :--- |
| 1 | Adicionar uma peça ao carrinho e clicar em `Iniciar Compra` (`RF0033`). | Sistema carrega `/checkout` com endereço pré-cadastrado selecionado (`RF0035`) e cartão preferencial carregado (`RF0036`). |
| 2 | Alterar manualmente o valor do cartão único para `15.00` (menor que o total do pedido) e clicar em `Confirmar Pedido`. | O sistema bloqueia a operação exibindo alerta `"Operação não permitida"` e permanece em `/checkout`. |
| 3 | Restaurar o valor do cartão para o total exato da compra, clicar em `Confirmar Pedido` e, no modal de confirmação, clicar em `Autorizar Pagamento`. | O pedido é registrado com sucesso e exibido em `/profile/orders` com status `EM PROCESSAMENTO` (`RF0038`). |

| Campo | Descrição |
| :--- | :--- |
| **Pós-condições** | Pedido gravado com status inicial `EM PROCESSAMENTO`. |
| **Automatizado?** | Sim; Cypress — `front-end/cypress/e2e/compras_checkout.cy.ts` (teste 2 e teste 7). |
| **Resultado da execução** | Aprovado; 18/10/2026; Responsável: Matheus Schalch; Sem defeitos. |

---

#### CT017 — Realizar compra cadastrando novo endereço e novo cartão no checkout e incorporá-los ao perfil

| Campo | Descrição |
| :--- | :--- |
| **Requisitos rastreados** | `RF0035`, `RF0036`, `RN0023`, `RN0024`, `RN0025` |
| **Caso de uso relacionado** | `CDU01 - Gerenciar Vendas Eletrônicas` |
| **Nível / Tipo** | Sistema (E2E) / Funcional |
| **Técnica de projeto** | Partição de equivalência (incorporação opcional de endereço e cartão ao perfil durante o checkout) |
| **Prioridade** | Alta |
| **Pré-condições** | Cliente `lucas.mendes@email.com` autenticado e com item no checkout (`/checkout`). |
| **Dados de teste** | Novo Endereço: `Casa Praia <timestamp>`, `Casa`, CEP `11600-000`, `Avenida Beira Mar`, `777`, `Praia Grande`, `São Sebastião - SP`, opção `Salvar no perfil` marcada; Novo Cartão: `4111222233334444`, `LUCAS NOVO CARTAO`, `VISA`, CVV `888`, opção `Salvar no perfil` marcada. |

| Passo | Ação | Resultado esperado |
| :---: | :--- | :--- |
| 1 | No `/checkout`, clicar em `Novo Endereço`, preencher todos os campos obrigatórios (`RN0023`) mantendo marcada a opção de incorporar ao perfil e salvar. | O novo endereço é selecionado para a entrega do pedido (`RF0035`). |
| 2 | Na seção de pagamento, selecionar digitação de novo cartão, preencher os dados (`RN0024`, `RN0025`) e marcar o checkbox `.check-salvar-cartao-perfil` (`RF0036`). | Dados do novo cartão prontos para pagamento. |
| 3 | Confirmar e autorizar o pedido no modal de confirmação. | Pedido finalizado e redirecionado para `/profile/orders`. |
| 4 | Acessar `/profile` e verificar as abas `Endereços` e `Cartões`. | Tanto o endereço `Casa Praia` quanto o cartão `VISA 4111222233334444` aparecem salvos no perfil do cliente. |

| Campo | Descrição |
| :--- | :--- |
| **Pós-condições** | Pedido criado e novos endereço e cartão permanentemente associados ao cadastro do cliente. |
| **Automatizado?** | Sim; Cypress — `front-end/cypress/e2e/compras_checkout.cy.ts` (teste 3). |
| **Resultado da execução** | Aprovado; 18/10/2026; Responsável: Matheus Schalch; Sem defeitos. |

---

#### CT018 — Pagar com mais de um cartão de crédito respeitando o valor mínimo de R$ 10,00 por cartão

| Campo | Descrição |
| :--- | :--- |
| **Requisitos rastreados** | `RF0036`, `RN0034` |
| **Caso de uso relacionado** | `CDU01 - Gerenciar Vendas Eletrônicas` |
| **Nível / Tipo** | Sistema (E2E) / Funcional |
| **Técnica de projeto** | Análise de valor limite (valor por cartão $\ge \text{R\$ } 10,00$ em múltiplos cartões) |
| **Prioridade** | Alta |
| **Pré-condições** | Cliente `beatriz.rocha@email.com` autenticada em `/checkout` com 2 unidades da peça no carrinho. |
| **Dados de teste** | Cartão 1 (`MASTERCARD`): `R$ 30,00` ($\ge 10,00$); Cartão 2 (`VISA`): saldo restante (`Total - 30,00` $\ge 10,00$). |

| Passo | Ação | Resultado esperado |
| :---: | :--- | :--- |
| 1 | No `/checkout`, clicar no botão `Adicionar Outro Cartão` (`.btn-adicionar-outro-cartao`). | O sistema passa a exibir 2 blocos de cartão de crédito (`.card-pagamento-item`). |
| 2 | Preencher os dados do Cartão 1 com valor `30.00` e do Cartão 2 com o valor restante exato da compra (ambos $\ge \text{R\$ } 10,00$, cumprindo `RN0034`). | Soma dos dois cartões iguala o valor total do pedido. |
| 3 | Clicar em `Confirmar Pedido` e depois em `Autorizar Pagamento`. | A transação com múltiplos cartões é aprovada e o pedido é registrado com status `EM PROCESSAMENTO`. |

| Campo | Descrição |
| :--- | :--- |
| **Pós-condições** | Pedido salvo com dois registros vinculados em `pedido_pagamentos`. |
| **Automatizado?** | Sim; Cypress — `front-end/cypress/e2e/compras_checkout.cy.ts` (teste 4). |
| **Resultado da execução** | Aprovado; 18/10/2026; Responsável: Matheus Schalch; Sem defeitos. |

---

#### CT019 — Pagar com cartão de crédito combinado a cupons com saldo residual inferior a R$ 10,00

| Campo | Descrição |
| :--- | :--- |
| **Requisitos rastreados** | `RF0036`, `RF0037`, `RN0033`, `RN0035` |
| **Caso de uso relacionado** | `CDU01 - Gerenciar Vendas Eletrônicas` |
| **Nível / Tipo** | Sistema (E2E) / Funcional |
| **Técnica de projeto** | Análise de valor limite e Tabela de decisão (exceção da `RN0035` permitindo cartão $< \text{R\$ } 10,00$ quando há cupons aplicados) |
| **Prioridade** | Alta |
| **Pré-condições** | Cliente `marina.silva@email.com` autenticada em `/checkout`; cupons `TROCA-50` (R$ 50,00) e `CARAMELO20` (R$ 20,00) ativos. |
| **Dados de teste** | Subtotal + Frete: `R$ 79,50`; Cupom de Troca: `TROCA-50` (`-R$ 50,00`); Cupom Promocional: `CARAMELO20` (`-R$ 20,00`); Saldo residual no cartão: `R$ 9,50` ($< \text{R\$ } 10,00$). |

| Passo | Ação | Resultado esperado |
| :---: | :--- | :--- |
| 1 | No `/checkout`, informar o cupom de troca `TROCA-50` e clicar em `Aplicar`. | O cupom de R$ 50,00 é adicionado à lista de cupons de troca aplicados. |
| 2 | Informar o cupom promocional `CARAMELO20` e clicar em `Aplicar` (`RN0033`). | O desconto promocional de R$ 20,00 é aplicado, reduzindo o saldo restante para um valor inferior a R$ 10,00. |
| 3 | Verificar o valor calculado para o cartão de crédito, clicar em `Confirmar Pedido` e autorizar pagamento. | O sistema permite o pagamento no cartão com valor inferior a R$ 10,00 por tratar-se de saldo residual de cupons (`RN0035`) e registra o pedido em `EM PROCESSAMENTO`. |

| Campo | Descrição |
| :--- | :--- |
| **Pós-condições** | Pedido criado com sucesso e cupom `TROCA-50` inativado no banco. |
| **Automatizado?** | Sim; Cypress — `front-end/cypress/e2e/compras_checkout.cy.ts` (teste 5). |
| **Resultado da execução** | Aprovado; 18/10/2026; Responsável: Matheus Schalch; Sem defeitos. |

---

#### CT020 — Utilizar cupom de troca superior ao total da compra (gerando troco) e bloquear cupom desnecessário

| Campo | Descrição |
| :--- | :--- |
| **Requisitos rastreados** | `RF0037`, `RF0038`, `RN0036`, `RNF0012` |
| **Caso de uso relacionado** | `CDU01 - Gerenciar Vendas Eletrônicas` |
| **Nível / Tipo** | Sistema (E2E) / Funcional |
| **Técnica de projeto** | Tabela de decisão (soma de cupons $>$ total da compra + tentativa de adição de cupom excedente) |
| **Prioridade** | Alta |
| **Pré-condições** | Cliente `lucas.mendes@email.com` autenticado em `/checkout` com 1 peça no carrinho; cupons `TROCA-200` (R$ 200,00) e `TROCA-15` (R$ 15,00) ativos. |
| **Dados de teste** | Cupom 1: `TROCA-200` (cobre 100% da compra e gera troco); Cupom 2 (excedente): `TROCA-15`. |

| Passo | Ação | Resultado esperado |
| :---: | :--- | :--- |
| 1 | No `/checkout`, digitar o código `TROCA-200` e clicar em `Aplicar`. | O cupom é aplicado, o saldo a pagar zera e o sistema exibe o alerta `.alert-troco-cupom` informando que será gerado um novo cupom de troca com o valor da diferença (`RN0036`). |
| 2 | Tentar aplicar um segundo cupom de troca (`TROCA-15`) quando a compra já está 100% coberta. | O sistema bloqueia a inclusão exibindo `.alert-cupom-troca` informando que o cupom é desnecessário (`RN0036`). |
| 3 | Confirmar e autorizar o pedido sem necessidade de cartão de crédito. | O pedido é finalizado com status `EM PROCESSAMENTO` e um novo cupom `TROCA-XXXXXXXX` com o valor residual é gerado para o cliente no banco. |

| Campo | Descrição |
| :--- | :--- |
| **Pós-condições** | Cupom `TROCA-200` inativado, novo cupom de troco gerado e ativo para o cliente, e `TROCA-15` preservado intacto. |
| **Automatizado?** | Sim; Cypress — `front-end/cypress/e2e/compras_checkout.cy.ts` (teste 6). |
| **Resultado da execução** | Aprovado; 18/10/2026; Responsável: Matheus Schalch; Sem defeitos. |

---

#### CT021 — Validar KPIs, gráfico de linhas e filtros por período e categorias no Dashboard Analítico

| Campo | Descrição |
| :--- | :--- |
| **Requisitos rastreados** | `RF0055`, `RF0056`, `RN0065`, `RNF0011`, `RNF0051` |
| **Caso de uso relacionado** | `UC07 - Consultar Dashboard e Relatórios` |
| **Nível / Tipo** | Sistema (E2E) / Funcional e Não funcional |
| **Técnica de projeto** | Partição de equivalência (filtragem por subconjunto de categorias e intervalo de datas válido) |
| **Prioridade** | Média |
| **Pré-condições** | Administrador autenticado (`cy.loginAdmin()`) e pedidos históricos populados pela Migration V9. |
| **Dados de teste** | Categorias: `Bowls`, `Pratos`, `Xícaras`, `Vasos`, `Travessas`; Filtro específico: apenas `Vasos`. |

| Passo | Ação | Resultado esperado |
| :---: | :--- | :--- |
| 1 | Acessar a rota `/dashboard`. | A página carrega em menos de 1 segundo (`RNF0011`) exibindo "Painel Analítico de Vendas" e os 4 cards de KPI (`Vendas Totais`, `Pedidos Realizados`, `Novos Clientes` e `Trocas Solicitadas`). |
| 2 | Verificar a presença dos seletores de data, botões de categoria (`Bowls`, `Pratos`, `Xícaras`, `Vasos`, `Travessas`) e do gráfico Recharts. | O componente `svg.recharts-surface` é renderizado com linhas por categoria, legendas e tooltips em moeda (`RNF0051`). |
| 3 | Clicar em `Limpar`, selecionar apenas a categoria `Vasos` e clicar em `Aplicar Filtros`. | O gráfico é atualizado exibindo a série histórica filtrada para a categoria `Vasos`. |
| 4 | Clicar em `Selecionar Todas` e `Aplicar Filtros`. | Todas as 5 categorias voltam a ser exibidas no gráfico. |

| Campo | Descrição |
| :--- | :--- |
| **Pós-condições** | Dados analíticos exibidos com consistência em relação aos pedidos válidos da base. |
| **Automatizado?** | Sim; Cypress — `front-end/cypress/e2e/carrinho_deslogado_e_dashboard.cy.ts` (teste 2). |
| **Resultado da execução** | Aprovado; 18/10/2026; Responsável: Matheus Schalch; Sem defeitos. |

---

#### CT022 — Impedir filtragem no Dashboard quando a data final for anterior à data inicial

| Campo | Descrição |
| :--- | :--- |
| **Requisitos rastreados** | `RF0056` |
| **Caso de uso relacionado** | `UC07 - Consultar Dashboard e Relatórios` |
| **Nível / Tipo** | Sistema / Funcional |
| **Técnica de projeto** | Análise de valor limite / Dados inválidos (`dataFim < dataInicio`) |
| **Prioridade** | Média |
| **Pré-condições** | Administrador autenticado na tela `/dashboard`. |
| **Dados de teste** | Data de Início: `2026-10-15`; Data de Fim: `2026-10-01`. |

| Passo | Ação | Resultado esperado |
| :---: | :--- | :--- |
| 1 | Na tela `/dashboard`, informar `2026-10-15` como Data de Início e `2026-10-01` como Data de Fim. | Datas preenchidas nos campos de filtro. |
| 2 | Submeter o formulário clicando em `Aplicar Filtros`. | O sistema impede a requisição inválida e exibe o alerta `"A data de fim não pode ser anterior à data de início (RF0056)."` |

| Campo | Descrição |
| :--- | :--- |
| **Pós-condições** | O gráfico permanece íntegro sem disparar consulta inconsistente ao back-end. |
| **Automatizado?** | Não; execução manual. |
| **Resultado da execução** | Aprovado; 18/10/2026; Responsável: Matheus Schalch; Sem defeitos. |

---

## 8. MATRIZ DE RASTREABILIDADE

| Requisito | Descrição resumida | Casos de teste | Situação |
| :--- | :--- | :--- | :--- |
| **RF0021** | Cadastrar cliente no sistema | CT001, CT002, CT003, CT004 | Coberto |
| **RF0022** | Alterar dados cadastrais de cliente | CT005 | Coberto |
| **RF0023** | Inativar e reativar cadastro de cliente | CT007 | Coberto |
| **RF0024** | Consultar clientes com base em filtro definido pelo usuário | CT005 | Coberto |
| **RF0025** | Consultar todas as transações realizadas pelo cliente | CT008 | Coberto |
| **RF0026** | Associar múltiplos endereços de entrega identificados por frase curta | CT009, CT010 | Coberto |
| **RF0027** | Associar múltiplos cartões de crédito ao cliente (incluindo preferencial) | CT011, CT012 | Coberto |
| **RF0028** | Alterar apenas a senha do cliente sem alterar demais dados | CT006 | Coberto |
| **RF0031** | Gerenciar itens no carrinho de compras (adicionar, alterar, visualizar) | CT013, CT014, CT015 | Coberto |
| **RF0032** | Definir e editar a quantidade de itens no momento da adição e no carrinho | CT013, CT014 | Coberto |
| **RF0033** | Iniciar e realizar o processo de compra a partir do carrinho | CT015, CT016 | Coberto |
| **RF0034** | Calcular o valor do frete com base no CEP/endereço e peso das peças | CT013 | Coberto |
| **RF0035** | Selecionar ou cadastrar novo endereço de entrega durante a compra (incorporando ao perfil) | CT016, CT017 | Coberto |
| **RF0036** | Selecionar ou cadastrar cartões de crédito para pagamento na compra (incorporando ao perfil) | CT016, CT017, CT018, CT019 | Coberto |
| **RF0037** | Utilizar cupons promocionais e de troca como forma de pagamento | CT019, CT020 | Coberto |
| **RF0038** | Finalizar compra registrando o pedido com status inicial `EM PROCESSAMENTO` | CT015, CT016, CT020 | Coberto |
| **RF0055** | Consultar histórico de vendas em gráfico de linhas no Dashboard | CT021 | Coberto |
| **RF0056** | Filtrar análise de vendas por período de datas e categorias de produtos | CT021, CT022 | Coberto |
| **RN0021** | Obrigatoriedade de ao menos um endereço de cobrança no cadastro do cliente | CT001, CT004 | Coberto |
| **RN0022** | Obrigatoriedade de ao menos um endereço de entrega no cadastro do cliente | CT001, CT004 | Coberto |
| **RN0023** | Composição obrigatória dos campos de endereço (residência, logradouro, nº, bairro, CEP, cidade, UF) | CT001, CT009, CT010, CT017 | Coberto |
| **RN0024** | Dados obrigatórios do cartão de crédito (número, nome impresso, bandeira e CVV) | CT011, CT012, CT017 | Coberto |
| **RN0025** | Validação de bandeira do cartão vinculada às bandeiras permitidas pelo sistema | CT011, CT012, CT017 | Coberto |
| **RN0026** | Obrigatoriedade dos dados cadastrais do cliente (gênero, nome, nascimento, CPF, telefone, e-mail, senha) | CT001, CT004 | Coberto |
| **RN0031** | Validação de disponibilidade de estoque ao definir quantidade de itens no carrinho | CT013, CT014 | Coberto |
| **RN0032** | Bloqueio/alerta quando a quantidade selecionada superar o estoque disponível | CT014 | Coberto |
| **RN0033** | Permissão de apenas um cupom promocional por compra | CT019 | Coberto |
| **RN0034** | Valor mínimo de R$ 10,00 por cartão em pagamentos com múltiplos cartões de crédito | CT018 | Coberto |
| **RN0035** | Permissão de pagamento em cartão inferior a R$ 10,00 para cobrir saldo residual após uso de cupons | CT019 | Coberto |
| **RN0036** | Geração de cupom de troca para a diferença quando cupons superarem o total e bloqueio de cupons desnecessários | CT020 | Coberto |
| **RN0065** | Consolidação de vendas no Dashboard considerando apenas pedidos válidos | CT021 | Coberto |
| **RNF0011** | Tempo de resposta das consultas inferior a 1 segundo | CT021 | Coberto |
| **RNF0012** | Registro de log de auditoria (data, hora, usuário e detalhes) nas operações de escrita | CT001, CT005, CT007, CT020 | Coberto |
| **RNF0031** | Exigência de senha forte (mín. 8 caracteres, maiúscula, minúscula e especial) e criptografia | CT003, CT006 | Coberto |
| **RNF0032** | Exigência de confirmação de senha por dupla digitação | CT002, CT006 | Coberto |
| **RNF0034** | Inclusão de novos endereços sem necessidade de alterar demais dados cadastrais | CT009 | Coberto |
| **RNF0035** | Atribuição automática de código único (`CLI-`) para todo cliente cadastrado | CT001 | Coberto |
| **RNF0051** | Exibição de gráficos interativos com tooltips formatados em moeda (R$) e legendas | CT021 | Coberto |

---

## 9. CRONOGRAMA E RESPONSABILIDADES

*(Cálculo PERT utilizado: $E = \frac{O + 4M + P}{6}$, alinhado à planilha `estimativa_prazos_final.csv` do projeto).*

| Atividade | Responsável | O | M | P | E (h) | Prazo |
| :--- | :--- | :---: | :---: :---: | :---: | :---: | :---: |
| Projeto dos casos de teste | Matheus Schalch | 1,5 | 3,0 | 4,5 | 3,0 | 12/10 |
| Preparação do ambiente e da massa de dados (Flyway V5, V6, V9 e reset) | Matheus Schalch | 1,5 | 3,0 | 4,5 | 3,0 | 14/10 |
| Implementação dos testes automatizados (Suíte Cypress E2E) | Matheus Schalch | 6,5 | 13,0 | 19,5 | 13,0 | 17/10 |
| Execução e registro de resultados | Matheus Schalch | 1,0 | 2,0 | 3,0 | 2,0 | 18/10 |
| Reteste e regressão | Matheus Schalch | 1,0 | 2,0 | 3,0 | 2,0 | 18/10 |
| **TOTAL** | — | **11,5** | **23,0** | **34,5** | **23,0** | — |

---

## 10. RISCOS E CONTINGÊNCIAS

| Risco | Probabilidade | Impacto | Ação de contingência |
| :--- | :---: | :---: | :--- |
| **Inativação de cupons de troca (`TROCA-50`, `TROCA-200`) após a primeira execução dos testes E2E, causando falha na reexecução** | Alta | Alto | Implementado endpoint dedicado `POST /api/cupons/reset-testes` invocado automaticamente no bloco `beforeEach` do Cypress para restaurar o status ativo dos cupons antes de cada teste. |
| **Conflito de unicidade de CPF e E-mail (`ValidarCpfUnicoStrategy` / `ValidarEmailUnicoStrategy`) em execuções repetidas de cadastro de cliente** | Alta | Médio | Criada função utilitária `gerarCpfValido()` em `cypress/support/commands.ts` combinada a `Date.now()` no e-mail para gerar massas inéditas e válidas a cada execução. |
| **Ambiguidade no DRS entre `RN0034` e `RF0036` sobre edição manual do valor quando apenas 1 cartão é utilizado sem cupom** | Média | Médio | Registrada e comunicada ao professor: o sistema preenche automaticamente o valor total no cartão único e bloqueia submissões caso o usuário altere o valor para um montante divergente do total da compra (validado no `CT016`). |
| **Ambiguidade no DRS entre `RN0028` (baixa de estoque ao sair de `EM PROCESSAMENTO`) e `RN0044` (bloqueio temporário no carrinho)** | Baixa | Médio | Documentada na Especificação de Caso de Uso (`CDU01`) e comunicada ao professor: nesta entrega, valida-se a disponibilidade em estoque na criação do pedido (`ValidarEstoquePedidoStrategy`), ficando a baixa definitiva pós-aprovação fora do escopo atual. |
| **Indisponibilidade temporária da API externa ViaCEP durante os testes de frete** | Baixa | Médio | Implementado cálculo de contingência (fallback local por faixa de CEP e peso em `shippingService.ts`) garantindo que a simulação de frete no carrinho e checkout não interrompa a suíte E2E. |

---

## 11. GESTÃO DE DEFEITOS

### 11.1 Classificação de severidade

| Severidade | Critério |
| :--- | :--- |
| **Crítica** | Impede o uso de uma funcionalidade essencial, sem alternativa de contorno |
| **Alta** | Funcionalidade com resultado incorreto, com alternativa de contorno |
| **Média** | Falha em regra secundária ou mensagem incorreta |
| **Baixa** | Problema cosmético (layout, texto, alinhamento) |

### 11.2 Registro de defeitos

*Os defeitos identificados durante o desenvolvimento e execução da suíte Cypress são registrados e acompanhados no quadro Kanban / GitHub Issues do repositório do projeto e sintetizados na tabela abaixo:*

| ID | Caso de teste | Descrição | Severidade | Situação |
| :--- | :--- | :--- | :---: | :--- |
| **DF001** | CT016 | **Comportamento observado:** Ao utilizar apenas 1 cartão de crédito no checkout, era possível digitar manualmente apenas o valor do frete (`R$ 15,00`) e submeter o formulário.<br>**Comportamento esperado:** O sistema deve exigir que o cartão único cubra 100% do saldo total da compra, exibindo alerta `"Operação não permitida"` caso o valor seja alterado. | Alta | Corrigido |
| **DF002** | CT019, CT020 | **Comportamento observado:** Na segunda execução consecutiva da suíte Cypress, os testes de cupom falhavam porque `TROCA-50` e `TROCA-200` haviam sido inativados no banco na primeira execução.<br>**Comportamento esperado:** Os cupons de teste devem estar ativos no início de cada bateria automatizada (solucionado via endpoint `/api/cupons/reset-testes`). | Média | Corrigido |
| **DF003** | CT015 | **Comportamento observado:** Usuário deslogado que clicava em "Finalizar Compra" no carrinho fazia login mas era redirecionado para a Home (`/`) em vez de retornar ao `/checkout`.<br>**Comportamento esperado:** Após autenticar-se a partir do fluxo de compra, o cliente deve ser redirecionado diretamente para `/checkout` com todos os itens do carrinho preservados. | Alta | Corrigido |

---

## 12. ENTREGÁVEIS

- Este Plano de Testes preenchido (`Template_Plano_de_Testes.docx`).
- Scripts de testes automatizados E2E em Cypress versionados no repositório do grupo:
  - `front-end/cypress/e2e/clientes.cy.ts`
  - `front-end/cypress/e2e/regras_negocio_cliente.cy.ts`
  - `front-end/cypress/e2e/compras_checkout.cy.ts`
  - `front-end/cypress/e2e/carrinho_deslogado_e_dashboard.cy.ts`
  - `front-end/cypress/support/commands.ts`
- Scripts de preparação de massa de dados versionados via Flyway (`V5__seed_clientes_e_pecas.sql`, `V6__create_table_logs_transacao_e_novos_cupons.sql` e `V9__seed_pedidos_dashboard.sql`).
- Evidências de execução (relatório do Cypress Test Runner, capturas de tela e demonstração em vídeo/apresentação).
