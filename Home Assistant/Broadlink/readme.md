# Como enviar los codigos capturados en Home Assistant de tus BROADLINK

Para la creación de tarjetas de nuestros mandos a distancia, lo primero que haremos será aprender los códigos utilizando los diferentes dispositivos Broadlink (RM mini3, RM4 Pro...).

En el link teneis el vídeo explicando como hacerlo: https://www.youtube.com/watch?v=_VKYm8MWXpU&t=456s

## Ejemplos de tarjetas para usar nuestros dispositivos con BROADLINK

### Ejemplo 1
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
