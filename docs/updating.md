# Updating Instructions

This page outlines instructions on how to update EasyAdmin between versions.


## Version 6.2 and newer

### Permissions change

Permissions have been changed majorly from 5.* to 6.2 and above, Permissions now have a "category" they belong to, there have also been new permissions added for existing features.

As an example

```
add_ace group.moderator easyadmin.kick allow
```

has been changed to

```
add_ace group.moderator easyadmin.player.kick allow
```
Existing Permissions now have either "player" or "server" as a prefix, here is a list of Permissions as of 6.2, do note that they should all be prefixed with `easyadmin.`

Important to note is that `manageserver` no longer exists, and `teleport.player` has been renamed to `player.teleport.single`, implying the ability to teleport a single player at once.


```
player.ban.temporary
player.ban.permanent
player.kick
player.spectate
player.unban
player.teleport.single
player.teleport.everyone
player.slap
player.freeze
player.screenshot
player.mute
player.warn
player.reports.view
player.reports.process
server.cleanup.cars
server.cleanup.props
server.cleanup.peds
server.permissions.read
server.permissions.write
server.shortcut.add
server.reminder.add
server.convars
server.resources.start
server.resources.stop
immune
anon
```

___

### FiveM Keybinds

The ea_MenuButton convar has been changed and now requires a string for a key, as per [this docs entry](https://docs.fivem.net/docs/game-references/input-mapper-parameter-ids/keyboard/), as an example:

```
setr ea_MenuButton "289"
```

now becomes

```
setr ea_MenuButton "f2"
```

**Note:** This is a one-time action, once a player joins with that Keybind set they will have to change it from their Control Settings inside of FiveM, FiveM currently does not provide any way to override this for all players.

This **does not** apply to RedM.
