# N8N Self-Hosted on Hetzner (with Coolify)
This repository contains the necessary Docker Compose configuration to deploy a complete self-hosted N8N environment, including its workers and a PostgreSQL database. The architecture is optimized for deployment on the Coolify automation platform.

## 🛠️ Stack Components
- n8n: The main N8N instance that manages the user interface and webhooks.
- n8n-worker: (Optional) Dedicated instances for processing workflow executions in parallel.
- postgres: The persistent database for storing all N8N data, such as workflows and credentials.
- Coolify: The platform that automates the deployment and management of the entire stack on a server.

## 🚀 Deployment Guide with Coolify
To deploy this stack on your server, follow these simple steps:

1. **Connect the Repository to Coolify:**
- Open the Coolify dashboard in your browser.
- Navigate to the "Resources" section and click "Add Resource".
- Select the "Compose" option.
- Configure the connection to this GitHub repository.

2. **Configure Environment Variables:**
- Coolify will automatically import the docker-compose.yml file.
- Go to the "Environment Variables" section within the resource settings.
- Add each variable listed in the /.env.example file with its corresponding value. For security, do not save a .env file with real values in the repository.

3. **Configure the Domain and Port:**
- In the Coolify resource settings, assign the domain you purchased (for example, n8n.yourdomain.com).
- Coolify will handle the SSL certificate and reverse proxy setup automatically.

4. **Deploy the Stack:**
- Once all configurations are in place, click the "Deploy" button. Coolify will build the environment, start the containers, and get your N8N instance up and running.

## 🧩 Environment Variables
The following variables must be configured in Coolify for the stack to work correctly.

| Variable |	Description |	Example Value |
|:---- |:---- |:---- |
| POSTGRES_USER |	The username for the PostgreSQL database. | coolify_n8n_user |
| POSTGRES_PASSWORD |	The password for the PostgreSQL user.	| your-secure-password |
| POSTGRES_DB |	The name of the database.	| n8n_db |
| POSTGRES_NON_ROOT_USER |	The PostgreSQL user with limited permissions.	| n8n |
| POSTGRES_NON_ROOT_PASSWORD |	The password for the N8N user.	| another-secure-password |
| GENERIC_TIMEZONE |	The timezone for N8N. |	America/Bogota |

## 📈 Scaling Workers (WIP)
To add more workers to your N8N instance and increase its processing capacity, simply edit the docker-compose.yml file to add or modify the number of replicas for the n8n-worker service. Coolify will detect the change and deploy it automatically.