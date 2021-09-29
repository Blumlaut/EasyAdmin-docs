# Adding Admins

ACEs use your server config file or commands to add / remove admins and set permissions, here is an example:

```
add_principal identifier.ip:127.0.0.1 group.admin
add_principal identifier.license:aaaabbbbcccddeeeeeeffff group.moderator
add_principal identifier.steam:1100001021asfd5 group.moderator
```
Layout of this command is

```
add_principal identifier.IDENTIFIER group.GROUP_NAME
```

Identifier in this case can be anything FiveM recognizes, for example, [steam](steamapikey.md), license, discord and so on, there are no restrictions on which identifier can be used.


We recommend only using lowercase letters in the identifiers, as uppercase letters may not work correctly.

