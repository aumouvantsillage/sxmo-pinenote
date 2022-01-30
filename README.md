SXMO on the PineNote
====================

This repository contains my configuration files for SXMO on the PineNote.

Resources used:

* [Instructions to install Archlinux on the Pinenote](https://github.com/DorianRudolph/pinenotes), by Dorian Rudolph.
* My setup is based on the [Manjaro minimal image for Quartz64](https://github.com/manjaro-arm/quartz64-bsp-images/releases) and the [Linux kernel branch maintained by smaeul](https://github.com/smaeul/linux/tree/rk356x-ebc-dev).
* SXMO can be installed using the script [sxmo-alarm](https://github.com/justinesmithies/sxmo-alarm), by Justine Smithies.
* [Backlight controls](https://github.com/alamedyang/pinenote-backlights) by alamedyang

Issues and workarounds
----------------------

### `sxmo-alarm` fails with a compilation error for package `pn`.

Solution: remove `Orange-OpenSource/pn` from the `repos` variable.

### The SXMO session does not start after a successful login.

* Create a dummy device profile script:

```
sudo touch /usr/bin/sxmo_deviceprofile_pinenoterockchip.sh
sudo chmod +x /usr/bin/sxmo_deviceprofile_pinenoterockchip.sh
```

* Edit `/etc/X11/xdm/Xsetup_0` and comment these lines:

```
sxmo_setpineled red 0
sxmo_setpineled blue 0
sxmo_setpineled green 0
echo 750 > /sys/devices/platform/backlight/backlight/backlight/brightness #scale goes from 0-1000 on kernel 5.8
```

### Missing packages

```
sudo pacman -S xprintidle
```

### Status bar

For some reason, the `start` hook is not run automatically.
The status bar only shows the text "dwm-6.2".

- [ ] Add solution.

Custom settings
---------------

- [ ] Setup autologin (using tiny-dm instead of xdm)
- [ ] Input handlers
- [ ] Add applications to menu

### Color scheme

The `.Xresources` file defines a color scheme for dwm, dmenu and svkbd.
Add the file to your home folder.

### Frontlight control

Install yad:

```
sudo pacman -S yad
```

Follow the instructions in the [README](https://github.com/alamedyang/pinenote-backlights/blob/main/README.md) to update the `sudoers` file.

Copy the script [backlight.sh](https://github.com/alamedyang/pinenote-backlights/blob/main/backlight.sh)
to `$HOME/.config/sxmo/userscripts`.
