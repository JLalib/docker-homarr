# 🦞 Homarr
Dashboard Homarr con Docker Compose

Este repositorio proporciona la configuración de Docker Compose para desplegar el dashboard Homarr, una solución moderna y potente para centralizar el acceso y la gestión de tus servicios autoalojados (self-hosted).

## ✨ Características de Homarr
- **Panel de Control Centralizado:** Accede a todas tus aplicaciones desde una única interfaz web.
- **Integración de Widgets:** Muestra información en tiempo real de servicios populares como clientes Torrent, media servers (Sonarr/Radarr), y más.
- **Gestión de Docker:** La configuración incluida permite iniciar, detener y reiniciar tus contenedores Docker directamente desde el dashboard.
- **Personalización:** Interfaz modular y altamente configurable.

## 🚀 Instalación y Despliegue Rápido

### 1. Prerrequisitos
Necesitas tener **Docker** y **Docker Compose** instalados en tu servidor.

### 2. Archivo de Configuración (`docker-compose.yml`)
Tu configuración define un servicio **homarr** que utiliza la imagen oficial más reciente y monta volúmenes para la persistencia de datos y la integración con Docker.

Crea (o verifica) el archivo `docker-compose.yml` con el siguiente contenido:

```yaml
services:
  homarr:
    container_name: homarr
    image: ghcr.io/homarr-labs/homarr:latest
    restart: unless-stopped
    volumes:
      # Permite a Homarr interactuar con el servicio Docker (requerido para widgets de Docker)
      - /var/run/docker.sock:/var/run/docker.sock 
      # Directorio para guardar la configuración y los iconos
      - ./homarr/appdata:/appdata
    environment:
      # Clave de encriptación para datos sensibles.
      - SECRET_ENCRYPTION_KEY=49bf5e6c6ab292ce328e5139ddcdf51270d79e43d620d67990b6f973a112471f
    ports:
      # Puerto de acceso: Host (7575) -> Contenedor (7575)
      - '7575:7575'
```

🔑 **Nota de Seguridad:** La `SECRET_ENCRYPTION_KEY` es fundamental para cifrar los datos del dashboard.  
Mantenla segura y, si es posible, considera cambiarla por una clave generada por ti mismo (por ejemplo, usando `openssl rand -hex 32`).

### 3. Ejecución
Navega al directorio donde guardaste el archivo `docker-compose.yml` y ejecuta:

```bash
docker compose up -d
```

Este comando descargará la imagen y pondrá el contenedor en funcionamiento en segundo plano.

## 💻 Acceso al Dashboard
Una vez iniciado el contenedor, puedes acceder a Homarr en tu navegador:

```
http://<DIRECCION_IP_DE_TU_SERVIDOR>:7575
```

En el primer acceso, serás guiado a través de la configuración inicial para establecer tu usuario y contraseña.

## Nueva versión
<img width="1916" height="947" alt="screenshot" src="https://github.com/user-attachments/assets/da41510e-4377-4a5d-9df9-f071b1d3a4bd" />

## Antigua versión
![Screenshot_1](https://github.com/user-attachments/assets/5a3ec085-2644-475e-9b5a-b031e70d9330)

