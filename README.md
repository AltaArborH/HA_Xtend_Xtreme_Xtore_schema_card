# HA_Xtend_Xtreme_Xtore_schema_card

This Fork is based on the [HA_Xtend_Xtreme_schema_card](https://github.com/webpatrick/HA_Xtend_Xtreme_schema_card). 

With this card, the information from the Xtore is also added to the schema-card made by [WebPatrick](https://github.com/webpatrick).  


<img width="400" alt="schema-card" src="https://github.com/AltaArborH/HA_Xtend_Xtreme_Xtore_schema_card/blob/main/Schema-card_Xtend_Xtreme_Xtore_v0.1.png" />

To retrieve the correct data used in this card, see my other GitHub page [AltaArborH/HA_Xtend-Xtreme-Xtore](https://github.com/AltaArborH/HA_Xtend-Xtreme-Xtore).

## Installation

Copy the code from the xtend_xtreme_schema_card.yaml into an empty card.

### Dependencies
- <a href="https://github.com/DSchoutsen/HA_connection_Xtend">HA_connection_Xtend</a> for the connection to and sensors from Xtend and Xtreme
- <a href="https://github.com/thomasloven/lovelace-card-mod">Card Mod (HACS)</a> for animation and styling
- <a href="https://github.com/piitaya/lovelace-mushroom">Mushroom Title Card (HACS)</a> for some headers

In addition to the Xtend and Xtreme template sensors (from DSchouten HA_connection_Xtend) some extra calculated sensors are added to use in this card:

### Xtend
```yaml
- binary_sensor:
    - name: xtend_actief_check
      unique_id: xtend_actief_check
      state: "{{ states('sensor.xtend_heatpumpmode') == 'Heating' }}"
      icon: >
        {% if states('sensor.xtend_heatpumpmode') == 'Heating' %}
          mdi:fire
        {% else %}
          mdi:fire-off
        {% endif %}
```

### Xtreme
```yaml
# Custom calculated xtreme entities
- sensor:
    - name: xtreme_deltaT
      unique_id: 11932596-f4ae-4c89-9dad-2163f442711c
      unit_of_measurement: "°C"
      device_class: temperature
      state_class: measurement
      state: >
        {{ (states('sensor.xtreme_tBoilerSupply') | int - states('sensor.xtreme_tBoilerReturn') | int) | float | round(1) }}
      icon: mdi:thermometer-check

- binary_sensor:
    - name: "Xtreme Actief Check"
      unique_id: 0e3bae55-3c03-4722-a306-b919c78f0cb8
      state: "{{ states('sensor.xtreme_deltat') | float(0) > 0.5 }}"
      icon: >
        {% if states('sensor.xtreme_deltat') | float(0) > 0.5 %}
          mdi:fire
        {% else %}
          mdi:fire-off
        {% endif %}
```

I hope I covered all dependencies. Made this repository after everything was running smooth.

#### My current cards including the Xtore:

<img width="400" alt="Screenshot Xtore-related cards" src="https://github.com/AltaArborH/HA_Xtend_Xtreme_Xtore_schema_card/blob/main/Schema-cards_including_Xtore_v0.1.png" />
