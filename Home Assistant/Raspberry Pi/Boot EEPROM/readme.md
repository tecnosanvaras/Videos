[Tecnosanvaras en YouTube][1]
===
![Tecnosanvaras en YouTube](https://github.com/tecnosanvaras/Videos/blob/main/cabecera/CABECERA.jpg)

Este documento es unicamente para la Raspberry Pi 4. En el caso de Raspberry pi 3 la forma de hacerlo es totalmente diferente y para ello podeis consultar el tutorial en mi canal en el siguiente vídeo: https://www.youtube.com/watch?v=O5JWYo1ss00

Los pasos a seguir son los siguientes:
-	Tener instalado en nuestra Raspberry Pi 4 el sistema operativo Raspberry Pi OS
- Actualizar el sistema operativo: **sudo apt update && sudo apt full-upgrade**
- Comprobar si hay disponible una actualización de la eeprom. Ejecutamos el siguiente comando y si nos aparece **"critical"** lo cambiamos por **"stable"**
- Listamos los bootloader disponibles de la siguiente forma: **ls /lib/firmware/raspberrypi/bootloader/stable/**
- Una vez comprobado la última versión disponible (segun la fecha en formato yyyy-mm-dd), actualizamos de la siguiente forma: **sudo rpi-eeprom-update -d -f /lib/firmware/raspberrypi/bootloader/stable/pieeprom-2020-09-03.bin** (cambiamos el pieeprom por el último disponible)
- Reiniciamos el sistema: sudo reboot
- Si todo se realizado de forma satisfactoria, con el siguiente comando: **vcgencmd bootloader_config** podremos comprobar que en el boot_order aparece 0xf41. Esto quiere decir que primero intentará arrancar desde la SD y si no es posible intentará como segunda opción, el USB
- El último paso seria copiar nuestra SD al dispositivo externo desde el cual queramos iniciar nuestra Raspberry: USB o SSD

### Y ya tendríamos lista nuestra Raspberry Pi 4 para arrancarla desde un dispositivo externo sin necesitar la SD

  [1]: https://www.youtube.com/channel/UCMddiVH-CzGZ97sVgZrKg6A
