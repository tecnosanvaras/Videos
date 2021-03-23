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

Actualizar el sistema
```
sudo apt update && sudo apt upgrade -y && sudo apt autoremove –y
```

## Permitir acceso root en Debian
Con el siguiente comando editamos el fichero:
```
sudo nano /etc/ssh/sshd_config
```
Aqui buscamos PermitRootLogin. Quitamos la # de delante y borramos "prohibit-password" y lo sustituimos por "yes".

Guardamos con Ctrl+x y reiniciamos con "reboot".

## Montar Disco Duro en nuestra Raspberry Pi
1. Para ver las unidades conectadas a la raspberry:
```
sudo blkid
```
2. Para que el formato NTFS sea compatible ejecutamos:
```
sudo apt-get install ntfs-3g -y
```
3. Comprobamos las particiones:
```
sudo fdisk -l
```
4. Creamos carpeta:
```
sudo mkdir /media/HDD
```
5. Le damos permisos:
 ```
sudo chmod 777 /media/HDD
```
6. Configuramos el automontaje editando el fichero:
```
sudo nano /etc/fstab	
UUID=e25b1db5-5127-4779-8312-bd611edfc64d /media/HDD ext4 defaults 0 0
```

## Instalación de Docker Compose en Debian 10
```
sudo apt install -y libffi-dev libssl-dev
sudo apt install -y python3-pip
sudo pip3 install docker-compose
sudo apt update && sudo apt upgrade
```

## Instalación de Portainer
```
docker volume create portainer_data
docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce
```
