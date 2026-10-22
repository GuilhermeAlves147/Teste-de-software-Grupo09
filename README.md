# 🧪 Teste de Software — Grupo 09

<p align="center">
  <strong>Projeto Final</strong>
  <br>
  Planejamento, execução e documentação de testes de software em um sistema de marketplace.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Projeto-Acadêmico-blue?style=for-the-badge" alt="Projeto acadêmico">
  <img src="https://img.shields.io/badge/Área-Qualidade_de_Software-purple?style=for-the-badge" alt="Qualidade de software">
  <img src="https://img.shields.io/badge/Plataforma-GitHub-black?style=for-the-badge&logo=github" alt="GitHub">
</p>

---

## 📌 Sobre o projeto

Este projeto tem como objetivo aplicar os conceitos e as técnicas de **teste de software** estudados durante a disciplina, utilizando como referência um sistema de marketplace que simula operações de comércio eletrônico.

A proposta envolve o planejamento dos testes, a definição de casos de teste, a documentação de histórias de usuário e a elaboração de relatórios para avaliar o comportamento do sistema.

Com isso, buscamos compreender a importância de um processo de testes bem estruturado para identificar possíveis falhas, verificar funcionalidades e contribuir para a qualidade do software.

## 🎯 Objetivos

- Aplicar técnicas de teste de software na prática.
- Elaborar um planejamento de testes.
- Definir casos de teste para funcionalidades do sistema.
- Documentar histórias de usuário e seus comportamentos esperados.
- Registrar os resultados e produzir relatórios de testes.
- Compreender a importância da qualidade e da validação de software.

## 🛒 Sistema utilizado

O sistema de referência é um marketplace com funcionalidades relacionadas a:

| Funcionalidade | Descrição |
|---|---|
| 👤 Usuários | Representação dos usuários da plataforma |
| 🏪 Vendedores | Gerenciamento de produtos |
| 🛍️ Produtos | Cadastro, visualização e exclusão de produtos |
| 🗂️ Categorias | Organização dos produtos |
| 🛒 Carrinho | Organização dos itens de compra |
| 📦 Pedidos | Representação do processo de compra |

Os testes documentados neste repositório incluem histórias de usuário relacionadas ao cadastro, à visualização e à exclusão de produtos.

---

## ⚙️ Como executar o projeto

Para executar os testes na prática, é preciso colocar o sistema de marketplace (API em Spring Boot com banco MySQL) em funcionamento. Siga os passos abaixo.

### 1. O que precisa estar instalado

- **JDK** (a versão do `pom.xml`/`build.gradle`; Java 17 ou superior costuma servir para Spring Boot 3).
- **Maven** ou **Gradle**, ou use o wrapper do projeto (`mvnw` / `gradlew`), que dispensa a instalação.
- **MySQL 8.0 ou superior**, em execução.
- **Git**, para clonar o repositório.
- (Opcional) **Postman**, para chamar a API, e **MySQL Workbench** ou DBeaver, para consultar o banco.

### 2. Clonar o repositório

```bash
git clone <URL-DO-REPOSITORIO>
cd <pasta-do-projeto>
```

### 3. Criar o banco de dados

Os scripts ficam na pasta `sql/` e devem ser executados nesta ordem:

```bash
mysql -u root -p < sql/01_ddl.sql      # cria o banco marketplace_db, tabelas, triggers e papéis
mysql -u root -p < sql/02_carga.sql    # carga de dados de teste
```

> ⚠️ O `01_ddl.sql` apaga e recria o banco `marketplace_db`. Não rode em um banco com dados que você queira manter.
> O Hibernate **não** cria tabelas: o esquema vem só do script (`ddl-auto` desativado).

Usuários da carga (senha de todos: `Senha@123`), por exemplo:
`daniel.santos@email.com` e `gabriela.nascimento@email.com`.

### 4. Configurar as credenciais do banco

Abra `src/main/resources/application.properties` e ajuste a conexão:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/marketplace_db?useSSL=false&serverTimezone=America/Sao_Paulo&allowPublicKeyRetrieval=true
spring.datasource.username=SEU_USUARIO
spring.datasource.password=SUA_SENHA
spring.jpa.hibernate.ddl-auto=none
```

As credenciais não devem ser versionadas. Duas formas de evitar isso:

- Usar variáveis de ambiente no arquivo e definir os valores na sua máquina:

  ```properties
  spring.datasource.username=${DB_USER}
  spring.datasource.password=${DB_PASSWORD}
  ```

- Ou criar um `application-local.properties` (já ignorado pelo `.gitignore`) e iniciar com o perfil `local`.

> Confira no seu `application.properties` os nomes exatos das chaves (por exemplo, a do segredo do JWT, se existir) e a porta do servidor. O padrão do Spring Boot é a `8080`.

### 5. Executar a aplicação

```bash
./mvnw spring-boot:run        # Maven
# ou
./gradlew bootRun             # Gradle
```

Quando aparecer `Started ... in X seconds`, a API está no ar em `http://localhost:8080`.

### 6. Testar rapidamente

1. No Postman, envie `POST http://localhost:8080/auth/login` com e-mail e senha de um usuário da carga.
2. Copie o token JWT da resposta.
3. Nas demais requisições, envie o cabeçalho `Authorization: Bearer <token>`.

### 🩺 Problemas comuns

| Sintoma | Causa provável |
|---|---|
| `Access denied for user` | Usuário ou senha errados em `application.properties` |
| `Unknown database 'marketplace_db'` | O `01_ddl.sql` ainda não foi executado |
| `Communications link failure` | MySQL parado ou porta diferente de 3306 |
| `Port 8080 already in use` | Defina `server.port=8081` no `application.properties` |

---

## 📂 Documentação do projeto

Os documentos estão disponíveis diretamente neste repositório.

### 📋 Planejamento e requisitos

- [📄 Planejamento de Testes](./PlanejamentoTeste.docx)
- [📄 Documento de Visão](./ts_documento_de_visao.pdf)

### 🧪 Casos e histórias de teste

- [📄 Casos de Teste](./Casos_de_Teste.docx)
- [📄 História de Usuário — Cadastrar Produto](./ts_historia_de_usuario_cadastrarProduto.pdf)
- [📄 História de Usuário — Visualizar Produto](./ts_historia_de_usuario_visualizarProduto.pdf)
- [📄 História de Usuário — Excluir Produto](./ts_historia_de_usuario_excluirProduto.pdf)

### 📊 Relatório

- [📄 Relatório de Teste de Software](./Relatorio%20Teste%20de%20Software.pdf)

---

## 🔍 Etapas do trabalho

O desenvolvimento do projeto é organizado nas seguintes etapas:

1. **Análise do sistema:** compreensão das funcionalidades e do comportamento esperado.
2. **Planejamento:** definição do escopo e da organização dos testes.
3. **Documentação:** elaboração das histórias de usuário e dos casos de teste.
4. **Verificação:** análise dos cenários e dos resultados obtidos.
5. **Relatório:** registro das atividades e consolidação da documentação.

---

## 👥 Integrantes

| Integrante |
|---|
| Guilherme Alves de Paulo |
| Luís Felipe da Costa Maciel |
| Valter Junio Lopes Xavier |
| Ewerthon Klaiver Soares Marques |

---

## 🎓 Contexto acadêmico

**Projeto:** Teste de Software — Grupo 09  
**Finalidade:** aplicação prática dos conceitos de planejamento, documentação e verificação de software.

---

<p align="center">
  Desenvolvido para fins acadêmicos.
  <br>
  <strong>Grupo 09 • 2026</strong>
</p>
