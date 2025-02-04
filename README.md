# Energy-Charging
Energy Charging Recommendation Template for Home Assistant

# Idea / Why this macro

After switching to an exchange-based electricity provider, I wanted to be able to cover my electricity needs with cheap electricity even during the expensive hours. The solution here was to use the PV system's electricity storage unit. This means that when the electricity price is cheap, the forecast for the solar yield is low and the efficiency of the system allows it, electricity from the grid should be charged into the house battery.

There are many parameters:
1. own electricity consumption/hour
2. predicted amount of solar power/hour
3. electricity price/hour
4. efficiency of the inverter+battery

## How to install

You need to have Home Assistant 2023.11 or higher installed to use this custom template.

For a install you can copy the contents of  `energy_charging.jinja`  to a jinja file in your  `custom_templates`  folder. Run the  `homeassistant.reload_custom_templates`  service call to load the file.

**Done**

## Configuration
