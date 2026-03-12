<div align="center">

# AlberguePro

**Sistema Web de Gestão de Albergues para Pessoas em Situação de Vulnerabilidade**

[![Java](https://img.shields.io/badge/Java-21-ED8B00?style=flat-square&logo=openjdk&logoColor=white)](https://openjdk.org/projects/jdk/21/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.4.9-6DB33F?style=flat-square&logo=springboot&logoColor=white)](https://spring.io/projects/spring-boot)
[![MySQL](https://img.shields.io/badge/MySQL-8.0-4479A1?style=flat-square&logo=mysql&logoColor=white)](https://www.mysql.com/)
[![Bootstrap](https://img.shields.io/badge/Bootstrap-5.3-7952B3?style=flat-square&logo=bootstrap&logoColor=white)](https://getbootstrap.com/)
[![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?style=flat-square&logo=docker&logoColor=white)](https://docs.docker.com/compose/)
[![License](https://img.shields.io/badge/Licen%C3%A7a-Acad%C3%AAmica-blue?style=flat-square)](#)

</div>

---

## 📋 Sobre o Projeto

O **AlberguePro** é um sistema web desenvolvido como Trabalho de Conclusão de Curso (TCC) do curso de Sistemas para Internet da **UniALFA** (2025). A plataforma foi projetada para apoiar a gestão operacional de albergues e casas de acolhimento, centralizando o controle de acolhidos, estoque, patrimônio e leitos em uma única interface.

### ✨ Funcionalidades

| Módulo | Descrição |
|---|---|
| 🔐 **Autenticação** | Login com controle de acesso por papéis (Admin / Master) via Spring Security |
| 👤 **Acolhidos** | Cadastro completo multi-etapas: dados pessoais, saúde, vínculos, histórico de rua |
| 📦 **Estoque** | Controle de produtos (alimentos, higiene, limpeza), baixas e histórico de movimentações |
| 🏛️ **Patrimônio** | Cadastro e rastreamento de bens da instituição |
| 🛏️ **Quartos & Vagas** | Gestão de leitos com alocação de acolhidos por vaga disponível |
| 👥 **Usuários** | Gerenciamento de contas com hierarquia de permissões |
| 📊 **Relatórios** | Geração de relatórios estratégicos em PDF e Excel (JasperReports / Apache POI / iText) |

---

## 🛠️ Stack Tecnológica

### Backend
- **Java 21** + **Spring Boot 3.4.9**
- **Spring Data JPA** (Hibernate) — ORM e persistência
- **Spring Security** — autenticação e autorização
- **Spring Boot Validation** — validação de entidades
- **Lombok** — redução de boilerplate
- **MySQL Connector/J** — driver JDBC
- **Google Cloud SQL Socket Factory** — suporte a Cloud SQL

### Frontend
- **Thymeleaf** + `thymeleaf-extras-springsecurity6` — templates server-side
- **Bootstrap 5.3.3** — framework CSS (via CDN)
- **Bootstrap Icons 1.11.3** — ícones (via CDN)
- **ApexCharts** — gráficos interativos no dashboard
- **Inter** (Google Fonts) — tipografia

### Relatórios
- **JasperReports 6.21.3**
- **Apache POI 5.2.3** (xlsx)
- **iText 5.5.13.3** (PDF)

### Infraestrutura
- **Docker** + **Docker Compose**
- **MySQL 8.0** (container)
- **Spring Boot DevTools** (Hot Reload em desenvolvimento)

---

## 🚀 Executando Localmente (Desenvolvimento)

### Pré-requisitos

Certifique-se de ter instalado na sua máquina:

| Ferramenta | Versão mínima | Download |
|---|---|---|
| JDK | 21 | [openjdk.org](https://openjdk.org/projects/jdk/21/) |
| Maven | 3.9+ | [maven.apache.org](https://maven.apache.org/download.cgi) |
| MySQL | 8.0 | [mysql.com](https://dev.mysql.com/downloads/) |
| Git | qualquer | [git-scm.com](https://git-scm.com/) |

> **Alternativa:** Se preferir não instalar o MySQL localmente, use o [método com Docker](#-executando-com-docker) — ele sobe o banco automaticamente.

### Passo a Passo

**1. Clone o repositório**

```bash
git clone https://github.com/danilorosa82/18-SI-UniALFA-TCC-2025-02.git
cd 18-SI-UniALFA-TCC-2025-02
```

**2. Crie o banco de dados no MySQL**

Conecte-se ao seu MySQL local e execute:

```sql
CREATE DATABASE IF NOT EXISTS alberguepro CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

**3. Configure as credenciais do banco**

Edite o arquivo `src/main/resources/application.properties` (ou crie um `application-local.properties`) com suas credenciais:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/alberguepro?createDatabaseIfNotExist=true&useSSL=false&serverTimezone=America/Sao_Paulo
spring.datasource.username=seu_usuario
spring.datasource.password=sua_senha
spring.jpa.hibernate.ddl-auto=update
```

**4. Instale as dependências e compile**

```bash
./mvnw clean install -DskipTests
```

> No Windows, substitua `./mvnw` por `mvnw.cmd`.

**5. Execute a aplicação**

```bash
./mvnw spring-boot:run
```

Ou, se preferir rodar o JAR diretamente após o build:

```bash
java -jar target/alberguepro-0.0.1-SNAPSHOT.jar
```

**6. Acesse no navegador**

```
http://localhost:8080
```

> ⚠️ A aplicação utiliza recursos de CDN (Bootstrap, Fontes, Ícones). **Conexão com internet é necessária** para carregar a interface corretamente.

---

## 🐳 Executando com Docker

A forma mais rápida de subir o ambiente completo (aplicação + banco de dados) sem nenhuma configuração adicional.

### Pré-requisitos

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) instalado e em execução

### Passo a Passo

**1. Clone o repositório**

```bash
git clone https://github.com/danilorosa82/18-SI-UniALFA-TCC-2025-02.git
cd 18-SI-UniALFA-TCC-2025-02
```

**2. Compile o projeto**

```bash
./mvnw clean install -DskipTests
```

**3. Suba os containers**

```bash
docker-compose up -d
```

Isso irá:
- Construir a imagem Docker da aplicação
- Subir um container MySQL 8.0
- Subir a aplicação Spring Boot conectada ao banco

**4. Acesse no navegador**

```
http://localhost:8081
```

**5. (Opcional) Acompanhe os logs**

```bash
docker-compose logs -f alberguepro
```

### Parando a aplicação

```bash
docker-compose down
```

Para remover também os volumes (dados do banco):

```bash
docker-compose down -v
```

### Portas utilizadas (Docker)

| Serviço | Porta no host | Porta no container |
|---|---|---|
| Aplicação | `8081` | `8081` |
| MySQL | `3307` | `3306` |

> A porta do MySQL foi mapeada para `3307` no host para evitar conflito com instalações locais.

---

## 📁 Estrutura do Projeto

```
alberguepro/
├── src/
│   ├── main/
│   │   ├── java/edu/unialfa/alberguepro/
│   │   │   ├── config/          # Configurações (Security, MVC, etc.)
│   │   │   ├── controller/      # Controllers Spring MVC
│   │   │   ├── model/           # Entidades JPA
│   │   │   ├── repository/      # Repositórios Spring Data
│   │   │   ├── service/         # Camada de negócio
│   │   │   └── AlberguePro*.java # Classe principal
│   │   └── resources/
│   │       ├── static/
│   │       │   └── css/         # Design system (custom-new.css)
│   │       ├── templates/       # Templates Thymeleaf
│   │       │   ├── fragments/   # Componentes reutilizáveis
│   │       │   ├── estoque/
│   │       │   ├── patrimonio/
│   │       │   ├── vaga/
│   │       │   ├── Quarto/
│   │       │   ├── cadastroAcolhido/
│   │       │   ├── admin/
│   │       │   └── relatorios/
│   │       └── application.properties
│   └── test/
├── CHANGELOG.md                 # Histórico de versões
├── docker-compose.yml
├── Dockerfile
├── mvnw / mvnw.cmd
└── pom.xml
```

---

## 👥 Autoria

| Nome | Papel |
|---|---|
| **Gabriel Paiva** | Desenvolvedor — TCC SI UniALFA 2025 |
| **Danilo Rosa** | Desenvolvedor — TCC SI UniALFA 2025 |
| **Thiago da Silva** | Desenvolvedor — TCC SI UniALFA 2025 |

---

## 📄 Licença

Este projeto foi desenvolvido para fins acadêmicos como Trabalho de Conclusão de Curso no curso de **Sistemas de Informação** da **UniALFA** (2025). Todos os direitos reservados ao autor.
