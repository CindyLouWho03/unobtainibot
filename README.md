# Unobtainibot
A sloppily coded discord bot which does absolutley nothing of use. In fact, the code is so sloppy that
I don't even know how it works myself. You are not expected to be able to understand it.

If you're somehow able to wrap your head around this bot's god awful codebase and want to contribute,
go ahead and fork and make a PR. But seriously, don't do that, it's not worth the effort.

## Config
`config.json` - General config.

- `prefix` - The default prefix used when the bot is added to a
new server.  
- `botownerid` - The bot owner's user ID.  
- `statustimeout` - An amount of time in seconds which decides
how long the bot waits inbetween status changes. Setting this
to `0` disables automatic status changes.
- `statuses` - An array of strings to be used as statuses. The bot
will randomly change to one of these every `statustimeout` seconds.
- `usecounter` - An integer which tells how many times a bot command has been used.

`logins.json` - Logins.

- `discordtoken` - The token of your bot.

`servers.json` - The server "database", so to speak.  
Every server the bot is in (or has been in) is inside this file.
The servers are keyed with `sid############`, and follow this object
structure:

- `servername` - The name of the server.  
- `serverownerid` - The server owner's user ID.  
- `prefix` - The prefix used for this server.  
- `disabledcommands` - An array of strings denoting commands, without
the prefix, that are disabled on this server.  
- `modrolename` - The name of the role used for moderators on the
server.  
- `adminrolename` - The name of the role used for admins on the server.  
- `quotes` - An array of strings used as quotes for the `quote` command.  
- `customcommnads` - An array of objects used to denote custom comands.

## Hardcoded commands
Key: `[required]`, `[required and repeatable ... ]`, `<optional>`, `<optional and repeatable ... >`

### Config
`changeprefix [prefix] <server|default>`: Changes the bot command prefix. (userlevel: 2)  
`[prefix]`: What to change the prefix to.  
`<server|default>`: Specify whether or not to change the server's prefix, or the default prefix.
If omitted, defaults to `server`. This arg requires userlevel 4.

`setulrolenames [modrole] <adminrole>`: Changes the moderator/admin role names. (userlevel: 2)  
`[modrole]`: The moderator role name.  
`<adminrole>`: The admin role name. If ommited, defaults to whatever the current admin role name is.

### Quotes

`addquote [quote ... ]`: Adds a quote to the list. (userlevel: 1)  
`[quote ... ]`: The quote to add.

`delquote [index|all]`: Removes a quote from the list. (userlevel: 1)  
`[index|all]`: A number corrosponding to the index of the quote to be removed, or `all`,
which removes all quotes.

`quote <index|list>`: Prints out a quote from the list. (userlevel: 0)  
`<index|list>`: Either a number corrospoding to the index of the  quote to be printed, or `list`.
If `list`, the user will be PM'd a list of quotes and their indexes. If omitted, prints a random quote.

`8ball [question ... ]`: Prints out a random Magic 8-Ball quote. (userlevel: 0)  
`[question ... ]`: The question to ask the Magic 8-Ball.

### Commands

`help <command>`: PMs the user info regarding the commands this bot supports. (userlevel: 0)  
`<command>`: A command name, without the prefix, to get information on. If omitted, PMs the user
a list of all commands they can use in that serever.

`toggle [command]`: Toggles a command on or off on the current server. (userlevel: 2)  
`[command]`: The name of the command, without prefix, to toggle.

`addcom simple [name] [userlevel] [reply-in-pm] [content ... ]`: Adds a simple custom command to the server.
(userlevel: 2)  
`[name]`: The name of the command to add, without prefix.  
`[userlevel]`: An integer corrosponding to the userlevel required to use the command.
`0` for everyone, `1` for mod, `2` for admin, `3` for server owner, and `4` for bot owner.  
`[reply-in-pm]`: An integer that specifies whether or not this command should reply to the user in
a PM rather than in the channel it was sent from. `0` for false, `1` for true.  
`[content ... ]`: The content the command will print when used.

`addcom quotesys [name] [userlevel] [addcomname] [addcomuserlevel] [delcomname]`:
Adds a full custom quote system to the server, including the addcom and delcom commands. (userlevel: 2)  
`[name]`: The name of the quote system.  
`[userlevel]`:  An integer corrosponding to the userlevel required to use the quote command.  
`[addcomname]`: The name of the command used to add to the quote system.  
`[addcomlevel]`:  An integer corrosponding to the userlevel required to use the addquote command.  
`[delcomname]`: The name of the command used to remove from the quote system.  
`[delcomlevel]`:  An integer corrosponding to the userlevel required to use the delquote command.  

`addcom quote [name] [userlevel]`: Adds a quote system to the server without adding the addquote
and delquote commands. (userlevel: 2)  
`[name]`: The name of the quote system.  
`[userlevel]`:  An integer corrosponding to the userlevel required to use the command.

`addcom addquote [name] [userlevel] [quotesys]`: Adds an addquote command for a custom quote system.
(userlevel: 2)  
`[name]`: The name of the command, without prefix.  
`[userlevel]`:  An integer corrosponding to the userlevel required to use the command.  
`[quotesys]`: The name of the custom quote system this command will edit.

`addcom delquote [name] [userlevel] [quotesys]`: Adds an delquote command for a custom quote system.
(userlevel: 2)  
`[name]`: The name of the command, without prefix.  
`[userlevel]`:  An integer corrosponding to the userlevel required to use the command.  
`[quotesys]`: The name of the custom quote system this command will edit.

`delcom [name]`: Removes a custom command from the server. (userlevel: 2)  
`[name]`: The name of the command to remove.

`userlevel`: Tells you what userlevel you have. (userlevel: 0)

### External lookups

`src [game] [category ... ]`: Gets the speedrun.com WR for a given game and category. (userlevel: 0)  
`[game]`: The game to get the WR for.
`[category ... ]`: The category to get the WR for.

### Misc

`test <args ... >`: Prints the arguments specified. (userlevel: 0)  
`<args ... >`: The arguments to print. If omitted, no arguments are printed.

`tf`: Flip some tables. (╯°□°）╯︵ ┻━┻ (userlevel: 0)

`stats`: Shows some stats about the bot. (userlevel: 0)  
The stats shown are how many servers the bot is in, how many members of said servers
are online, the bot's command usage counter, and the bot's uptime.

`eval [code ... ]`: Takes the provided Python expression, and `eval`s it. (userlevel: 4)  
`[code ... ]`: The Python code to be evaluated.

`exec [code ... ]`: Takes the provided Python code, and `exec`s it. (userlevel: 4)  
`[code ... ]`: The Python code to be executed.

## Custom commands
Custom commands can be added per-server using the `addcom` command. These commands can have different
types, and the structure of the command object in the JSON is different depending on this type, but
every type will always have a `type`, `name`, and `content` key.

- `type`: The type of the command.
- `name`: The name of the command.
- `content`: This is the most complex one as its value depends on what the type of the command is.  
    - For `simple` type commands, it is a string contaning the message the command will print when used.  
    - For `quote` type commands, it is a string array containing the quotes this command will return.  
    - For `addquote` and `delquote` type commands, it is a string with the name of the quote system the command
      will modify.
- `userlevel`: The minimum userlevel required to use the command.
- `replyinpm`: If `1`, replies to the user in a PM. If `0`, it replies to the user in the same channel
the command was used from. `simple` type only.
