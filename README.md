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
A documentação detalhada com os passos, resultados esperados e critérios de aceite (Gherkin) está disponível no link abaixo:

👉 **[https://docs.google.com/spreadsheets/d/1jTlhlIxeFiyEtN9nBMO5G7AlfYcXVjfZT0WhXLtPNTE/edit?usp=sharing]** *(link do Google Sheets)*

---

## 📝 Cenários de Teste BDD

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
* **Dado** que existe pelo menos um curso cadastrado na "LISTAR CURSOS""
* **Quando** clico no botão de "Excluir" (ícone de lixeira) do curso desejado
* **E** confirmo a exclusão na janela de alerta (pop-up)
* **Então** o sistema deve exibir uma mensagem de sucesso: "Curso removido com sucesso"
* **E** o registro deve desaparecer da listagem imediatamente sem necessidade de atualizar a página.

---

## 3. Registro de Bugs Encontrados
Durante a execução dos testes, foram identificados os seguintes problemas:

#### **BUG-01: [Título Resumido do Erro]**
* **Passos para reproduzir:** 1. Acessar tal tela; 2. Clicar em tal botão; 3. Preencher X.
* **Resultado Atual:** [O que aconteceu de errado]
* **Resultado Esperado:** [O que deveria ter acontecido]
* **Severidade:** [Crítica / Alta / Média / Baixa]

---

## 4. Evidências de Execução
Os prints e gravações de tela comprovando os testes realizados podem ser acessados na pasta abaixo:

📁 **[LINK PARA O GOOGLE DRIVE/PASTA DE EVIDÊNCIAS]**

---
**Candidato:** [Elton de Souza Costa]
**Data:** 06/03/2026
