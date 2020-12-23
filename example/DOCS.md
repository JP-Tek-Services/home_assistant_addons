# Home Assistant Community Add-on: example
[![Support JP-Tek-Services on Patreon][patreon-shield]][patreon]


## About



## Requirements



## Installation

The installation of this add-on is pretty straightforward and not different in
comparison to installing any other Home Assistant add-on.

1. Add [JPTS Community Home Assistant Addons](https://github.com/JP-Tek-Services/home_assistant_addons) repo to your Home Assisat Addon Store.
1. Search for the "example" add-on in the Supervisor add-on store and install it.
1. Plug in USB RTL-SDR to Home Assistant host.
1. Configure paramater like example below.
1. Start the "example" add-on.
1. Check the logs of the "example" to see if everything went well.
1. Ready to go!

## Varables
| Varable | Description | Required | Default |
| ----------- | ----------- | ----------- | ----------- |




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

```

## Sensor config
**Note**: _Add this to your config.yaml as is._
```yaml
```

## Automation Example
**Note**: _Triggers an alert message readout to the alexa media group "everywhere" anytime OWR sends an alert_
```yaml
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

[contributors]: https://github.com/jpeterson37/addon-example/graphs/contributors
[discord-ha]: https://discord.gg/c5DvZ4e
[discord]: https://discord.gg/EXjEee3dnw
[jpeterson]: https://github.com/Jpeterson37
[issue]: https://github.com/JP-Tek-Services/addon-example/issues
[releases]: https://github.com/JP-Tek-Services/addon-example/releases
[maintenance-shield]: https://img.shields.io/maintenance/yes/2020.svg
[patreon-shield]: https://jpeterson37.github.io/patreon/patreon.png
[patreon]: https://www.patreon.com/jptekservices