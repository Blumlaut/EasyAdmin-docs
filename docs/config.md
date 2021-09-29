# Configuring EasyAdmin

Configuration of EasyAdmin is done via convars, these can be set via your server config file or by typing it as a command inside your servers' console ( this method may not always work with EasyAdmin and the settings will reset after the server has been restarted. )


```
setr ea_LanguageName "en"                # set our language to english
setr ea_MenuButton "F2"			# set our menu button to F2. default: "289"
setr ea_alwaysShowButtons "false"	# we don't want to see buttons we can't even access, do we? default: "false"
set ea_moderationNotification "false"   # this can be either "false" or a discord webhook address, this will send a discord message if an admin takes actions against a player  ( such as banning and kicking )
set ea_custombanlist "false"            # read docs for this, dont touch it
set ea_enableCallAdminCommand "true"
set ea_enableReportCommand "true"
```




## Basic Configuration

|       Command/Convar        |  Type   |                                   Usage                                    |                                                                                                                Description                                                                                                                 |
|-----------------------------|---------|----------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ea_LanguageName             | Convar  | `setr ea_LanguageName "en"`                                                | This Convars dictates in which language EasyAdmin is displayed ( this includes but is not limited to GUI, Kick Messages, Reasons, Hud Elements.. ) Available options: cs, de, en, es, fr, it, nl, pl, pt, sv                                                  |
| ea_MenuButton               | Convar  | FiveM: `setr ea_MenuButton "F2"` RedM: `setr ea_MenuButton "PhotoModePc"` | Key which is used to open the Menu, [FiveM Keys](https://docs.fivem.net/docs/game-references/input-mapper-parameter-ids/keyboard/), [RedM Keys](https://github.com/Blumlaut/EasyAdmin/blob/master/dependencies/Controls.lua#L3)                                            |
| ea_minIdentifierMatches     | Convar  | `set ea_minIdentifierMatches 2`                                            | The Minimum Amount of Identifiers that have to match before a Player gets "Declined" for being banned. Never put this below 1. If some form of Proxy is used on the server, you should add 1 to this number for every Proxy IP                                                                                                            |

## Webhook & Screenshot Configuration

|       Command/Convar        |  Type   |                                   Usage                                    |                                                                                                                Description                                                                                                                 |
|-----------------------------|---------|----------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ea_moderationNotification   | Convar  | `set ea_moderationNotification "https://discordapp/api/webhooks/123/456"`  | Logs Actions via Discord Webhook                                                                                                                                                                                                           
| ea_reportNotification | Convar  | `set ea_reportNotification "https://discordapp/api/webhooks/123/456"`  | Sends Report Notifications to a Seperate Webhook, will use ea_moderationNotification if unset.
| ea_detailNotification   | Convar  | `set ea_detailNotification "https://discordapp/api/webhooks/123/456"`  | Sends Detail Notifications (Convar Changes, Freeze and Spectate) to a seperate Webhook, will use ea_moderationNotification if unset.
| ea_excludeWebhookFeature    | Command | `ea_excludeWebhookFeature freeze teleport`                                 | Allows Specific Webhook Alerts to be disabled, available options: `kick ban slap warn teleport freeze spectate settings calladmin report reports screenshot permissions`                                                                                                                        |
| ea_dateFormat				  | Convar  | `setr ea_dateFormat "%d/%m/%Y %H:%M:%S"`									 | Allows a custom DateTime format to be displayed in EasyAdmin, available options: https://www.lua.org/pil/22.1.html																														  |
| ea_screenshoturl            | Convar  | `setr ea_screenshoturl "https://wew.wtf/upload.php"`                       | Defines an Image Uploader for the created Screenshots, make sure `ea_screenshotfield` is also configured correctly.                                                                                                                        |
| ea_screenshotfield          | Convar  | `setr ea_screenshotfield "files[]"`                                        | Defines the name for the form field to add the file to. See [screenshot-basic](https://github.com/citizenfx/screenshot-basic/blob/master/README.md) for further information.                                                               |
| ea_screenshotOptions        | Convar  | `setr ea_screenshotOptions "{}"`                                           | Defines any arguments that should be passed through to screenshot-basic as a JSON String. See [screenshot-basic](https://github.com/citizenfx/screenshot-basic/blob/master/README.md) for further information.                             |
| ea_enableReportScreenshots  | Convar  | `set ea_enableReportScreenshots "true"`									 | When a player is Reported, this Convar will cause a screenshot to be taken of the reported player's game, if screenshot-basic is set up																									  |
| ea_logIdentifier			  | Convar  | `set ea_logIdentifier "steam"`											 | Shows the specified identifier in Webhook Messages next to the player name

## Command Configuration

|       Command/Convar        |  Type   |                                   Usage                                    |                                                                                                                Description                                                                                                                 |
|-----------------------------|---------|----------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ea_enableCallAdminCommand   | Convar  | `set ea_enableCallAdminCommand "true"`                                     | Enables "calladmin" command, will print a message via webhook.                                                                                                                                                                             |
| ea_enableReportCommand      | Convar  | `set ea_enableReportCommand "true"`                                        | Enables "report" command                                                                                                                                                                                                                   |
| ea_callAdminCommandName     | Convar  | `set ea_callAdminCommandName "calladmin"`									 | Defines what the command to call an admin will be
| ea_reportCommandName     | Convar  | `set ea_reportCommandName "report"`									 		 | Defines what the command to report a player will be
| ea_callAdminCooldown        | Convar  | `set ea_callAdminCooldown 60`                                              | In Seconds, how long a Player will not be able to use callAdmin after using it once.                                                                                                                                                       |
| ea_defaultMinReports        | Convar  | `set ea_defaultMinReports 3`                                               | Minimum Reports to Ban someone below ea_MinReportPlayers Threshold, if ea_MinReportModifierEnabled, this is the amount always needed for a player to be banned.                                                                            |
| ea_ReportBanTime            | Convar  | `set ea_ReportBanTime 86400`                                               | Ban Time in unix time, how long the temporary ban should last after getting reported by x users                                                                                                                                            |
| ea_MinReportModifierEnabled | Convar  | `set ea_MinReportModifierEnabled "true"`                                   | Allows "Variable" Minimum Report Count, Will Divide Current Player Count by ea_MinReportModifier.                                                                                                                                          |
| ea_MinReportPlayers         | Convar  | `set ea_MinReportPlayers 12`                                               | Minimum Amount of Players for the "Report Modifier" to enable, would not recommend setting below this number.                                                                                                                              |
| ea_MinReportModifier        | Convar  | `set ea_MinReportModifier 4`                                               | Amount by which Player Count gets divided to get "minimum reports needed" count, so if 12 Players are on the server and this value is 4, 12/4= 3 Reports                                                                                   |

## Administration Configuration

|       Command/Convar        |  Type   |                                   Usage                                    |                                                                                                                Description                                                                                                                 |
|-----------------------------|---------|----------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ea_maxWarnings              | Convar  | `set ea_maxWarnings 3`                                                     | Defines how many times a player can get warned before actions are taken Automatically.                                                                                                                                                     |
| ea_warnAction               | Convar  | `set ea_warnAction "kick"`                                                 | Defines how the player will get acted upon, if maximum warnings are reached, can be `kick` or `ban`                                                                                                                                        |
| ea_warningBanTime           | Convar  | `set ea_warningBanTime 604800`                                             | How long a player will stay banned after being warned and banned, accepts a unix time string.                                                                                                                                              |
| ea_IpPrivacy				  | Convar	| `setr ea_IpPrivacy "true"`												 | Weither or not to Hide IP Identifiers in the GUI, won't prevent them being used for Bans.

## Backup Configuration


|       Command/Convar        |  Type   |                                   Usage                                    |                                                                                                                Description                                                                                                                 |
|-----------------------------|---------|----------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ea_backupFrequency          | Convar  | `set ea_backupFrequency 24`                                     | time (in hours) between Banlist Backups.                                                                                                                                                                                                   |
| ea_maxBackupCount           | Convar  | `set ea_maxBackupCount 10`                                                 | the maximum amount of backups that can be created. Old backups will be deleted.                                                                                                                                                            |


## Other Features

|       Command/Convar        |  Type   |                                   Usage                                    |                                                                                                                Description                                                                                                                 |
|-----------------------------|---------|----------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ea_chatReminderTime         | Convar  | `set ea_chatReminderTime 0`                                                | Time ( in minutes ) of how often there should be a random Chat Reminder printed to Chat, disabled if 0.                                                                                                                                    |
| ea_addReminder              | Command | `ea_addReminder "Online Admins: ^3@admins^7"`                              | **Make sure to add this parameter BELOW the EasyAdmin start line, otherwise it won't work** Adds a Reminder Text to the pool of available options, can support infinite reminders, [More detailed informations](reminders.md)                                           |
| ea_playerCacheExpiryTime    | Convar  | `set ea_playerCacheExpiryTime 900`                                         | Defines, in seconds, how long it takes for a Cached Player to get removed from Cache, 30 Minutes by Default, however, higher Values are recommended for sparsely Moderated Servers, should not exceed a few hours for performance reasons. |
| ea_addShortcut    		  | Command | `ea_addShortcut rdm RDMing is not allowed, please read our Rules! (/rules)`| Creates a shortcut which can be used to use an abreviated reason text, for example typing `rdm` instead of having to type out an entire reason. |


## Advanced Configuration

|       Command/Convar        |  Type   |                                   Usage                                    |                                                                                                                Description                                                                                                                 |
|-----------------------------|---------|----------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ea_enableDebugging          | Convar  | `setr ea_enableDebugging "true"`                                           | **DEPRECATED, USE `ea_logLevel` INSTEAD!**
| ea_logLevel				  | Convar 	| `setr ea_logLevel 3`														 | Sets the level of debug messages that should be displayed, 1-4 (1=errors only, 2=errors&warnings only, 3=errors, warnings and info messages, 4=everything, including spammy developer prints, not recommended)
| ea_custombanlist            | Convar  | `set ea_custombanlist "true"`                                              | Enables custom Banlist systems, currently unsupported.                                                                                                        |
| ea_enableTelemetry          | Convar  | `set ea_enableTelemetry "true"`                                            | Enable or Disable Telemetry                                                                                                                                                                                                                |
| ea_useTokenIdentifiers      | Convar  | `set ea_useTokenIdentifiers "true"`                                        | Weither or not to use Tokens as Identifiers when banning users, keep activated unless multiple server instances access the same banlist file.                                                                                              |
| ea_enableSplash			  | Convar  | `set ea_enableSplash "false"`												 | Enables or Disables the Ascii Art when EasyAdmin Starts.	