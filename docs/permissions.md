# Configuring Permissions


You can modify Permissions by using ACE in your server config file, each permission can either have a `allow` or `deny` value, you can add infinite groups, just make sure to add permissions for each group.

```
add_ace group.moderator easyadmin.player.kick allow				# allow kicking
add_ace group.moderator easyadmin.player.spectate allow			# allow spectating
add_ace group.moderator easyadmin.player.teleport allow			# allow teleportation
add_ace group.moderator easyadmin.player.slap allow			# allow slapping 
add_ace group.moderator easyadmin.player.freeze allow			# allow freezing
```

you can also allow all permissions by writing:
```
add_ace group.admin easyadmin allow
```
This will allow **all** permissions for the "admin" group. 

**Note:** This will also make you immune from being kicked/banned as it grants you the `easyadmin.immune` permission. 




# Possible permissions are:

|         Permission          |                                                  Description                                                   |
|-----------------------------|----------------------------------------------------------------------------------------------------------------|
| easyadmin.player.ban.temporary     | Allows Admins to Temporarily Ban Users                                                                         |
| easyadmin.player.ban.permanent     | Allows Admins to Permanently Ban Users                                                                         |
| easyadmin.player.unban             | Allows Admins to Unban Users                                                                                   |
| easyadmin.player.kick              | Allows Admins to Kick Users                                                                                    |
| easyadmin.player.spectate          | Allows Admins to Spectate Users                                                                                |
| easyadmin.player.teleport.single   | Allows Admins to Teleport To/From Players                                                                      |
| easyadmin.player.teleport.everyone | Allows Admins to Teleport *everyone* at once.                                                                  |
| easyadmin.player.slap              | Allows Slapping of Users (take away hp)                                                                        |
| easyadmin.player.freeze            | Allows Admins to Freeze Players in place                                                                       |
| easyadmin.player.mute              | Allows Admins to "Mute" other Players from chat activity.                                                      |
| easyadmin.player.warn              | Allows Admins to "Warn" other Players.                                                                         |
| easyadmin.player.screenshot        | Allows Admins to Create Screenshots of users, these will be generated and uploaded to your Configured Uploader |
| easyadmin.player.reports.view		 | Allows Admins to View Reports made by Users															          |
| easyadmin.player.reports.process	 | Allows Admins to Delete Reports made by Users													              |
| easyadmin.server.shortcut.add      | Allows Admins to use the ea_addShortcut command, however, these are not persistant							  |
| easyadmin.server.reminder.add      | Allows Admins to use the ea_addReminder command, these are also not persistan                                  |
| easyadmin.server.permissions.read  | Allows Admins to view all (add_ace & add_principal) Permissions the server has configured                      |
| easyadmin.server.permissions.write | Allows Admins to edit and delete (add_ace & add_principal) Permissions                                         |
| easyadmin.server.cleanup.cars		 | Allows Admins to cleanup all Vehicles on the Server, except ones currently occupied by players		  		  |
| easyadmin.server.cleanup.props	 | Allows Admins to cleanup all Props on the Server, including ones spawned by resources or hacks, does not include maps |
| easyadmin.server.cleanup.peds		 | Allows Admins to cleanup all Peds on the Server																  |
| easyadmin.server.convars		 | Allows Admins edit Server Convars, this is a dangerous permission, only assign to people you trust!				  |
| easyadmin.server.resources.start   | Allows Admins to start Resources on the Server			 													  |
| easyadmin.server.resources.stop    | Allows Admins to stop Resources on the Server											     				  |
| easyadmin.immune            | Prevents Admins from being kicked/banned by other admins.                                                   	      |
| easyadmin.anon              | Allows the "Anonymous Admin" Feature, will hide Username in Kicks/Bans/Admin Logs                         		      |

