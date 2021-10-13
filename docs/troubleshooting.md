# Basic Troubleshooting


## Help, i'm getting an Error!

```
Error resuming coroutine: admin_server.lua:496: bad argument #1 to 'for iterator' (table expected, got nil)
stack traceback:
        [C]: in for iterator 'for iterator'
        admin_server.lua:496: in function 'updateBlacklist'
        admin_server.lua:608: in function 'loopUpdateBlacklist'
        admin_server.lua:618: in function <admin_server.lua:23>
```
Solution:
Your banlist.json file has a formatting error, if it's empty, delete it, if there are bans inside of it, use a [json validator](https://jsonformatter.curiousconcept.com/) and fix any errors inside of the file.

## What about this one?

```
Error resuming coroutine: citizen:/scripting/lua/json.lua:397: bad argument #1 to 'strfind' (string expected, got nil)
stack traceback:
        [C]: in function 'string.find'
        citizen:/scripting/lua/json.lua:397: in upvalue 'scanwhite'
        citizen:/scripting/lua/json.lua:553: in function <citizen:/scripting/lua/json.lua:551>
        (...tail calls...)
        admin_server.lua:24: in function <admin_server.lua:23>
```

Solution: The language file you set in the ea_LanguageName Convar does not exist in EasyAdmin\language, change it to one that exists.


## My Permissions dont work right/I cant open the Menu!
Add
```
setr ea_logLevel 3
```

To your server.cfg, reboot the server and then join, EasyAdmin will now print all permissions for the joined user, these are the permissions that easyadmin can see via ACE, double check your configured permission and correct it accordingly.

## Getting a different problem? Join the (Support Discord)[https://discord.gg/GugyRU8]! 
