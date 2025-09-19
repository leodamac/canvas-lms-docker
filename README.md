## 📖 Repositorio de Canvas LMS con Docker

Este repositorio contiene las configuraciones de Docker para ejecutar [Canvas LMS](https://github.com/instructure/canvas-lms) en un entorno de contenedores. Es un fork de [canvas-lms-docker](https://github.com/ahamana/canvas-lms-docker).

-----

### 🌟 Características

  * Configuraciones de Docker para entornos basados en **Debian** y **Alpine Linux**.
  * Integración con base de datos **PostgreSQL**.
  * Soporte para caché **Redis**.
  * **Mailpit** para pruebas de correo electrónico.

-----

### ✅ Requisitos

Para comenzar, necesitarás instalar **Docker** y **Docker Compose**, además de **Task**.

<details>
<summary>Cómo instalar Docker, Docker Compose y Task</summary>

-----

#### 🐳 Instalación de Docker

Para instalar Docker en Ubuntu, sigue estos pasos.

1.  **Actualizar el sistema**:

    ```bash
    sudo apt-get update
    ```

2.  **Instalar dependencias necesarias**:

    ```bash
    sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
    ```

3.  **Añadir la clave GPG de Docker**:

    ```bash
    sudo mkdir -p /etc/apt/keyrings
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    ```

4.  **Configurar el repositorio de Docker**:

    ```bash
    echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    ```

5.  **Instalar Docker Engine, Docker Compose y otros componentes**:

    ```bash
    sudo apt-get update
    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
    ```

6.  **Añadir tu usuario al grupo `docker` (opcional, pero recomendado)**:

    ```bash
    sudo usermod -aG docker $USER
    newgrp docker
    ```

    *Esto te permite ejecutar comandos de Docker sin `sudo`.*

-----

#### 🏃‍♂️ Instalación de Task

**Task** es una herramienta de ejecución de tareas que automatiza los comandos complejos. La forma más sencilla de instalarla es con el siguiente comando:

```bash
sh -c "$(curl --location https://taskfile.dev/install.sh)" -- -d -b /usr/local/bin
```

*Este comando descarga e instala Task directamente en el directorio `/usr/local/bin`.*

-----

</details>

-----

### 🚀 Guía de Inicio Rápido

Con Docker y Task instalados, puedes configurar y ejecutar el entorno rápidamente.

1.  Clonar y acceder al repositorio:
   
   ```bash
   git clone https://github.com/leodamac/canvas-lms-docker.git
   cd canvas-lms-docker
   ```

## **Configuración basada en Debian**
### Las imágenes de Debian son más grandes, pero ofrecen un entorno más completo y familiar para los desarrolladores

  Carga y genera los datos necesarios para trabajar con canvas.
  
  ```bash
  task setup DISTRIBUTION=debian
  ```
  
  #### **Ejecutar**
  - Ejecuta el servicio de canvas (para acceder solo ingresa en el navegador a http://localhost:80)
  
  ```bash
  task run DISTRIBUTION=debian
  ```
  
  #### 🛑Apagar el Entorno
  
  - Para detener los servicios
  
  ```bash
  task shutdown DISTRIBUTION=debian
  ```

## **Configuración basada en Alpine**
### Alpine es una distribución de Linux ultra-ligera diseñada específicamente para contenedores y pruebas rápidas.

  Carga y genera los datos necesarios para trabajar con canvas.
  
  ```bash
  task setup DISTRIBUTION=alpine
  ```
  
  #### **Ejecutar**
  - Ejecuta el servicio de canvas (para acceder solo ingresa en el navegador a http://localhost:80)
  
  ```bash
  task run DISTRIBUTION=alpine
  
  ```
  #### 🛑 Apagar el Entorno
  
  - Para detener los servicios
  
  ```bash
  task shutdown DISTRIBUTION=alpine
  ```
-----

### ⚙️ Configuración

El entorno se configura a través del archivo **`.env`**, el cual contiene todas las variables de entorno necesarias.

#### **Valores por defecto**

  * `EMAIL_DOMAIN`: `example.com` - Dominio de los correos electrónicos.
  * `EMAIL_HOST_USER`: `user` - Nombre de usuario para autenticación SMTP.
  * `EMAIL_HOST_PASSWORD`: `password` - Contraseña para autenticación SMTP.
  * `EMAIL_SENDER_ADDRESS`: `canvas@${EMAIL_DOMAIN}` - Dirección de correo del remitente.
  * `EMAIL_SENDER_NAME`: `Instructure Canvas` - Nombre de visualización del remitente.
  * `CANVAS_LMS_DOMAIN`: `localhost` - Dominio para la aplicación.
  * `CANVAS_LMS_ADMIN_EMAIL`: `admin@${EMAIL_DOMAIN}` - Correo del administrador.
  * `CANVAS_LMS_ADMIN_PASSWORD`: `password` - Contraseña del administrador.
  * `CANVAS_LMS_ACCOUNT_NAME`: `Canvas Admin` - Nombre de la cuenta principal de Canvas.
  * `CANVAS_LMS_STATS_COLLECTION`: `opt_out` - Controla la recolección de estadísticas (`opt_in`, `opt_out` o `anonymized`).
  * `POSTGRES_USER`: `canvas` - Nombre de usuario para la base de datos PostgreSQL.
  * `POSTGRES_PASSWORD`: `canvas` - Contraseña para la base de datos PostgreSQL (se recomienda cambiarla).
  * `POSTGRES_DB`: `canvas` - Nombre de la base de datos PostgreSQL.
  * `TZ`: `America/Guayaquil` - Zona horaria.

**El entorno provee:**

  * **Base de Datos**: PostgreSQL
  * **Caché**: Redis
  * **Pruebas de Correo**: Mailpit (accesible en `http://localhost:8025`)
  * **Interfaz de Canvas LMS**: `http://localhost:80`

-----


### 📜 Licencia

Consulta el archivo [LICENSE](https://www.google.com/search?q=LICENSE) para más detalles.
