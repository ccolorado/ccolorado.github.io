---
layout: post
title: "Mute group chats on Skype's Linux client"
categories: productivity tip
date:   2015-04-25 18:56:56
---

So you probably have at least one group with a free topic at work. Perhaps this chat has
everyone on the office/team, where they talk about not always work related stuff. Weekend
plans, personal updates, lunch plans an occasionally discussion about work or even some
light gossip about friends in common or the job market. The is a number of reasons to be
on this kind of groups. But usually there is one reason not to be on them, and that is
that they emit constant notifications, which can be distracting.  Sure you can set your
status on `busy`, and get no notifications at all, but what happens when your task
requires some sort of responsive communication with other contacts or groups over chat.

You definitely want some notifications to go away, but  not all of them. Perhaps you only
don't want those off topic groups. Achieving this on both Windows and OS X is pretty
straight forward, there is an option on the context menu to mute a specific group
conversation. Unfortunately on the Linux client this option is not included on the
graphical interface. But worry no more, Skype has a set of instructions that you can
access by sending commands as messages. Most of this commands control roles, and status,
but the one we are interested right now is:

```
/alertsoff
```

You can revert this change with the command `/alertson`. Alternative `/alertson
production` will enable notifications when the word 'production' is mentioned on the chat.
You can also issue the command `/help` or consult the more descriptive and complete list on
[Skype's reference page](https://support.skype.com/en/faq/FA10042/what-are-chat-commands-and-roles),
to see what other commands are available, just make sure that you click on the "Cloud-based
chat commands and roles" or "P2P-based chat commands and roles" since the content you need is
only visible after un-collapsing it by clicking on those sections.


#Bonus tip
The empty slash invokes the search dialog, just like vim. Well isn't this nice.

#TL;DNR
Send `/alertsoff` to mute the current chat's notifications.
