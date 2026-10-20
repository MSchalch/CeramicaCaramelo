# Especificação do Caso de Uso de Gestão de Vendas

**Nome do Caso de Uso:** CDU01 - Gerenciar Vendas Eletrônicas
**Objetivo:** Gerenciar o fluxo completo de uma compra eletrônica, contemplando a montagem do carrinho, controle de estoque, pagamento, rastreamento de status de entrega e processo de troca.
**Descrição:** Este caso de uso descreve a interação do Cliente e do Administrador com o sistema ao longo do ciclo de vida de uma venda de cerâmicas. O processo abrange desde a inserção das peças no carrinho e bloqueio temporário de estoque, passando pelo checkout, até a tramitação dos estados do pedido (processamento, transporte, entrega) e a gestão de devoluções (emissão de cupom de troca e reentrada de estoque).

**Requisitos Funcionais:**
- RF0031 Gerenciar carrinho
- RF0032 Definir quantidade
- RF0033 Realizar compra
- RF0034 Calcular frete
- RF0035 Selecionar endereço
- RF0036 Selecionar pagamento
- RF0037 Uso de cupom
- RF0038 Finalizar Compra
- RF0039 Despachar produtos
- RF0040 Produtos entregues
- RF0041 Solicitar troca
- RF0042 Autorizar trocas
- RF0043 Visualização de trocas
- RF0044 Confirmar recebimento de itens
- RF0045 Gerar cupom de troca
- RF0053 Baixa em estoque
- RF0054 Reentrada em estoque

**Tipo de Caso de Uso:** Concreto.

**Atores:**
- Cliente (Primário)
- Administrador (Secundário)

**Pré-condições:**
- O Cliente deve estar autenticado no sistema.
- Os itens adicionados ao carrinho devem possuir quantidade em estoque maior que zero (RN0031, RN0061).

**Fluxo Principal:**
P1. O Cliente acessa o carrinho de compras.
P2. O sistema exibe os itens adicionados e o subtotal.
P3. O Cliente ajusta a quantidade dos itens desejados (RF0032) [Fluxo de Exceção E2].
P4. O sistema valida a disponibilidade, realiza o bloqueio temporário dos itens no estoque (RN0044) e inicia um timer de expiração [Fluxo Alternativo FA1].
P5. O Cliente informa ou seleciona o endereço de entrega (RF0035).
P6. O sistema calcula o valor do frete (RF0034).
P7. O Cliente seleciona a forma de pagamento e insere cupons promocionais ou de troca, se houver (RF0036, RF0037, RN0033, RN0035).
P8. O Cliente confirma a compra (RF0038).
P9. O sistema registra o pedido e atribui o status inicial **EM PROCESSAMENTO**.
P10. O sistema valida os dados do pagamento junto à operadora do cartão e verifica a integridade dos cupons (RN0037) [Fluxo de Exceção E1].
P11. O sistema aprova o pagamento, e altera o status do pedido para **APROVADA** (RN0038).
P12. O sistema retira o bloqueio temporário e efetua a baixa definitiva no estoque das peças (RF0053, RN0028).
P13. O Administrador visualiza o pedido, prepara o pacote e despacha os produtos (RF0039).
P14. O Administrador altera o status do pedido para **EM TRANSPORTE** (RN0039).
P15. O Administrador recebe a confirmação logística e finaliza o envio no sistema (RF0040).
P16. O Administrador altera o status do pedido para **ENTREGUE** (RN0040) [Fluxo Alternativo FA2].
O caso de uso é encerrado.

**Fluxos Alternativos:**
*FA1 - Remoção de item por expiração de prazo*
Inicia no passo P4.
FA1.1. O sistema (Ator) identifica que o tempo limite do bloqueio temporário no carrinho expirou (RN0045).
FA1.2. O sistema remove os itens bloqueados do carrinho e os devolve ao estoque disponível.
FA1.3. O sistema notifica o Cliente sobre a expiração da reserva.
O fluxo retorna ao passo P1.

*FA2 - Processo de Troca de Peças*
Inicia após o passo P16 (Condição: O pedido está ENTREGUE).
FA2.1. O Cliente acessa seu histórico e solicita a troca de um ou mais itens (RF0041).
FA2.2. O sistema gera a solicitação e o Cliente altera o status do pedido para **EM TROCA** (RN0041).
FA2.3. O Administrador visualiza a justificativa e autoriza a solicitação de devolução (RF0042).
FA2.4. O Administrador altera o status para **TROCA AUTORIZADA** (RN0046).
FA2.5. O Cliente realiza o envio físico das peças e o Administrador confirma o recebimento no sistema (RF0044).
FA2.6. O Administrador altera o status final da solicitação para **TROCADO** (RN0042).
FA2.7. O sistema gera automaticamente um cupom de troca no valor correspondente à peça devolvida e o vincula ao perfil do Cliente (RF0045).
FA2.8. O Administrador avalia a integridade da cerâmica devolvida e realiza a reentrada no estoque, se aplicável (RF0054).
O caso de uso é encerrado.

**Fluxos de Exceção:**
*E1 - Pagamento Reprovado*
Inicia no passo P10.
E1.1. A operadora de cartão rejeita a transação financeira ou a validação de cupons falha.
E1.2. O sistema altera o status do pedido para **REPROVADA** (RN0038).
E1.3. O sistema cancela o bloqueio temporário e realiza a liberação dos itens de volta ao estoque disponível (RN0028).
E1.4. O sistema notifica o Cliente sobre a falha no processamento.
O caso de uso é encerrado.

*E2 - Falta de Estoque na Definição de Quantidade*
Inicia no passo P3.
E2.1. O Cliente seleciona uma quantidade que supera o limite em estoque do produto (RN0031).
E2.2. O sistema exibe um alerta bloqueando a ação e ajusta ou remove o item automaticamente (RN0032).
O fluxo retorna ao passo P3.

**Protótipos de Tela:**
*(Nota: Substituir pelas imagens reais dos protótipos na entrega)*
1. **Tela de Carrinho:**
   - Elemento: `Input numérico` | Tipo: Campo de entrada | Status: Editável | Comportamento: Define a quantidade de peças (Passo P3).
   - Elemento: `Botão Continuar` | Tipo: Botão | Status: Habilitado se houver estoque | Comportamento: Avança para o Checkout (Passo P4).
2. **Tela de Checkout:**
   - Elemento: `Radio Endereço` | Tipo: Seleção | Status: Editável | Comportamento: Define destino da entrega (Passo P5).
   - Elemento: `Input Cupom` | Tipo: Texto | Status: Editável | Comportamento: Aplica desconto ao total (Passo P7).
   - Elemento: `Botão Finalizar` | Tipo: Botão | Status: Habilitado | Comportamento: Confirma a compra (Passo P8).
3. **Painel do Administrador (Gestão de Pedidos):**
   - Elemento: `Select de Status` | Tipo: Lista Suspensa | Status: Editável | Comportamento: Altera status para TRANSPORTE/ENTREGUE (Passos P14, P16).

**Pós-condições:**
- O pedido fica registrado de forma definitiva no sistema sob o status APROVADA, ENTREGUE, REPROVADA ou TROCADO.
- O controle de estoque das peças de cerâmica é atualizado (baixa definitiva ou reentrada).
- Se houver devolução, um cupom de troca ativo é atrelado ao cadastro do Cliente.

**Requisitos Não Funcionais:**
- RNF0012 Log de transação (Operações de escrita como registro de pedido e mudança de status devem registrar data, hora e usuário).
- RNF0042 Itens retirados (Reinserção de peças bloqueadas temporariamente).

**Ponto de Extensão:**
- Não aplicável neste fluxo.

**Critérios de Aceite:**
- Nenhuma compra pode ser concretizada se a validação de quantidade exceder o estoque atual disponível da cerâmica.
- A transição obrigatória dos status (EM PROCESSAMENTO -> APROVADA -> EM TRANSPORTE -> ENTREGUE) deve ser rigorosamente respeitada, com os atores corretos sendo os responsáveis por acionar o evento.
- O estoque não deve sofrer baixa permanente se a compra for "REPROVADA".

**Observações:**
- *Interpretação do DRS:* O documento especifica que a baixa no estoque apenas ocorre quando a compra sair do status EM PROCESSAMENTO (RN0028). Sendo assim, o fluxo adota o comportamento de que o estoque sofre apenas um "bloqueio temporário" (RN0044) até a aprovação financeira efetiva.
- *Prioridade:* Desenvolvimento crítico (Alta), visto que compõe a atividade fim do e-commerce.

**Referências:**
- Documento de Requisitos de Software (DRS) - Caramelo Cerâmicas.
- Documento de Visão de Projeto (DVP).
