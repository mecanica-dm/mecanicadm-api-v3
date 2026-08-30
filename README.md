# Mecânica DM - API de Gestão para Oficinas

[![SonarCloud](https://img.shields.io/badge/SonarCloud-Security_&_Quality-orange?logo=sonarcloud)](https://sonarcloud.io/project/overview?id=mecanica-dm_mecanicadm-api-v2)
![Versão da API](https://img.shields.io/badge/version-0.0.1-blue)

API RESTful para o sistema **Mecânica DM**, uma solução completa para gerenciamento de ordens de serviço, clientes, estoque e fluxo de trabalho em oficinas mecânicas.

Na **Fase 03** do 15SOAT, temos o objetivo de melhorar a estrutura separando o projeto em diversos repositórios, implementar monitoramento/observabilidade, e melhorar a infraestrutura do projeto.

---

## 📚 Documentação Externa e Modelagem

- **[Storytelling (Egon.io)](https://github.com/user-attachments/assets/fd2adfad-1fa9-469d-958a-1cf902666b36)**: Storytelling inicial do fluxo de funcionamento da mecânica.
- **[Dicionário de Dados (Notion)](https://lopsided-hourglass-4f8.notion.site/Dicion-rio-de-dados-32f0a8ca8e738075ae44c9ec0b5180b3?source=copy_link)**: Visão detalhada das entidades e relacionamentos do banco de dados.
- **[Event Storming (Miro)](https://miro.com/app/board/uXjVIT7cD_4=/?share_link_id=217316260154)**: Mapeamento de domínio e comportamento orientado a eventos do sistema.
- **[Dashboard do SonarCloud](https://sonarcloud.io/project/overview?id=mecanica-dm_mecanicadm-api-v2)**: Análise contínua de qualidade de código, vulnerabilidades e cobertura de testes.

---

## ✨ Funcionalidades Principais

- **🔩 Gestão de Ordens de Serviço**: Ciclo de vida completo, desde a criação, diagnóstico, execução até a entrega.
- **💰 Geração e Controle de Orçamentos**: Criação detalhada de orçamentos vinculados às O.S., controle de status de aprovação pelo cliente e gestão de custos de peças e mão de obra.
- **🖨️ Impressão de Orçamento**: Geração de relatórios de orçamento em formato PDF, retornados via API como string Base64 para facilitar o tráfego e a integração.
- **👤 Gestão de Clientes e Veículos**: Cadastro e consulta de clientes e veículos.
- **📦 Controle de Estoque**: Gerenciamento de materiais, com dedução automática de estoque ao adicionar em uma O.S.
- **🛠️ Catálogo de Serviços (Mão de Obra)**: Cadastro dos serviços prestados pela oficina.
- **🔐 Autenticação e Autorização**: Segurança baseada em JWT e criptografia de credenciais.
- **📊 Analytics**: Endpoints para extração de métricas e relatórios de performance.
- **🌐 Suporte a Múltiplos Idiomas**: Mensagens de erro e validação em Português, Inglês e Espanhol.

### 🖨️ Testando a Impressão de Orçamento (Base64 -> PDF)

A rota de impressão de orçamentos retorna o arquivo PDF codificado em uma string **Base64**. Para visualizar o arquivo gerado durante os seus testes no Swagger ou Postman:

1. Copie a string Base64 retornada no corpo da resposta (`response body`).
2. Acesse uma ferramenta confiável de conversão online, como:
    - **[Base64.guru - Decode Base64 to PDF](https://base64.guru/converter/decode/pdf)**
3. Cole a string copiada no campo principal do site e clique em "Decode". A visualização do arquivo PDF começará imediatamente.

---

## 🚀 Tecnologias Utilizadas

| Categoria        | Tecnologia                                            |
|------------------|-------------------------------------------------------|
| **Core**         | Java 21, Spring Boot 3                                |
| **Dados**        | Spring Data JPA, PostgreSQL, Flyway (Migrations)      |
| **Segurança**    | Spring Security, JWT (Java JWT)                       |
| **Documentação** | Springdoc (Swagger/OpenAPI 3)                         |
| **Testes**       | JUnit 5, Mockito, REST Assured, H2 (Banco em memória) |
| **Build**        | Maven                                                 |
| **Container**    | Docker, Docker Compose                                |

---

## 🏛️ Arquitetura e Decisões

O projeto segue uma arquitetura em camadas, inspirada em princípios de _Clean Architecture_ e _Domain-Driven Design (DDD)_, para garantir separação de responsabilidades, testabilidade e manutenibilidade. Além disso, as diretrizes de código são guiadas por **Architecture Decision Records (ADRs)** armazenadas no projeto.

- `domain`: Contém as entidades, agregados e regras de negócio principais.
- `usecase`: Orquestra o fluxo de operações, implementando os casos de uso através de `Commands` e `Queries`.
- `adapter`: Conecta o núcleo da aplicação com o mundo exterior (Controllers, Repositories).
- `service`: Implementações concretas dos casos de uso isolados.
- `infra`: Configurações de infraestrutura, segurança, tratamento global de exceções e configurações de banco de dados.

### 📝 ADRs (`docs/adr/`):

- **[ADR 001 - Nomenclatura de Consultas](docs/adr/001-nomenclatura_consultas.md)**
- ~~**[ADR 002 - Padrão UseCases e Commands](docs/adr/002-padrao_usecases_commands.md)**~~ 💤 Substituída por ADR 011
- **[ADR 003 - Lógica de Negócio no Domínio](docs/adr/003-logica_negocio_dominio.md)**
- **[ADR 004 - Padrão de Exceções Modulares](docs/adr/004-padrao_excecoes_modulares.md)**
- ~~**[ADR 005 - Estratégia de Soft Delete e Auditoria](docs/adr/005-estrategia_soft_delete_auditoria.md)**~~ 💤 Substituída por ADR 011
- **[ADR 006 - Contrato de Exceções de Domínio e i18n](docs/adr/006-contrato_excecoes_dominio_i18n.md)**
- **[ADR 007 - Pirâmide e Tipos de Testes](docs/adr/007-piramide_tipos_testes.md)**
- **[ADR 008 - Padrões de Testes de Integração](docs/adr/008-padroes_testes_integracao.md)**
- **[ADR 009 - Nomenclatura e Documentação de Testes](docs/adr/009-nomenclatura_documentacao_testes.md)**
- **[ADR 010 - Estratégia de i18n e Múltiplos Idiomas](docs/adr/010-estrategia_i18n_multi_idioma.md)**
- **[ADR 011 - Arquitetura Limpa Purista para Novas Features 🆕](docs/adr/011-arquitetura-limpa-purista-novas-features.md)**

### 📝 RFCs (`docs/rfc/`):

- **[RFC 001 - Escolha de nuvem](docs/rfc/001-escolha_de_nuvem.md)**
- **[RFC 002 - Escolha de banco de dados](docs/rfc/002-escolha_banco_de_dados.md)**

### Componentes da aplicação

![Componentes da aplicação](docs/assets/c4-componentes-mecanicadm.png)

### Fluxo de deploy

[Link para imagem do fluxo](docs/assets/fluxo-deploy-fase-03.png)

<div align="center">

```mermaid
flowchart LR
    TRIGGER[Disparo do Workflow] --> COND{Evento}
    COND -->|push| M1[Branch: main]
    COND -->|pull_request| PR[Pipeline PR]
    COND -->|workflow_dispatch| WD[Manual]

    M1 --> BUILD
    PR --> BUILD
    WD --> BUILD

    subgraph BUILD[build-and-test]
        direction LR
        A1[Checkout]
        A2[Setup JDK 21]
        A3[Build e Testes]
        A4[Análise Sonar]
        A1 --> A2 --> A3 --> A4
    end

    subgraph SEC[security-scan]
        direction LR
        S1[Checkout]
        S2[Subir aplicação]
        S3[ZAP Scan OpenAPI]
        S4[Upload Relatório]
        S5[Parar containers]
        S1 --> S2 --> S3 --> S4 --> S5
    end

    BUILD -->|sucesso| SEC

    subgraph PUB[publish-and-deploy]
        direction LR
        P1[Login Docker Hub]
        P2[Build e push imagem]
        P3[Disparar deploy K8s]
        P1 --> P2 --> P3
    end

    SEC -->|sucesso| GATE{Em main?}
    GATE -->|sim| PUB
    GATE -->|não| FIM1[Fim - sem deploy]
    PUB --> FIM2[Deploy no K8s]
```

</div>

* build-and-test: Responsável por fazer o maven build e executar os testes da aplicação
* security-scan: Rodamos o ZAP Scan para verificar problemas de segurança
* publish-and-deploy: Aqui fazemos o build da imagem docker e publicamos para o Docker Hub, além disso fazemos um trigger para rodar a próxima pipe do repositório de k8s

### Diagrama de Entidade-Relacionamento

[Link para imagem do diagrama](docs/assets/erd-mecanicadm.png)

```mermaid
erDiagram
    USERS ||--o{ USER_ROLES : "possui"
    USERS ||--o{ PASSWORD_RESET_TOKENS : "solicita"

    CLIENTS ||--o{ WORK_ORDERS : "possui"
    VEHICLE ||--o{ WORK_ORDERS : "é utilizado em"

    LABORS ||--o{ WORK_ORDER_LABOR_ITEMS : "é registrado em"
    MATERIALS ||--o{ WORK_ORDER_MATERIAL_ITEMS : "é usado em"
    MATERIALS ||--o{ STOCK_MOVEMENTS : "gera"

    WORK_ORDERS ||--o{ WORK_ORDER_LABOR_ITEMS : "tem"
    WORK_ORDERS ||--o{ WORK_ORDER_MATERIAL_ITEMS : "tem"
    WORK_ORDERS ||--o{ WORK_ORDER_BUDGETS : "tem"
    WORK_ORDERS ||--o{ STOCK_MOVEMENTS : "registra"
    WORK_ORDERS ||--o{ BUDGET_DECISION_TOKENS : "gera"

    USERS {
        uuid id PK
        timestamp date_created
        timestamp date_updated
        timestamp deleted_at
        varchar email UK
        varchar password
        varchar name
    }

    USER_ROLES {
        uuid user_id PK,FK
        varchar role PK
    }

    PASSWORD_RESET_TOKENS {
        uuid id PK
        varchar token UK
        uuid user_id FK
        timestamp expiry_date
    }

    VEHICLE {
        varchar license_plate PK
        varchar model
        varchar brand
        smallint model_year
        timestamp date_created
        timestamp date_updated
        timestamp deleted_at
    }

    CLIENTS {
        uuid id PK
        varchar name
        varchar email UK
        varchar document UK
        varchar phone
        timestamp date_created
        timestamp date_updated
        timestamp deleted_at
    }

    LABORS {
        uuid id PK
        varchar name
        decimal price
        timestamp date_created
        timestamp date_updated
        timestamp deleted_at
    }

    MATERIALS {
        uuid id PK
        varchar name
        varchar brand
        text description
        decimal price
        varchar type
        timestamp date_created
        timestamp date_updated
        timestamp deleted_at
    }

    WORK_ORDERS {
        uuid id PK
        uuid client_id FK
        varchar vehicle_id FK
        text description
        int status
        timestamp execution_start_at
        timestamp execution_end_at
        timestamp date_created
        timestamp date_updated
        timestamp deleted_at
    }

    WORK_ORDER_LABOR_ITEMS {
        uuid id PK
        uuid work_order_id FK
        uuid labor_id FK
        varchar status
        timestamp execution_start_at
        timestamp execution_end_at
    }

    WORK_ORDER_MATERIAL_ITEMS {
        uuid id PK
        uuid work_order_id FK
        uuid material_id FK
        int quantity
    }

    WORK_ORDER_BUDGETS {
        uuid work_order_id PK,FK
        decimal total_price
        varchar status
        text observation
    }

    STOCK_MOVEMENTS {
        uuid id PK
        uuid material_id FK
        uuid work_order_id FK
        int quantity
        varchar type
        timestamp date_created
        timestamp date_updated
        timestamp deleted_at
    }

    BUDGET_DECISION_TOKENS {
        uuid id PK
        uuid work_order_id FK
        varchar token UK
        boolean used
        timestamp created_at
    }
```

### Infraestrutura provisionada

![Infraestrutura provisionada](docs/assets/old-assets/infra-provisionada_02.png)

* VPC: Virtual Private Cloud, um ambiente seguro e isolado onde podemos rodar os nossos recursos.  
* Internet Gateway: Necessário para comunicação da VPC com a internet.
* EC2: Elastic Compute Cloud, as máquinas que criamos para executar os nossos serviços.
* EKS: Elastic Kubernetes Service, serviço onde orquestramos os containers Kubernetes.

Para ir mais a fundo em como executar o terraform do projeto, basta acessar a doc de [instruções do terraform](infra/terraform/instrucoes.md).

---

## 🏁 Como Começar

Obs: Caso queira executar o ambiente sem o kubernetes, o passo a passo para execução com apenas o docker compose pode ser encontrado no README da fase um no [diretório de READMEs antigos](docs/old-readme/README-fase01.md).
* Apenas se atentar para criar o arquivo .env, temos o exemplo .env.example para isso

### Pré-requisitos

- [Docker](https://www.docker.com/get-started) e [Docker Compose](https://docs.docker.com/compose/install/)
- [Kubectl](https://kubernetes.io/pt-br/docs/tasks/tools/)

### Ambiente Completo com Docker e Kubernetes (Fase 02)

Utilize o Kustomize para aplicar todos os manifestos de uma vez:

 ```bash
 kubectl apply -k ./k8s/
 ```

Confirme se todos os Pods, Services e Deployments foram criados no namespace correto:

 ```bash
 kubectl get all -n mecanicadm
 ```
 
Para testar o HPA, criamos um bash script simples que gera stress na API:
```bash
 ./k8s/load-test.sh
 ```

Para ir mais a fundo em como executar o kubernetes no projeto, basta acessar a doc de [instruções do kubernetes](k8s/instrucoes.md).

---

## 📄 Documentação da API

Com a API em execução, a documentação interativa do Swagger UI fica disponível em:

`http://localhost:80/swagger-ui.html`

A especificação OpenAPI 3 pode ser acessada em `/v3/api-docs`.

### 🔑 Credenciais de Acesso Iniciais

- **Email**: `admin@mecanicadm.com`
- **Senha**: `Senha123`

---

## ✅ Testes

O projeto possui uma suíte de testes unitários e de integração para garantir a qualidade e a estabilidade do código.

Para executar todos os testes via Maven:
```bash
mvn clean verify
```
Os relatórios de cobertura de testes (Jacoco) são gerados em `target/site/jacoco/`.

---
