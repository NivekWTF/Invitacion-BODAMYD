# Invitacion Boda - Deploy con Docker + Nginx

Este proyecto ya incluye configuracion para desplegar en VPS con un solo comando.

## Requisitos en VPS

- Docker
- Docker Compose plugin

Instalacion rapida en Ubuntu/Debian:

```bash
sudo apt update
sudo apt install -y docker.io docker-compose-plugin
sudo systemctl enable --now docker
```

## Deploy con un solo comando

En la carpeta del proyecto:

```bash
npm run docker:up
```

Ese comando:

1. Construye la imagen (Vite build en etapa builder)
2. Levanta Nginx sirviendo `dist`
3. Deja el contenedor en segundo plano

## Comandos utiles

```bash
npm run docker:logs
npm run docker:down
```

## Puerto

Por defecto publica en el puerto 80.

Si quieres otro puerto:

```bash
APP_PORT=8080 npm run docker:up
```

## Estructura agregada

- `Dockerfile` -> build multietapa Node + Nginx
- `docker/nginx.conf` -> configuracion SPA (`try_files ... /index.html`)
- `docker-compose.yml` -> servicio listo para VPS
- `.dockerignore` -> build mas rapido y limpio

