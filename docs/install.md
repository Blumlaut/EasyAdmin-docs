# Installing EasyAdmin

Install it like any other Resource.

Simply Drag&Drop your `EasyAdmin` folder into the `resources` folder of your Server.

## Configuration

To get started with EasyAdmin, simply copypaste this template into your `server.cfg` file.

You can adjust the Language and MenuButton here.

```
ensure EasyAdmin

setr ea_LanguageName "en"                # set our language to english
setr ea_defaultKey "F2"		 # set our menu button to F2, this is a one-time setting!

add_ace group.admin easyadmin allow
```

## Adding yourself as an Admin

### ZAP Hosting (non-txAdmin)
Enter your Steam ID in the Settings Page under Admins, add a new line for each SteamId.

### ZAP Hosting (txAdmin)

See the [DIY Section](https://easyadmin.readthedocs.io/en/latest/install/#do-it-yourself-self-hosted-txadmin)

### Do it Yourself (self-hosted, txAdmin)

You can use this template to fill out your desired Values

```
add_principal identifier.IDENTIFIERNAME:IDENTIFIER group.admin
```


You can use any Identifier available in FiveM for this, however, in this example we will describe how to use your Steam ID.

```
add_principal identifier.steam:1100001000056ba group.admin
```


You can get your `HexID` from [vacbanned.com](http://www.vacbanned.com/) by typing in your steam URL.

To use Steam IDs as an identifier, a Steam WebAPIKey needs to be set up. Follow this [guide](steamapikey.md) to create one.

You can also use other identifiers, as EasyAdmin is not specifically limited to SteamIDs, all available identifiers can be used, such as `discord`, `xbl` or `license`, to name a few examples.

