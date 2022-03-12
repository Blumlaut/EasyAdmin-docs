# Installing EasyAdmin

Install it like any other Resource.

Simply Drag&Drop your `EasyAdmin` folder into the `resources` folder of your Server.

## Getting Started

To get started with EasyAdmin, simply copypaste this template into your `server.cfg` file.

```
ensure EasyAdmin


add_ace group.admin easyadmin allow
```

The Menu key is no longer defined using a convar, see [Keybind](keybind.md).

More Configuration options can be found [here](config.md).


## Adding an Admin


=== "Manually"

	You can use this template to fill out your desired Values

	```
	add_principal identifier.IDENTIFIERNAME:IDENTIFIER group.admin
	```


	You can use any Identifier available in FiveM for this, however, in this example we will describe how to use your Steam ID.




	After installing EasyAdmin, start EasyAdmin and join your Server, once you are connected enter `ea_printIdentifiers 1` in your Server Console, 1 represents your ingame ID, so make sure you use the correct id, EasyAdmin will then print a list of your identifiers:
	![grafik](https://user-images.githubusercontent.com/13604413/139588546-a64da751-7f1c-41ae-8abd-f6c7e7b0735e.png)

	we can now simply fill out the value described above, it will look like this:

	```
	add_principal identifier.steam:1100001018c7433 group.admin
	```

	> To use Steam IDs as an identifier, a Steam WebAPIKey needs to be set up. Follow this [guide](steamapikey.md) to create one.

	You can also use other identifiers, as EasyAdmin is not specifically limited to SteamIDs, all available identifiers can be used, such as `discord`, `xbl` or `license`, to name a few examples.

=== "ZAP-Hosting"

    > Note: This **only** works for ZAP-Hosting's FiveM Windows or Linux Server see the "Manually" Tab for txAdmin
    
    Enter your Steam ID (64, not Hex) in the Settings Page under Admins, add a new line for each SteamId.

=== "Discord ACE Permissions"

	EasyAdmin ships with a Discord Permission implementation by default, to use this, the [Discord Bot](discordbot.md) has to be configured.

	Once the bot has been configured, follow [this guide](https://easyadmin.readthedocs.io/en/6.6/discordbot/#discord-ace-permissions) to set it up.