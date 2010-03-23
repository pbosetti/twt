twt - A simple CLI Twitter client
=================================
twt is a Twitter client designed to be as easy as possible to be used from CLI. You'll never have to switch from your preferred console to the browser and check latest tweets anymore.

Installation
============
You need a working Ruby environment. On Linux and OS X, the default ruby 1.8.7 is OK, and it also work with Ruby 1.9.x

Then you have to install twt via rubygems:

    % sudo gem install twt
    
This will also install a few dependencies.

If you are on Windows, well, just try and let me know if it works.

Since version 0.2.1, twt checks online for new version availability. If found, it remembers you to upgrade your gem.

Usage
=====
A short guide appears if you type:

    % twt

Login
-----
This version relies on OAuth for authentication. This means that the very first time you try to do something, twt will launch your browser and ask Twitter for connection. You have to confirm the request (within the browser), copy the PIN it gives you back, and past the PIN after the prompt that twt is presenting you.
Since now, you are connected and each subsequent command would not require additional authentication, until you would logout.

Logout
------
If you want to remove your credentials, just type:
    
    % twt logout
    
Read friends of user timelines
------------------------------

To read you friends timeline, your own timeline, and the tweets mentioning you, simply issue:

    % twt friends
    % twt user
    % twt mention
    
You can also get a specific user's timeline (in the example, mine):
    
    % twt user p4010
    
Post a message
--------------
To post a new message, issue:

    % twt post "Ho! This is a nice new message from twt!"

Note that twt will automatically cut your message down to 137 characters and add tree points at the end ("...") if your original message would result longer than 140 characters. You will be noticed about this shortening operation.

*NEW in ver. 0.2!* If you are not connected to the Internet when you post a message, the message will be queued. You can view and manipulate your queued messages with the command:

    % twt queue
    0. test1
    1. test2
    2. test3
    % twt dequeue 0 2           # deletes messages 0 and 2 from the queue
    Messages 0, 2 dequeued
    % twt dequeue               # deletes all the queued messages
    Message queue is now empty

When you go back online, you can then deliver all the queued messages with the command:

    % twt deliver
    Delivering 3 queued messages:
    message 0... Succesfully posted "test1"
    sent
    message 1... Succesfully posted "test2"
    sent
    message 2... Succesfully posted "test3"
    sent
    Message queue is now empty
    
Monitor your followers
----------------------
If you want to monitor your followers and discover the name of the last ugly people that left your list, use the delta command:

    % twt delta
    
*This is new since version 0.1.5.*

Reset the environment
---------------------
twt keeps a few configuration variables (those marked as "sticky" in the short help) beside to the login in a hidden configuration file. If you want to reset to default values (and clean login information too), issue:

    % twt reset
    
Options
-------
At the moment, the following options are supported:

- -cN: limits ANY subsequent query to N results (i.e. tweets). **If you set the number to 0 (zero) you only get the new messages since your last query** (sticky)
- -wN: format messages to be nicely represented in a console of width N (sticky)
- -r:  prints out results in raw format (useful for debug or Twitter API inspection)
- -s:  toggles the insertion of an empty line between each result (sticky)
- -p:  toggles between compact and readable view for tweet heading (sticky)
- -kCOLOR: sets the color for tweet user name (sticky)

Valid color codes are:

- off       =>  Turn off all attributes
- bright    =>  Set bright mode
- underline =>  Set underline mode
- blink     =>  Set blink mode
- inverse   =>  Exchange foreground and background colors
- hide      =>  Hide text (foreground color would be the same as background)
- black     =>  Black text
- red       =>  Red text
- green     =>  Green text
- yellow    =>  Yellow text
- blue      =>  Blue text
- magenta   =>  Magenta text
- cyan      =>  Cyan text
- white     =>  White text
- default   =>  Default text color

Example: this will read the latest 10 tweets from your friends, and this limit of ten messages will remain valid for every subsequent call, until modified or until a reset:

    % twt -c10 friends

To Dos
======

- Support more commands (eg search).
- Implement the daemon command together with the -t/--time, that will spawn a process that periodically checks for new tweets every given seconds. This will save a PID file on the ~/.twitter dir, that will be used to shut down that daemon (command name?).
- Accept suggestions.
