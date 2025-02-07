# Idea

After switching to an exchange-based electricity provider, I wanted to be able to cover my electricity needs with cheap electricity even during the expensive hours. The solution here was to use the PV system's electricity storage unit. This means that when the electricity price is cheap, the forecast for the solar yield is low and the efficiency of the system allows it, electricity from the grid should be charged into the house battery.

There are many parameters:
1. own electricity consumption/hour
2. predicted amount of solar power/hour
3. electricity price/hour
4. efficiency of the inverter+battery

ApexChart (see below):
![ApexChart](https://github.com/rybe/energy-charging/blob/main/docu/apexcharts.png)

Debug output:

    Status │ Zeit │   Preis │ üMin% │ uMax% │ uBat  │ chBat │ Bedarf │   solC │   calcB │ NetzB │     EDE │    SoC │     LF 
    ───────┼──────┼─────────┼───────┼───────┼───────┼───────┼────────┼────────┼─────────┼───────┼─────────┼────────┼────────
       <>A │ 09   │ 0.37450 │  19.3 │  -4.3 │ False │ False │    610 │    680 │     144 │ True  │     144 │      0 │        
         A │ 10   │ 0.35550 │  13.3 │  -9.1 │ False │ False │    680 │    568 │     350 │ True  │     350 │      0 │        
     <>S-A │ 11   │ 0.33290 │   6.1 │ -14.9 │ False │ True  │    720 │    268 │     704 │ False │       0 │      0 │        
         A │ 12   │ 0.32810 │   4.5 │ -16.1 │ False │ True  │    810 │    298 │     796 │ False │       0 │      0 │        
         A │ 13   │ 0.32340 │   3.0 │ -17.3 │ False │ True  │    830 │    715 │     406 │ False │       0 │      0 │        
         A │ 14   │ 0.32690 │   4.2 │ -16.4 │ False │ True  │    860 │   1177 │     -16 │ False │       0 │     16 │        
         A │ 15   │ 0.32930 │   4.9 │ -15.8 │ False │ True  │    840 │    672 │     462 │ False │       0 │      0 │        
         A │ 16   │ 0.34720 │  10.6 │ -11.2 │ False │ True  │    890 │    140 │    1062 │ False │       0 │      0 │        
       <>A │ 17   │ 0.36620 │  16.7 │  -6.4 │ False │ False │    830 │      0 │    1120 │ True  │    1120 │      0 │        
         A │ 18   │ 0.37340 │  19.0 │  -4.6 │ False │ False │   1000 │      0 │    1350 │ True  │    1350 │      0 │        
         A │ 19   │ 0.36740 │  17.1 │  -6.1 │ False │ False │   1140 │      0 │    1539 │ True  │    1539 │      0 │        
     <>S-A │ 20   │ 0.34720 │  10.6 │ -11.2 │ False │ True  │   1000 │      0 │    1350 │ False │       0 │      0 │        
         A │ 21   │ 0.31500 │   0.4 │ -19.5 │ False │ True  │   1000 │      0 │    1350 │ False │       0 │      0 │        
         A │ 22   │ 0.31390 │   0.0 │ -19.8 │ False │ True  │    730 │      0 │     986 │ False │       0 │      0 │        
         A │ 23   │ 0.31500 │   0.4 │ -19.5 │ False │ True  │    670 │      0 │     904 │ False │       0 │      0 │        
    ───────┼──────┼─────────┼───────┼───────┼───────┼───────┼────────┼────────┼─────────┼───────┼─────────┼────────┼────────
    Status │ Zeit │   Preis │ üMin% │ uMax% │ uBat  │ chBat │ Bedarf │   solC │   calcB │ NetzB │     EDE │    SoC │     LF 
    ───────┼──────┼─────────┼───────┼───────┼───────┼───────┼────────┼────────┼─────────┼───────┼─────────┼────────┼────────
        +* │ 9    │ 0.37450 │  19.3 │  -4.3 │ False │ False │    610 │    680 │     144 │ True  │     144 │      0 │    0.0 
        +* │ 10   │ 0.35550 │  13.3 │  -9.1 │ False │ False │    680 │    568 │     350 │ True  │     350 │      0 │    0.0 
        +L │ 11   │ 0.33280 │   6.1 │ -14.9 │ False │ True  │    720 │    268 │     704 │ False │       0 │      0 │  0.992 
        +L │ 12   │ 0.32810 │   4.5 │ -16.1 │ False │ True  │    810 │    298 │     796 │ False │       0 │      0 │  1.008 
        +L │ 13   │ 0.32330 │   3.0 │ -17.3 │ False │ True  │    830 │    715 │     406 │ False │       0 │      0 │  1.023 
         L │ 14   │ 0.32690 │   4.2 │ -16.4 │ False │ True  │    860 │   1177 │     -16 │ False │       0 │     16 │  1.011 
        +L │ 15   │ 0.32930 │   4.9 │ -15.8 │ False │ True  │    840 │    672 │     462 │ False │       0 │      0 │  1.004 
        +L │ 16   │ 0.34710 │  10.6 │ -11.3 │ False │ True  │    890 │    140 │    1062 │ False │       0 │      0 │  0.947 
        +* │ 17   │ 0.36620 │  16.7 │  -6.4 │ False │ False │    830 │      0 │    1120 │ True  │    1120 │      0 │    0.0 
        +* │ 18   │ 0.37330 │  18.9 │  -4.6 │ False │ False │   1000 │      0 │    1350 │ True  │    1350 │      0 │    0.0 
        +* │ 19   │ 0.36740 │  17.0 │  -6.1 │ False │ False │   1140 │      0 │    1539 │ True  │    1539 │      0 │    0.0 
        +L │ 20   │ 0.34710 │  10.6 │ -11.3 │ False │ True  │   1000 │      0 │    1350 │ False │       0 │      0 │  0.947 
        +L │ 21   │ 0.31500 │   0.4 │ -19.5 │ False │ True  │   1000 │      0 │    1350 │ False │       0 │      0 │  1.049 
        +L │ 22   │ 0.31380 │   0.0 │ -19.8 │ False │ True  │    730 │      0 │     986 │ False │       0 │      0 │  1.053 
        +L │ 23   │ 0.31500 │   0.4 │ -19.5 │ False │ True  │    670 │      0 │     904 │ False │       0 │      0 │  1.049 
      
        SoC:                   0 W (0%)
        PV Total:              0 W
        Strombedarf:           0 W / 10 h (0 W/h)
        Aktueller Preis:       0.3745 Euro
        Laden zwischen:        0.3139 - 0.3531 Euro
        Batterie nicht nutzen: 0.3531 - 0.3924 Euro
        Batterie nutzen:       0.3924 - 0.3912 Euro
        Laden mit:             0 W/h 0.0 %
    
        Gültig von:            2025-02-07 09:00:00+01:00
        Gültig bis:            2025-02-07 23:00:00+01:00
        

## How to install

You need to have Home Assistant 2023.11 or higher installed to use this custom template.

For a install you can copy the contents of  `energy_charging.jinja`  to a jinja file in your  `custom_templates`  folder. Run the  `homeassistant.reload_custom_templates`  service call to load the file.

The necessary sensors for the exchange price and solar forecast are selected automatically. To do this, install “Nord Pool integration for Home Assistant” from HACS and “HA Solcast PV Solar Forecast Integration” from https://github.com/BJReplay/ha-solcast-solar. Further information can be found in HACS or on the websites.

**Done**

## Use

### Minimum parameters
    {%- from 'energy_charging.jinja' import energy_charging -%}
    {{- energy_charging(BatteriesSoC='sensor.sunny_tripower_10_0_se_battery_soc_total', 
                        PVTotal='sensor.pv_power_total',
                       )|float
    -}}

### Parameters in practice
    {%- from 'energy_charging.jinja' import energy_charging -%}
    {{- energy_charging(getValue='recommandation',
                        BatteriesSoC='sensor.sunny_tripower_10_0_se_battery_soc_total', 
                        PVTotal='sensor.pv_power_total', 
                        addOnCosts = 'input_number.stromzusatzkosten',
                        SafetyMargin = states('input_number.le_safetymargin')|float,
                        dissipation = states('input_number.le_dissipation')|float,
                       )|int
    -}}

## Parameters

|Parameter|Type|Default - Options|Explanation|
|--|--|--|--|
| debug | boolean | false | Displays a table of all values |
| getValue | string |**recommandation** | Displays the recommended charge value in watts (W)|
|||price | shows the current electricity price
|||maxprice|shows the maximum electricity price
|||minprice|shows the minimum electricity price
|||loadinguntil|shows the charge limit in euros
|||usebatteriesuntil|indicates when the battery should be used
|||getforecast|shows the future load values based on the current values
|||getforecastSoC|shows the future charge values based on the current values (SoC)
|||validityrange|specifies the validity range
|actualHour|number|now().hour|specifies the hour for which the values are to be calculated
|BatteriesSoC|number or string|0| Current SoC of the battery. E.g.: 'sensor.sunny_tripower_10_0_se_battery_soc_total' or 10 (for 10%)
|PVTotal|number or string|0|Current power of the PV system in W (float) or name of the sensor ('sensor.pv_power_total')
|addOnCosts|number or string|0|Additional electricity costs (€) or name of the sensor ('input_number.stromzusatzkosten')
|tax|number| 1.19|Value added tax
|recalcPrices| boolean| false | Calculates the charging limits from the current hour (otherwise the entire 24 hours are taken into account)
|recalcValuesMinCount|number|6| If recalcPrices = true valid. At least n entries must be pending
|EQE|string or number|**30**|If the current electricity price is so high that charging is not allowed, but the price is too low to discharge the battery, then this value is returned.
|||auto|a calculated value is returned, useful if you need to specify an “exact” value
|||static value|useful if this prevents the battery from discharging 
|||off|no value is returned, so no distinction can be made as to whether the battery may be discharged or not
|PowerRequirement|array||This array contains the normal consumption per hour. The standard values can be transferred as an array (see example) or stored directly in the jinja2 file.
||||Beispiel: `{%- set PowerRequirementWithoutPV =  [  630,  630,  610,  660,  620,  620,  700,  770,  830,  610,  680,  720, 810,  830,  860,  840,  890,  830, 1000, 1140, 1000, 1000,  730,  670] -%}`
|SafetyMargin|number|1.2|The percentage safety margin
|dissipation|number|0.125|The percentage dissipation
|capBatteries|number|13800|Total battery capacity in watts
|maxPowerLoad|number|10800|Total battery charging power in watts


## Template Sensors

      template:
        - trigger:
            - platform: time_pattern
              minutes: "/10"
            - platform: homeassistant
              event: start
            - platform: state
              entity_id: 
              - sensor.poetenweg_3_strompreis
              - sensor.pv_power_total
              - sensor.nordpool_energiepreise
              - input_boolean.le_recalcprices
              - input_number.le_recalcvaluesmincount
              - input_number.le_safetymargin
              - input_number.le_dissipation
          sensor:
            - unique_id: pv_ladeempfehlung_sensor
              device_class: power
              state_class: measurement
              unit_of_measurement: W
              name: PV Ladeempfehlung
              state: >
                {%- from 'energy_charging.jinja' import energy_charging -%}
                {{- energy_charging(getValue='recommandation',
                                    BatteriesSoC='sensor.sunny_tripower_10_0_se_battery_soc_total', 
                                    PVTotal='sensor.pv_power_total', 
                                    addOnCosts = 'input_number.stromzusatzkosten',
                                    recalcPrices = states('input_boolean.le_recalcprices'), 
                                    recalcValuesMinCount = states('input_number.le_recalcvaluesmincount')|int,
                                    SafetyMargin = states('input_number.le_safetymargin')|float,
                                    dissipation = states('input_number.le_dissipation')|float,
                                    )|int
                -}}

Short description:
Sensors:
- sensor.pv_power_total
- sensor.nordpool_energiepreise
- input_boolean.le_recalcprices
- input_number.le_recalcvaluesmincount
- input_number.le_safetymargin
- input_number.le_dissipation

are defined here as triggers so that a new value is calculated when necessary. Why is this important? Depending on which values you want to calculate, you should not “overload” Home Assistant with them. My experience has shown that it doesn't like it if you trigger so often with the sensor 'sensor.pv_power_total', for example, and the recursion used leads to a “crash”.

Below are all my used template sensors (outsourced in template.yaml):

    - trigger:
        - platform: time_pattern
          minutes: "/10"
        - platform: homeassistant
          event: start
        - platform: state
          entity_id: 
          - sensor.poetenweg_3_strompreis
          - sensor.pv_power_total
          - sensor.nordpool_energiepreise
          - input_boolean.le_recalcprices
          - input_number.le_recalcvaluesmincount
          - input_number.le_safetymargin
          - input_number.le_dissipation
      sensor:
        - unique_id: pv_ladeempfehlung_sensor
          device_class: power
          state_class: measurement
          unit_of_measurement: W
          name: PV Ladeempfehlung
          state: >
            {%- from 'energy_charging.jinja' import energy_charging -%}
            {{- energy_charging(getValue='recommandation',
                                BatteriesSoC='sensor.sunny_tripower_10_0_se_battery_soc_total', 
                                PVTotal='sensor.pv_power_total', 
                                addOnCosts = 'input_number.stromzusatzkosten',
                                recalcPrices = states('input_boolean.le_recalcprices'), 
                                recalcValuesMinCount = states('input_number.le_recalcvaluesmincount')|int,
                                SafetyMargin = states('input_number.le_safetymargin')|float,
                                dissipation = states('input_number.le_dissipation')|float,
                                )|int
            -}}
    
    - trigger:
        - platform: homeassistant
          event: start
        - platform: state
          entity_id: 
          - sensor.nordpool_energiepreise
          - input_boolean.le_recalcprices
          - input_number.le_recalcvaluesmincount      
          - input_number.le_safetymargin
          - input_number.le_dissipation
      sensor:
        - unique_id: ladeempfehlung_forecastSoC_sensor
          device_class: power
          state_class: measurement
          unit_of_measurement: W
          name: "Ladeempfehlung Forecast"
          state: >
            {%- from 'energy_charging.jinja' import energy_charging -%}
            {{- energy_charging(getValue='recommandation',
                                BatteriesSoC='sensor.sunny_tripower_10_0_se_battery_soc_total', 
                                PVTotal='sensor.pv_power_total', 
                                addOnCosts = 'input_number.stromzusatzkosten',
                                recalcPrices = states('input_boolean.le_recalcprices'), 
                                recalcValuesMinCount = states('input_number.le_recalcvaluesmincount')|int,
                                SafetyMargin = states('input_number.le_safetymargin')|float,
                                dissipation = states('input_number.le_dissipation')|float,
                                )|int
            -}}
          attributes:
            loadingUntil: >
                {%- from 'energy_charging.jinja' import energy_charging -%}
                {{- energy_charging(getValue='loadingUntil',
                                    BatteriesSoC='sensor.sunny_tripower_10_0_se_battery_soc_total', 
                                    PVTotal='sensor.pv_power_total', 
                                    addOnCosts = 'input_number.stromzusatzkosten',
                                    recalcPrices = states('input_boolean.le_recalcprices'), 
                                    recalcValuesMinCount = states('input_number.le_recalcvaluesmincount')|int,
                                    SafetyMargin = states('input_number.le_safetymargin')|float,
                                    dissipation = states('input_number.le_dissipation')|float,
                                    )|float
                -}}
            useBatteriesUntil: >
                {%- from 'energy_charging.jinja' import energy_charging -%}
                {{- energy_charging(getValue='useBatteriesUntil',
                                    BatteriesSoC='sensor.sunny_tripower_10_0_se_battery_soc_total', 
                                    PVTotal='sensor.pv_power_total', 
                                    addOnCosts = 'input_number.stromzusatzkosten',
                                    recalcPrices = states('input_boolean.le_recalcprices'), 
                                    recalcValuesMinCount = states('input_number.le_recalcvaluesmincount')|int,
                                    SafetyMargin = states('input_number.le_safetymargin')|float,
                                    dissipation = states('input_number.le_dissipation')|float,
                                    )|float
                -}}
            cheapestforecast: >
                {%- from 'energy_charging.jinja' import energy_charging -%}
                {{- energy_charging(getValue='getcheapestforecast',
                                    BatteriesSoC='sensor.sunny_tripower_10_0_se_battery_soc_total', 
                                    PVTotal='sensor.pv_power_total', 
                                    addOnCosts = 'input_number.stromzusatzkosten',
                                    recalcPrices = states('input_boolean.le_recalcprices'), 
                                    recalcValuesMinCount = states('input_number.le_recalcvaluesmincount')|int,
                                    SafetyMargin = states('input_number.le_safetymargin')|float,
                                    dissipation = states('input_number.le_dissipation')|float,
                                    )
                -}}
            forecast: >
                {%- from 'energy_charging.jinja' import energy_charging -%}
                {{- energy_charging(getValue='getforecast',
                                    BatteriesSoC='sensor.sunny_tripower_10_0_se_battery_soc_total', 
                                    PVTotal='sensor.pv_power_total', 
                                    addOnCosts = 'input_number.stromzusatzkosten',
                                    recalcPrices = states('input_boolean.le_recalcprices'), 
                                    recalcValuesMinCount = states('input_number.le_recalcvaluesmincount')|int,
                                    SafetyMargin = states('input_number.le_safetymargin')|float,
                                    dissipation = states('input_number.le_dissipation')|float,
                                    )
                -}}
            forecastSoC: >
                {%- from 'energy_charging.jinja' import energy_charging -%}
                {{- energy_charging(getValue='getForecastSoC',
                                    BatteriesSoC='sensor.sunny_tripower_10_0_se_battery_soc_total', 
                                    PVTotal='sensor.pv_power_total', 
                                    addOnCosts = 'input_number.stromzusatzkosten',
                                    recalcPrices = states('input_boolean.le_recalcprices'), 
                                    recalcValuesMinCount = states('input_number.le_recalcvaluesmincount')|int,
                                    SafetyMargin = states('input_number.le_safetymargin')|float,
                                    dissipation = states('input_number.le_dissipation')|float,
                                    recursion=true)
                -}}        
    - trigger:
        - platform: time_pattern
          minutes: "/10"
        - platform: homeassistant
          event: start
        - platform: state
          entity_id: 
          - sensor.nordpool_energiepreise
          - input_boolean.le_recalcprices
          - input_number.le_recalcvaluesmincount
          - input_number.le_safetymargin
          - input_number.le_dissipation
          
      sensor:
        - unique_id: ladeempfehlung_minPrice_sensor
          name: Ladeempfehlung Mindestpreis
          unit_of_measurement: "€"
          state: >
            {%- from 'energy_charging.jinja' import energy_charging -%}
            {{- energy_charging(getValue='useBatteriesUntil',
                                BatteriesSoC='sensor.sunny_tripower_10_0_se_battery_soc_total', 
                                PVTotal='sensor.pv_power_total', 
                                addOnCosts = 'input_number.stromzusatzkosten',
                                recalcPrices = states('input_boolean.le_recalcprices'), 
                                recalcValuesMinCount = states('input_number.le_recalcvaluesmincount')|int,
                                SafetyMargin = states('input_number.le_safetymargin')|float,
                                dissipation = states('input_number.le_dissipation')|float,
                                )|float
            -}}
    - trigger:
        - platform: time_pattern
          minutes: "/10"
        - platform: homeassistant
          event: start
        - platform: state
          entity_id: 
          - sensor.nordpool_energiepreise
          - input_boolean.le_recalcprices
          - input_number.le_recalcvaluesmincount      
          - input_number.le_safetymargin
          - input_number.le_dissipation
      sensor:
        - unique_id: ladeempfehlung_maxPrice_sensor
          name: Ladeempfehlung Maximalpreis
          unit_of_measurement: "€"
          state: >
            {%- from 'energy_charging.jinja' import energy_charging -%}
            {{- energy_charging(getValue='loadingUntil',
                                BatteriesSoC='sensor.sunny_tripower_10_0_se_battery_soc_total', 
                                PVTotal='sensor.pv_power_total', 
                                addOnCosts = 'input_number.stromzusatzkosten',
                                recalcPrices = states('input_boolean.le_recalcprices'), 
                                recalcValuesMinCount = states('input_number.le_recalcvaluesmincount')|int,
                                SafetyMargin = states('input_number.le_safetymargin')|float,
                                dissipation = states('input_number.le_dissipation')|float,
                                )|float
            -}}
            
    - trigger:
        - platform: time_pattern
          minutes: "/10"
        - platform: homeassistant
          event: start
        - platform: state
          entity_id: 
          - sensor.nordpool_energiepreise
          - input_boolean.le_recalcprices
          - input_number.le_recalcvaluesmincount      
          - input_number.le_safetymargin
          - input_number.le_dissipation
      sensor:
        - unique_id: Ladeempfehlung_Min_Strompreis
          name: Ladeempfehlung Min-Strompreis
          unit_of_measurement: "€"
          state: >
            {%- from 'energy_charging.jinja' import energy_charging -%}
            {{- energy_charging(getValue='minPrice',
                                BatteriesSoC='sensor.sunny_tripower_10_0_se_battery_soc_total', 
                                PVTotal='sensor.pv_power_total', 
                                addOnCosts = 'input_number.stromzusatzkosten',
                                recalcPrices = states('input_boolean.le_recalcprices'), 
                                recalcValuesMinCount = states('input_number.le_recalcvaluesmincount')|int,
                                SafetyMargin = states('input_number.le_safetymargin')|float,
                                dissipation = states('input_number.le_dissipation')|float,
                                )|float
            -}}
            
    - trigger:
        - platform: time_pattern
          minutes: "/10"
        - platform: homeassistant
          event: start
        - platform: state
          entity_id: 
          - sensor.nordpool_energiepreise
          - input_boolean.le_recalcprices
          - input_number.le_recalcvaluesmincount
          - input_number.le_safetymargin
          - input_number.le_dissipation
      sensor:
        - unique_id: Ladeempfehlung_Max_Strompreis
          name: Ladeempfehlung Max-Strompreis
          unit_of_measurement: "€"
          state: >
            {%- from 'energy_charging.jinja' import energy_charging -%}
            {{- energy_charging(getValue='maxPrice',
                                BatteriesSoC='sensor.sunny_tripower_10_0_se_battery_soc_total', 
                                PVTotal='sensor.pv_power_total', 
                                addOnCosts = 'input_number.stromzusatzkosten',
                                recalcPrices = states('input_boolean.le_recalcprices'), 
                                recalcValuesMinCount = states('input_number.le_recalcvaluesmincount')|int,
                                SafetyMargin = states('input_number.le_safetymargin')|float,
                                dissipation = states('input_number.le_dissipation')|float,
                                )|float
            -}}
    
    - trigger:
        - platform: time_pattern
          minutes: "/10"
        - platform: homeassistant
          event: start
        - platform: state
          entity_id: 
          - sensor.nordpool_energiepreise
          - input_boolean.le_recalcprices
          - input_number.le_recalcvaluesmincount      
          - input_number.le_safetymargin
          - input_number.le_dissipation
      sensor:
        - unique_id: Ladeempfehlung_Strompreis
          name: Ladeempfehlung Strompreis
          unit_of_measurement: "€"
          state: >
            {%- from 'energy_charging.jinja' import energy_charging -%}
            {{- energy_charging(getValue='Price',
                                BatteriesSoC='sensor.sunny_tripower_10_0_se_battery_soc_total', 
                                PVTotal='sensor.pv_power_total', 
                                addOnCosts = 'input_number.stromzusatzkosten',
                                recalcPrices = states('input_boolean.le_recalcprices'), 
                                recalcValuesMinCount = states('input_number.le_recalcvaluesmincount')|int|int,
                                SafetyMargin = states('input_number.le_safetymargin')|float,
                                dissipation = states('input_number.le_dissipation')|float,
                                )|float
            -}}

Here is my ApexChart configuration:

    type: custom:apexcharts-card
    experimental:
      color_threshold: true
    apex_config:
      grid:
        show: true
        borderColor: "#505050"
      chart:
        height: 400px
        offsetY: -10
      tooltip:
        enabled: true
        followCursor: true
        x:
          show: false
        fixed:
          enabled: false
    yaxis:
      - min: 0
        max: 10600
        opposite: true
        apex_config:
          tickAmount: 10
          forceNiceScale: true
        id: links2
      - min: 12
        max: "|3|"
        apex_config:
          tickAmount: 10
          forceNiceScale: false
        id: links
      - min: 0
        max: 1
        show: false
        apex_config:
          forceNiceScale: false
        id: rechts
      - opposite: true
        min: 0
        max: 100
        show: true
        apex_config:
          forceNiceScale: false
        id: rechts2
    header:
      show: true
      show_states: true
      colorize_states: true
      standard_format: false
    now:
      show: true
      color: 9E9E9E
      label: jetzt
    graph_span: 42h
    span:
      start: hour
      offset: "-8h"
    series:
      - entity: sensor.sunny_tripower_10_0_se_battery_soc_total
        color: rgb(66, 135, 245)
        show:
          in_header: raw
          name_in_header: true
        name: Akku-Füllstand
        unit: "%"
        type: area
        opacity: 0.2
        extend_to: now
        stroke_width: 2
        float_precision: 2
        fill_raw: last
        yaxis_id: rechts2
      - entity: sensor.ladeempfehlung_forecast
        name: Akku nutzen
        yaxis_id: links
        show:
          in_header: false
          in_chart: true
          in_legend: false
        type: area
        curve: stepline
        extend_to: false
        color: red
        color_threshold:
          - value: 0
            color: black
          - value: 30
            color: red
        opacity: 0.1
        stroke_width: 0
        float_precision: 2
        data_generator: |
          const noon = new Date();
          noon.setHours(0, 0, 0, 11);
          const item = entity.attributes.cheapestforecast;
          const data = [];
          let h = item[0].hour*1;
          let v = 0;
          for(let i = 0; i < item.length+h; i++) {
            var nh = i;
            if (i >= h && i<item.length+h) {
              v = (item[i-h].useBatteries == true)
              v = v*item[i-h].price*100;
            }
            data.push([noon.getTime() + nh * 1000 * 3600, v]);
          }
          data.push([noon.getTime() + (nh+1) * 1000 * 3600, v]);
          return data; 
      - entity: sensor.ladeempfehlung_forecast
        name: Akku nicht nutzen
        yaxis_id: links
        show:
          in_header: false
          in_chart: true
          in_legend: false
        type: area
        curve: stepline
        extend_to: false
        color: yellow
        color_threshold:
          - value: 0
            color: black
          - value: 25
            color: yellow
        opacity: 0.15
        stroke_width: 0
        float_precision: 2
        data_generator: |
          const noon = new Date();
          noon.setHours(0, 0, 0, 10);
          const item = entity.attributes.cheapestforecast;
          const data = [];
          var h = item[0].hour*1;
          for(let i = 0; i < item.length+h; i++) {
            var v = 0;
            var nh = i;
            if (i >= h && i<item.length+h) {
              v = (item[i-h].useBatteries == false && item[i-h].chargeBatteries == false)*1;
              v = v*item[i-h].price*100;
            }
            data.push([noon.getTime() + nh * 1000 * 3600, v]);
          }
          data.push([noon.getTime() + (nh+1) * 1000 * 3600, v]);
          return data;
      - entity: sensor.ladeempfehlung_forecast
        name: Laden
        yaxis_id: links
        show:
          in_header: false
          in_chart: true
          in_legend: false
        type: area
        curve: stepline
        extend_to: false
        color: green
        color_threshold:
          - value: 0
            color: black
          - value: 20
            color: green
        opacity: 0.1
        stroke_width: 0
        float_precision: 2
        data_generator: |
          const noon = new Date();
          noon.setHours(0, 0, 0, 9);
          const item = entity.attributes.cheapestforecast;
          const data = [];
          var h = item[0].hour*1;
          for(let i = 0; i < item.length+h; i++) {
            var v = 0;
            var nh = i;
            if (i >= h && i<item.length+h) {
              v = item[i-h].chargeBatteries*1;
              v = v*item[i-h].price*100;
            }
            data.push([noon.getTime() + nh * 1000 * 3600, v]);
          }
          data.push([noon.getTime() + (nh+1) * 1000 * 3600, v]);
          return data; 
      - entity: sensor.ladeempfehlung_forecast
        name: Laden unter
        unit: Cent
        yaxis_id: links
        show:
          in_header: false
          in_chart: true
        type: line
        opacity: 0.4
        curve: stepline
        extend_to: false
        color: white
        stroke_width: 1
        stroke_dash: 0
        float_precision: 2
        data_generator: |
          const noon = new Date()
          noon.setHours(0, 0, 0, 8)
          const item = entity.attributes.forecast;
          const h = item[0].hour*1;      
          const price = entity.attributes.useBatteriesUntil*100;
          const data = [];
          for(let i = h+1; i <= 48; i++) {
            data.push([noon.getTime() + i * 1000 * 3600, price])
          }
          return data;    
      - entity: sensor.ladeempfehlung_mindestpreis
        name: Laden unter (Historie)
        unit: Cent
        yaxis_id: links
        show:
          in_header: false
          in_chart: true
        type: line
        opacity: 0.4
        curve: stepline
        group_by:
          duration: 10min
          func: min
        extend_to: false
        color: white
        stroke_width: 1
        stroke_dash: 0
        float_precision: 1
        transform: return Number(x)*100;
      - entity: sensor.ladeempfehlung_forecast
        yaxis_id: links
        name: Batterie nutzen
        unit: Cent
        show:
          in_header: false
          in_chart: true
        type: line
        stroke_dash: 1
        curve: stepline
        extend_to: false
        color: red
        stroke_width: 1
        float_precision: 2
        data_generator: |
          const noon = new Date()
          noon.setHours(0, 0, 0, 7)
          const item = entity.attributes.forecast;
          const h = item[0].hour*1;
          const prices = entity.attributes.loadingUntil*100;
          const data = [];
          for(let i = h+1; i <= 48; i++) {
            data.push([noon.getTime() + i * 1000 * 3600, prices])
          }
          return data;    
      - entity: sensor.ladeempfehlung_maximalpreis
        yaxis_id: links
        name: Batterie nutzen (Historie)
        unit: Cent
        show:
          in_header: false
          in_chart: true
        type: line
        stroke_dash: 1
        curve: stepline
        extend_to: false
        group_by:
          duration: 10min
          func: min
        color: red
        stroke_width: 1
        float_precision: 4
        transform: |
          return Number(x)*100;
      - entity: sensor.ladeempfehlung_min_strompreis
        unit: Cent
        yaxis_id: links
        show:
          in_header: true
          name_in_header: true
          in_chart: false
        name: Min.
        color: var(--google-grey)
        transform: |
          return Number(x) * 100;
      - entity: sensor.ladeempfehlung_max_strompreis
        unit: Cent
        transform: |
          return Number(x) * 100;
        show:
          in_header: true
          name_in_header: true
          in_chart: false
        name: Max.
        color: rgb(66, 135, 245)
      - entity: sensor.ladeempfehlung_strompreis
        show:
          name_in_header: true
          in_chart: false
        opacity: 1
        extend_to: now
        curve: stepline
        stroke_width: 1
        float_precision: 2
        name: Aktueller Strompreis
        color: rgb(255, 166, 150)
        yaxis_id: strom
        transform: |
          return Number(x) * 100;    
        unit: Cent/kWh
      - entity: sensor.sunny_tripower_10_0_se_battery_power_charge_total
        show:
          in_header: raw
          name_in_header: true
          in_chart: true
        type: area
        unit: W
        curve: straight
        opacity: 0.2
        extend_to: now
        stroke_width: 1
        float_precision: 2
        name: Ladung
        color: darkorange
        group_by:
          func: avg
          duration: 10min
        yaxis_id: links2
      - entity: sensor.pv_ladeempfehlung
        unit: W
        show:
          in_header: true
          name_in_header: true
          in_chart: true
        type: area
        opacity: 0.3
        curve: stepline
        extend_to: now
        stroke_width: 2
        float_precision: 2
        name: Ladeempfehlung
        color: darkgreen
        yaxis_id: links2
        transform: |
          return Number(x)*1.00;
      - entity: sensor.nordpool_energiepreise
        unit: Cent
        yaxis_id: links
        show:
          in_header: false
          extremas: true
          name_in_header: false
          header_color_threshold: true
        name: Preis
        color_threshold:
          - value: 0
            color: lime
          - value: 15
            color: green
          - value: 20
            color: Khaki
          - value: 25
            color: Gold
          - value: 30
            color: darkorange
          - value: 35
            color: orangered
          - value: 40
            color: red
        type: line
        curve: stepline
        extend_to: false
        stroke_width: 1
        opacity: 0.85
        float_precision: 2
        data_generator: >
          const noon = new Date();  noon.setHours(0, 0, 0, 0);  const prices =
          entity.attributes.prices;  const data = [];  for(let i = 0; i <
          prices.length; i++) {
            data.push([noon.getTime() + i * 1000 * 3600, prices[i]*100]);
          }  data.push([noon.getTime() + prices.length * 1000 * 3600,
          prices[prices.length-1]*100]); return data;
      - entity: sensor.ladeempfehlung_forecast
        name: SoC Forecast
        yaxis_id: rechts2
        unit: "%"
        show:
          in_header: false
          in_legend: true
          in_brush: true
          in_chart: true
        type: area
        curve: straight
        extend_to: false
        color: magenta
        color_threshold:
          - value: 0
            color: black
          - value: 10
            color: magenta
        opacity: 0.1
        stroke_width: 1
        stroke_dash: 1
        float_precision: 1
        data_generator: |
          const noon = new Date();
          noon.setHours(0, 0, 0, 1);
          const item = entity.attributes.forecastSoC;
          const item2 = entity.attributes.forecast;
          const data = [];
          var h = item[0].hour*1;
          var v = 0;
          var v2 = 0;
          var vh = 0;
          for(let i = h; i < item.length+h; i++) {
            var nh = i+1;
            if (i >= h && i<item.length+h) {
              v = item[i-h].forecastSoC;
              if (v>100) v = 100;
              v2 = (item2[i-h].useBatteries == false && item2[i-h].chargeBatteries == false)*1;
              if ((item[i-h].forecastPower == 0) && (v>0) && (v2==0)) {
                vh = vh+(item2[i-h].PowerRequirement/138);
              }
            }
            data.push([noon.getTime() + nh * 1000 * 3600, v-vh]);
          }
          return data;
      - entity: sensor.ladeempfehlung_forecast
        name: W Forecast
        yaxis_id: links2
        unit: W
        show:
          in_header: false
          in_chart: true
          in_legend: true
        type: area
        curve: stepline
        extend_to: false
        color: lime
        color_threshold:
          - value: 0
            color: black
          - value: 500
            color: lime
        opacity: 0.1
        stroke_width: 1
        stroke_dash: 1
        float_precision: 1
        data_generator: |
          const noon = new Date();
          noon.setHours(0, 0, 0, 2);
          const item = entity.attributes.forecastSoC;
          const data = [];
          var h = item[0].hour*1;
          var v = 0;
          for(let i = h; i <= item.length+h; i++) {
            var nh = i;
            if (i >= h && i<item.length+h) {
              v = item[i-h].forecastPower;
            }
            data.push([noon.getTime() + nh * 1000 * 3600, v]);
          }
          return data;   
      - entity: sensor.solcast_pv_forecast_prognose_heute
        name: PV Prognose heute
        yaxis_id: links2
        unit: W
        show:
          in_header: false
          in_chart: true
          in_legend: true
        type: area
        curve: straight
        extend_to: false
        color: yellow
        color_threshold:
          - value: 0
            color: black
          - value: 500
            color: yellow
        opacity: 0.1
        stroke_width: 1
        stroke_dash: 1
        float_precision: 1
        data_generator: |
          const noon = new Date();
          noon.setHours(0, 0, 0, 3);
          const item = entity.attributes.detailedHourly;
          const data = [];
          var v = 0;
          for(let i = 0; i < item.length; i++) {
            var nh = i;
            v = item[i].pv_estimate*1000;
            data.push([noon.getTime() + nh * 1000 * 3600, v]);
          }
          return data;       
      - entity: sensor.solcast_pv_forecast_prognose_morgen
        name: PV Prognose morgen
        yaxis_id: links2
        unit: W
        show:
          in_header: false
          in_chart: true
          in_legend: true
        type: area
        curve: straight
        extend_to: false
        color: yellow
        color_threshold:
          - value: 0
            color: black
          - value: 500
            color: yellow
        opacity: 0.1
        stroke_width: 1
        stroke_dash: 1
        float_precision: 1
        data_generator: |
          const noon = new Date();
          noon.setHours(0, 0, 0, 4);
          const item = entity.attributes.detailedHourly;
          const data = [];
          var v = 0;
          for(let i = 0; i < item.length; i++) {
            var nh = i+24;
            v = item[i].pv_estimate*1000;
            data.push([noon.getTime() + nh * 1000 * 3600, v]);
          }
          return data;
      - entity: sensor.ladeempfehlung_forecast
        name: Laden
        yaxis_id: rechts2
        unit: "%"
        show:
          in_header: false
          in_chart: true
          in_legend: true
        type: area
        curve: straight
        extend_to: false
        color: cyan
        color_threshold:
          - value: 0
            color: black
          - value: 20
            color: cyan
        opacity: 0.2
        stroke_width: 1
        stroke_dash: 1
        float_precision: 1
        data_generator: |
          const noon = new Date();
          noon.setHours(0, 0, 0, 5);
          const item = entity.attributes.forecastSoC;
          const item2 = entity.attributes.forecast;
          const data = [];
          var h = item[0].hour*1;
          noon.setHours(h, 0, 0, 0);
          var v = 0;
          var v2 = 0;
          var v3 = 0;
          var vh = 0;
          for(let i = 0; i < item.length; i++) {
            var nh = i+1;
            if (i >= 0 && i<item.length) {
              v = item[i].forecastSoC;
              if (v>100) v = 100;
              v2 = (item2[i].useBatteries == false && item2[i].chargeBatteries == false)*1;
              if ((item[i].forecastPower == 0) && (v>0) && (v2==0)) {
                vh = vh+(item2[i].PowerRequirementWithoutPV/(138));
              }
              if (i >= 0 && i<item.length) {
                v3 = parseFloat(item2[i].CapPowerRequirement);
              }
            }
            v = v-vh+(v3/138);
            if (v>100) v = 100;
            data.push([noon.getTime() + nh * 1000 * 3600, v]);
          }
          return data;      
