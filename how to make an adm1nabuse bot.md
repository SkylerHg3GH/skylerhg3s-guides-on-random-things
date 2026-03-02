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
To create an event handler, add `with ms.EventQueue() as events:` <br>
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
Here's an example message you can get<br>
`[123] VIP SkylerHg3: hello guys`<br>
You will need to break this down into parts: the Wins, the prefix, The name, and the message<br>
using `event.message.partition(':')[0]`, `event.message.partition(':')[2]` you can get the thing after the `:`<br>
Now in the thing before the `:` break it into parts using `.split(' ')`.<br>
It is also necessary to include a length check of that result so you can get real messages<br>
`[123] VIP SkylerHg3: hello guys` -> `[123] VIP SkylerHg3` -> [`[123]`, `VIP`, `SkylerHg3`]<br>
Here the first item (Python starts at 0 indexing so `[0]`) is [123] the wins so you need to remove the brackets by using `[1:-1]`.<br>
The prefix is the second item (`[1]`)<br>
And the name is the last item which is (`[-1]`).<br>

## Create a message queue
To send messages, it is necessary to make a queue so you don't get spammed<br>
For this, you can make a message queue<br>
`MessageQueue = []`<br>
And make a handler<br>
`handle_queue()`<br>
that does `ms.chat(MessageQueue.pop)` to do the queue <br>
In my bot, it does this whenever someone executes a command.<br>

## Create a command handler
This should be very easy<br>
Get the message which is the thing after `:` in your `event.message`, and feed it to `shlex.split` which turns it into a list and now you can do the command handler<br>

Now you are done<br>
Just start it up and you've got a bot!<br>
