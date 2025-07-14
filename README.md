# 💡 Azure Database for MySQL – Tutorial passo a passo

Este repositório é um guia prático para criar e utilizar um banco de dados **MySQL no Azure**, realizando a conexão via **DBeaver** para executar comandos SQL remotamente.

---

## ✅ Pré-requisitos

Antes de começar, certifique-se de ter:
- Uma conta ativa no [Portal do Azure](https://portal.azure.com)
- O [DBeaver Community](https://dbeaver.io/download/) instalado

---

## 🧭 Etapas do tutorial

### 1. Acesse o Portal do Azure
Acesse [https://portal.azure.com](https://portal.azure.com) e entre com sua conta.

---

### 2. Crie um Banco de Dados MySQL

> 🔽 Clique em "**Criar um recurso**" > "**Banco de dados**" > "**Banco de dados para MySQL - servidor flexível**"

- Selecione **Criação rápida**
- Defina:
  - Nome do servidor: `trainning-sql1` (exemplo)
  - Versão: `8.0`
  - Tipo de carga: `Desenvolvimento`
  - Região: escolha uma disponível (ex: `West US 2`)
  - Usuário administrador: `adminmysql`
  - Senha: escolha uma senha forte
- Avance até a opção de **exibir e criar**, clique em **Criar**
- Aguarde a implantação ser concluída

---

### 3. Configure o Firewall

- Após criado, vá até o recurso do servidor
- Clique em **Regras de firewall**
- Clique em **+ Adicionar o endereço IP do cliente atual**
- Salve

---

### 4. Conectando com o DBeaver

> Abra o DBeaver e siga os passos:

- Clique em **Nova Conexão**
- Escolha **MySQL** > Avançar
- Preencha:

| Campo               | Valor (exemplo)                                  |
|--------------------|--------------------------------------------------|
| Host               | `trainning-sql1.mysql.database.azure.com`        |
| Porta              | `3306`                                           |
| Usuário            | `adminmysql@trainning-sql1`                      |
| Senha              | `sua_senha_aqui`                                 |


O Azure **exige conexões seguras via SSL/TLS** para o banco de dados MySQL.

#### ✅ Para testes (modo mais simples):
- Vá até a aba **SSL** da conexão
- Marque **Use SSL**
- No campo **SSL Mode**, selecione `require`
- Baixe o certificado público (CA Certificate) em:
  👉 [Documentação oficial Microsoft – Download do certificado SSL](https://learn.microsoft.com/pt-br/azure/mysql/flexible-server/how-to-connect-tls-ssl#download-the-public-ssl-certificate)
- Informe o certificado na aba **SSL** do DBeaver no campo **CA Certificate** ou Certificado CA

Após configurar, clique em **Testar Conexão** e depois em **Concluir**.
---

### 5. Criando o banco e tabelas

Clique em **SQL Editor** no DBeaver e execute o seguinte:

```sql
CREATE DATABASE escola;

USE escola;

CREATE TABLE cursos (
  id INT PRIMARY KEY AUTO_INCREMENT,
  nome VARCHAR(100) NOT NULL,
  limite_alunos INT DEFAULT 30
);

CREATE TABLE alunos (
  id INT PRIMARY KEY AUTO_INCREMENT,
  nome VARCHAR(100) NOT NULL
);

CREATE TABLE curso_aluno (
  id INT PRIMARY KEY AUTO_INCREMENT,
  aluno_id INT,
  curso_id INT,
  FOREIGN KEY (aluno_id) REFERENCES alunos(id) ON DELETE CASCADE,
  FOREIGN KEY (curso_id) REFERENCES cursos(id) ON DELETE CASCADE
);

