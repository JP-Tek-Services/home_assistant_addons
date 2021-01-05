# Home Assistant Community Add-on: Open Wather Radio
[![Release][owr-release-shield]][owr-release] ![Project Stage][project-stage-shield] [![License][license-shield]](LICENSE.md)
![Supports aarch64 Architecture][aarch64-shield]
![Supports amd64 Architecture][amd64-shield]
![Supports armhf Architecture][armhf-shield]
![Supports armv7 Architecture][armv7-shield]
![Supports i386 Architecture][i386-shield]
![Project Maintenance][maintenance-shield]


[![Support JP-Tek-Services on Patreon][patreon-shield]][patreon]


## About
Open Weather Radio is a docker container the leverages [RTL-SDR](https://amzn.to/3au9W0J) to listen for SAME messages sent via [NWR stations](https://www.weather.gov/nwr/station_listing) and send the decoded alerts via STDOUT and/or MQTT(if a broker is provided). An http OGG stream is also provided on http://hostip:1050 and can be used with [Home Assastant Media Extractor](https://www.home-assistant.io/integrations/media_extractor/)


## Requirements
* [RTL-SDR](https://amzn.to/3au9W0J)
* Docker
* MQTT Broker for sensor


## Installation

The installation of this add-on is pretty straightforward and not different in
comparison to installing any other Home Assistant add-on.

1. Add [JPTS Community Home Assistant Addons](https://github.com/JP-Tek-Services/home_assistant_addons) repo to your Home Assisat Addon Store.
1. Search for the "Open Weather Radio" add-on in the Supervisor add-on store and install it.
1. Plug in USB RTL-SDR to Home Assistant host.
1. Configure paramater like example below.
1. Start the "Open Weather Radio" add-on.
1. Check the logs of the "Open Weather Radio" to see if everything went well.
1. Ready to go!

## Varables
| Varable | Description | Required | Default |
| ----------- | ----------- | ----------- | ----------- |
| freq | Frequency for [NWR stations](https://www.weather.gov/nwr/station_listing) | yes | 162.550M |
| ppm | ppm error | no | 0 |
| gain | Tuner gain | no | 40 |
| same | SAME code to use | no | |
| dsamelog | Set log level (int 10,20,30,40,50) | no | |
| mqttsvr | MQTT Broker server address | no | |
| mqttport | MQTT Broker Port | no | 1883 |
| mqttusr | MQTT Broker Username | no | |
| mqttpwd | MQTT Broker Password | no | |
| test | If true, will trigger a static EASE decode after 10 seconds. Good for testing MQTT and Automation. | no | false | 



### Option: `log_level`

The `log_level` option controls the level of log output by the addon and can
be changed to be more or less verbose, which might be useful when you are
dealing with an unknown issue. Possible values are:

- `trace`: Show every detail, like all called internal functions.
- `debug`: Shows detailed debug information.
- `info`: Normal (usually) interesting events.
- `warning`: Exceptional occurrences that are not errors.
- `error`:  Runtime errors that do not require immediate action.
- `fatal`: Something went terribly wrong. Add-on becomes unusable.

Please note that each level automatically includes log messages from a
more severe level, e.g., `debug` also shows `info` messages. By default,
the `log_level` is set to `info`, which is the recommended setting unless
you are troubleshooting.



## Configuration

**Note**: _Remember to restart the add-on when the configuration is changed._

**Note**: _This is just an example, don't copy and paste it! Create your own!_

Example add-on configuration, with all available options:

```yaml
freq: "162.550M"
ppm: 0
gain: 40
same: "029165 029161 02916"
dsamelog: 1
mqttsvr: 127.0.0.1
mqttport: 1883
mqttusr: username
mqttpwd: password
log_level: info
test: (true/false)
```

## Sensor config
**Note**: _Add this to your config.yaml as is._
```yaml
sensor:
  - platform: mqtt
    name: "Open Weather Radio"
    icon: mdi:weather-cloudy-alert
    state_topic: "open_weather_radio/alerts"
    value_template: "{{ value_json.alert }}"
    availability_topic: "open_weather_radio/status"
    payload_available: "online"
    payload_not_available: "offline"
    expire_after: 300
    json_attributes_topic: "open_weather_radio/alerts"
    json_attributes_template: "{{ value_json.attr | tojson }}"
```

## Automation Example
**Note**: _Triggers an alert message readout to the alexa media and mobile device anytime OWR sends an alert_
**Note**: _Change "notify.alexa_media_{mediaplayer}", "media_player.{mediaplayer}" and "notify.mobile_app_{phone}"_
```yaml
alias: 'Open Weather Radio: Send Alert'
description: >-
  Send alert to Alexa and mobile whenever sensor.open_weather_radio is updated
  excluding online messages.
trigger:
  - platform: state
    entity_id: sensor.open_weather_radio
condition:
  - condition: not
    conditions:
      - condition: state
        entity_id: sensor.open_weather_radio
        state: online
action:
  - data_template:
      data:
        method: all
        type: announce
      message: '{{ state_attr("sensor.open_weather_radio", "message").split(".")[0] }}'
      target:
        - #media_player.{mediaplayer}
      title: Open Weather Radio
    service: #notify.alexa_media_{mediaplayer}
  - data:
      title: Open Weather Radio
      message: '{{ state_attr("sensor.open_weather_radio", "message").split(".")[0] }}'
      data:
        icon_url: 'https://jpeterson37.github.io/logos/owr.png'
        tag: Open_Weather_Radio
    service: #notify.mobile_app_{phone}
mode: single
max: 2
```


## Support

Got questions?

You have several options to get them answered:

- The [JP Tek Services Home Assistant Community Add-on][discord] for add-on
  support and feature requests.
- The [Home Assistant Discord chat server][discord-ha] for general Home
  Assistant discussions and questions.

You could also [open an issue here][issue] GitHub.



## Authors & contributors

The original setup of this repository is by [Joshua Peterson][jpeterson].

For a full list of all authors and contributors,
check [the contributor's page][contributors].



## License

MIT License

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

[contributors]: https://github.com/jpeterson37/addon-agentdvr/graphs/contributors
[discord-ha]: https://discord.gg/c5DvZ4e
[discord]: https://discord.gg/EXjEee3dnw
[jpeterson]: https://github.com/Jpeterson37
[issue]: https://github.com/JP-Tek-Services/addon-open-weather-radio/issues
[releases]: https://github.com/JP-Tek-Services/addon-open-weather-radio/releases
[maintenance-shield]: https://img.shields.io/maintenance/yes/2020.svg
[patreon-shield]: https://jpeterson37.github.io/patreon/patreon.png
[patreon]: https://www.patreon.com/jptekservices
[owr-release-shield]: https://img.shields.io/badge/version-v0.0.5-blue.svg
[owr-release]: https://github.com/JP-Tek-Services/addon-open-weather-radio/
[amd64-shield]: https://img.shields.io/badge/amd64-yes-green.svg
[i386-shield]: https://img.shields.io/badge/i386-yes-green.svg
[aarch64-shield]: https://img.shields.io/badge/aarch64-yes-green.svg
[armhf-shield]: https://img.shields.io/badge/armhf-no-red.svg
[armv7-shield]: https://img.shields.io/badge/armv7-yes-green.svg
[project-stage-shield]: https://img.shields.io/badge/project%20stage-experimental-yellow.svg
[license-shield]: https://img.shields.io/github/license/JP-Tek-Services/addon-open-weather-radio