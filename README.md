# bar-card

![](images/examples.gif)

## Description

Bar Card is a customizable animated card for the Home Assistant Lovelace front-end.

### Features
- Customizable bar, text and animation.
- Automatic animation mode. Starts animating based on value increase or decrease.
- Charge based animation mode. Will show increase based on custom entity state.

## Options

| Name | Type | Default | Description
| ---- | ---- | ------- | -----------
| type | string | **Required** | `custom:bar-card`
| entity | string | **Required** | Entity State
| entities | array | none | A list of entities. Cards will share config.
| columns | number | none | Defines the number of columns when using entities list.
| attribute | string | none | Defines the attribute to be displayed.
| unit_of_measurement | string | none | Defines the unit of measurement to be displayed.
| title | string | none | Title displayed next to the bar.
| title_position | string | left | Position of the title. `left`,`right`,`top`,`bottom`,`inside`
| animation | string | auto | Sets the mode of animation `auto`, `charge`, `off`.
| indicator | string | auto | Sets position off the indicator `auto`,`auto-vertical`,`left`,`right`,`top`,`bottom`,`off`
| hue | number | 220 | Changed the color hue of the bar `0`-`360`.
| saturation | string | 50% | Scales saturation of the bar.
| height | string | 40px | Scales the height of the bar.
| width | string | 70% | Scales the width of the bar.
| padding | string | 4px | Sets padding amount around the card.
| min | number | 0 | The minimum entity value to be displayed. Accepts entity id as value.
| max | number | 100 | The maximum entity value to be displayed. Accepts entity id as value.
| target | number | none | Sets a target marker, must be a value between min and max value. Accepts entity id as value.
| speed | number | 2500 | The speed of the bar animation in milliseconds.
| delay | number| 7500 | The amout of time between the bar animation loop in milliseconds.
| direction | string | right | Direction of the bar. `left`,`right`,`up`,`down`
| severity | object | none | A list of severity values.
| card_style | object | none | A list of CSS styles applied to the card background.
| bar_style | object | none | A list of CSS styles applied to the bar.
| title_style | object | none | A list of CSS styles applied to the title.
| indicator_style | object| none | A list of CSS styles applied to the indicator.
| charge_entity | string | none | Charge enitity, **required** when using charge animation mode. States can be `on`/`off`, `true`/`false`, `charging`/`discharging`

## Examples

### Default

![](images/default_increase.gif)

```yaml
- type: custom:bar-card
  title: Default
  entity: sensor.default
```
### Severity

![](images/severity.gif)

```yaml
- type: custom:bar-card
  title: Severity
  entity: sensor.default
  severity:
  - value: 25
    hue: '0'
  - value: 50
    hue: '40'
  - value: 100
    hue: '120'
```
### Hue

![](images/hue.gif)

```yaml
- type: custom:bar-card
  title: Default
  entity: sensor.default
  hue: 300
```
### Speed & Delay

![](images/speed_delay.gif)

```yaml
- type: custom:bar-card
  title: Default
  entity: sensor.default
  speed: 5000
  delay: 10000
```

### Entities + [Auto Entities](https://github.com/thomasloven/lovelace-auto-entities)

![](images/entities_example.png)

```yaml
- type: custom:auto-entities
  card:
    type: custom:bar-card
    severity:
      - value: 50
        hue: '0'
      - value: 75
        hue: '40'
      - value: 100
        hue: '120'
    title_position: inside
    columns: 3
    padding: 2px
    title_style:
      text-align: left
      font-size: 16px
    bar_style:
      align-items: flex-start
      font-size: 8px
  filter:
    include:
      - entity_id: "*_battery"

- type: custom:auto-entities
  card:
    type: custom:bar-card
    attribute: battery
    unit_of_measurement: "%"
    severity:
      - value: 50
        hue: '0'
      - value: 75
        hue: '40'
      - value: 100
        hue: '120'
    title_position: inside
    padding: 2px
    columns: 2
  filter:
    include:
      - attributes:
          battery: "<=100"
    exclude:
      - entity_id: "*_humidity"
      - entity_id: "*_pressure"
      - entity_id: "*_battery"

- type: custom:bar-card
  attribute: temperature
  unit_of_measurement: "°C"
  title_position: inside
  columns: 5
  height: 200px
  min: 15
  max: 32
  target: 22.5
  width: 100%
  padding: 2px
  direction: up
  entities:
    - binary_sensor.motion_hallway
    - binary_sensor.motion_living_room
    - binary_sensor.motion_kitchen
    - binary_sensor.motion_bathroom
    - binary_sensor.motion_toilet
```

## Credits
Inspired by [Big Number Card](https://github.com/ciotlosm/custom-lovelace/tree/master/bignumber-card) by [ciotlosm](https://github.com/ciotlosm).

## Links
[Home Assistant Community Topic](https://community.home-assistant.io/t/lovelace-bar-card/87503)
