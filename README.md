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

## 📝 Exemplos de Casos de Teste (BDD)

**Cenário: Validar impedimento de cadastro com carga horária negativa**
* **Dado** que estou no formulário de cadastro de curso
* **Quando** preencho o nome "QA Especialista"
* **E** insiro o valor "-10" no campo de carga horária
* **E** clico em "Salvar"
* **Então** o sistema deve exibir a mensagem de erro "Valor inválido"
* **E** o curso não deve ser adicionado à listagem.

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
