# 📡 Meshtastic APRS Gateway (Docker)

Este proyecto proporciona un **gateway Meshtastic ↔ APRS** con soporte para **Telegram Bot** y **Broker JSONL**, empaquetado en contenedores Docker listos para usar.  

👉 Los usuarios no necesitan el código fuente, solo descargar las imágenes desde **GitHub Container Registry (GHCR)** y levantar los servicios con `docker-compose`.

---

## 🚀 Requisitos

- [Docker](https://docs.docker.com/get-docker/)  
- [Docker Compose](https://docs.docker.com/compose/install/)  

---

## 📦 Instalación

1. Clonar este repositorio:

```bash
git clone https://github.com/jmmpcc/meshtastic-aprs-public.git
cd meshtastic-aprs-public
```

2. Copiar el archivo de variables de entorno y editarlo con tus datos:

```bash
cp .env-example .env
```

3. Levantar los servicios:

```bash
docker compose up -d
```

---

## ⚙️ Variables de entorno

El archivo `.env` controla los parámetros de configuración.  
Ejemplo (`.env-example`):

```dotenv
# === Nodo Meshtastic ===
MESHTASTIC_HOST=192.168.1.201
BROKER_PORT=8765
BACKLOG_PORT=8766

# === Telegram ===
TELEGRAM_TOKEN=xxxxxxxxxxxxx
ADMIN_IDS=123456789

# === APRS ===
APRS_CALL=EB2XXX-11
KISS_HOST=host.docker.internal
KISS_PORT=8100
MESHTASTIC_CH=0
BOT_START_DELAY=90
```

---

## 🛠️ Servicios

El `docker-compose.yml` arranca tres contenedores:

### 🔌 Broker
- Imagen: `ghcr.io/jmmpcc/meshtastic-broker:latest`
- Función: conecta al nodo Meshtastic y expone la API JSONL.  
- Puertos:
  - `8765` → Broker JSONL
  - `8766` → Backlog server (control interno)

### 📡 APRS Gateway
- Imagen: `ghcr.io/jmmpcc/meshtastic-aprs:latest`
- Función: puente bidireccional entre Meshtastic y APRS (vía KISS TCP).  

### 🤖 Telegram Bot
- Imagen: `ghcr.io/jmmpcc/meshtastic-bot:latest`
- Función: control remoto vía comandos de Telegram.  
- Necesita el token del bot (`TELEGRAM_TOKEN`) y los IDs de administradores (`ADMIN_IDS`).  

---

## 📥 Actualización

Para actualizar a la última versión publicada en GHCR:

```bash
docker compose pull
docker compose up -d
```

---

## 📝 Notas

- El código fuente **no está incluido** en este repo.  
- Todas las imágenes se publican automáticamente en **GitHub Container Registry (GHCR)** desde un repositorio privado.  
- Puedes inspeccionar y descargar las imágenes en:  
  👉 https://github.com/jmmpcc?tab=packages&repo_name=meshtastic-aprs-public  

---

## 📄 Licencia

Este proyecto está disponible bajo licencia **MIT**.  
