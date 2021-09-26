# Telegram Bot Shell Script

This is a telegram bot implemented in ([Bourne](https://en.wikipedia.org/wiki/Bourne_shell))
shell script. It runs on OpenWRT and/or a Linux server/desktop.

You can implement your own commands by adding a simple shell script in the
`/usr/lib/telegram/commands` directory. The script should be executable.
The second line of the script is the command description which is used for
the response to the `/help` command.


## Installing

**First create a Telegram bot** as described here:
[Bots FAQ](https://core.telegram.org/bots/faq#how-do-i-create-a-bot).

Your bot is created with the `BotFather` which is itself a bot.
The command `/newbot` first asks for a descriptive name for your bot,
and then it asks for a username for that same bot (rather confusing).

It can be really, really difficult to come up with a username for the bot
which isn't dismissed with:
*`Sorry, this username is already taken. Please try something different`*
But be patient, eventually you will be able to come up with a name.
Note down the bot API token you get from `BotFather`

Then get your own ID from `IDBot` with the `/getid` command.

### Installing on OpenWRT

**Create a configuration file**

For OpenWRT, create a file `/etc/config/telegram` with the following
contents.
```
config global 'global'
  option token '1078673890:ABYw1q-eGwefIAoP--Ewc-1as5WNgG0-asd'
  option chat_id '8603212134'
```

where the value of the `token` should be replaced by the one you obtained
from the Telegram BotFather

**Copy files to your router**

```
$ cd telegram-bot
$ rsync -av usr etc root@192.168.1.2:/
```
(replace the IP address of your router)

**Launch the bot**

TODO: update this
```
/usr/lib/telegram/bot
```

### Installing on Linux (not tested)

Create a file `~/.telegram-bot.conf`  with the following contents:
```
token="1078673890:ABYw1q-eGwefIAoP--Ewc-1as5WNgG0-asd"
chat_id="8603212134"
```

```
$ cd telegram-bot
$ sudo rsync -av usr /
```


## Similar projects

  * [ixiumu/openwrt-telegram-bot: Telegram bot for router with firmware Lede/Openwrt.](https://github.com/ixiumu/openwrt-telegram-bot)
  * [alexwbaule/telegramopenwrt: Telegram Scripts for OpenWrt/Lede Project](https://github.com/alexwbaule/telegramopenwrt)

## Resources

  * [Telegram Bot API](https://core.telegram.org/bots/api)
  * **Creating Packages for OpenWRT**
    * [Hotplug](https://openwrt.org/docs/guide-user/base-system/hotplug)
    * [Using the SDK](https://openwrt.org/docs/guide-developer/toolchain/using_the_sdk)
    * [Build system usage](https://openwrt.org/docs/guide-developer/toolchain/use-buildsystem) describes how to insert your own (local) package feed into `feeds.conf.default` using `src-link` (path must be absolute)
    * [OpenWrt packages](https://openwrt.org/docs/guide-developer/package-policies)
    * [Creating packages](https://openwrt.org/docs/guide-developer/packages)
    * ["Hello, world!" for OpenWrt](https://openwrt.org/docs/guide-developer/helloworld/start)
    * [procd init script parameters](https://openwrt.org/docs/guide-developer/procd-init-scripts)
    * [Create a sample procd init script](https://openwrt.org/docs/guide-developer/procd-init-script-example)
  * **Luci Documentation and Examples**
    * [openwrt/luci Wiki](https://github.com/openwrt/luci/wiki/Documentation)
    * [Weimarnetz - Howto write new LuCI apps](https://weimarnetz.de/blog/artikel/howto-write-new-luci-apps)
      * [packages/utils/luci-app-example at brauhaus-19.07 · weimarnetz/packages](https://github.com/weimarnetz/packages/tree/brauhaus-19.07/utils/luci-app-example)
  * **Pushover**
    * [Pushover: API](https://pushover.net/api)

## Building An Installable OpenWRT IPK Package

TODO


## TODO

Make this into a general OpenWRT notification framework/package supporting:

  * [Pushover](https://pushover.net)
  * [Gotify](https://gotify.net)
  * SMTP
