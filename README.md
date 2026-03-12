# Active Directory Bulk User Management

Projeto em PowerShell para gerenciamento em massa de usuários no Active Directory utilizando arquivos CSV.

O objetivo deste projeto é facilitar operações administrativas comuns como criação e remoção de usuários, permitindo adaptação fácil para diferentes ambientes apenas alterando algumas configurações no script.

---

## 📂 Estrutura do Projeto

```
ad-user-management
│
├── nome_do_arquivo_de_criacao_de_usuarios.ps1
├── nome_do_arquivo_de_exclusao_de_usuarios.ps1
└── README.md
```

### Scripts disponíveis

**nome_do_arquivo_de_criacao_de_usuarios.ps1**

Script responsável pela criação de usuários no Active Directory a partir de um arquivo CSV.

Funcionalidades:

- criação em massa de usuários
- definição da OU de destino
- definição de senha inicial
- geração de relatório de erros
- estrutura adaptável para diferentes CSVs

---

**nome_do_arquivo_de_exclusao_de_usuarios.ps1**

Script responsável pela remoção de usuários no Active Directory utilizando um arquivo CSV contendo os logins.

Funcionalidades:

- remoção em massa de usuários
- verificação se o usuário existe
- geração de relatório de erros
- estrutura adaptável para diferentes CSVs

---

## ⚙️ Requisitos

Antes de executar os scripts, verifique se o ambiente atende aos seguintes requisitos:

- Windows Server ou máquina com RSAT instalado
- módulo ActiveDirectory disponível
- permissões para criar ou remover usuários no AD
- PowerShell 5 ou superior

Para verificar se o módulo está disponível:

```
Get-Module -ListAvailable ActiveDirectory
```

---

## 📄 Estrutura do CSV

Os scripts utilizam arquivos CSV como entrada.

Exemplo de estrutura:

```
RA,NOME,CPF
12345,João Silva,12345678900
12346,Maria Souza,98765432100
```

### Colunas utilizadas

| Coluna | Descrição |
|------|------|
| RA | Login do usuário |
| NOME | Nome completo |
| CPF | Senha inicial |

Esses nomes podem ser alterados diretamente nos scripts na seção:

```
$csvMapping
```

Isso permite utilizar diferentes formatos de CSV sem alterar a lógica principal dos scripts.

---

## 🔧 Configuração dos Scripts

Antes de executar, edite as variáveis de configuração no início de cada script.

### Caminho do arquivo CSV

```
$csvFilePath = "C:\AD.csv"
```

Define o caminho do arquivo que contém os dados dos usuários.

---

### OU de destino (apenas no script de criação)

```
$ouPath = "OU=Usuarios,DC=DOMAIN,DC=corp"
```

Define a Unidade Organizacional onde os usuários serão criados.

---

### Domínio utilizado no UPN

```
$domain = "DOMAIN.corp"
```

Usado para montar o campo UserPrincipalName.

Exemplo gerado:

```
usuario@DOMAIN.corp
```

---

### Relatório de erros

```
$errorReportPath = "C:\erros.csv"
```

Caso ocorram erros durante a execução, eles serão registrados neste arquivo.

---

## ▶️ Execução

### Criar usuários

Execute:

```
.\nome_do_arquivo_de_criacao_de_usuarios.ps1
```

O script irá:

1. Ler o CSV
2. Criar os usuários no Active Directory
3. Registrar possíveis erros em um relatório

---

### Remover usuários

Execute:

```
.\nome_do_arquivo_de_exclusao_de_usuarios.ps1
```

O script irá:

1. Ler o CSV
2. Buscar os usuários no Active Directory
3. Remover as contas encontradas
4. Registrar possíveis erros em um relatório

---

## 📊 Relatório de erros

Caso ocorram erros durante o processamento, um arquivo CSV será gerado contendo informações como:

- login
- nome (quando aplicável)
- descrição do erro

Esse relatório permite identificar falhas e corrigir os dados antes de executar novamente o processo.

---

## ⚠️ Boas práticas

Antes de executar os scripts em produção:

- testar com poucos usuários
- validar a estrutura do CSV
- confirmar permissões administrativas
- garantir que os logins não estejam duplicados
- validar a OU de destino

---

## 🧩 Possíveis melhorias futuras

Este projeto pode ser facilmente expandido para incluir:

- verificação se usuário já existe antes de criar
- exigência de troca de senha no primeiro login
- modo simulação (dry-run)
- log centralizado de execução
- arquivo de configuração externo (JSON ou ENV)

---

## 📜 Licença

Este projeto pode ser utilizado e adaptado livremente conforme a necessidade do ambiente.
