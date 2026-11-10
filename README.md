[![hacs_badge](https://img.shields.io/badge/HACS-Default-41BDF5.svg?style=for-the-badge)](https://github.com/hacs/integration)
[![](https://img.shields.io/github/license/mickecamino/nibe_energy_conversion?style=for-the-badge)](LICENSE)
[![](https://img.shields.io/badge/COMMUNITY-FORUM-success?style=for-the-badge)](https://community.home-assistant.io)

# A FORK of NIBE Energy Conversion (nibe_energy_conversion)
# This is my fork of the above repository - all cooling sensors removed
This software REQUIRES that you have installed [Nibe Heat Pump](https://www.home-assistant.io/integrations/nibe_heatpump/)

Nibe S735 does not have cooling feature. And that made it impossible to install this software. So I forked it and removed all instances used for cooling.

## Tested on a Nibe S735
Custom Home Assistant integration that converts NIBE “past hour” energy sensors (kWh) into cumulative totals and COP metrics.

## Features
- UI configuration for 6 input sensors (past-hour kWh)
- UI options for update schedule (minute past hour) and run-on-start
- 6 cumulative energy totals (total_increasing)
- 2 cumulative sums (produced/used)
- 3 COP sensors for last hour (total, hot water, heating)
- No helper entities; state stored internally

## Installation
### HACS
1) In Home Assistant, open HACS → Integrations.
2) Open the menu in the top right corner and choose Custom repositories.
3) Add `https://github.com/mickecamino/nibe_energy_conversion` as category `Integration`.
4) Find `NIBE Energy Conversion` in HACS and install it.
5) Restart Home Assistant.
6) Add the integration in Settings → Devices & Services → Add Integration.

### Manual
1) Copy `custom_components/nibe_energy_conversion` into your Home Assistant config directory under `custom_components/`.
2) Restart Home Assistant.
3) Add integration: Settings → Devices & Services → Add Integration → “NIBE Energy Conversion”.

## Configuration
### Inputs (GUI)
Select these 6 “past hour” sensors:
#### Produced:
* sensor.energy_log_energy_produced_for_heat_during_past_hour_32284
* sensor.energy_log_energy_produced_for_hot_water_during_past_hour_32286
#### Used:
* sensor.energy_log_energy_used_for_heat_during_past_hour_32292
* sensor.energy_log_energy_used_for_hot_water_during_past_hour_32294
#### Auxiliary used:
* sensor.energy_log_energy_used_by_additional_heater_for_heat_during_past_hour_32300
* sensor.energy_log_energy_used_by_additional_heater_for_hot_water_during_past_hour_32302

### Options (GUI)
- `update_minute`: minute past the hour to process the last hour (default 15)
- `run_on_start`: run once on HA start (only if the minute has passed)

## Outputs
### Energy totals (kWh, total_increasing)
- Produced heating/hot water
- Used heating/hot water
- Auxiliary used heating/hot water

### Sums (kWh, total_increasing)
- Produced total
- Used total

### COP (last hour)
- COP total
- COP hot water
- COP heating

## Notes
- Aggregation runs only at the scheduled time (and optionally at start).
- Double-count protection uses the hour-end timestamp internally.
- COP is computed from the same last-hour inputs and updated on schedule.


## Changelog
[2026-11-09]  
Removed all instances of cooling, does not work with Nibe S735

### v1.0.5
