

Telepathy: An OSINT toolkit for investigating Telegram chats. Developed by Jordan Wildon. Version 2.1.10.


## Installation

### Pip install (recommended)

```
$ pip3 install telepathy
```

### Install from source

```
$ git clone https://github.com/jordanwildon/Telepathy.git
$ cd Telepathy
$ pip install -r requirements.txt
```

## Setup

On first use, Telepathy will ask for your Telegram API details (obtained from my.telegram.org). Once those are set up, it will prompt you for an authorization code which will be sent to your Telegram account. If you have two-factor authentication enabled, you'll be asked to input your Telegram password.


## Usage:

```
telepathy [OPTIONS]
```

Options:
- **'--target', '-t' [CHAT]**

this option will identify the target of the scan. The specified chat must be public. To get the chat name, look for the 't.me/chatname' link, and subtract the 't.me/'.

For example:

```
$ telepathy -t durov
```

The default is a basic scan which will find the title, description, number of participants, username, URL, chat type, chat ID, access hash, first post date and any applicable restrictions to the chat. For group chats, Telepathy will also generate a memberlist (up to 5,000 members).


- **'--comprehensive', '-c'**

A comprehensive scan will offer the same information as the basic scan, but will also archive a chat's message history.

For example:

```
$ telepathy -t durov -c
```


- **'--forwards', '-f'**

This flag will create an edgelist based on messages forwarded into a chat. It can be used alongside either a default or comprehensive scan.

For example:

```
$ telepathy -t durov -f
```


- **'--media', '-m'**

Use this flag to include media archiving alongside a comprehensive scan. This makes the process take significantly longer and should also be used with caution: you'll download all media content from the target chat, and it's up to you to not store illegal files on your system.

For example, this will run a comprehensive scan, including media archiving:

```
$ telepathy -t durov -c -m
```


- **'--user', '-u' [USER]**

Looks up a specified user ID. This will only work if your account has "encountered" the user before (for example, after archiving a group).

```
$ telepathy -u 0123456789
```


- **'--location', '-l' [COORDINATES]**

Finds users near to specified coordinates. Input should be longitude followed by latitude, seperated by a comma.

```
$ telepathy -l 51.5032973,-0.1217424
```

- **'--alt', '-a'**

Flag for running Telepathy from an alternative number. You can use the same API key and Hash but authenticate with a different phone number. Allows for running multiple scans at once.

```
$ telepathy -t Durov -c -a
```

- **'--export', '-e'**

Exports all chats your account is part of to a CSV file. In a future release, this may assist with setting up multiple accounts following the same groups.

```
$ telepathy -e
```
  
- **'--reply', '-r'**

Flag for enable the reply retrieval for the target channel, it will map users who replied in the channel and it will dump the full conversation chain 

```
$ telepathy -t [CHANNEL] -c -r 
```


## A note on how Telegram works

Telegram chats are organised into three key types: Channels, Megagroups/Supergroups and Gigagroups. Each module works slightly differently depending on the chat type. Channels can have seemingly unlimited subscribers and are where an admin will broadcast messages to an audience, Megagroups can have up to 200,000 members, each of whom can participate (if not restricted), and Gigagroups sit somewhere between the two.


## Upcoming changes
In some environments (particularly Windows), Telepathy struggles to effectively manage files and can sometimes produce errors. Fixes for these errors will come in due course.

Upcoming features include:

  - [ ] Adding a time specification flag to set archiving for specific period.
  - [x] The ability to archive comments on messages to channels.
  - [ ] The ability to gather the number of reactions to messages, including statistics on engagement rate.
  - [ ] Finding a method to once again gather complete memberlists (currently restricted by the API).
  - [x] Introducing the ability to scan multiple targets at once.
  - [ ] Improved statistics: including timestamp analysis for channels.
  - [ ] Generating an entirely automated complete report, including visualisation for some statistics.
  - [x] Making it easier to scan private groups which your account is a member of.
  - [ ] Hate speech analytics.
  - [x] Clean code, efficiency tweaks.
  - [x] Add user lookup.
  - [x] Add location lookup.
  - [ ] Maximise compatibility of edgelists with Gephi.
  - [ ] Include sockpuppet account provisioning (creation of accounts from previous exported lists).
  - [ ] Automated EXIF data report and analytics when media archiving is enabled.


## feedback

Please send feedback to @jordanwildon on Twitter. You can follow [@TelepathyDB](twitter.com/TelepathyDB) for updates.


## Usage terms

You may use Telepathy however you like, but your usecase is your responsibility. Be safe and respectful.


## Credits

All tools created by Jordan Wildon (@jordanwildon). Special thanks go to [Giacomo Giallombardo](https://github.com/aaarghhh) for adding additional features and code refactoring, and [Alex Newhouse](twitter.com/AlexBNewhouse) for help and guidance with Telepathy v1.

Where possible, credit for the use of this tool in published research is desired, but not required. This can either come in the form of crediting the author, or crediting Telepathy itself (preferably with a link).
