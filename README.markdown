twt - A simple CLI Twitter client
=================================
twt is a Twitter client designed to be as easy as possible to be used from CLI. You'll never have to switch from your preferred console to the browser and check latest tweets anymore.

Installation
============
You need a working Ruby environment. On Linux and OS X, the default ruby 1.8.7 is OK (but if you want Ruby 1.9.2 is OK too).

Then you have to install twt via rubygems:

    % sudo gem install twt
    
This will also install a few dependencies.

If you are on Windows, well, just try and let me know if it works.

Usage
=====
A short guide appears if you type:

    % twt

Login
-----
Provided that your Twitter username and password are USER and PWD, respectively, you first have to login by issuing the command:

    % twt login USER:PWD

The command tells you if the login was successful or not, then exits. The login information gets actually saved on a hidden file, available for any subsequent request until logout (see next).

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

Example: this will read the latest 10 tweets from your friends, and this limit of ten messages will remain valid for every subsequent call, until modified or until a reset:

    % twt -c10 friends

To Dos
======

- Support more commands (eg search).
- Accept suggestions.
