Práctica 1: Instalación y Configuración de Docker 🐳
Autor: Edwind Isaías
Matrícula: 20240318
Entorno: Ubuntu/Debian Server (Local o Cloud)

📌 Objetivo
Instalar Docker, descargar la imagen oficial de NGINX, y desplegar un contenedor web con un volumen persistente mapeado al puerto 8888 del host.

🚀 Pasos de Implementación
1. Instalación del Motor de Docker
Actualizamos los repositorios del sistema e instalamos los paquetes necesarios para ejecutar Docker.

Bash
# Actualizar repositorios
sudo apt update

# Instalar Docker
sudo apt install docker.io -y

# Habilitar el servicio para que inicie con el sistema
sudo systemctl enable --now docker
2. Descargar la Imagen de NGINX
Obtenemos la imagen oficial del servidor web NGINX directamente desde Docker Hub.

Bash
sudo docker pull nginx
3. Configuración del Volumen Persistente y Contenedor
Creamos el directorio en el host (servidor físico) que servirá como volumen persistente, y luego levantamos el contenedor mapeando los puertos y el volumen.

Bash
# Crear directorio persistente en el host
sudo mkdir -p /home/website

# Crear y ejecutar el contenedor
sudo docker run -d \
  --name mi_servidor_web \
  -p 8888:80 \
  -v /home/website:/usr/share/nginx/html \
  nginx
4. Inyección del Código HTML
Creamos el archivo index.html directamente en el volumen persistente del host (/home/website). Debido al mapeo (-v), el contenedor NGINX servirá este archivo automáticamente.

Bash
# Crear el archivo index.html
echo '<!DOCTYPE html>
<html>
<head>
    <title>Práctica 1 - Docker</title>
    <meta charset="utf-8">
</head>
<body style="text-align: center; font-family: Arial; margin-top: 50px;">
    <h1>Práctica 1: Instalación y configuración de Docker</h1>
    <h2>Nombre: Edwind Isaías</h2>
    <h2>Matrícula: 20240318</h2>
    <p>¡Contenedor NGINX con volumen persistente funcionando perfectamente!</p>
</body>
</html>' | sudo tee /home/website/index.html
5. Verificación y Pruebas
Para confirmar que el contenedor está sirviendo la página correctamente:

Abrir un navegador web.

Ingresar la dirección IP del servidor seguida del puerto configurado:

Local: http://127.0.0.1:8888

Servidor Remoto: http://<IP_PUBLICA_DEL_SERVIDOR>:8888

Nota de Solución de Problemas: Si el puerto 8888 ya está en uso, se puede modificar el comando de ejecución cambiando el parámetro de mapeo a -p 8889:80 (o cualquier otro puerto disponible).
