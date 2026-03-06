# DESAFIO-QA-BEEDOO-2026

Repositório destinado ao desafio técnico de análise e teste do módulo de cursos.

---

## 1. Exploração da Aplicação

### **Qual o objetivo da aplicação?**
O sistema tem como objetivo principal o **gerenciamento de cursos**, permitindo o controle administrativo através do cadastro, consulta (listagem), edição e exclusão de registros educacionais.

### **Principais Fluxos Disponíveis**
* **Cadastro:** Inclusão de novos cursos com campos de nome, carga horária e instrutor.
* **Listagem:** Visualização em tempo real dos cursos armazenados.
* **Edição:** Alteração de dados de cursos previamente cadastrados.
* **Exclusão:** Remoção definitiva de registros da base de dados.

### **Pontos Críticos para Teste**
* **Persistência de Dados:** Garantir que as informações não se percam após o recarregamento da página.
* **Validações de Input:** Impedir o cadastro de campos vazios ou caracteres inválidos em campos numéricos.
* **Feedback ao Usuário:** Verificar se as mensagens de erro/sucesso aparecem corretamente.
* **Integridade da Listagem:** Confirmar se os dados exibidos na tabela correspondem exatamente ao que foi digitado no formulário.

---

## 2. Cenários e Casos de Teste
A documentação detalhada com os passos, resultados esperados e critérios de aceite (Gherkin), estão disponíveis no link abaixo:

**[https://docs.google.com/spreadsheets/d/1jTlhlIxeFiyEtN9nBMO5G7AlfYcXVjfZT0WhXLtPNTE/edit?usp=sharing]** *(link do Google Sheets)*

---

## Cenários de Teste BDD

### **CT-01: Cadastro de curso com sucesso**
* **Dado** que estou na tela de "CADASTRAR CURSO"
* **Quando** preencho o nome do curso, instrutor e carga horária válida
* **E** clico no botão de salvar
* **Então** o sistema deve exibir uma mensagem de confirmação
* **E** redirecionar para a "LISTA DE CURSOS" exibindo o novo registro.

---

### **CT-02: Validação de campos obrigatórios**
* **Dado** que estou no formulário de cadastro
* **Quando** clico em salvar sem preencher nenhum campo
* **Então** o sistema deve destacar os campos obrigatórios em vermelho
* **E** impedir o envio dos dados.

---

### **CT-03: Listagem de cursos**
* **Dado** que existem cursos cadastrados na "LISTA DE CURSOS"
* **Quando** Clico na “LISTA DE CURSOS”
* **Então** Deverá aparecer os cursos cadastrados.

---

### **CT-04: Excluir um curso com sucesso**
* **Dado** que existe pelo menos um curso cadastrado na "LISTAR CURSOS"
* **Quando** clico no botão de "Excluir" (ícone de lixeira) do curso desejado
* **E** confirmo a exclusão na janela de alerta (pop-up)
* **Então** o sistema deve exibir uma mensagem de sucesso: "Curso removido com sucesso"
* **E** o registro deve desaparecer da listagem imediatamente sem necessidade de atualizar a página.

---

### **CT-05: Validar impedimento de cadastro duplicado**
* **Dado** que já existe um curso cadastrado com o nome "Curso de Teste de QA" e instrutor "Elton Costa"
* **Quand** tento cadastrar um novo curso com exatamente os mesmos dados (Nome e Instrutor)
* **Então** o sistema deve exibir uma mensagem de alerta: "Este curso já está cadastrado"
* **E** não deve permitir a criação do registro duplicado na listagem.

---

### **CT-06: Validar geração de link de acesso na listagem**
* **Dado** que realizei o cadastro de um novo curso com sucesso
* **Quand** acesso a tela de "LISTA DE CURSOS"
* **E** tento clicar no título ou no card do curso recém-criado para acessar seu conteúdo
* **Então** o sistema deve me redirecionar para a página específica do curso
* **E** a URL deve conter o identificador correto do registro.

---

## 3. Registro de Bugs Encontrados
Durante a execução dos testes, foram identificados os seguintes problemas:

Abaixo estão detalhados os cenários de teste aplicados, seguidos pelo status de cada execução e observações técnicas.

* **Plano de Testes e Resultados de Execução**

| ID        | Cenário de Teste                 | Status | Severidade | Observações                                         |
|:---|:---|:---:|:---:|:---|
| **CT-01** | Cadastro de curso com sucesso    | PASSOU | Baixa      | Fluxo executado conforme o esperado.                |
| **CT-02** | Validação de campos obrigatórios | FALHOU | CRÍTICA    | Sistema permite salvar registros com campos vazios. |
| **CT-03** | Listagem de cursos cadastrados   | PASSOU | Baixa      | Os cursos são exibidos corretamente na grid.        |
| **CT-04** | Excluir um curso com sucesso     | FALHOU | CRÍTICA    | O registro permanece na base mesmo após a exclusão. |
| **CT-05** | Validar impedimento de cadastro duplicado     | FALHOU | CRÍTICA    | O sistema permite cadastrar o mesmo curso múltiplas vezes, gerando redundância de dados. |  
| **CT-06** | Validar geração de link de acesso na listagem     | FALHOU | CRÍTICA    | O sistema renderiza o card do curso na listagem, mas não gera um hyperlink que permita ao usuário acessar os detalhes do curso. O componente está estático, impedindo o consumo do conteúdo. | 

---

## Detalhamento dos Bugs Encontrados

### **BUG-01: Ausência de Validação em Campos Mandatórios (CT-02)**
* **Severidade:** **CRÍTICA** (Impacta a integridade dos dados).
* **Descrição:** O sistema não valida a presença de dados nos campos "Nome do Curso", "Descrição do curso"; "instrutor", "URL da imagem de capa", "Data de inicio", "Data de fim",
  "Número de vagas", Tipo do curso", "Link de inscrição", permitindo o cadastro de cursos com informações em branco.
* **Resultado Atual:** O formulário é submetido com sucesso mesmo sem preenchimento.
* **Resultado Esperado:** O sistema deve bloquear o cadastro e exibir alertas visuais nos campos obrigatórios.

### **BUG-02: Falha Funcional na Persistência de Exclusão (CT-04)**
* **Severidade:** **CRÍTICA** (Viola as regras de negócio do CRUD).
* **Descrição:** Ao acionar o comando de exclusão e confirmar no pop-up, o sistema não remove o registro da base de dados.
* **Passos para Reproduzir:** 1. Localizar um curso na lista.
    2. Clicar no ícone de lixeira.
    3. Confirmar a exclusão.
    4. Atualizar a página (F5).
* **Resultado Atual:** O registro permanece visível e persistido.
* **Resultado Esperado:** O curso deve ser removido permanentemente da listagem e do banco de dados.

### **BUG-03: Falha de Roteamento e Ausência de Link de Acesso (CT-06)**
* **Severidade:** **CRÍTICA** (Impede o consumo do produto principal).
* **Descrição:** Após o cadastro bem-sucedido de um curso, o card correspondente é renderizado na tela de "LISTA DE CURSOS", porém o título e o card não possuem um elemento de link funcional (`href`). Isso impossibilita que o usuário acesse os detalhes, lições ou a página interna do curso criado.
* **Passos para Reproduzir:**
    1. Realizar o cadastro de um curso preenchendo os campos obrigatórios.
    2. Navegar até a tela de **"LISTA DE CURSOS"**.
    3. Tentar clicar no nome do curso ou sobre o card para abrir os detalhes.
    4. Observar que o cursor do mouse não altera para "pointer" (mãozinha) e nenhuma ação de redirecionamento é disparada.
* **Resultado Atual:** O registro é exibido visualmente na listagem, mas permanece como um elemento estático, sem gerar uma URL de acesso ou link de navegação.
* **Resultado Esperado:** O título do curso (ou um botão específico de "Acessar") deve ser um hyperlink funcional que redirecione o usuário para a rota de detalhes (ex: `/detalhes-curso/ID_DO_CURSO`).
* **Possível Causa Técnica:** Falha na lógica de renderização do Front-end, onde o ID retornado pela API não está sendo vinculado ao componente de link, ou ausência de configuração de rotas dinâmicas no projeto (SPA).

---

* **Nota do QA:** Os bugs **BUG-02 (Validação)**, **BUG-04 (Exclusão)** e **BUG-06 (Link de Acesso)**, quando analisados em conjunto, sugerem uma falha crítica na camada de persistência e na sincronia entre o banco de dados e a interface. Isso compromete o ciclo de vida básico da aplicação (**CRUD**), afetando diretamente a confiabilidade do produto e a experiência do usuário final.

---

## Sugestões de Melhorias (UX & Regras de Negócio)

Para elevar a qualidade da aplicação e a experiência do usuário, foram identificadas as seguintes oportunidades de melhoria:

1. **Implementação de Sistema de Filtros Avançados:**
* Adicionar um campo de busca global na "LISTA DE CURSOS" que permita a filtragem dinâmica por **Título do curso**, **Nome do Instrutor** e **Tipo de curso**.
* *Motivo:* Facilita a escalabilidade do sistema quando houver um grande volume de dados cadastrados.

2. **Regra de Unicidade (Evitar Duplicidade):**
* Implementar uma validação no backend/frontend que impeça o cadastro de cursos com o mesmo nome e instrutor já existentes na base.
* *Motivo:* Garante a integridade da base de dados e evita poluição visual na listagem para o usuário final.

3. **Feedback de Ações (Toasts/Alertas):**
* Adicionar notificações visuais (ex: cantos da tela) após ações de Cadastro, Edição e Exclusão.
* *Motivo:* Melhora a percepção de sucesso ou erro da operação realizada.

---

## 4. Evidências de Execução
Os prints e gravações de tela comprovando os testes realizados podem ser acessados na pasta abaixo:

**[LINK PARA O GOOGLE DRIVE/PASTA DE EVIDÊNCIAS]**

---
**Candidato:** [Elton de Souza Costa]
**Data:** 06/03/2026
