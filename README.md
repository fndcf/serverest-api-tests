# Testes Automatizados API ServeRest

## Tecnologias Utilizadas

- **Postman** - Ferramenta de testes de API
- **Newman 6.1+** - CLI do Postman para execução automatizada
- **Newman Reporter HTMLExtra** - Gerador de relatórios visuais
- **Node.js 18** - Runtime JavaScript
- **GitHub Actions** - Pipeline CI/CD
- **JavaScript** - Scripts de teste
- **Node.js 18+**
- npm (incluído com Node.js)

---

### Instalação e Execução

```bash
# 1. Clone o repositório
git clone https://github.com/fndcf/serverest-api-tests.git
cd serverest-api-tests/postman

# 2. Instale as dependências
npm install

# 3. Execute os testes
npm test

# 4. Gerar relatório HTML
npm run test:report

# 5. Abrir relatório no navegador
start newman-report.html  # Windows
open newman-report.html   # Mac/Linux
```

---

## Estrutura do Projeto

```
serverest-api-tests/
├── .github/
│   └── workflows/
│       └── postman-tests.yml        # Pipeline CI/CD
│
├── postman/
│   ├── ServeRest-API-Tests.postman_collection.json  #Collection Postman
│   └── package.json
│
├── .gitignore
└── README.md
```

## Resultados

| Métrica               | Valor               |
| --------------------- | ------------------- |
| **Requests**          | 21                  |
| **Assertions**        | 55                  |
| **Taxa de Sucesso**   | 100% (55/55)        |
| **Tempo de Execução** | 2.1 segundos        |
| **Tempo Médio**       | 77ms por request    |
| **Performance**       | 100% < 2000ms (SLA) |

---

---

## Cobertura de Testes

### Endpoints Testados

| Endpoint         | Método | Cenários | Status |
| ---------------- | ------ | -------- | ------ |
| `/login`         | POST   | 5        | 100%   |
| `/usuarios`      | GET    | 3        | 100%   |
| `/usuarios`      | POST   | 7        | 100%   |
| `/usuarios/{id}` | GET    | 2        | 100%   |
| `/usuarios/{id}` | PUT    | 2        | 100%   |
| `/usuarios/{id}` | DELETE | 2        | 100%   |

**Total:** 21 requests com cobertura completa.

---

## Casos de Teste

### Autenticação

- Login com sucesso = Token JWT
- Login com email inválido = 401
- Login com senha incorreta = 401
- Login sem email = 400
- Login sem senha = 400

### Usuários - Criação

- Criar usuário com dados válidos = 201
- Criar usuário com email duplicado = 400
- Criar usuário sem nome = 400
- Criar usuário sem email = 400
- Criar usuário com email inválido = 400
- Criar usuário sem senha = 400
- Criar usuário sem campo administrador = 400

### Usuários - Listagem

- Listar todos os usuários = 200
- Filtrar usuários por nome = 200
- Filtrar usuários administradores = 200

### Usuários - Busca por ID

- Buscar usuário existente = 200
- Buscar usuário inexistente = 400

### Usuários - Atualização

- Atualizar usuário existente = 200
- Criar usuário via PUT (upsert) = 201

### Usuários - Exclusão

- Excluir usuário existente = 200
- Excluir usuário inexistente = 200

---

## Validações Implementadas

- **Status Codes** - Validação de códigos HTTP
- **Mensagens de Resposta** - Verificação das mensagens da API
- **JSON Schema Validation** - Validação das estrutura de dados
- **Campos Obrigatórios** - Teste de todos os campos obrigatórios
- **Formatos** - Validação de email e outros formatos
- **Regras de Negócio** - Email único, etc
- **Performance (SLA)** - Todas requisições serem < 2000ms

---

## Scripts Disponíveis

```bash
# Executar testes básicos
npm test

# Executar e gerar relatório HTML completo
npm run test:report

# Executar para CI/CD (gera JSON)
npm run test:ci
```

---

## CI/CD - GitHub Actions

### Pipeline Automatizada

A pipeline é executada automaticamente em:

- Push para `main`, `master` e `develop`
- Pull Requests para `main` e `master`
- Execução manual (workflow_dispatch)
- Agendamento diário às 6h UTC

### O que a Pipeline Faz

1. **Setup** - Instala Node.js 18 e dependências Newman
2. **Execução** - Roda todos os testes da collection
3. **Relatórios** - Gera relatórios HTML e JSON
4. **Artefatos** - Publica relatórios (30 dias de retenção)
5. **Resumo** - Mostra resultados no GitHub Actions

### Visualizar Resultados

1. Acesse: https://github.com/fndcf/serverest-api-tests/actions
2. Clique no workflow executado
3. Veja o resumo dos testes
4. Baixe os artefatos:
   - `newman-report-html` - Relatório visual completo
   - `newman-report-json` - Dados estruturados

### Executar Manualmente

1. Vá em **Actions**
2. Clique em **Postman API Tests**
3. Clique em **"Run workflow"**
4. Selecione a branch
5. Clique em **"Run workflow"** novamente

---

## Relatórios

### Relatório HTML (Newman HTMLExtra)

O relatório HTML fornece:

- Dashboard visual com gráficos
- Timeline de execução
- Detalhes de cada request/response
- Status de cada assertion
- Métricas de performance
- Sumário executivo

**Como visualizar:**

```bash
npm run test:report
start newman-report.html
```

### Relatório JSON

Dados estruturados para análise programática:

```bash
npm run test:ci
# Arquivo gerado: newman-results.json
```

---

## Opções de Execução

### Opção 1: Postman Desktop (Interface Visual)

1. Baixe: https://www.postman.com/downloads/
2. Importe: `postman/ServeRest-API-Tests.postman_collection.json`
3. Clique em **"Run"** para executar toda a collection

### Opção 2: Newman CLI (Linha de Comando)

```bash
cd postman
npm install
npm test
```

### Opção 3: GitHub Actions (CI/CD Automático)

A pipeline executa automaticamente em cada push para `main`.

---

# GitHub Actions

Este guia mostra como configurar a pipeline de testes automatizados no GitHub Actions.

---

## Pré-requisitos

- Conta no GitHub
- Projeto Postman configurado localmente
- Testes executando com sucesso (`npm test`)
- Criação de repósitorio no GitHub

---

#### 1 Acessar GitHub Actions

1. Vá para seu repositório: `https://github.com/SEU_USUARIO/serverest-api-tests`
2. Clique na aba **"Actions"**
3. Você verá o workflow **"Postman API Tests"** executando

#### 1.2 Aguardar Execução

A pipeline executará automaticamente após o push

#### 1.3 Ver Detalhes

Clique no workflow para ver:

- Logs de execução
- Testes executados
- Relatórios gerados

---

### Passo 2: Baixar Relatórios -Artefatos

#### Via Interface:

1. Vá para **Actions**
2. Clique no **Workflow** executado
3. Role até **"Artifacts"** no final da página
4. Baixe os artefatos:
   - `newman-report-html` (relatório visual)
   - `newman-report-json` (dados estruturados)

### Relatório HTML:

1. Baixe `newman-report-html.zip`
2. Extraia o arquivo
3. Abra `newman-report.html` no navegador

---

### O que a Pipeline Faz:

1. **Trigger Automático:**

   - Push para `main`, `master`, `develop`
   - Pull Request para `main`, `master`
   - Execução manual (workflow_dispatch)
   - Agendamento diário (6h UTC)

2. **Setup:**

   - Instala Node.js 18
   - Instala Newman + newman-reporter-htmlextra
   - Cache de dependências npm

3. **Execução:**

   - Roda `npm test` (todos os testes)
   - Gera relatório HTML
   - Gera relatório JSON

4. **Relatórios:**
   - Upload de artefatos (HTML, JSON)
   - Retenção: 30 dias
   - Resumo no GitHub Actions

---

## Triggers Configurados

### 1. Push Automático

```yaml
on:
  push:
    branches: [main, master, develop]
```

Pipeline executa **automaticamente** ao fazer push.

### 2. Pull Request

```yaml
on:
  pull_request:
    branches: [main, master]
```

Testa **antes** de mergear o PR.

### 3. Execução Manual

```yaml
on:
  workflow_dispatch:
```

Permite executar manualmente:

- Vá em **Actions**
- Selecione o workflow
- Clique em **"Run workflow"**

### 4. Agendamento

```yaml
on:
  schedule:
    - cron: "0 6 * * *"
```

Executa **diariamente às 6h UTC** (3h BRT).

---
