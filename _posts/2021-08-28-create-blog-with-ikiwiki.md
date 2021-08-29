---
title: Create blog with ikiwiki
author: Alejo GZ
date: 2021-08-29
categories: [Tutorials]
tags: [Ikiwiki blog tutorial]
pin: true
---
# Setup Ikiwiki with docker thttpd 

## Installation on Ubuntu or Debian

```bash
  $ apt-get install ikiwiki
```

## Create
Create your wiki

All it takes to create a fully functional wiki using ikiwiki is running one command.

For more control, advanced users may prefer to set up a wiki by hand.

```bash
  % ikiwiki --setup /etc/ikiwiki/auto.setup
```


Or, set up a blog with ikiwiki, run this command instead.

```bash
  % ikiwiki --setup /etc/ikiwiki/auto-blog.setup
```

`librpc-xml-perl` and `python-docutils` dependencies are needed.

Either way, it will ask you a couple of questions.

```
What will the wiki be named? foo
What revision control system to use? git
What wiki user (or openid) will be admin? joey
Choose a password:

Then, wait for it to tell you an url for your new site..

Successfully set up foo:
    url:         http://example.com/~joey/foo
    srcdir:      ~/foo
    destdir:     ~/public_html/foo
    repository:  ~/foo.git
To modify settings, edit ~/foo.setup and then run:
    ikiwiki --setup ~/foo.setup
```

Done!


## Build
### Build on linux local machine


### Build on docker


## Run server
[](https://ikiwiki.info/tips/dot_cgi)
[](https://hub.docker.com/r/larsks/thttpd)

Run next command

```bash
docker run -v C:\workspace\ikiwiki\public_html\blog:/content -p 8181:80 larsks/thttpd -d /content
```


## Resources

- **CSS market for Ikiwiki sites**: https://ikiwiki.info/css_market/
- **Ikiwiki Themes**:
	- https://ikiwiki.info/themes/
	- https://ikiwiki.info/theme_market/