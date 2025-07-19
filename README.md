# Stack n8n + Evolution API + Redis + Postgres

[![Docker Compose](https://img.shields.io/badge/docker-compose-blue?logo=docker)](https://docs.docker.com/compose/)
[![PostgreSQL](https://img.shields.io/badge/postgres-15-blue?logo=postgresql)](https://www.postgresql.org/)
[![Redis](https://img.shields.io/badge/redis-7.x-red?logo=redis)](https://redis.io/)
[![n8n](https://img.shields.io/badge/n8n-automation-orange?logo=n8n)](https://n8n.io/)

Este repositorio contiene un **docker-compose.yml** listo para levantar un entorno con [n8n](https://n8n.io/), **Evolution API**, Redis y PostgreSQL.  
Es un fork de [PauloVaz-dev/n8n_evolution-api_redis_postgres](https://github.com/PauloVaz-dev/n8n_evolution-api_redis_postgres) y busca simplificar la puesta en marcha local de estos servicios.

---
## Servicios incluidos

- **n8n** – Plataforma de automatización y orquestación de flujos.
- **Evolution API** – Servicio para integraciones de WhatsApp que utiliza Redis y Postgres.
- **Redis** – Motor de almacenamiento en memoria empleado para caché y mensajes.
- **Postgres** – Base de datos relacional para datos persistentes.

Cada servicio se declara en `docker-compose.yml` y se conecta a la red `my_network`.

---
## Configuración

1. Copia el archivo de ejemplo y ajusta las variables necesarias:

   ```bash
   cp .env-example .env
   # Edita .env para establecer tus credenciales y dominios
   ```

   Las variables principales son:

   | Variable                  | Descripción                              |
   |---------------------------|------------------------------------------|
   | `DOMAIN_NAME`             | Dominio principal (por ej. `example.com`) |
   | `SUBDOMAIN`               | Subdominio donde se expondrá n8n          |
   | `GENERIC_TIMEZONE`        | Zona horaria por defecto                  |
   | `AUTHENTICATION_API_KEY`  | Clave global para Evolution API           |
   | `DATABASE_CONNECTION_URI` | URI de conexión para Postgres             |

   El archivo `.env-example` incluye muchas más opciones que puedes revisar para personalizar Evolution API (colas, cache, webhooks, etc.).

2. Crea la red (si aún no existe):

   ```bash
   docker network create my_network
   ```

---
## Uso

Levanta el stack con:

```bash
docker compose up -d
```

Una vez inicializado podrás acceder a:

- **n8n** → `https://<SUBDOMAIN>.<DOMAIN_NAME>:5678`
- **Evolution API** → `http://localhost:8080`
- **Postgres** → puerto `5432`
- **Redis** → puerto `6379`

Para detener y eliminar los contenedores ejecuta:

```bash
docker compose down
```

---
## Ejemplo de flujo en n8n

1. Accede a la interfaz web de n8n.
2. Crea un nuevo workflow y añade nodos que consuman la Evolution API o cualquier otro servicio.
3. Guarda y ejecuta tu workflow para validar que los contenedores están corriendo correctamente.

---
## Créditos

Basado en el trabajo original de [PauloVaz-dev](https://github.com/PauloVaz-dev/n8n_evolution-api_redis_postgres). ¡Muchas gracias por compartir la configuración!
