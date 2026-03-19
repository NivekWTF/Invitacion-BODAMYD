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

Por defecto publica en `127.0.0.1:8080` para usarse detras de Nginx (reverse proxy).

Si quieres otro puerto:

```bash
APP_PORT=8080 npm run docker:up
```

Si quieres exponerlo directo a internet (sin reverse proxy):

```bash
APP_BIND=0.0.0.0 APP_PORT=80 npm run docker:up
```

Nota: para esto, el puerto 80 debe estar libre en el VPS.

## Usar un dominio existente (ejemplo: bodamyd.kevinsg.site)

1. Levanta el contenedor:

```bash
npm run docker:up
```

2. En Nginx del VPS, en el `server` HTTPS del dominio, usa este bloque:

```nginx
location / {
	proxy_pass http://127.0.0.1:8080;
	proxy_http_version 1.1;
	proxy_set_header Host $host;
	proxy_set_header X-Real-IP $remote_addr;
	proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
	proxy_set_header X-Forwarded-Proto $scheme;
}
```

3. Recarga Nginx:

```bash
sudo nginx -t
sudo systemctl reload nginx
```

## Modo directo en VPS (sin reverse proxy)

1. Deten cualquier servicio que use 80/443 en el host:

```bash
sudo systemctl stop nginx apache2 2>/dev/null || true
sudo systemctl disable nginx apache2 2>/dev/null || true
```

2. Levanta la app directo en puerto 80:

```bash
APP_BIND=0.0.0.0 APP_PORT=80 npm run docker:up
```

3. Verifica puertos del contenedor:

```bash
docker ps
```

Debes ver algo como `0.0.0.0:80->80/tcp`.

4. DNS del dominio:

- Registro A de `bodamyd.kevinsg.site` apuntando a la IP publica del VPS.

Con esto el sitio queda servido directamente por el contenedor.

## Modo HTTPS directo (Docker + Caddy + Let's Encrypt)

Este modo no usa Nginx del host. Caddy corre en Docker y gestiona SSL automatico.

### Requisitos

- El dominio apunta a la IP publica del VPS (registro A)
- Puertos 80 y 443 abiertos en firewall/IONOS
- No tener Nginx/Apache ocupando esos puertos en el host

### Pasos

1. Deten servicios del host que usen 80/443:

```bash
sudo systemctl stop nginx apache2 2>/dev/null || true
sudo systemctl disable nginx apache2 2>/dev/null || true
```

2. Crea tu archivo de entorno HTTPS:

```bash
cp .env.https.example .env.https
nano .env.https
```

`.env.https` se queda solo en el VPS (no se sube al repo).

Contenido esperado:

```env
DOMAIN=bodamyd.kevinsg.site
LETSENCRYPT_EMAIL=tu-email@dominio.com
```

3. Levanta el stack HTTPS:

```bash
npm run docker:https:up
```

4. Verifica logs de certificados/arranque:

```bash
npm run docker:https:logs
```

5. Abrir en navegador:

- https://bodamyd.kevinsg.site

### Actualizar deploy

```bash
git pull
npm run docker:https:up
```

### Apagar stack HTTPS

```bash
npm run docker:https:down
```

## Estructura agregada

- `Dockerfile` -> build multietapa Node + Nginx
- `docker/nginx.conf` -> configuracion SPA (`try_files ... /index.html`)
- `docker-compose.yml` -> servicio listo para VPS
- `docker-compose.https.yml` -> stack HTTPS directo con Caddy
- `.dockerignore` -> build mas rapido y limpio
- `docker/Caddyfile` -> reverse proxy y SSL automatico

