# Avaliação — Engenharia de Software
**Sistema Integrado de Gestão de Farmácia — MVP Definido pelo Estudante**

Aluno: Gabriel Novais Corsini  
RA: 25000766  
Data: 25/03/2026 

---

# 1. Definição do MVP
O Sistema Integrado de Gestão "Saúde & Vida", esta aqui para resolver o problema com a falta de gerenciamento de estoque e vendas.

## Saúde & Vida traz dentro do sistema

#### -Vendas presencial:
Registra vendas à vista ou a prazo;

#### -Gestão de estoque:
Registra as quantidades dos produtos dentro do estoque em tempo real;

#### -Segurança da venda de medicamento controlado:
Exigi uma validação do perfil do farmacêutico para liberar a venda;

#### -Cadastro de cliente:
Registra o cliente dentro do sistema para ver os historicos de compra e permitir vendas a prazo;

#### -Financeiro:
Registra automático em contas a receber e lançamento manuel em contas a pagar;

#### -Relatorio de falta:
Lista de produtos abaixo do estoque mínimo para evitar falta de mercadoria;

## O que esta fora do sistema

- Por que você fez essas escolhas  

Exemplo de início:  
> “Meu MVP cobre o processo de venda desde a identificação/cadastro do cliente até a emissão do comprovante, incluindo tratamento de estoque insuficiente.”

---

# 2. Regras de Negócio 


**RN01 —** Vendas de Controlados
O sistema permite as vendas de remedios controlados só com a receita do farmacêutico.

**RN02 —** Vendas a Prazo
O cliente não pode fazer pagamentos a prazo se o registro dele estiver com um pagamento pedente.

**RN03 —** Gerenciamento de Estoque
O sistema deve modificar o estoque em toda venda feita ou a chegada de novas mercadorias.

**RN04 —** Estoque Mínimo
O sistema deve bloquear a venda de um produto que não esta no estoque.

**RN05 —** Registro de Caixa
O sistema deve gerar um registro imediato de entrada a vendas a vista, enquanto vendas a prazo geram títulos no financeiro.


---

# 3. Requisitos Funcionais 


**RF01 —** Alerta de Estoque
O sistema deve alertar o gerente quando um produto atingir um limite mínimo no estoque.

**RF02 —** Procura Rapida
O sistema permite fazer uma busca atraves do nome, código de barras ou fabricante.

**RF03 —**  Cadastro do Cliente
Realizar o cadastro do cliente no momento da venda.

**RF04 —** Verificação do historico de venda
Verifica o historico de venda do cliente.

**RF05 —** Controle do Status do cliente
Controlar o status de títulos como aberto, pago, atrasado no módulo financeiro.

**RF06 —** Registro do Contas a Pagar
O registrar o valor correspondente em contas a pagar, com datas de vencimento e status aberto, pago, atrasado.

**RF07 —** Relatorio de Produtos
Gerar relatórios de produtos mais vendidos e itens sem giro.

**RF08 —**  Cadastro de produto
O sistema pode cadastrar novos produtos, colocando o valor, codigo do fabricante e se ele precisa de receita.



---

# 🛡 4. Requisitos Não Funcionais
Liste os RNFs do sistema conforme seu MVP.

**RNF01 —** Usabilidade
O sistema deve pedir Login e senha.

**RNF02 —** Tempo Inativo 
O sistema deve sair do usuario depois de 15 minutos sem nenhum acesso.

**RNF03 —**  Segurança 
O sistema deve implementar controle de acesso baseado em perfis.

**RNF04 —** Integridade
Operações que envolvem estoque e financeiro devem utilizar transações de banco de dados para evitar dados parciais.


---

# 5. Casos de Uso 
### UC01- Realizar Venda
### UC02: Consultar Estoque
### UC03: Autenticar Usuário
### UC04: Registrar Conta a Receber
### UC05: Validar Receita Médica
### UC06: Cadastrar Cliente 
### UC07: Aplicar Desconto Especial 
### UC08: Registrar Compra de Fornecedor
### UC09: Gerar Relatório de Desempenho
### UC10: Ajustar Estoque Manualmente
<img width="702" height="595" alt="image" src="https://github.com/user-attachments/assets/67fcf8d7-2aa5-43d2-a0b7-6959c9647838" />


---

# 6. Documentação dos Casos de Uso

## **UC01 — Realizar Venda**
**Ator(es):*Atendente*  
**Descrição:*Registro rápido de saída de produtos através da busca no catálogo, verificação de disponibilidade e processamento do pagamento final.*  
**Pré-condições:*Atendente logado; Terminal de venda operável.*  
**Pós-condições:*Cupom de venda emitido; Estoque da unidade atualizado; Registro de entrada financeira (Caixa ou Contas a Receber).*  

### Fluxo Principal
1. O Atendente pesquisa o produto (por nome ou código de barras).
2. O Atendente informa a quantidade e o sistema valida o estoque (UC02). 
3.  O Atendente confirma os itens e o valor total calculado pelo sistema.
4.  O Atendente seleciona a forma de pagamento e finaliza a operação. 

### Fluxos Alternativos / Exceções
- FA01 — Cliente com pendência: Se a venda for a prazo e o cliente tiver débitos, o sistema bloqueia a venda conforme a RN02.
- FA02 — Cadastro de Cliente: Se o cliente for novo e desejar comprar a prazo, o sistema abre a tela de cadastro (UC06).  


### Relacionamentos
- **Include:** UC02 (Consultar Estoque), UC03 (Autenticar Usuário).
- **Extend:** UC04 (Registrar Conta a Receber), UC05 (Validar Receita), UC06 (Cadastrar Cliente).

<img width="602" height="596" alt="image" src="https://github.com/user-attachments/assets/6c498cc3-f9da-4ffc-9e1c-84d995906776" />


## **UC02 —  Consultar Estoque**
**Ator(es):*Atendente, Gerente*  
**Descrição:*Permite a visualização em tempo real da quantidade disponível de um produto específico na unidade atual.*  
**Pré-condições:*Usuário autenticado; Produto previamente cadastrado no sistema.*  
**Pós-condições:*Informação de saldo exibida na tela (não altera dados).*  

### Fluxo Principal
1. O Usuário acessa a função de consulta ou bipa o código de barras do produto.
2. O Sistema localiza o item no banco de dados da unidade. 
3.  O Sistema exibe a descrição, o preço atualizado e a quantidade disponível em prateleira.
4.  O Usuário visualiza a informação e encerra a consulta.

### Fluxos Alternativos / Exceções
- FA01 — Produto não encontrado: Se o código ou nome não existir, o sistema exibe a mensagem "Produto não cadastrado".
- FA02 — Saldo Zero: Se a quantidade for igual a 0, o sistema destaca a informação em vermelho para alertar sobre a ruptura de estoque.


### Relacionamentos
- **Include:** UC03 (Autenticar Usuário).
- **Extend:** (Não se aplica).

<img width="702" height="491" alt="image" src="https://github.com/user-attachments/assets/53478bbe-6d77-4b8a-9803-f7113b9cfb4c" />


## **UC03 —  Autenticar Usuário**
**Ator(es):*Atendente, Farmacêutico, Gerente, Financeiro.*  
**Descrição:*Valida as credenciais de acesso (usuário e senha) para permitir a utilização das funcionalidades do sistema conforme o perfil do colaborador.*  
**Pré-condições:*Usuário previamente cadastrado no sistema pela administração.*  
**Pós-condições:*Sessão do usuário iniciada; Acesso liberado às telas permitidas para o seu cargo.*  

### Fluxo Principal
1. O Usuário insere seu identificador (login) e senha na tela inicial do sistema.
2.O Sistema criptografa a senha inserida e compara com os dados do banco.
3.O Sistema valida o perfil de acesso do colaborador (ex: Atendente ou Gerente).
4.O Sistema libera o menu principal com as funcionalidades específicas daquele perfil.

### Fluxos Alternativos / Exceções
- FA01 — Credenciais Inválidas: Se o login ou a senha estiverem incorretos, o sistema exibe a mensagem "Usuário ou Senha incorretos" e bloqueia o acesso.
- FA02 —  Usuário Inativo: Se o colaborador estiver desligado ou bloqueado pela matriz, o sistema impede a entrada e solicita contato com o Administrador.



### Relacionamentos
- **Include:** (Não se aplica).
- **Extend:** (Não se aplica).

<img width="606" height="520" alt="image" src="https://github.com/user-attachments/assets/3ca34288-3e3f-4287-a3ef-8a0690d56783" />

## **UC04 —  Registrar Conta a Receber**
**Ator(es):*Atendente (dispara o registro), Financeiro (gerencia o título).*  
**Descrição:*Cria um título de cobrança no sistema vinculado ao cadastro do cliente, definindo valor, data de vencimento e status da dívida.*  
**Pré-condições:*Venda finalizada na modalidade "A Prazo"; Cliente devidamente cadastrado (UC06) e sem pendências (RN02).*  
**Pós-condições:*Lançamento financeiro gerado com status "Aberta"; Histórico do cliente atualizado com o novo débito.*  

### Fluxo Principal
1. O Sistema identifica que a forma de pagamento selecionada no UC01 foi "A Prazo".
2.O Sistema recupera o valor total da venda e os dados do cliente vinculado.
3.O Sistema gera um título financeiro com a data de vencimento (padrão da rede ou acordada com o cliente).
4.O Sistema registra o lançamento no módulo financeiro com o status inicial "Aberta".

### Fluxos Alternativos / Exceções
- FA01 — Limite de Crédito Excedido: Se o valor da compra somado aos débitos atuais do cliente ultrapassar o limite permitido, o sistema bloqueia o registro e solicita outra forma de pagamento.
- FA02 — Erro de Registro: Caso o sistema não consiga gravar o título, a venda é estornada para evitar que o produto saia sem o devido lançamento financeiro.




### Relacionamentos
- **Include:** UC03 (Autenticar Usuário).
- **Extend:** (Não se aplica).

<img width="451" height="541" alt="image" src="https://github.com/user-attachments/assets/655df341-eb51-4815-8a0b-501787835113" />

## **UC05 —  Validar Receita Médica**
**Ator(es):*Farmacêutico (Principal), Atendente (Solicitante).*  
**Descrição:*Processo de conferência obrigatória de dados da receita médica (CRM do médico, data de emissão e paciente) para liberar a venda de medicamentos retidos ou controlados.*  
**Pré-condições:*Medicamento do tipo "Controlado" adicionado ao carrinho no UC01; Farmacêutico presente e autenticado no sistema.*  
**Pós-condições:*Item liberado para venda; Dados da receita vinculados ao registro da operação para fins de fiscalização.*  

### Fluxo Principal
1.O Sistema identifica um produto controlado e bloqueia a finalização da venda.
2.O Farmacêutico assume o terminal e insere suas credenciais de validação.
3.O Farmacêutico confere a receita física e digita os dados no sistema (Nome do Médico, CRM e UF).
4.O Sistema valida os dados e registra a autorização, liberando o item para o pagamento.

### Fluxos Alternativos / Exceções
- FA01 — Receita Vencida ou Inválida: Se o Farmacêutico identificar irregularidades na receita, ele nega a validação no sistema e o item é removido do carrinho.
- FA02 —Ausência do Farmacêutico: Caso não haja um farmacêutico logado para validar, a venda do item específico não pode ser concluída.



### Relacionamentos
- **Include:** UC03 (Autenticar Usuário).
- **Extend:** (Não se aplica).

<img width="563" height="605" alt="image" src="https://github.com/user-attachments/assets/fd282bec-a6ea-4789-9b9b-f8bb5d0557bb" />

## **UC06 —  Cadastrar Cliente**
**Ator(es):*Atendente.*  
**Descrição:*Permite o registro rápido de novos clientes no banco de dados, coletando dados pessoais para histórico de compras e análise de crédito.*  
**Pré-condições:*Atendente autenticado no sistema; Cliente ainda não possuir registro (verificado por CPF).*  
**Pós-condições:*Novo registro de cliente criado; ID do cliente disponível para vinculação imediata na venda (UC01).*  

### Fluxo Principal
1.O Atendente acessa a tela de cadastro (ou é redirecionado durante uma venda).
2.O Atendente solicita o CPF do cliente para verificar se já existe registro.
3.O Atendente insere os dados obrigatórios (Nome, Telefone, Endereço).
4.O Sistema valida o formato dos dados e salva o novo cadastro no banco de dados.

### Fluxos Alternativos / Exceções
- FA01 — CPF já cadastrado: Se o sistema identificar que o CPF já existe, ele exibe os dados atuais e pergunta se o Atendente deseja apenas atualizar as informações.
- FA02 — Dados Obrigatórios Ausentes: Se o Atendente tentar salvar sem preencher campos essenciais (ex: Telefone), o sistema emite um alerta e impede a gravação.



### Relacionamentos
- **Include:** UC03 (Autenticar Usuário).
- **Extend:** (Não se aplica).

<img width="673" height="575" alt="image" src="https://github.com/user-attachments/assets/3571281e-db67-47f4-98eb-9e2c667ac16c" />

## **UC07 — Aplicar Desconto Especial**
**Ator(es):*Gerente (Autorizador), Atendente (Solicitante).*  
**Descrição:*Permite a aplicação de um percentual de desconto extra sobre o valor total da venda ou em itens específicos, superando os limites padrão do sistema.*  
**Pré-condições:*Venda em andamento no UC01; Itens já adicionados ao carrinho; Presença do Gerente para liberação.*  
**Pós-condições:*Valor total da venda recalculado; Registro do desconto e do responsável pela autorização no banco de dados.*  

### Fluxo Principal
1.O Atendente solicita a aplicação de um desconto manual acima do permitido.
2.O Sistema bloqueia a operação e solicita a senha de nível gerencial.
3.O Gerente insere suas credenciais e informa o percentual ou valor do desconto.
4.O Sistema valida se o desconto não deixa o produto abaixo do preço de custo.
5.O Sistema aplica o novo valor e atualiza o total da venda.

### Fluxos Alternativos / Exceções
- FA01 — Desconto Abaixo do Custo: Se o desconto solicitado resultar em prejuízo (valor de venda < valor de custo), o sistema emite um alerta e exige uma confirmação extra ou bloqueia a operação.
- FA02 — Senha Gerencial Inválida: Se a senha do gerente estiver incorreta, o desconto não é aplicado e o valor original é mantido.



### Relacionamentos
- **Include:** UC03 (Autenticar Usuário).
- **Extend:** (Não se aplica).

<img width="681" height="580" alt="image" src="https://github.com/user-attachments/assets/9bf03753-4eab-41cc-aa62-c615d59d4bc3" />

## **UC08 — Registrar Compra de Fornecedor**
**Ator(es):Gerente (ou Responsável por Compras).*  
**Descrição:*Registra a entrada de novos produtos no sistema através da nota fiscal do fornecedor, atualizando o saldo de estoque e gerando um título no Contas a Pagar.*  
**Pré-condições:*Usuário autenticado com perfil de Gerente; Fornecedor e produtos previamente cadastrados.*  
**Pós-condições:*Saldo de estoque incrementado; Título gerado no financeiro (Contas a Pagar); Custo médio do produto atualizado.*  

### Fluxo Principal
1.O Gerente acessa o módulo de compras e seleciona o fornecedor.
2.O Gerente insere os dados da nota fiscal (número, série e data).
3.O Gerente adiciona os produtos comprados, informando a quantidade e o preço de custo unitário.
4.O Sistema calcula o valor total da nota e solicita a data de vencimento para o pagamento.
5.O Sistema confirma a operação, aumenta o estoque físico e lança o valor no Contas a Pagar.

### Fluxos Alternativos / Exceções
- FA01 — Produto Novo: Se um item da nota fiscal não existir no sistema, o sistema interrompe a compra e solicita o cadastro do novo produto (RF08).
- FA02 — Divergência de Preço: Se o preço de custo for muito superior ao histórico, o sistema emite um alerta para conferência manual.


### Relacionamentos
- **Include:** UC03 (Autenticar Usuário), UC02 (Consultar Estoque - para conferência).
- **Extend:** (Não se aplica).

<img width="497" height="858" alt="image" src="https://github.com/user-attachments/assets/d43e5f0d-2360-44a8-b84d-e2b4bf694603" />

## **UC09 — Gerar Relatórios de Desempenho**
**Ator(es):Gerente, Administrador, Financeiro.*  
**Descrição:*Permite a extração de dados consolidados sobre vendas, giro de estoque e saúde financeira (contas a pagar/receber) em períodos específicos.*  
**Pré-condições:*Usuário autenticado com perfil gerencial ou superior; Dados de movimentação existentes no banco de dados.*  
**Pós-condições:*Exibição do relatório em tela ou exportação em arquivo (PDF/Planilha) para análise.*  

### Fluxo Principal
1.O Usuário acessa o módulo de relatórios e escolhe o tipo desejado (ex: Produtos mais vendidos, Vendas por dia ou Inadimplência).
2.O Usuário define os filtros de busca (Data Inicial, Data Final, Unidade da Farmácia).
3.O Sistema processa as transações do banco de dados e consolida os valores.
4.O Sistema exibe os resultados organizados por categorias e totais.

### Fluxos Alternativos / Exceções
- FA01 — Nenhum Dado Encontrado: Se não houver movimentação no período filtrado, o sistema exibe a mensagem "Nenhum registro encontrado para os filtros aplicados".
- FA02 — Erro de Permissão: Se um Atendente tentar acessar este módulo, o sistema bloqueia a entrada conforme o RNF03.


### Relacionamentos
- **Include:** UC03 (Autenticar Usuário), UC02 (Consultar Estoque - para conferência).
- **Extend:** (Não se aplica).

<img width="572" height="704" alt="image" src="https://github.com/user-attachments/assets/ff7e0c3d-136e-44b6-8d16-89e1cd01d684" />


## **UC010 — Ajustar Estoque Manualmente**
**Ator(es):Gerente.*  
**Descrição:*Permite a alteração direta da quantidade de um produto no sistema sem a necessidade de uma venda ou nota fiscal de compra, geralmente utilizado para correções de inventário, perdas ou quebras.*  
**Pré-condições:*Usuário autenticado com perfil de Gerente (UC03); Produto já cadastrado no sistema.*  
**Pós-condições:*Saldo do produto atualizado no banco de dados; Registro de log (histórico) contendo o motivo do ajuste e quem o realizou.*  

### Fluxo Principal
1.O Gerente acessa o módulo de inventário e pesquisa o produto desejado.
2.O Sistema exibe a quantidade atual registrada.
3.O Gerente insere a nova quantidade física real encontrada na prateleira.
4.O Gerente seleciona o motivo do ajuste (Ex: Quebra, Vencimento, Erro de Contagem).
5.O Sistema calcula a diferença, atualiza o saldo e grava o histórico da alteração.

### Fluxos Alternativos / Exceções
- FA01 — Ajuste Negativo Crítico: Se o ajuste for para uma quantidade negativa (abaixo de zero), o sistema bloqueia a operação e solicita revisão.
- FA02 — Justificativa Ausente: Se o Gerente não selecionar um motivo para o ajuste, o sistema impede a gravação para manter a auditabilidade.


### Relacionamentos
- **Include:** UC03 (Autenticar Usuário), UC02 (Consultar Estoque).
- **Extend:** (Não se aplica).

<img width="702" height="667" alt="image" src="https://github.com/user-attachments/assets/d9776961-9fd9-4442-9083-19fd6aedd63e" />
/>












---

> Repita essa estrutura para **todos os seus casos de uso** (mínimo 10).
