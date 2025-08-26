# n8n Cloud

This repository contains the Docker Compose setup and scripts to deploy **n8n** on a personal VM using **NGINX reverse proxy** with **HTTPS via Let's Encrypt**. It is designed for homelab or small production scenarios. Sensitive credentials are stored in a `.env` file and **must not** be committed to this repository.

---

## Features

- n8n workflow automation
- SQLite persistent storage
- NGINX reverse proxy
- Automatic HTTPS certificates (Let's Encrypt)
- Environment variables for sensitive configuration
- Ready for CI/CD via GitHub Actions

---

## Directory Structure

n8n-cloud/  
├── docker-compose.yml # main stack definition  
├── .env.example # example env variables (DO NOT EDIT in repo)  
├── n8n_data/ # persistent n8n data (ignored in git)    
├── nginx_data/ # nginx proxy data (ignored in git)     
└── .github/workflows/ # GitHub Actions workflow

---

## Environment Variables

Copy `.env.example` to `.env` and fill in your values:

```dotenv
# Domain used to access n8n
DOMAIN=n8n.yourdomain.com

# Let's Encrypt email
LETSENCRYPT_EMAIL=youremail@domain.com

# n8n Basic Auth
N8N_BASIC_AUTH_USER=admin
N8N_BASIC_AUTH_PASSWORD=super-secure-password
```

Make sure .env is added to .gitignore and never pushed.

## Deploy Instructions

1. Create folders on the VM

```bash
mkdir -p ~/n8n-stack/n8n_data ~/n8n-stack/nginx_data
cd ~/n8n-stack
```

2. Copy .env with your credentials

3. Start the stack

```bash
docker compose --env-file .env up -d
```
4. Access n8n

    ```https://${DOMAIN}``` with the credentials you defined in .env.

## CI/CD

You can set up GitHub Actions to automatically deploy updates to your VM when pushing to main. Make sure to configure SSH keys and secrets as described in ```.github/workflows/deploy.yml```.

## Security Tips

Never commit .env or sensitive data.

Use strong passwords for Basic Auth.

Restrict access if exposing your VM to the internet.
