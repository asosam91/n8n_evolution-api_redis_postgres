# Projeto Docker Compose: N8N, Evolution API, Redis e Postgres

Este repositório fornece um arquivo **docker-compose.yml** que orquestra múltiplos serviços (N8N, Evolution API, Redis e Postgres), facilitando a configuração e execução de todo o ambiente de forma integrada.

---

## Visão Geral

Este projeto reúne:

- **n8n**: Uma plataforma de automação e fluxo de trabalho que permite integrar diferentes serviços por meio de uma interface de arrastar e soltar.
- **Evolution API**: Um serviço personalizado (baseado em imagem `atendai/evolution-api:homolog`) que depende do Redis e Postgres para armazenar dados e fornecer uma API.
- **Redis**: Banco de dados em memória, utilizado para cache e armazenamento de dados de rápida consulta.
- **Postgres**: Banco de dados relacional, usado para persistência de dados a longo prazo.

O objetivo é disponibilizar todos esses serviços integrados numa mesma stack, simplificando o desenvolvimento, a homologação e o deploy.

---

## Estrutura do Projeto

---

## Pré-requisitos

- **Docker** instalado em sua máquina (versão 20+).
- **Docker Compose** (versão 2.0 ou superior, ou Docker Desktop com suporte nativo a Compose).
- Opcionalmente, um arquivo **.env** com as variáveis de ambiente necessárias (ex: `SUBDOMAIN`, `DOMAIN_NAME`, `GENERIC_TIMEZONE`, etc.).

---

## Configuração

Antes de executar, verifique as variáveis de ambiente usadas pelos serviços:

Rede

```bash
docker network create my_network
```

## Como Executar

1. **Clone o repositório**:

   ```bash
   git clone https://github.com/seu_usuario/seu_repositorio.git
   cd seu_repositorio
   ```

## Em construção
