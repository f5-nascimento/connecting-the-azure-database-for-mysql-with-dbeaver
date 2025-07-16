# 💡 Conectando o Azure Database for MySQL com o Dbeaver

Este repositório é um guia prático para criar e utilizar um banco de dados **MySQL no Azure**, realizando a conexão via **DBeaver** para executar comandos SQL remotamente.

---

## ✅ Pré-requisitos

Antes de começar, certifique-se de ter:
- Uma conta ativa no [Portal do Azure](https://portal.azure.com)
- O [DBeaver Community](https://dbeaver.io/download/) instalado

---

## 🧭 Etapas do tutorial

### 1. Acesse o Portal do Azure
- Acesse: [https://portal.azure.com](https://portal.azure.com)
- Faça login com sua conta Microsoft.

---

### 2. Crie um Banco de Dados MySQL

<img width="1376" height="395" alt="azuredatabasemysql" src="https://github.com/user-attachments/assets/8f907039-cfce-4080-896b-c15f90a6b842" />

- No campo de busca do portal, digite **Azure Database for MySQL**
- Clique no ícone conforme a imagem acima.
- Você será direcionado a uma tela para *Selecionar a opção de implantação do Banco de Dados do Azure para MySQL*
- Em **Servidor fléxivel**, selecione **Criação Rápida**
- **Assinatura**: Selecione sua assinatura ativa (ex: `Azure for Students` ou `Azure subscription 1`)
- **Grupo de recursos**: Selecione um existente (ex: `lab-sql`) ou clique em **Criar novo**
- **Nome do servidor:** Defina um nome exclusivo para o servidor (ex: `server-mysql255`)
- **Região**: Escolha uma região próxima ou mais barata (ex: `West US 2`)
- **Logon do administrador**: Insira um nome de administrador (ex: `adminmysql`) 
- **Senha**: Insira a senha de administrador (ex: `MySQLadmin255`) 
- **Confirmar senha**: Repita a senha informada
- **Tipo de carga de trabalho**: selecione `Desenvolvimento/Teste`
- Marque a opção *Adicionar a regra de firewall ao endereço de IP atual*
- Clique em **Examinar e criar**
- Clique em **Criar**
---

### 3. Crie um Banco de Dados MySQL

<img width="1884" height="446" alt="azureconection" src="https://github.com/user-attachments/assets/0e456857-1307-4331-9fae-98fb8a54fa5b" />

- Após a implantação, clique em **Ir para o grupo de recursos**.
- Depois clique no servidor listado (ex: `server-mysql255`).
> Algumas informações são importantes para a conexão com o DBeaver: `Nome do servidor` será o seu servidor e `Logon do administrador` será o seu Nome de usuário. Além disso você precisará de um Certificado SSL.
- No menu lateral, clique em **Configurações**
- Selecione **Rede**
- Clique em **Baixar o Certificado SSL**
- Uma nova página será carregada, clique em **certificado SSL público** para realizar o download
> Você também pode baixar o certificado público (CA Certificate) em:
  👉 [Documentação oficial Microsoft – Download do certificado SSL](https://learn.microsoft.com/pt-br/azure/mysql/flexible-server/how-to-connect-tls-ssl#download-the-public-ssl-certificate)
---

### 4. Conectando com o DBeaver

<img width="1723" height="939" alt="codebaver" src="https://github.com/user-attachments/assets/8110fa01-a540-4829-936d-d308141eebea" />

- Abra o DBeaver e siga os passos:
- Clique em **Nova Conexão**
- Escolha **MySQL** > Avançar
- Preencha:

| Campo               | Valor (exemplo)                                  |
|--------------------|--------------------------------------------------|
| Servidor               | `server-mysql255.mysql.database.azure.com`        |
| Porta              | `3306`                                           |
| Usuário            | `adminmysql`                      |
| Senha              | `sua_senha_aqui`                                 |


- Vá até a aba **SSL** da conexão
- Marque **Use SSL**
- No campo **Avançado**, marque `Exigir SSL`
- Em **Certificado CA**, selecione o arquivo de certificado SSL que foi baixado anteriormente.
- Clique em **Testar conexão**
- Após a mensagem de Conectador ser exibida, clique em **Concluir**.
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

