# Wafe 350EFS2 via modbus TCP for homeassistant
Configuration, action scripts and lovelace cards source codes.

## Preface
[Wafe 350EFS2](https://www.wafe.eu/en/product/wafe-350-efs2) is standalone recuperation unit driven by RasPi controller with ModBus TCP protocol. 
Unit can be controller by [online web application](https://www.wafe.eu/en/product/mywafe).

## Solution
Homeassistant can communicate with [ModBus protocol](https://www.home-assistant.io/integrations/modbus/). Homeassistant can easily connect via TCP protocol and interface can be easily configured for current unit.

## Software setup
Software setup is very easy:
1. Copy `src/configuration.yaml` to homeassistant configuration file a set `host` to your local IP address of Wafe350 unit.
```
modbus:
  - name: Wafe
    type: tcp
    host: 10.0.0.76
    port: 502
```
2. Copy `src/scripts.yaml` to homeassistant scripts file.
3. Check syntax of configuration file and restart homeassistant.

![alt text](res/hassio-server-check.png)

4. Check `Developer Tools` to unsure that sensors work properly.

![alt text](res/hassio-developer-tools.png)

5. Configure lovelace card as usual, for exaqmple:
```
type: vertical-stack
cards:
  - type: horizontal-stack
    cards:
      - type: entity
        entity: sensor.indoor_air
        name: Inside
      - type: entity
        entity: sensor.outside_air
        name: Outside
  - type: horizontal-stack
    cards:
      - type: gauge
        entity: sensor.humidity_inside_out
        min: 0
        max: 100
        name: Humidity
        severity:
          green: 40
          yellow: 60
          red: 80
      - type: gauge
        entity: sensor.fresh_air_fan_perc
        min: 0
        max: 100
        name: Ventilation
        severity:
          green: 30
          yellow: 60
          red: 90
      - type: gauge
        entity: sensor.co2_inside
        min: 0
        max: 2000
        severity:
          green: 500
          yellow: 1000
          red: 1500
        name: CO2
```

![alt text](res/hassio-lovelace-card.png)