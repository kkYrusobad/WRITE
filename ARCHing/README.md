## INSTALLING .deb PACKAGES
- install debtap(aur) `yay -S debtap`
- `debtap -u` first time only, then `debtap <file_name>`
- debtap converts the debian package file into tar file, extract `tar -xvf <file_name>`
- this provides an /opt and /usr directories which contains compiled binary to the package.(completely depends on the package provider how internal directories are managed.)
- make a desktop entry or put them in systems /opt and /usr dir.

* * *

## DESKTOP ENTRIES
- executable text files respnsable for creating a custom launch menu item for a perticular software.
- finally, use `dex` to invoke desktop file, can also bind keyboard shortcuts to invoke `dex` and application.

* * *

## LIGHTDM (failed to start)
- error occurs on boot : lightdm failed to start, graphical interface reached.
- reason :: lightdm initially, after install lightdm sets up seat* in such a way that it can work with currently installed graphics drivers. 
- Nvidia users are supposed to install nvidia drivers first `sudo pacman -S nvidia` 
- head to `cd /etc/lightdm/`
- create a file like `sudo touch displayscript.sh`
- input :: `sudo <any_text_editor> displayscript.sh` uses vim? then `sudo vim displayscript.sh`
```BASH
#!/bin/sh
xrandr --setprovideroutputsource modesetting NVIDIA-0
xrandr --auto
```
- save (in vim quit --insert-- instance and `:wq`)
- `sudo chmod +x displayscript.sh`
- edit file "lightdm.conf", under seat* find line with "display-setup-script" then delete "#" and insert path to the "displayscript"
~~~~
[Seat:*]
...
#display-setup-script=
...
~~~~
changes to 
~~~~
[Seat:*]
...
display-setup-script=/etc/lightdm/displayscript.sh
...
~~~~
- finally enable lightdm to start at boot, `sudo systemctl enable lightdm.service` and `reboot`

* * *

## STEAM Segmentation fault
quite common on fresh install, also rather simpler solution..
`$ sudo pacman -S lib32-nvidia-utils`

* * *
