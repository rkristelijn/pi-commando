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

So what can I do with lynx?

| site | experience |
| --- | --- |
| google.com | seems ok |
| github.com | at this stage I started look for the setting 'cookies: accept all', seems to work, pages are a bit long due to the menus |
| dev.to | I can read posts, but login seems to be impossible, probably is in the 'loading...' section where javascript should kick in |
| gmail.com | meh. after login, says need JavaScript |
