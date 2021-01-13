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

Dentro de HACS podeis encontrar muchos addons que pueden ser de gran utilidad para modificar nuestro Lovelace.
Los que yo he utilizado o utilizo para personalizar mi Home Assistant son los siguientes:
 - Card Mod: https://github.com/thomasloven/lovelace-card-mod
 - Text Divider Row: https://github.com/iantrich/text-divider-row
 - Check Button Card: https://github.com/custom-cards/check-button-card
 - Button Card: https://github.com/custom-cards/button-card
 - Slider Entity Row: https://github.com/thomasloven/lovelace-slider-entity-row
 - Light Entity Card: https://github.com/ljmerza/light-entity-card
 - Auto Entities: https://github.com/thomasloven/lovelace-auto-entities
 
 Por supuesto existen muchas más y por supuesto las habrá mejores y peores.
 Pero es de agradecer a sus creadores que pongan a nuestra disposición sus conocimientos.
 
 El ejemplo del final del vídeo es una configuración muy simple realizada con combinaciones de las diferentes pilas.
 Os dejo el ejemplo para que os hagais una idea de lo que sería el editor de código:
 ```yaml
 type: vertical-stack
cards:
  - type: horizontal-stack
    cards:
      - type: button
        tap_action:
          action: toggle
        entity: light.xxxxx
      - type: button
        tap_action:
          action: toggle
        entity: switch.xxxxx
      - type: button
        tap_action:
          action: toggle
        entity: switch.xxxxx
      - type: button
        tap_action:
          action: toggle
        entity: switch.xxxxx
      - type: button
        tap_action:
          action: toggle
        entity: light.xxxxx
      - type: button
        tap_action:
          action: toggle
        entity: switch.xxxxx
      - type: button
        tap_action:
          action: toggle
        entity: switch.xxxxx
  - type: horizontal-stack
    cards:
      - type: grid
        cards:
          - type: button
            tap_action:
              action: toggle
            entity: switch.xxxxx
          - type: button
            tap_action:
              action: toggle
            entity: switch.xxxxx
      - type: grid
        cards:
          - type: button
            tap_action:
              action: toggle
            entity: switch.xxxxx
          - type: button
            tap_action:
              action: toggle
            entity: switch.xxxxx
      - type: grid
        cards:
          - type: button
            tap_action:
              action: toggle
            entity: light.xxxxx
          - type: button
            tap_action:
              action: toggle
            entity: switch.xxxxx
          - type: button
            tap_action:
              action: toggle
            entity: light.xxxxx
  - type: horizontal-stack
    cards:
      - type: grid
        columns: 6
        square: false
        cards:
          - type: button
            tap_action:
              action: toggle
            entity: light.xxxxx
          - type: button
            tap_action:
              action: toggle
            entity: light.xxxxx
          - type: button
            tap_action:
              action: toggle
            entity: light.xxxxx
          - type: button
            tap_action:
              action: toggle
            entity: light.xxxxx
          - type: button
            tap_action:
              action: toggle
            entity: switch.xxxxx
          - type: button
            tap_action:
              action: toggle
            entity: switch.xxxxx
  - type: horizontal-stack
    cards:
      - type: grid
        columns: 4
        cards:
          - type: 'custom:shutter-card'
            title: "El nombre que querais"
            entities:
              - entity: cover.xxxxx
                name: Porcentaje
                buttons_position: left
                title_position: bottom
          - type: thermostat
            entity: climate.xxxxx
          - type: thermostat
            entity: climate.xxxxx
          - type: 'custom:shutter-card'
            title: "El nombre que querais"
            entities:
              - entity: cover.xxxxx
                name: Porcentaje
                buttons_position: left
                title_position: bottom
  - type: horizontal-stack
    cards:
      - type: grid
        columns: 5
        square: false
        cards:
          - type: 'custom:mini-media-player'
            artwork: full-cover
            icon: 'mdi:amazon'
            tts:
              platform: alexa
              enity_id: media_player.xxxxx
            entity: media_player.xxxxx
          - type: 'custom:mini-media-player'
            artwork: full-cover
            icon: 'mdi:amazon'
            tts:
              platform: alexa
              enity_id: media_player.xxxxx
            entity: media_player.xxxxx
          - type: 'custom:mini-media-player'
            artwork: full-cover
            icon: 'mdi:google-home'
            tts:
              platform: google
              enity_id: media_player.xxxxx
            entity: media_player.xxxxx
            volume_stateless: true
          - type: media-control
            entity: media_player.xxxxx
          - type: media-control
            entity: media_player.xxxxx
  - type: horizontal-stack
    cards:
      - type: picture-entity
        entity: camera.xxxxx
        show_state: false
      - type: picture-entity
        entity: camera.xxxxx
        show_name: false
        show_state: false

 
 ```
 
 Espero que os haya resultado de utilidad
