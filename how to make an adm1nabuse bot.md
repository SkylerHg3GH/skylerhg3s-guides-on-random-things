# how to make an adm1nabuse bot 

## requirements
you will need
- Minescript
- Minecraft obviously
- Python
- some other python libraries
(I use the neoforge Minescript)

## Startup
First, Lets look at bot.py 
```
# -*- encoding: UTF-8 -*-
import system.lib.minescript as ms
import time
import shlex
```
well that's nice

## Create the event handler
To create an event handler, add `with ms.EventQueue() as events:` 
Here's an example of the thing i do for my bot
```
with ms.EventQueue() as events:
    events.register_chat_listener()
    ms.echo("Bot started!")

    while True:
        try:
            # process the msg here
```
The text on the event message is from `event.message`

## Create a message parser
Here's an example message you can get
`[123] VIP SkylerHg3: hello guys`
You will need to break this down into parts: the Wins, the prefix, The name, and the message
using `event.message.partition(':')[0]`, `event.message.partition(':')[2]` you can get the thing after the `:`
Now in the thing before the `:` break it into parts using `.split(' ')`.
It is also necessary to include a length check of that result so you can get real messages
`[123] VIP SkylerHg3: hello guys` -> `[123] VIP SkylerHg3` -> [`[123]`, `VIP`, `SkylerHg3`]
Here the first item (Python starts at 0 indexing so `[0]`) is [123] the wins so you need to remove the brackets by using `[1:-1]`.
The prefix is the second item (`[1]`)
And the name is the last item which is (`[-1]`).

## Create a message queue
To send messages, it is necessary to make a queue so you don't get spammed
For this, you can make a message queue
`MessageQueue = []`
And make a handler
`handle_queue()`
that does `ms.chat(MessageQueue.pop)` to do the queue 
In my bot, it does this whenever someone executes a command.

## Create a command handler
This should be very easy
Get the message which is the thing after `:` in your `event.message`, and feed it to `shlex.split` which turns it into a list and now you can do the command handler

Now you are done
Just start it up and you've got a bot!
