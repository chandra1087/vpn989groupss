🔴Cara Buat Bot group Butler 🔴
Sebelum Memulai Clone this Repository , open file config lua insert your token bot ...
Superadmin replace your id & admin replace your second id .
Harus ada vps .
Combine dengan ovpn / ssh pun boleh !

# Tested on Ubuntu 14.04, 15.04 and 16.04, Debian 7, Linux Mint 17.2

$ sudo apt-get update
$ sudo apt-get upgrade
$ sudo apt-get install libreadline-dev libssl-dev lua5.2 liblua5.2-dev git make unzip redis-server curl libcurl4-gnutls-dev

# We are going now to install LuaRocks and the required Lua modules

$ wget http://luarocks.org/releases/luarocks-2.2.2.tar.gz
$ tar zxpf luarocks-2.2.2.tar.gz
$ cd luarocks-2.2.2
$ ./configure; sudo make bootstrap
$ sudo luarocks install luasec
$ sudo luarocks install luasocket
$ sudo luarocks install redis-lua
$ sudo luarocks install lua-term
$ sudo luarocks install serpent
$ sudo luarocks install dkjson
$ sudo luarocks install Lua-cURL
$ cd ..

# Clone the repository and give the launch script permissions to be executed
# If you want to clone the beta branch, use git clone with the [-b beta] option

$ git clone https://github.com/chandra1087/vpn989groupss.git
$ cd GroupButler
$ sudo chmod 777 launch.sh
```

Other things to check before running the bot:

**First of all, take a look at your bot settings:**

> • Make sure privacy is disabled (more info can be found by heading to the [official Bots FAQ page](https://core.telegram.org/bots/faq#what-messages-will-my-bot-get)). Send `/setprivacy` to [@BotFather](http://telegram.me/BotFather) to check the current status of this setting.

**Before you do anything else, open config.lua (in a text editor) and make the following changes:**

> • Set `bot_api_key` to the authentication token that you received from [`@BotFather`](http://telegram.me/BotFather).
>
> • Insert your numerical Telegram ID into the `superadmins` table. Other superadmins can be added too. It is important that you insert the numerical ID and NOT a string.
>
> • Set your `log.chat` (the ID of the chat where the bot will send all the bad requests received from Telegram) and your `log.admin` (the ID of the user that will receive execution errors).

Before you start the bot, you have to start the Redis process.
```bash
# Start Redis

$ sudo service redis-server start


## Starting the process

To start the bot, run `./launch.sh`. To stop the bot, press Control <kbd>CTRL</k
You may also start the bot with `lua bot.lua`, however it will not restart automatically.

* * *
## Something that you should known before run the bot

  * You can change some settings of the bot. All the settings are placed in `config.lua`, in the `bot_settings` table
    * `cache_time.adminlist`: the permanence in seconds of the adminlist in the cache. The bot caches the adminlist to avoid to hit Telegram limits
    * `notify_bug`: if `true`, the bot will send a message that notifies that a bug has occured to the current user, when a plugin is executed and an error happens
    * `log_api_errors`: if `true`, the bot will send in the `log_chat` (`config.lua`) all the relevant errors returned by an api request toward Telegram
    * `stream_commands`: if `true`, when an update triggers a plugin, the match will be printed on the console
  * There are some other useful fields that can be filled in `config.lua`
    * `db`: the selected Redis database (if you are running Redis with the default config, the available databases are 16). The database will be selected on each start/reload. Default: 2
  * Other things that may be useful
    * Administrators commands start for `$`. They are not documented, look at the triggers of `plugins/admin.lua` plugin for the whole list
    * If the main function of a plugin returns `true`, the bot will continue to try to match the message text with the missing triggers of the `plugins` table
    * You can send yourself a backup of the zipped bot folder with the `$backup` command
    * The Telegram Bot API has some undocumented "weird behaviors" that you may notice while using this bot
       * In supergroups, the `kickChatMember` method returns always a positive response if the `user_id` has been part of the group at least once, it doesn't matter if the user is not in the group when you use this method
       * In supergroups, the `unbanChatMember` method returns always a positive response if the `user_id` has been part of the group at least once, it doesn't matter if the user is not in the group or is not in the group blacklist


## Some notes about the database
