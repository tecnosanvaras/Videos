# Como enviar los codigos capturados en Home Assistant de tus BROADLINK

Para la creación de tarjetas de nuestros mandos a distancia, lo primero que haremos será aprender los códigos utilizando los diferentes dispositivos Broadlink (RM mini3, RM4 Pro...).

En el link teneis el vídeo explicando como hacerlo: https://www.youtube.com/watch?v=_VKYm8MWXpU&t=456s

## Ejemplos de tarjetas para usar nuestros dispositivos con BROADLINK

### Ejemplo 1
Ejemplo de una tarjeta combinada de pila vertical y horizontal con cards tipo 'button'.

![Tecnosanvaras en YouTube](https://github.com/tecnosanvaras/Videos/blob/main/cabecera/CABECERA.jpg)

```
type: vertical-stack
cards:
  - type: horizontal-stack
    cards:
      - type: button
        tap_action:
          action: toggle
        entity: script.power_tv
        show_name: false
  - type: horizontal-stack
    cards:
      - type: horizontal-stack
        cards:
          - type: button
            tap_action:
              action: toggle
            entity: script.canal_uno_tv
            show_name: false
          - type: button
            tap_action:
              action: toggle
            entity: script.canal_dos_tv
            show_name: false
          - type: button
            tap_action:
              action: toggle
            entity: script.canal_tres_tv
            show_name: false
          - type: button
            tap_action:
              action: toggle
            entity: script.canal_cuatro_tv
            show_name: false
          - type: button
            tap_action:
              action: toggle
            entity: script.canal_cinco_tv
            show_name: false
  - type: horizontal-stack
    cards:
      - type: button
        tap_action:
          action: toggle
        entity: script.canal_seis_tv
        show_name: false
      - type: button
        tap_action:
          action: toggle
        entity: script.canal_siete_tv
        show_name: false
      - type: button
        tap_action:
          action: toggle
        entity: script.canal_ocho_tv
        show_name: false
      - type: button
        tap_action:
          action: toggle
        entity: script.canal_nueve_tv
        show_name: false
      - type: button
        tap_action:
          action: toggle
        entity: script.canal_cero_tv
        show_name: false
```

### Ejemplo 2:
Ejemplo de tarjeta con un complemento de HACS llamado 'Custom button card'
```
type: vertical-stack
cards:
  - type: horizontal-stack
    cards:
      - type: 'custom:button-card'
        entity: script.power_tv
        color_type: card
        tap_action:
          action: toggle
        state:
          - value: 'on'
            color: red
            styles:
              card:
                - animation: blink 2s ease infinite
          - operator: default
            color: green
        styles:
          card:
            - height: 100px
  - type: horizontal-stack
    cards:
      - type: 'custom:button-card'
        entity: script.canal_uno_tv
        color_type: card
        tap_action:
          action: toggle
        state:
          - value: 'on'
            color: red
            styles:
              card:
                - animation: blink 2s ease infinite
          - operator: default
            color: blue
        styles:
          card:
            - height: 100px
      - type: 'custom:button-card'
        entity: script.canal_dos_tv
        color_type: card
        tap_action:
          action: toggle
        state:
          - value: 'on'
            color: red
            styles:
              card:
                - animation: blink 2s ease infinite
          - operator: default
            color: blue
        styles:
          card:
            - height: 100px
      - type: 'custom:button-card'
        entity: script.canal_tres_tv
        color_type: card
        tap_action:
          action: toggle
        state:
          - value: 'on'
            color: red
            styles:
              card:
                - animation: blink 2s ease infinite
          - operator: default
            color: blue
        styles:
          card:
            - height: 100px
  - type: horizontal-stack
    cards:
      - type: 'custom:button-card'
        entity: script.canal_cuatro_tv
        color_type: card
        tap_action:
          action: toggle
        state:
          - value: 'on'
            color: red
            styles:
              card:
                - animation: blink 2s ease infinite
          - operator: default
            color: blue
        styles:
          card:
            - height: 100px
      - type: 'custom:button-card'
        entity: script.canal_cinco_tv
        color_type: card
        tap_action:
          action: toggle
        state:
          - value: 'on'
            color: red
            styles:
              card:
                - animation: blink 2s ease infinite
          - operator: default
            color: blue
        styles:
          card:
            - height: 100px
      - type: 'custom:button-card'
        entity: script.canal_seis_tv
        color_type: card
        tap_action:
          action: toggle
        state:
          - value: 'on'
            color: red
            styles:
              card:
                - animation: blink 2s ease infinite
          - operator: default
            color: blue
        styles:
          card:
            - height: 100px
  - type: horizontal-stack
    cards:
      - type: 'custom:button-card'
        entity: script.canal_siete_tv
        color_type: card
        tap_action:
          action: toggle
        state:
          - value: 'on'
            color: red
            styles:
              card:
                - animation: blink 2s ease infinite
          - operator: default
            color: blue
        styles:
          card:
            - height: 100px
      - type: 'custom:button-card'
        entity: script.canal_ocho_tv
        color_type: card
        tap_action:
          action: toggle
        state:
          - value: 'on'
            color: red
            styles:
              card:
                - animation: blink 2s ease infinite
          - operator: default
            color: blue
        styles:
          card:
            - height: 100px
      - type: 'custom:button-card'
        entity: script.canal_nueve_tv
        color_type: card
        tap_action:
          action: toggle
        state:
          - value: 'on'
            color: red
            styles:
              card:
                - animation: blink 2s ease infinite
          - operator: default
            color: blue
        styles:
          card:
            - height: 100px
```

### Ejemplo 3
Ejemplo con una tarjeta de entidades
```
type: entities
entities:
  - entity: script.canal_uno_tv
  - entity: script.canal_dos_tv
  - entity: script.canal_tres_tv
  - entity: script.canal_cuatro_tv
  - entity: script.canal_cinco_tv
  - entity: script.canal_seis_tv
  - entity: script.canal_siete_tv
  - entity: script.canal_ocho_tv
  - entity: script.canal_nueve_tv
  - entity: script.power_tv
title: Television
```

### Ejemplo 4
Ejemplo con una tarjeta picture-elements
```
type: picture-elements
image: /local/mando.png
aspect_ratio: '3:2'
elements:
  - entity: script.luz_ventilador
    icon: 'mdi:lightbulb'
    type: state-icon
    tap_action:
      action: toggle
    style:
      top: 38%
      left: 35%
  - entity: script.fan_off_ventilador
    icon: 'mdi:fan-off'
    type: state-icon
    tap_action:
      action: toggle
    style:
      top: 38%
      left: 68%
  - entity: script.hi_ventilador
    icon: 'mdi:fan-speed-3'
    type: state-icon
    tap_action:
      action: toggle
    style:
      top: 53%
      left: 26%
  - entity: script.med_ventilador
    icon: 'mdi:fan-speed-2'
    type: state-icon
    tap_action:
      action: toggle
    style:
      top: 53%
      left: 51%
  - entity: script.low_ventilador
    icon: 'mdi:fan-speed-1'
    type: state-icon
    tap_action:
      action: toggle
    style:
      top: 53%
      left: 76%
  - entity: script.h2
    icon: 'mdi:numeric-2-circle'
    type: state-icon
    tap_action:
      action: toggle
    style:
      top: 68%
      left: 26%
  - entity: script.h4
    icon: 'mdi:numeric-4-circle'
    type: state-icon
    tap_action:
      action: toggle
    style:
      top: 68%
      left: 51%
  - entity: script.h8
    icon: 'mdi:numeric-8-circle'
    type: state-icon
    tap_action:
      action: toggle
    style:
      top: 68%
      left: 76%
```

### Ejemplo 5
Tarjeta que combina un poco de todo
```
cards:
  - entity: media_player.lg_webos_smart_tv
    type: media-control
  - cards:
      - action: service
        color: 'rgb(255, 0, 0)'
        color_type: card
        icon: 'mdi:volume-plus'
        tap_action:
          action: call-service
          service: webostv.button
          service_data:
            button: VOLUMEUP
            entity_id: media_player.lg_webos_smart_tv
        type: 'custom:button-card'
      - action: service
        color: 'rgb(255, 0, 0)'
        color_type: card
        icon: 'mdi:volume-minus'
        tap_action:
          action: call-service
          service: webostv.button
          service_data:
            button: VOLUMEDOWN
            entity_id: media_player.lg_webos_smart_tv
        type: 'custom:button-card'
      - action: service
        color: 'rgb(255, 0, 0)'
        color_type: card
        icon: 'mdi:home'
        tap_action:
          action: call-service
          service: webostv.button
          service_data:
            button: HOME
            entity_id: media_player.lg_webos_smart_tv
        type: 'custom:button-card'
      - action: service
        color: 'rgb(255, 0, 0)'
        color_type: card
        icon: 'mdi:arrow-up-thick'
        tap_action:
          action: call-service
          service: webostv.button
          service_data:
            button: UP
            entity_id: media_player.lg_webos_smart_tv
        type: 'custom:button-card'
      - action: service
        color: 'rgb(255, 0, 0)'
        color_type: card
        icon: 'mdi:arrow-down-thick'
        tap_action:
          action: call-service
          service: webostv.button
          service_data:
            button: DOWN
            entity_id: media_player.lg_webos_smart_tv
        type: 'custom:button-card'
    type: horizontal-stack
  - cards:
      - action: service
        color: 'rgb(255, 0, 0)'
        color_type: card
        icon: 'mdi:exit-to-app'
        tap_action:
          action: call-service
          service: webostv.button
          service_data:
            button: EXIT
            entity_id: media_player.lg_webos_smart_tv
        type: 'custom:button-card'
      - action: service
        color: 'rgb(255, 0, 0)'
        color_type: card
        icon: 'mdi:backup-restore'
        tap_action:
          action: call-service
          service: webostv.button
          service_data:
            button: BACK
            entity_id: media_player.lg_webos_smart_tv
        type: 'custom:button-card'
      - action: service
        color: 'rgb(255, 0, 0)'
        color_type: card
        icon: 'mdi:check'
        tap_action:
          action: call-service
          service: webostv.button
          service_data:
            button: ENTER
            entity_id: media_player.lg_webos_smart_tv
        type: 'custom:button-card'
      - action: service
        color: 'rgb(255, 0, 0)'
        color_type: card
        icon: 'mdi:arrow-left-thick'
        tap_action:
          action: call-service
          service: webostv.button
          service_data:
            button: LEFT
            entity_id: media_player.lg_webos_smart_tv
        type: 'custom:button-card'
      - action: service
        color: 'rgb(255, 0, 0)'
        color_type: card
        icon: 'mdi:arrow-right-thick'
        tap_action:
          action: call-service
          service: webostv.button
          service_data:
            button: RIGHT
            entity_id: media_player.lg_webos_smart_tv
        type: 'custom:button-card'
    type: horizontal-stack
  - cards:
      - color_type: card
        entity: script.canal_tv_live
        show_entity_picture: true
        show_label: false
        show_name: false
        show_state: false
        styles:
          entity_picture:
            - align-self: middle
            - height: 50px
            - width: 50px
        type: 'custom:button-card'
      - color_type: card
        entity: script.canal_netflix
        show_entity_picture: true
        show_label: false
        show_name: false
        show_state: false
        styles:
          entity_picture:
            - align-self: middle
            - height: 50px
            - width: 50px
        type: 'custom:button-card'
      - color_type: card
        entity: script.canal_amazon_tv
        show_entity_picture: true
        show_label: false
        show_name: false
        show_state: false
        styles:
          entity_picture:
            - align-self: middle
            - height: 50px
            - width: 50px
        type: 'custom:button-card'
      - color_type: card
        entity: script.canal_hbo
        show_entity_picture: true
        show_label: false
        show_name: false
        show_state: false
        styles:
          entity_picture:
            - align-self: middle
            - height: 50px
            - width: 50px
        type: 'custom:button-card'
    type: horizontal-stack
  - cards:
      - color_type: card
        entity: script.canal_tve1
        show_entity_picture: true
        show_label: false
        show_name: false
        show_state: false
        styles:
          entity_picture:
            - align-self: middle
            - height: 50px
            - width: 50px
        tap_action:
          action: call-service
          service: script.canal_tve1
          service_data:
            entity_id: script.canal_tve1
        type: 'custom:button-card'
      - color_type: card
        entity: script.canal_tve2
        show_entity_picture: true
        show_label: false
        show_name: false
        show_state: false
        styles:
          entity_picture:
            - align-self: middle
            - height: 50px
            - width: 50px
        tap_action:
          action: call-service
          service: script.canal_tve2
          service_data:
            entity_id: script.canal_tve2
        type: 'custom:button-card'
      - color_type: card
        entity: script.canal_antena_tres
        show_entity_picture: true
        show_label: false
        show_name: false
        show_state: false
        styles:
          entity_picture:
            - align-self: middle
            - height: 50px
            - width: 50px
        tap_action:
          action: call-service
          service: script.canal_antena_tres
          service_data:
            entity_id: script.canal_antena_tres
        type: 'custom:button-card'
      - color_type: card
        entity: script.canal_cuatro
        show_entity_picture: true
        show_label: false
        show_name: false
        show_state: false
        styles:
          entity_picture:
            - align-self: middle
            - height: 50px
            - width: 50px
        tap_action:
          action: call-service
          service: script.canal_cuatro
          service_data:
            entity_id: script.canal_cuatro
        type: 'custom:button-card'
      - color_type: card
        entity: script.canal_tele_5
        show_entity_picture: true
        show_label: false
        show_name: false
        show_state: false
        styles:
          entity_picture:
            - align-self: middle
            - height: 50px
            - width: 50px
        tap_action:
          action: call-service
          service: script.canal_tele_5
          service_data:
            entity_id: script.canal_tele_5
        type: 'custom:button-card'
    type: horizontal-stack
  - cards:
      - color_type: card
        entity: script.canal_la_sexta
        show_entity_picture: true
        show_label: false
        show_name: false
        show_state: false
        styles:
          entity_picture:
            - align-self: middle
            - height: 50px
            - width: 50px
        tap_action:
          action: call-service
          service: script.canal_la_sexta
          service_data:
            entity_id: script.canal_la_sexta
        type: 'custom:button-card'
      - color_type: card
        entity: script.canal_divinity
        show_entity_picture: true
        show_label: false
        show_name: false
        show_state: false
        styles:
          entity_picture:
            - align-self: middle
            - height: 50px
            - width: 50px
        tap_action:
          action: call-service
          service: script.canal_divinity
          service_data:
            entity_id: script.canal_divinity
        type: 'custom:button-card'
      - color_type: card
        entity: script.canal_24_horas
        show_entity_picture: true
        show_label: false
        show_name: false
        show_state: false
        styles:
          entity_picture:
            - align-self: middle
            - height: 50px
            - width: 50px
        tap_action:
          action: call-service
          service: script.canal_24_horas
          service_data:
            entity_id: script.canal_24_horas
        type: 'custom:button-card'
      - color_type: card
        entity: script.canal_telemadrid
        show_entity_picture: true
        show_label: false
        show_name: false
        show_state: false
        styles:
          entity_picture:
            - align-self: middle
            - height: 50px
            - width: 50px
        tap_action:
          action: call-service
          service: script.canal_telemadrid
          service_data:
            entity_id: script.canal_telemadrid
        type: 'custom:button-card'
    type: horizontal-stack
type: vertical-stack
```
