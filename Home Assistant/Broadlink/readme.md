# Como enviar los codigos capturados en Home Assistant de tus BROADLINK

Para la creación de tarjetas de nuestros mandos a distancia, lo primero que haremos será aprender los códigos utilizando los diferentes dispositivos Broadlink (RM mini3, RM4 Pro...).

En el link teneis el vídeo explicando como hacerlo: https://www.youtube.com/watch?v=_VKYm8MWXpU&t=456s

## Ejemplos de tarjetas para usar nuestros dispositivos con BROADLINK

### Ejemplo 1
Ejemplo de una tarjeta combinada de pila vertical y horizontal con cards tipo 'button'
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
