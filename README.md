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

### 5. Criando o banco de dados

<img width="1301" height="431" alt="bd" src="https://github.com/user-attachments/assets/93b2204c-a98c-4c11-9fdf-025441fb8005" />

- No DBeaver, selecione o seu servidor MySQL listado (ex: server-mysql255.mysql.database.azure.com)
- Em Banco de dados, clique com o botão direito do mouse e depois cliquem em Criar novo(a) Banco de dados.
- Em **Nome do banco de dados**, digite o nome do banco (ex. regencia)
- Clique em **Ok**

### 6. Criando a tabela Cursos

<img width="1198" height="832" alt="create" src="https://github.com/user-attachments/assets/d4337be3-94d6-499c-a35f-3d6d67d5426e" />

- Clique em **SQL Editor** no DBeaver.
- Clique em **Abrir script SQL** ou `F3`e execute o seguinte:

```sql
CREATE TABLE Cursos (
  id INT PRIMARY KEY AUTO_INCREMENT,
  nome VARCHAR(100) NOT NULL,
  carga_horaria INT NOT NULL
);
```
- Clique em **Executar instrução SQL** ou `CTRL+Enter` para executar o código.

### 7. Inserindo registros em Cursos

- Para adicionar registros, execute o seguinte:
```sql
insert into cursos (nome, carga_horaria) values 
('Programador Back-End',100),
('Programador Front-End',100),
('Administrador de Banco de Dados',80),
('Operador de Sistemas Operacionais',120),
('Assistente Administrativo',200)
```
- Clique em **Executar instrução SQL** ou `CTRL+Enter` para executar o código.

### 8. Consultando registros em Cursos

- Para consultar os registros, execute o seguinte:
```sql
select * from cursos;
```
- Clique em **Executar instrução SQL** ou `CTRL+Enter` para executar o código.

### 9. Criando a tabela Instrutores

- Para criar a tabela Instrutores, execute o seguinte:

```sql
create table instrutores(
id_instrutor int primary key auto_increment,
nome_instrutor varchar(100)
);
```
- Clique em **Executar instrução SQL** ou `CTRL+Enter` para executar o código.

### 10. Inserindo registros em Instrutores

- Para adicionar registros execute o seguinte:
```sql
insert into instrutores (nome_instrutor) values 
('João da Silva Andrade'),
('Célia dos Santos Nascimento'),
('Amarildo André Sá');
```
- Clique em **Executar instrução SQL** ou `CTRL+Enter` para executar o código.

### 11. Consultando registros em Instrutores

- Para consultar os registros execute o seguinte:
```sql
select * from instrutores;
```
- Clique em **Executar instrução SQL** ou `CTRL+Enter` para executar o código.

### 12. Criando a tabela Alocação

- Para criar a tabela Alocação, execute o seguinte:

```sql
create table alocacao(
id_alocacao int primary key auto_increment,
curso int,
instrutor int,
foreign key (curso) references cursos (id),
foreign key (instrutor) references instrutores (id_instrutor)
);
```
- Clique em **Executar instrução SQL** ou `CTRL+Enter` para executar o código.

### 13. Inserindo registros em Alocação

- Para adicionar registros execute o seguinte:
```sql
insert into alocacao (curso, instrutor) values
(1,1),
(2,1),
(3,2),
(4,3),
(5,2);
```
- Clique em **Executar instrução SQL** ou `CTRL+Enter` para executar o código.

### 14. Consultando registros em Alocação

- Para consultar os registros execute o seguinte:
```sql
select id_alocacao as "ID", nome as "Curso", nome_instrutor as "Instrutor" from alocacao
join cursos on curso = id
join instrutores on instrutor = id_instrutor;
```
- Clique em **Executar instrução SQL** ou `CTRL+Enter` para executar o código.

