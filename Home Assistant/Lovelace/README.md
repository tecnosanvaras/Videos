# Personalizar nuestro Lovelace, Dashboard o Panel de Home Assistant


Para personalizar nuestro Lovelace, Dashboard o Panel de Home Assistant en determinados aspectos, hay que incluir en el configuration.yaml las siguientes lineas:
```yaml
homeassistant:
  customize: !include customize.yaml
```

Toda la información la podeis encontrar en la web oficial de Home Assistant: https://www.home-assistant.io/docs/configuration/customizing-devices/

**Para personalizar los iconos**, aquí teneis un ejemplo que hay que incluir dentro de nuestro customize.yaml:

```yaml
switch.XXXXXXXXX:
  entity_picture: /local/ico/fan.ico (Ruta donde tengamos nuestro icono).
```

```yaml
light.XXXXXXXXX:
  entity_picture: /local/ico/television.svg
```

Los iconos pueden tener diferentes formatos: .svg, .png, .ico, .jpg, .gif...

**Si lo que queremos es que cambie la imagen dependiendo del estado (encendido - apagado),** existen varias formas de hacerlo. Un ejemplo sencillo sería el siguiente:
```yaml
type: picture-entity
entity: swithc.lavadora
name: Lavadora
image: /local/lavadora.jpg
show_state: false
state_image:
  'off': /local/lavadora.jpg
  'on': /local/lavadora.gif
aspect_ratio: '1' (El aspect_ratio a '1' hace que el tamaño de la imagen sea proporcional al resto)
tap_action:
  action: toggle
```

**Si lo que queremos es que los iconos muestren un tamaño determinado,** primero debemos añadir un addon en HACS llamado "Custom Button Card".
Aquí teneis el repositorio: https://github.com/custom-cards/button-card
Teneis muchos ejemplos dentro del repositorio. Un ejemplo sencillo para cambiar el tamaño de un boton sería el siguiente:
```yaml
type: 'custom:button-card'
entity: light.XXXXXXXXX
name: "El nombre que querais"
show_state: true
styles:
  card:
    - width: 100px
    - height: 100px
```

**Otro ejemplo seria cambiar el brillo y la saturación de la imagen según el estado.** Aquí otro ejemplo:
```yaml
type: picture-entity
state_filter:
  'on': brightness(110%) saturate(1.2)
  'off': brightness(50%) hue-rotate(45deg)
entity: light.xxxxx
image: /local/tocador_on.jpg
show_state: false
tap_action:
  action: more-info
```

Las tarjetas de persianas las podeis encontrar en el repositorio: https://github.com/Deejayfool/hass-shutter-card
El addon se puede integrar desde HACS.
Una vez realizada la integración, el código lo podeis realizar con una tarjeta manual y sería el siguiente:
```yaml
type: 'custom:shutter-card'
title: 'Nombre de la Persiana'
entities:
  - entity: cover.persiana_XXXX
    name: Porcentaje
    buttons_position: left
    title_position: bottom
```
