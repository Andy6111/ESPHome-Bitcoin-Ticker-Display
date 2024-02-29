# ESPHome Bitcoin Ticker Display

**Useful and cheap crypto ticker for DYI projects. Its easily customizable to different crypto.**  

<img src="https://github.com/Andy6111/ESPHome-Bitcoin-Ticker-Display/blob/main/ticker_display.jpg)" width=50% height=50% >

## Main features: 

Small crypto ticker with display that shows Bitcoin/EUR:

- current price
- 1h change of price in % 
- 24h change of price in %
- last update of received data
- clock

(all data are updated every minute as default)

## Wiring

 **Board ESP32  - > Display ILI9341**
```
 3.3V -> VCC
  GND -> GND
  D13 -> CS
  D33 -> RESET
  D14 -> DC
  D27 -> SDI (MOSI) 
  D26 -> SCK  
  D25 -> LED
```
## Files required
```
bitcoin.png (logo used in project)
arial.ttf (font used in project)
```

## Data sources and Home assistant integration

It will require the Home Assistant integration with https://github.com/heyajohnny/cryptoinfo

**Configuration used in my project (stored in configuration.yaml in HA):**
```
sensor:  
- platform: cryptoinfo
  id: "main"
  cryptocurrency_name: "bitcoin"
  currency_name: "eur"
  unit_of_measurement: "€"
  multiplier: 1
  update_frequency: 1
        
- platform: template
  sensors: 
   cryptoinfo_main_bitcoin_eur_24h_change:
    value_template: "{{ state_attr('sensor.cryptoinfo_main_bitcoin_eur', '24h_change') | float(2) }}"
    unit_of_measurement: "%"
    
- platform: template
  sensors: 
   cryptoinfo_main_bitcoin_eur_1h_change:
    value_template: "{{ state_attr('sensor.cryptoinfo_main_bitcoin_eur', '1h_change') | float(2) }}"
    unit_of_measurement: "%"
    
- platform: template
  sensors:
    cryptoinfo_main_bitcoin_eur_last_update:
     value_template: "{{ state_attr('sensor.cryptoinfo_main_bitcoin_eur', 'last_update') }}"
```
## Backlight 
ESPHOME creates an entity in Home Assistant that can be used to control the brightness of the display, or turn it off with a schedule etc.


![Image](https://github.com/users/Andy6111/projects/1/assets/57748859/1a028b75-b35f-4791-b27e-66b7a3b1987f)

## Customization 

To change the ticker for different crypto you have to edit esphome yaml file same as Home assistant configuration.yaml file.
