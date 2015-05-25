---
layout: post
title: "DIY home PVR Server Part 1 Downloading Media"
categories: howto trasmission
date: 2015-05-24 22:31:50
comments: true
---

Why build a PVR server, perhaps like me, you have a less than stellar ISP that can't
reliably stream 1080p or perhaps you have some spare hardware and want to set a home
server that does a little more than just serving files or share printers. If the idea of
having to maintain and curate a library is not for you, I may suggest [popcorntime.io](popcorntime.io).

There are several services that let you create a parametrized torrent feed.
[Show RSS](http://showrss.info/)
allows you to create a feed with the shows of your choosing. On these feeds episodes
torrents are available within the hour of their airtime.

*Transmission* is a Linux torrent client that can be set to run on headless mode.
This is specially useful when you intend to remotely operate the application, fortunately
transmission comes with no shortage of mechanisms to operate the service. There exists a
number of applications for desktop, web and mobile that allow you to do it.
[Remote Transmission](https://play.google.com/store/apps/details?id=com.neogb.rtac) is my
favorite, but there is a number of applications on [Google's Play Store](https://play.google.com/store/search?q=transmission).

My personal setup consist on a media server built mostly with the spare parts I got laying around
after my last desktop upgrade and a raspberry-pi.

But that is perhaps getting ahead of your selves. So withouth further adiu, lets start
this guide.

Installing and configuring the transmission server

## Transmission installation

Install the transmission server package.

{% highlight bash %}
{
  sudo apt-get install transmission-cli transmission-common transmission-daemon
  sudo service transmission-daemon start
}
{% endhighlight%}

## Transmission configuration

`NOTE :` An important and not so obvious piece of information, transmission writes down
the any configuration change when it stops. Do in order to effectively edit the
settings, the service must be stopped while editing. If you don't, the configuration changes
will be overridden when the service is stopped or restarted
Once transmission is installed, there is a few configurations that you may need. In order
to use transmission you may want to edit the file __/etc/transmission-daemon/settings.json__
and lookout for the following parameters.

{% highlight json %}
{
  "incomplete-dir-enabled": "true",
  "download-dir": "/path/to/completed/files",
  "incomplete-dir": "/path/to/incomplete/files",
  "watch-dir": "/path/to/torrent/directory",
  "rpc-enabled": true,
  "rpc-username": "transmission",
  "rpc-password": "",
  "rpc-whitelist": "127.0.0.1",
  "rpc-whitelist-enabled": false,
}
{% endhighlight%}

The `incomplete-dir-enabled` enables to specify the path where files are stored during download.
`download-dir` and `incomplete-dir` are the directories where completed and incomplete files
will be stored respectably. And finally `watch-dir` will specify a directory that
transmission will monitor for torrent files. Any torrent file stored there, will be added
automatically to the download queue. This last option is one of the most important as its
what we will use to automate the syndical zed download of media.

`rpc-username` will be the username that you will desire to use to get remote access,
`rpc-password` will be the password. The password can be filed on plain text, and
transmission will replace whatever you put in with it's hash. `rpc-whitelist` will limit
the IP addresses that the server will respond to, but you can enable or disable this
feature with `rpc-whitelist-enabled`.

# Downloading Media automaticaly.

Once your transmission server is working correctly, you can set up a torrent feed at
[ showrss.io](http://showrss.io). Select one or more shows and add them to your
collection, or instead you can add the show's feed individually. We are going to use
python package manage pip in order to install flex but you can use whatever method you
find suitable to your environment.

{% highlight bash %}
{
  sudo apt-get install python-pip
  sudo pip install --upgrade setuptools
  sudo pip install --upgrade flexget
}
{% endhighlight%}

Once installed, you need to edit the flexget configuration file, this file will indicate
the RSS that will be monitored, as well as the destination directory. configuring the
download directory with transmission's watch-dir will automate the download of any show
you decide to add to the feed. Here is a sample of how __~/.flexget/config.yml__ should
look like. For this example I picked the 'Silicon Valley' public rss feed.

{% highlight yaml %}
{
tasks:
  showrss:
    rss: http://showrss.info/feeds/799.rss
    accept_all: yes
    download: /path/to/torrent/directory
}
{% endhighlight%}

To start downloading the torrents from the feed simply run `flexget execute` or better yet
add a cronjob like this one:

{% highlight bash %}
{
  59 * * * * /usr/bin/flexget execute
}
{% endhighlight%}
