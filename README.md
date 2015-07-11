flexgen
=======
[![Build Status](https://travis-ci.org/sideeffffect/flexgen.svg)](https://travis-ci.org/sideeffffect/flexgen)

flexgen generates sophisticated FlexGet configuration for a given list of TV shows.

Installation
-------------

Install Python 3 and Deluge torrent client. Optionaly you can also use [RapidPush](https://rapidpush.net/) to get updates to your phone.

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


Configuration
-------------

Sample config file `~/.config/flexgen.yml` with comments

```
# flexgen config file
# https://github.com/sideeffffect/flexgen
#
# waitForQuality       the video quality to wait for
#                      1080p or 720p
#                      http://flexget.com/wiki/Plugins/quality
#
# waitingTime          time to wait before resorting to a worse quality video
#                      "6 days", "13 hours", and so on
#                      http://flexget.com/wiki/Plugins/series/timeframe
#
# subtitleLanguage     language for subtitles to download
#                      3 character code
#                      https://en.wikipedia.org/wiki/ISO_639-3
#
# rapidpushApiKey      API key for the RapidPush service
#                      64 alphanumeric characters
#                      https://rapidpush.net/
#
# shows                list of shows
#                      put here the names of the TV shows that you want to be torrenting
#                      names should adhere to http://thetvdb.com/
#

rapidpushApiKey: keyNotSpecified
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
Copyright (c) 2014, 2015 Ondra Pelech

License GPL-3.0+

