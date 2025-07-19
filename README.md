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

1. Copia el archivo de ejemplo y ajusta las variables necesarias. Puedes crear
   un archivo `.env` para producción o `.env.local` para pruebas en WSL:

   ```bash
   cp .env-example .env
   # o para un entorno local
   cp .env-example .env.local
   ```

   Luego edita el archivo elegido para establecer tus credenciales y dominios.
   Las variables principales son:

   | Variable                  | Descripción                              |
   |---------------------------|------------------------------------------|
   | `DOMAIN_NAME`             | Dominio principal (por ej. `example.com`) |
   | `SUBDOMAIN`               | Subdominio donde se expondrá n8n          |
   | `GENERIC_TIMEZONE`        | Zona horaria por defecto                  |
   | `AUTHENTICATION_API_KEY`  | Clave global para Evolution API           |
   | `DATABASE_CONNECTION_URI` | URI de conexión para Postgres             |
   | `N8N_HOST`                | Hostname donde se publicará n8n           |
   | `N8N_PROTOCOL`            | `http` o `https` según el entorno        |
   | `N8N_LISTEN_ADDRESS`      | Dirección de escucha de n8n              |

   El archivo `.env-example` incluye muchas más opciones que puedes revisar para
   personalizar Evolution API (colas, cache, webhooks, etc.). Para un entorno
   local típico puedes usar `N8N_HOST=localhost` y `N8N_PROTOCOL=http`.

2. Crea la red (si aún no existe):

   ```bash
   docker network create my_network
   ```

---
## Uso

Para levantar el entorno basta con indicar el archivo de variables que prefieras:

```bash
# Producción
docker compose --env-file .env up -d

# Entorno local (WSL)
docker compose --env-file .env.local up -d
```

Una vez inicializado podrás acceder a:

- **n8n** → `https://<SUBDOMAIN>.<DOMAIN_NAME>:5678` (o `http://localhost:5678` en modo local)
- **Evolution API** → `http://localhost:8080`
- **Postgres** → puerto `5432`
- **Redis** → puerto `6379`

Para detener y eliminar los contenedores ejecuta:

```bash
# Con el mismo archivo de variables usado al levantar el stack
docker compose --env-file .env down
```

---
## Ejemplo de flujo en n8n

1. Accede a la interfaz web de n8n.
2. Crea un nuevo workflow y añade nodos que consuman la Evolution API o cualquier otro servicio.
3. Guarda y ejecuta tu workflow para validar que los contenedores están corriendo correctamente.

---
## Créditos

Basado en el trabajo original de [PauloVaz-dev](https://github.com/PauloVaz-dev/n8n_evolution-api_redis_postgres). ¡Muchas gracias por compartir la configuración!
