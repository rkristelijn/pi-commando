# pi-commando
Going full commando on my Raspberry Pi, Raspbian Lite (commandline) and try to do all from there... just because I'm curious if I can...

# Install Raspbian Lite

After installing a clean Raspbian Lite image using Noobs installer (I don't have to do anything with Wifi, because I'm connected to LAN), I'm doing the `apt-get update` and `apt-get upgrade` commands.

I've already set the language to US and also the keyboard layout to US in Noobs, but probably the first things you should do after installing a fresh Raspbian is:

- Update/Upgrade
- Set up security
- Localize (Timezone, Language, Keyboard)

# Security

See [the documentation](https://www.raspberrypi.org/documentation/configuration/security.md)

- Create new user alice
  - `adduser alice`
  - `sudo usermod -a -G adm,dialout,cdrom,sudo,audio,video,plugdev,games,users,input,netdev,gpio,i2c,spi alice`
  - add `alice ALL=(ALL) NOPASSWD: ALL` to end of the file `sudo visudo` to avoid having to type your password
- Disable pi user
  - `deluser pi`

# Things I want to do

- Surf the web (lynx? or something with JavaScript support)
- Fullstack JavaScript development (probably using vim)
- Read and respond to my e-mail
- Do my admin

# Surfing the web

[source](https://en.wikipedia.org/wiki/Text-based_web_browser) says:

|Browser | JS Support | Keyboard navigation | Runs on Raspberry Pi (ARM) |
|---|---|---|---|
| Charlotte Web Browser  |? | ? | ? |
| Emacs/W3 & EWW for GNU Emacs  |? | ? | ? |
| Line Mode Browser (by Tim Berners-Lee)  |? | ? | ? |
| Links  |? | ? | ? |
| ELinks  |? | ? | ? |
| Lynx  | <span style="color:red">No</span> | Yes | Yes |
| w3m |? | ? | ? |
| WebbIE |? | ? | ? |
| browsh | Yes | <span style="color:red">No</span> |  <span style="color:red">No</span> |
| Links2 | <span style="color:red">No</span> | Yes | Yes |


So what can I do with lynx?

| site | experience |
| --- | --- |
| google.com | seems ok |
| github.com | at this stage I started look for the setting 'cookies: accept all', seems to work, pages are a bit long due to the menus |
| dev.to | I can read posts, but login seems to be impossible, probably is in the 'loading...' section where javascript should kick in |
| gmail.com | meh. after login, says need JavaScript. I could try [cmdg](https://github.com/ThomasHabets/cmdg) |

Meh.

Let's try to get browsh up and running. (spoiler: doesn't work! [see here](https://github.com/browsh-org/browsh/issues/305) )

## Install docker [source](https://www.docker.com/blog/happy-pi-day-docker-raspberry-pi/)

add lines in my /etc/default/locale file: (caused by sshing into pi from mac?)

```
LC_CTYPE="en_US.UTF-8"
LC_ALL="en_US.UTF-8"
LANG="en_US.UTF-8"
```

```
sudo apt-get install apt-transport-https ca-certificates software-properties-common -y
curl -fsSL get.docker.com -o get-docker.sh && sh get-docker.sh\
sudo usermod -aG docker alice
sudo curl https://download.docker.com/linux/raspbian/gpg
```
add `deb https://download.docker.com/linux/raspbian/ stretch stable` to `sources.list`

`sudo vim /etc/apt/sources.list`

```
sudo apt-get update
sudo apt-get upgrade
sudo systemctl start docker.service
sudo docker info
```

## Install browsh - doesn't work

`docker run --rm -it browsh/browsh`

` "exec format error"` due cpu architecture mismatch. Cloning [repo](https://github.com/browsh-org/browsh), changing base image, no good.

Just for good measures, I installed browsh on my mac.. needed to install firefox too, however some words are clipped and you need a mouse to navigate. Seems like browsh is not for this use case. I've created an [Issue](https://github.com/browsh-org/browsh/issues/305) anyway.

## Install links2

`sudo apt-get install links2`

-> no JavaScript support
