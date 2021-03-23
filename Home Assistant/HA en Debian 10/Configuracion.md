# Guia de instalación de Home Assistant en Debian 10

Toda la información que aquí muestro sigue los pasos de la guía de la Comunidad de Home Assistant (https://community.home-assistant.io/t/installing-home-assistant-supervised-on-a-raspberry-pi-with-debian-10/247116).

## Configuración inicial una vez instalado Debian 10

1. Logarnos como root
2. Actualizar el sistema
```
apt update && apt upgrade -y
apt install sudo -y
```
3. Elegir un nombre de usuario
```
adduser TU_NOMBRE_DE_USUARIO
```
4. Añadir usuario al grupo
```
usermod -aG sudo TU_NOMBRE_DE_USUARIO
```

Una vez realizado esto, ya podemos entrar por SSH para la instalación de Home Assistant. Comprobar vuestra IP con algún programa como FING o Advanced IP Scanner.

## Instalación de Home Assistant Supervised
```
sudo -i

apt-get install -y software-properties-common apparmor-utils apt-transport-https ca-certificates curl dbus jq network-manager

systemctl disable ModemManager

systemctl stop ModemManager

curl -fsSL get.docker.com | sh

curl -sL "https://raw.githubusercontent.com/Kanga-Who/home-assistant/master/supervised-installer.sh" | bash -s -- -m raspberrypi4-64
```
