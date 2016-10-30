flexgen
=======
[![Build Status](https://travis-ci.org/sideeffffect/flexgen.svg)](https://travis-ci.org/sideeffffect/flexgen)

flexgen generates sophisticated [FlexGet](http://flexget.com/) configuration for a given list of TV shows.

Installation
-------------

Install Python 3 and Deluge torrent client. Optionaly you can also have emails sent as notifications about new downloads.

Put `flexgen` in your `PATH`. Notice, that `pip` by default installs to `/usr/local/bin` which might not be in `PATH` in the invironment where `cron` runs. One way to solve this is to create a symlink:

```
sudo ln -s /usr/local/bin/flexget /usr/bin/flexget
```

Add new item to `crontab`:

```
$ crontab -e
```

add

```
LANG=en_US.utf8
@hourly flexgen 1> $HOME/.config/flexget/config.yml 2> /dev/null ; flexget --loglevel critical --logfile /dev/null execute 1> /dev/null 2>&1
```

Here I assume, that your `flexget` config file is in `$HOME/.config/flexget`, so change this part if necessary.

Use the email template:

```
mkdir -p ~/.config/flexget/templates
ln -s ~/Projects/flexgen/simplehtml.template ~/.config/flexget/templates/simplehtml.template
```


Configuration
-------------

Sample config file `~/.config/flexgen.yml` with comments

```
# flexgen config file
# https://github.com/sideeffffect/flexgen
#
# shows                list of shows
#                      put here the names of the TV shows that you want to be torrenting
#                      names should adhere to http://thetvdb.com/
#
# waitForQuality       the video quality to wait for
#                      OPTIONAL, default: 1080p
#                      http://flexget.com/Plugins/quality
#
# waitingTime          time to wait before resorting to a worse quality video
#                      OPTIONAL, default: 6 days
#                      http://flexget.com/Plugins/series/timeframe
#
# subtitleLanguage     language for subtitles to download
#                      OPTIONAL, default: eng
#                      https://en.wikipedia.org/wiki/ISO_639-3
#
# email                specify parameters for sending notifications via email
#                      OPTIONAL, fields: from, to, smtp_host, smtp_port, smtp_username, smtp_password, ...
#                      http://flexget.com/Plugins/email
#

shows:
- Pioneer One
- My Favorite Show
- Another TV Show
subtitleLanguage: eng
waitForQuality: 1080p
waitingTime: 6 days
```


License
------------
Copyright (c) 2014, 2015, 2016 Ondra Pelech

License GPL-3.0+

