# 🏥 Projeto – Saúde Solidária (DevOps + Java Spring Boot)

O **Saúde Solidária** é uma aplicação que conecta **doadores** e **beneficiários** de medicamentos, promovendo solidariedade e eficiência na gestão de doações de forma digital.  
Desenvolvido em **Java Spring Boot**, o projeto foi totalmente **containerizado** e automatizado com **CI/CD via GitHub Actions** e **deploy em servidores Ubuntu (Oracle Cloud)**.

---

## 🚀 Como executar localmente com Docker

### Pré-requisitos:
- Docker e Docker Compose instalados
- MongoDB Atlas configurado (ou usar container local)
- Variáveis de ambiente definidas no `.env`

### Passos para executar:
```bash
# Clonar o repositório
git clone https://github.com/HugoCorrea01/saude-solidaria-front-spring.git
cd saude-solidaria-front-spring

# Build da imagem Docker
docker build -t saude-solidaria:latest .

# Subir containers (aplicação + banco, se configurado)
docker compose up -d
```

> A aplicação ficará disponível em:  
> 🌐 **http://localhost:8080**

---

## ⚙️ Pipeline CI/CD

O pipeline foi implementado com **GitHub Actions**, automatizando **build**, **testes**, **publicação no GHCR** e **deploy remoto**.

### 🧩 Etapas principais:
1. **Build & Test:** Maven compila e executa os testes automatizados.  
2. **Build da Imagem Docker:** A imagem é gerada e publicada no **GitHub Container Registry (GHCR)**.  
3. **Deploy Automatizado via SSH:**  
   - *Branch `develop` → deploy no ambiente Staging*  
   - *Branch `master` → deploy no ambiente Produção*

### 🔑 Secrets utilizados:
- `STAGING_HOST`, `STAGING_USER`, `STAGING_SSH_KEY`  
- `PROD_HOST`, `PROD_USER`, `PROD_SSH_KEY`  
- `GHCR_TOKEN` (para login no container registry)

---

## 🐳 Containerização

A aplicação é empacotada em um container Docker para garantir portabilidade e consistência entre os ambientes.

### **Dockerfile**
```dockerfile
FROM openjdk:17-jdk-slim
WORKDIR /app
COPY target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "/app/app.jar"]
```

### **Arquivos de orquestração**
- `docker-compose.staging.yml` → ambiente de homologação  
- `docker-compose.prod.yml` → ambiente de produção  
- `docker-compose.yml` → execução local (com MongoDB)

Cada arquivo define serviços, volumes e variáveis de ambiente específicos para cada etapa do ciclo DevOps.

---

## 🖼️ Prints e Evidências do Funcionamento

### ✅ **Evidência 1 — Pipeline CI/CD**
Workflow no GitHub Actions com jobs:
- `build/test`
- `docker`
- `deploy-staging`
- `deploy-production`

### ✅ **Evidência 2 — Imagem publicada no GHCR**
Repositório:  
`ghcr.io/hugocorrea01/saude-solidaria-front-spring:staging`  
`ghcr.io/hugocorrea01/saude-solidaria-front-spring:prod`

### ✅ **Evidência 3 — Containers em execução**
```bash
docker ps
```
Mostra os containers `saude-solidaria-staging` e `saude-solidaria-prod` ativos.

### ✅ **Evidência 4 — Aplicação acessível publicamente**
- **Staging:** http://163.176.223.17  
- **Produção:** http://163.176.223.17:8080  

Aplicação carregando dados em tempo real do **MongoDB Atlas**, confirmando integração completa entre **frontend, backend e banco de dados**.

---

## 🧠 Tecnologias Utilizadas

| Categoria | Ferramenta / Tecnologia |
|------------|------------------------|
| **Linguagem** | Java 17 |
| **Framework** | Spring Boot |
| **Banco de Dados** | MongoDB Atlas |
| **DevOps / CI/CD** | GitHub Actions |
| **Containerização** | Docker & Docker Compose |
| **Cloud Provider** | Oracle Cloud (Ubuntu Server) |
| **Gerenciador de Dependências** | Maven |
| **Registry** | GitHub Container Registry (GHCR) |

---

## 👨‍💻 Equipe
- **Hugo Correa Farranha – RM 558215**  
- **Milton Ribeiro – RM 556051**  
- **Victor Mazzola – RM 557130**  

📍 FIAP – Análise e Desenvolvimento de Sistemas | Fase: DevOps & Cloud Computing  
📅 Outubro / 2025
