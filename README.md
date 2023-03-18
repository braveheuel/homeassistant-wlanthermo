# WLANThermo for Home Assistant

The WLANThermo bbq thermometer (https://wlanthermo.de/) uses a local wifi and optional MQTT server to push the temperature changes to.

## Setup MQTT in WLANThermo
Link your WLANThermo to the same MQTT server which Home Assistant is using. You can do this easily on the provided web interface.


## Home Assistant Configuration
There are three different packages available:

* wlanthermo: Integrates sensors and settings into Home-Assistant
* wlanthermo_push_notify: Adds automations to notify a service upon reaching max/min limits of a channel. Please adapt `wlanthermo_push_notify/wlanthermo_automation.yaml` and replace the called service: `service: notify.mobile_app_sm_g970f`
* wlanthermo_timer: Adds sensors, notifications and settings for estimating time left to reach set target temperature of a channel

The packages can be added within the Home-Assistant `configuration.yaml`:

```
homeassistant:
  # Include packages
  packages:
    wlanthermo: !include_dir_merge_named wlanthermo
    wlanthermo_push_notify: !include_dir_merge_named wlanthermo_push_notify
    wlanthermo_timer: !include_dir_merge_named wlanthermo_timer
```

In `wlanthermo/wlanthermo_mqtt.yaml` and `wlanthermo/wlanthermo_template.yaml` adapt the MQTT topic of your WLANThermo: `state_topic: "WLanThermo/MINIV3/status/data"`, `state_topic: "WLanThermo/MINIV3/status/settings"` and `topic: WLanThermo/MINIV3/set/channels`. Change `WLanThermo/MINIV3` to match your main topic and device name.


## Home Assistant Lovelace

`wlanthermo_lovelace.yaml` contains an example how to integrate all three packages into the Home-Assistant frontend:

![WLANThermo in Home-Assitant](Screenshot_20220206_143819.png?raw=true "WLANThermo in Home-Assitant")


The lovelace example depends on a couple of custom components:

* https://github.com/thomasloven/lovelace-layout-card
* https://github.com/thomasloven/lovelace-badge-card
* https://github.com/iantrich/config-template-card
* https://github.com/RomRider/apexcharts-card
* https://github.com/ofekashery/vertical-stack-in-card
