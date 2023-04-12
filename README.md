# WORK IN PROGRESS

# home-assistant_OctopusAgile
Octopus Agile custom component for Home Assistant.


## The Origonal Source by markgdev is no longer maintained,
This is my modified version as I'm only interested in retreiving the Import and Export Rates.

## Installation
Clone this repo and copy custom_components/OctopusAgile to <homeassistant config>/custom_components/OctopusAgile

## Configuration
NOTE: the GUI configuration flow is currently not implemented, I will try and fix this.

See the example configuration.yaml config below

### region_code
This should match the [DNO region code](https://www.energy-stats.uk/dno-region-codes-explained/) as per the Octopus Agile API - look for "E-1R-AGILE-18-02-21-" on your [API dashboard](https://octopus.energy/dashboard/developer/) and the next letter is your region code.

### mpan, serial, and auth
Your MPAN and serial number are listed on your [API dashboard page](https://octopus.energy/dashboard/developer/). "*auth*" is your API key from the same page.

### agilerate
As of July 2022 there are now 3 Agile Tariffs :
  * AGILE-18-02-21 - The unit rate is capped at 35p/kWh (including VAT)
  * AGILE-22-07-22 - The unit rate is capped at 55p/kWh (including VAT)
  * AGILE-22-08-31 - The unit rate is capped at 78p/kWh (including VAT)

default if not set is AGILE-18-02-21


```yaml

octopusagile:
  region_code: "L"
  mpan: 00000000
  serial: 00000000
  auth: abc00000000
  startdate: "2020-05-08"
  
sensor:
- platform: "octopusagile"

```

## Entities
### octopusagile.rates
All future rates stored in entity attributes

### octopusagile.avg_rate_exc_peak
The average rate from the day update_timers runs at 23:00 to 22:30 the next day, excluding the 16:00 to 18:30 time periods where the peak rate is applied.

### octopusagile.avg_rate_inc_peak
The average rate from the day update_timers runs at 23:00 to 22:30 the next day, including the peak.

### octopusagile.region_code
Region code as set in configuration

### octopusagile.half_hour_timer_nextupdate
When the half hour timer will next run

### octopusagile.half_hour_timer_lastupdate
When the half hour timer last run

### octopusagile.update_timers_nextupdate
When the update timers timer will next run

### octopusagile.update_timers_lastupdate
When the update timers timer last run

## Example usage
### Rates card
[See here](https://github.com/markgdev/home-assistant_OctopusAgile/tree/master/custom_cards)
![Image of Card](https://raw.githubusercontent.com/markgdev/home-assistant_OctopusAgile/master/custom_cards/agile-rates-card-screenshot.png)

## Development

This repo uses `pipenv` to manage Python versions and dependencies. To get up and running:

* Install [pipenv](https://pipenv.pypa.io/en/latest/install/#installing-pipenv) if you don't already have it.
* Run `pipenv install` to install any required packages and create the right python environment.
