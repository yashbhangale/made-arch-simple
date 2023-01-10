# made arch simple

[Download the file](https://drive.google.com/file/d/1HueKhKpZu73Xjdsq7_8sBwA4LYCAGggO/view?usp=sharing)  download ova from here


# Cheat Sheet

## Wireless Network Configuration

    $ ip link set <interface> up
    $ wpa_supplicant -B -i <interface> -c <(wpa_passphrase <ssid> <passphrase>)
    $ dhcpd
    $ ping -c vg.no


## Post installation

### pacaur

First install needed dependencies from official repos:

    # pacman -S --needed binutils make gcc fakeroot pkg-config
    # pacman -S --needed expac yajl git

Install `cower` from aur:

    $ git clone --depth 1 https://aur.archlinux.org/cower.git
    $ cd cower && makepkg PKGBUILD -i --needed --skippgpcheck

Install `pacaur` from aur:

    $ git clone --depth 1 https://aur.archlinux.org/pacaur.git
    $ cd pacaur && makepkg PKGBUILD -i --needed


## Pacman tips & tricks

### Orphan packages

List orphan packages:

    $ pacman -Qdt

Remove orphan packages:

    $ pacman -Rns $(pacman -Qdtq)


### Clean the pacakge cache

    $ paccache -r
    $ paccache -ruk0

Consider creating a pacman hook to remove the pacakge cache. Create a file
`/etc/pacman.d/hooks/clean-pkg-cache.hook` with the following content:

    [Trigger]
    Operation = Upgrade
    Operation = Install
    Operation = Remove
    Type = Package
    Target = *

    [Action]
    Description = Clean the package cache…
    When = PostTransaction
    Exec = /usr/bin/paccache -r
    
    
    
    
    #commands
    
    pacman
======

view logs: /var/log/pacman.log

update system
# pacman -Syu

list installed packages
# pacman -Q

list packages no longer required by others
# pacman -Qdtq

search installed packages
# pacman -Qs <name>

search packages
# pacman -Ss <name>

install packages
# pacman -S <name>

remove package, its dependencies and config file backups
# pacman -Rns <name>

clean old packages in cache
# pacman -Sc

yaourt
======

same as pacman

systemd
=======

unit files: /usr/lib/systemd/system/ or /etc/systemd/system/

list running units
$ systemctl

check status
$ systemctl status <unit>

start/stop a service
# systemctl (start|stop) <unit>

enable/disable a service at bootup
# systemctl (enable|disable) <unit>

reload systemd
# systemctl daemon-reload

manual install of AUR packages
==============================

update repositories
# pacman -Sy

grab the package
$ curl -O <url> (e.g. https://aur.archlinux.org/packages/ya/yaourt/yaourt.tar.gz)

untar package
$ tar xzvf <package.tar.gz>

change into package directory
$ cd <package>

build and install
$ makepkg -si

java environments
=================

check status
$ archlinux-java status

set default version
# archlinux-java set <version>
