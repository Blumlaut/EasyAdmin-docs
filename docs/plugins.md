# Plugin API

Since 5.9 EasyAdmin Supports creating custom Plugins which allow Developers to create new Items in the Menu and add custom Functions, this is a Quick-Start Guide for Developers.


## Foreword

EasyAdmin is based on [Frazzle's NativeUILua](https://github.com/FrazzIe/NativeUILua), so when creating Menus, make sure that you follow it's API Properly.

Menu Items are generated when the Button for it is pressed, do note that the menu can and WILL be generated multiple times, so do not store any variables which may affect the menu generation on later iterations.


## Boilerplate Script

Here is a Boilerplate Script that can help you get started with EasyAdmin Plugins:

```lua
local somevalue = false

AddEventHandler("EasyAdmin:BuildPlayerOptions", function(playerId) -- BuildPlayerOptions is triggered after building options like kick, ban.. Passes a Player ServerId
	
	local thisItem = NativeUI.CreateItem("Example Item","Player ID is "..playerId) -- create our new item
	thisPlayer:AddItem(thisItem) -- thisPlayer is global.
	thisItem.Activated = function(ParentMenu,SelectedItem)
		-- enter your clientside code here, this will be run once the button has been activated.
		somevalue = true -- set some value we want to undo once the menu closes.
	end

	if permissions["kick"] then -- you can also check if a user has a specific Permission.
		local thisExampleMenu = _menuPool:AddSubMenu(thisPlayer,"Example Submenu","",true) -- Submenus work, too!
		thisExampleMenu:SetMenuWidthOffset(menuWidth)

		local thisItem = NativeUI.CreateItem("Example Submenu Item","")
		thisExampleMenu:AddItem(thisItem) -- Items dont require a trigger.
	end
end)


AddEventHandler("EasyAdmin:BuildCachedOptions", function(playerId) -- Options for Cached Players, do note that these do not not support Player natives! They're cached BY EASYADMIN
end)

AddEventHandler("EasyAdmin:BuildServerManagementOptions", function() -- Options for the Server Management Submenu, passes nothing.
end)

AddEventHandler("EasyAdmin:BuildSettingsOptions", function() -- Options for the Settings Page, once again, passes nothing
end)

AddEventHandler("EasyAdmin:MenuRemoved", function() -- this triggers if a player closes the menu or the menupool gets removed, this CAN trigger multiple times in a row.
	somevalue = false -- reset our value :)

end)
```


## Recieving Events

These are the Events that your Script can recieve and use, but should never trigger.


|                 Event                  | Arguments | Function |
|----------------------------------------|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| EasyAdmin:BuildPlayerOptions           | playerId  | This event is meant to be used if new Menu options are meant to be created inside a player's submenu, the playerId is passed, you can use the "thisPlayer" variable to access the Menu.                         |
| EasyAdmin:BuildCachedOptions           | cachedId  | This event is for adding Menu Options to cached players, do note that these are not real players and the Id cannot be interacted with with Natives. Menu is "thisPlayer".                              |
| EasyAdmin:BuildServerManagementOptions | none      | This event is meant to be used for adding menu options to the "Server Management" Submenu, the menu is called "servermanagement"                                                                       |
| EasyAdmin:BuildSettingsOptions         | none      | This event is meant to be used for adding menu options to the "Settings" Submenu, the menu is called "settingsMenu"                                                                                    |
| EasyAdmin:MenuRemoved                  | none      | This event is used when the EasyAdmin Menu is closed and/or Removed, this happens if the menu is closed and not active. This can trigger multiple times in a row so be careful what code you put here. |

## Sending Events

EasyAdmin has a powerful API with which you can already do lots of things, here are a few Server Events which you can Trigger:


|              Event              |             Arguments              |      Returns       |                                                                            Function                                                                                                                                    |
|---------------------------------|------------------------------------|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| EasyAdmin:amiadmin              | none                               | none               | Re-send Permissions list on a Player, this also gets done sometimes if a player opens the menu.                                                                                                                        |
| EasyAdmin:GetInfinityPlayerList | none                               | Table(PlayerCache) | This Event sends a Clientside event with the same name back, containing a Table of all Players                                                                                                                         |
| EasyAdmin:requestCachedPlayers  | none                               | Table(PlayerCache) | This Event sends an Event called `EasyAdmin:fillCachedPlayers` back which is a table of all cached Players, this includes active and not active players.                                                               |
| EasyAdmin:kickPlayer            | playerId,reason                    | none               | This Event Kicks a Player if the User has permissions to do so and sends a Webhook Message with it.                                                                                                                    |
| EasyAdmin:addBan                | playerId,reason,expireTime,offline | none               | This Event Bans a player (both online and cached) using EasyAdmin's Ban Feature, "Expires" has to be a timeframe(for ex. 1 week) in Unix Time. If the player is not on the Server make sure to pass "offline" as true. |
| EasyAdmin:requestBanlist        | none                               | table(banlist)     | This Event sends an event called `EasyAdmin:fillBanlist` back with a table of all Bans.                                                                                                                                |
| EasyAdmin:SlapPlayer            | playerId,slapAmount                | none               | This Event Slaps a player, taking away HP according to "SlapAmount".                                                                                                                                                   |
| EasyAdmin:TakeScreenshot        | playerId                           | httpResponse       | This Event Takes a screenshot of the player's screen and once successful, triggers `EasyAdmin:TookScreenshot` with the HTTP Response, screenshot-basic is required.                                                    |
| EasyAdmin:unbanPlayer           | banId                              | none               | Unbans a Player according to their Ban Id                                                                                                                                                                              |
| EasyAdmin:mutePlayer   		  | playerId                           | none               | Toggles a Mute on a Player. |


## Internal Events

These are Events that EasyAdmin may trigger to internally send informations to the Server or Clients, these may not be up to date, reading the Sourcecode to be sure is recommended.

| Event | Direction | Arguments |
|-------|-------|-------|
| EasyAdmin:adminresponse | S->C | A Table of Permissions and their respective values `[permissionName = true/false]` |
| EasyAdmin:SetSetting | S->C | A Function and a State, contains options such as Menu Keybind |
| EasyAdmin:SetLanguage | S->C | Passes a table of Strings from the Language Configured. |
| EasyAdmin:fillBanlist | S->C | Passes the Banlist as a Table |
| EasyAdmin:fillCachedPlayers | S->C | Same as above, but with Cached Players. |
| EasyAdmin:GetInfinityPlayerList | S->C | Same, but with Players. |
| EasyAdmin:getServerAces | S->C | Sends 2 tables, of aces and principals respectively |
| EasyAdmin:NewReport | S->C | Adds a new Report to the current Table of Reports | 
| EasyAdmin:RemoveReport | S->C | Removes a Report from the table of Reports |
| EasyAdmin:requestSpectate | S<->C | Is both the event to Request and start the spectate process | EasyAdmin:TeleportRequest | S->C | Tells a player to teleport to a specific location. Passes a target ID and/or Coordiantes |
| EasyAdmin:SlapPlayer | S->C | Slaps the current Player for the amount of HP |
| EasyAdmin:FreezePlayer | S->C | Same as above, except Freezing | 
| EasyAdmin:amiadmin | C->S | Will check all Permissions for a player and send back the permissions in `EasyAdmin:adminresponse` |
