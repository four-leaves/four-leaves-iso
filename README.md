Four Leaves ISO
===============

![](syslinux/splash-fourleaves.png)

En caso de no poder instalar el programa [archiso](https://wiki.archlinux.org/index.php/Archiso),
puede guardar la imagen [ArchTeXlive](https://sourceforge.net/projects/archtexlive/)
en una memoria USB (de preferencia de 8GB o más de almacenamiento) y ejecutar
siempre como usuario `root`.

Instalación de la herramienta `archiso`
---------------------------------------

```console
~ » yay -Sy archiso
:: Synchronizing package databases...
 core is up to date
 extra is up to date
 community is up to date
 multilib is up to date
resolving dependencies...
looking for conflicting packages...

Package (4)                 New Version  Net Change  Download Size

extra/arch-install-scripts  23-1           0.04 MiB       0.01 MiB
extra/lynx                  2.8.9-2        4.99 MiB       1.14 MiB
community/squashfs-tools    4.4-1          0.31 MiB       0.11 MiB
extra/archiso               43-1           0.12 MiB       0.07 MiB

Total Download Size:   1.33 MiB
Total Installed Size:  5.46 MiB

:: Proceed with installation? [Y/n] y
:: Retrieving packages...
 arch-install-scripts-23-1-any                                                13.8 KiB  4.49 MiB/s 00:00 [##############################################################] 100%
 lynx-2.8.9-2-x86_64                                                        1166.6 KiB  1716 KiB/s 00:01 [##############################################################] 100%
 archiso-43-1-any                                                             69.7 KiB  2.84 MiB/s 00:00 [##############################################################] 100%
 squashfs-tools-4.4-1-x86_64                                                 108.7 KiB  2.41 MiB/s 00:00 [##############################################################] 100%
(4/4) checking keys in keyring                                                                           [##############################################################] 100%
(4/4) checking package integrity                                                                         [##############################################################] 100%
(4/4) loading package files                                                                              [##############################################################] 100%
(4/4) checking for file conflicts                                                                        [##############################################################] 100%
(4/4) checking available disk space                                                                      [##############################################################] 100%
:: Processing package changes...
(1/4) installing arch-install-scripts                                                                    [##############################################################] 100%
(2/4) installing squashfs-tools                                                                          [##############################################################] 100%
(3/4) installing lynx                                                                                    [##############################################################] 100%
(4/4) installing archiso                                                                                 [##############################################################] 100%
:: Running post-transaction hooks...
(1/2) Arming ConditionNeedsUpdate...
(2/2) Updating linux initcpios...
==> Building image from preset: /etc/mkinitcpio.d/linux.preset: 'default'
  -> -k /boot/vmlinuz-linux -c /etc/mkinitcpio.conf -g /boot/initramfs-linux.img
==> Starting build: 5.6.3-arch1-1
  -> Running build hook: [base]
  -> Running build hook: [udev]
  -> Running build hook: [autodetect]
  -> Running build hook: [modconf]
  -> Running build hook: [block]
  -> Running build hook: [filesystems]
  -> Running build hook: [keyboard]
  -> Running build hook: [fsck]
==> Generating module dependencies
==> Creating gzip-compressed initcpio image: /boot/initramfs-linux.img
==> Image generation successful
==> Building image from preset: /etc/mkinitcpio.d/linux.preset: 'fallback'
  -> -k /boot/vmlinuz-linux -c /etc/mkinitcpio.conf -g /boot/initramfs-linux-fallback.img -S autodetect
==> Starting build: 5.6.3-arch1-1
  -> Running build hook: [base]
  -> Running build hook: [udev]
  -> Running build hook: [modconf]
  -> Running build hook: [block]
  -> Running build hook: [filesystems]
  -> Running build hook: [keyboard]
  -> Running build hook: [fsck]
==> Generating module dependencies
==> Creating gzip-compressed initcpio image: /boot/initramfs-linux-fallback.img
==> Image generation successful
```

Estructura del directorio `/usr/share/archiso`
----------------------------------------------

```
archiso
└── configs
    ├── baseline
    │   ├── isolinux
    │   └── syslinux
    └── releng
        ├── airootfs
        │   ├── etc
        │   │   ├── modprobe.d
        │   │   ├── systemd
        │   │   │   ├── scripts
        │   │   │   └── system
        │   │   │       └── getty@tty1.service.d
        │   │   └── udev
        │   │       └── rules.d
        │   └── root
        ├── efiboot
        │   └── loader
        │       └── entries
        ├── isolinux
        └── syslinux

20 directories
```

> **Consejo**:
> 
> Use la extensión [octotree](https://www.octotree.io) para visualizar
> los subdirectorios en la página del repositorio.

Nos enfocaremos en estudiar el perfil `releng` que está en `archiso/configs/releng`.
Como vimos en el diagrama de árbol de arriba, este comprende cuatro
directorios: `airootfs`, `efiboot`, `isolinux` y `syslinux`. Veamos
ahora en más detalle junto con los archivos contenidos allá.

```
releng
├── airootfs
│   ├── etc
│   │   ├── fstab
│   │   ├── hostname
│   │   ├── locale.conf
│   │   ├── machine-id
│   │   ├── modprobe.d
│   │   │   └── broadcom-wl.conf
│   │   ├── systemd
│   │   │   ├── scripts
│   │   │   │   └── choose-mirror
│   │   │   └── system
│   │   │       ├── choose-mirror.service
│   │   │       ├── etc-pacman.d-gnupg.mount
│   │   │       ├── getty@tty1.service.d
│   │   │       │   └── autologin.conf
│   │   │       └── pacman-init.service
│   │   └── udev
│   │       └── rules.d
│   │           └── 81-dhcpcd.rules
│   └── root
│       ├── customize_airootfs.sh
│       └── install.txt
├── build.sh
├── efiboot
│   └── loader
│       ├── entries
│       │   ├── archiso-x86_64-cd.conf
│       │   ├── archiso-x86_64-usb.conf
│       │   ├── uefi-shell-v1-x86_64.conf
│       │   └── uefi-shell-v2-x86_64.conf
│       └── loader.conf
├── isolinux
│   └── isolinux.cfg
├── mkinitcpio.conf
├── packages.x86_64
├── pacman.conf
└── syslinux
    ├── archiso.cfg
    ├── archiso_head.cfg
    ├── archiso_pxe.cfg
    ├── archiso_sys.cfg
    ├── archiso_tail.cfg
    ├── splash.png
    └── syslinux.cfg

15 directories, 30 files
```

## `airootfs`

## `efiboot`

## `isolinux`

## `syslinux`

Ejemplo del archivo `packages.x86_64`
-------------------------------------

```
arch-install-scripts
b43-fwcutter
broadcom-wl
btrfs-progs
clonezilla
crda
darkhttpd
ddrescue
dhclient
dhcpcd
dialog
diffutils
dmraid
dnsmasq
dnsutils
dosfstools
elinks
ethtool
exfat-utils
f2fs-tools
fsarchiver
gnu-netcat
gpm
gptfdisk
grml-zsh-config
grub
hdparm
ipw2100-fw
ipw2200-fw
irssi
iwd
jfsutils
lftp
linux-atm
linux-firmware
lsscsi
lvm2
man-db
man-pages
mc
mdadm
mtools
nano
ndisc6
netctl
nfs-utils
nilfs-utils
nmap
ntfs-3g
ntp
openconnect
openssh
openvpn
partclone
parted
partimage
ppp
pptpclient
refind-efi
reiserfsprogs
rp-pppoe
rsync
sdparm
sg3_utils
smartmontools
sudo
tcpdump
testdisk
usb_modeswitch
usbutils
vi
vim-minimal
vpnc
wget
wireless-regdb
wireless_tools
wpa_supplicant
wvdial
xfsprogs
xl2tpd
```

* [arch-install-scripts](https://git.archlinux.org/arch-install-scripts.git)
* [b43-fwcutter](https://wireless.wiki.kernel.org/en/users/Drivers/b43)
* [broadcom-wl](https://www.broadcom.com/support/download-search)
* [btrfs-progs](https://btrfs.wiki.kernel.org/index.php/Main_Page)
* [clonezilla](https://clonezilla.org)
* [crda](https://wireless.wiki.kernel.org/en/developers/regulatory/crda)
* [darkhttpd](https://unix4lyfe.org/darkhttpd)
* [ddrescue](https://www.gnu.org/software/ddrescue/ddrescue.html)
* [dhclient](https://www.isc.org/dhcp)
* [dhcpcd](https://roy.marples.name/projects/dhcpcd)
* [dialog](https://invisible-island.net/dialog)
* [diffutils](https://www.gnu.org/software/diffutils)
* [dmraid](https://people.redhat.com/~heinzm/sw/dmraid)
* [dnsmasq](http://www.thekelleys.org.uk/dnsmasq/doc.html)
* [dnsutils](https://www.isc.org/bind)
* [dosfstools](https://github.com/dosfstools/dosfstools)
* [elinks](http://elinks.or.cz)
* [ethtool](https://mirrors.edge.kernel.org/pub/software/network/ethtool)
* [exfat-utils](https://github.com/relan/exfat)
* [f2fs-tools](https://git.kernel.org/pub/scm/linux/kernel/git/jaegeuk/f2fs-tools.git/about)
* [fsarchiver](http://www.fsarchiver.org)
* [gnu-netcat](http://netcat.sourceforge.net)
* [gpm](https://www.nico.schottelius.org/software/gpm)
* [gptfdisk](https://www.rodsbooks.com/gdisk)
* [grml-zsh-config](https://grml.org/zsh)
* [grub](https://www.gnu.org/software/grub/)
* [hdparm](https://sourceforge.net/projects/hdparm)
* [ipw2100-fw](http://ipw2100.sourceforge.net)
* [ipw2200-fw](http://ipw2200.sourceforge.net)
* [irssi](https://irssi.org)
* [iwd](https://git.kernel.org/pub/scm/network/wireless/iwd.git)
* [jfsutils](http://jfs.sourceforge.net)
* [lftp](https://lftp.yar.ru)
* [linux-atm](http://linux-atm.sourceforge.net)
* [linux-firmware](https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git)
* [lsscsi](http://sg.danny.cz/scsi/lsscsi.html)
* [lvm2](https://sourceware.org/lvm2)
* [man-db](https://www.nongnu.org/man-db)
* [man-pages](http://man7.org/linux/man-pages/index.html)
* [mc](https://midnight-commander.org)
* [mdadm](https://git.kernel.org/pub/scm/utils/mdadm)
* [mtools](https://www.gnu.org/software/mtools)
* [nano](https://www.nano-editor.org)
* [ndisc6](https://www.remlab.net/ndisc6)
* [netctl](https://git.archlinux.org/netctl.git)
* [nfs-utils](http://nfs.sourceforge.net)
* [nilfs-utils](https://nilfs.sourceforge.io/en)
* [nmap](https://nmap.org)
* [ntfs-3g](https://www.tuxera.com/community/open-source-ntfs-3g)
* [ntp](http://www.ntp.org)
* [openconnect](https://www.infradead.org/openconnect)
* [openssh]()
* [openvpn](https://openvpn.net/community)
* [partclone](https://partclone.org)
* [ppp](https://ppp.samba.org)
* [pptpclient](http://pptpclient.sourceforge.net)
* [refind-efi](https://www.rodsbooks.com/refind/index.html)
* [reiserfsprogs](https://reiser4.wiki.kernel.org/index.php/Reiserfsprogs)
* [rp-pppoe](https://dianne.skoll.ca/projects/rp-pppoe)
* [rsync](https://rsync.samba.org)
* [sdparm](http://sg.danny.cz/sg/sdparm.html)
* [sg3_utils](http://sg.danny.cz/sg/sg3_utils.html)
* [smartmontools](https://www.smartmontools.org)
* [sudo](https://www.sudo.ws/sudo)
* [tcpdump](https://www.tcpdump.org)
* [testdisk](https://www.cgsecurity.org/wiki/TestDisk)
* [usb_modeswitch](https://www.draisberghof.de/usb_modeswitch)
* [usbutils](http://linux-usb.sourceforge.net)
* [vi](http://ex-vi.sourceforge.net)
* [vim-minimal](https://www.vim.org)
* [vpnc](https://github.com/streambinder/vpnc)
* [wget](https://www.gnu.org/software/wget/wget.html)
* [wireless-regdb](https://wireless.wiki.kernel.org/en/developers/regulatory)
* [wireless_tools](https://hewlettpackard.github.io/wireless-tools/Tools.html)
* [wpa_supplicant](https://hostap.epitest.fi/wpa_supplicant)
* [wvdial](https://web.archive.org/web/20110504183753/http://alumnit.ca:80/wiki/index.php?page=WvDial)
* [xfsprogs](https://xfs.org/index.php/Main_Page)
* [xl2tpd](https://www.xelerance.com/archives/202)

Ejemplo del archivo `pacman.conf`
---------------------------------

```
#
# /etc/pacman.conf
#
# See the pacman.conf(5) manpage for option and repository directives

#
# GENERAL OPTIONS
#
[options]
# The following paths are commented out with their default values listed.
# If you wish to use different paths, uncomment and update the paths.
#RootDir     = /
#DBPath      = /var/lib/pacman/
#CacheDir    = /var/cache/pacman/pkg/
#LogFile     = /var/log/pacman.log
#GPGDir      = /etc/pacman.d/gnupg/
#HookDir     = /etc/pacman.d/hooks/
HoldPkg     = pacman glibc
#XferCommand = /usr/bin/curl -L -C - -f -o %o %u
#XferCommand = /usr/bin/wget --passive-ftp -c -O %o %u
#CleanMethod = KeepInstalled
Architecture = auto

# Pacman won't upgrade packages listed in IgnorePkg and members of IgnoreGroup
#IgnorePkg   =
#IgnoreGroup =

#NoUpgrade   =
#NoExtract   =

# Misc options
#UseSyslog
#Color
#TotalDownload
CheckSpace
#VerbosePkgLists

# By default, pacman accepts packages signed by keys that its local keyring
# trusts (see pacman-key and its man page), as well as unsigned packages.
SigLevel    = Required DatabaseOptional
LocalFileSigLevel = Optional
#RemoteFileSigLevel = Required

# NOTE: You must run `pacman-key --init` before first using pacman; the local
# keyring can then be populated with the keys of all official Arch Linux
# packagers with `pacman-key --populate archlinux`.

#
# REPOSITORIES
#   - can be defined here or included from another file
#   - pacman will search repositories in the order defined here
#   - local/custom mirrors can be added here or in separate files
#   - repositories listed first will take precedence when packages
#     have identical names, regardless of version number
#   - URLs will have $repo replaced by the name of the current repo
#   - URLs will have $arch replaced by the name of the architecture
#
# Repository entries are of the format:
#       [repo-name]
#       Server = ServerName
#       Include = IncludePath
#
# The header [repo-name] is crucial - it must be present and
# uncommented to enable the repo.
#

# The testing repositories are disabled by default. To enable, uncomment the
# repo name header and Include lines. You can add preferred servers immediately
# after the header, and they will be used before the default mirrors.

#[testing]
#Include = /etc/pacman.d/mirrorlist

[core]
Include = /etc/pacman.d/mirrorlist

[extra]
Include = /etc/pacman.d/mirrorlist

#[community-testing]
#Include = /etc/pacman.d/mirrorlist

[community]
Include = /etc/pacman.d/mirrorlist

# If you want to run 32 bit applications on your x86_64 system,
# enable the multilib repositories as required here.

#[multilib-testing]
#Include = /etc/pacman.d/mirrorlist

#[multilib]
#Include = /etc/pacman.d/mirrorlist

# An example of a custom package repository.  See the pacman manpage for
# tips on creating your own repositories.
#[custom]
#SigLevel = Optional TrustAll
#Server = file:///home/custompkgs
```

# Comunicaciones

[realvnc-vnc-viewer 6.20.113-3](https://aur.archlinux.org/packages/realvnc-vnc-viewer) 7.60MiB
[yay](https://github.com/Jguer/yay) 6.26MiB
[telegram-desktop](https://www.archlinux.org/packages/community/x86_64/telegram-desktop) 43.41MiB
[texlive-fontsextra](https://www.archlinux.org/packages/extra/any/texlive-fontsextra) 1202.02MiB
[linux-firmware](https://www.archlinux.org/packages/core/any/linux-firmware) 514.04MiB
[rstudio-desktop-bin](https://aur.archlinux.org/packages/rstudio-desktop-bin) 487.40MiB
[racket](https://www.archlinux.org/packages/community/x86_64/racket) 457.36MiB
[sagemath](https://www.archlinux.org/packages/community/x86_64/sagemath) 416.59MiB
[texlive-core](https://www.archlinux.org/packages/extra/any/texlive-core) 396.52MiB
[miniconda3](https://aur.archlinux.org/packages/miniconda3) 387.19MiB
[docker](https://www.archlinux.org/packages/community/x86_64/docker) 264.44MiB
[vscodium-bin](https://aur.archlinux.org/packages/vscodium-bin) 238.55MiB
[firefox](https://www.archlinux.org/packages/extra/x86_64/firefox) 187.79MiB
[julia](https://www.archlinux.org/packages/community/x86_64/julia) 198.22MiB
[fricas](https://aur.archlinux.org/packages/fricas) 145.99MiB
[mongodb-bin](https://aur.archlinux.org/packages/mongodb-bin) 128.49MiB
[inkscape](https://www.archlinux.org/packages/extra/x86_64/inkscape) 124.00MiB
[emacs-lucid](https://aur.archlinux.org/packages/emacs-lucid) 126.96MiB
[mongodb-tools-bin](https://aur.archlinux.org/packages/mongodb-tools-bin) 85.91MiB
[noto-fonts](https://www.archlinux.org/packages/extra/any/noto-fonts) 91.19MiB
[octave](https://www.archlinux.org/packages/community/x86_64/octave) 65.52MiB
[openboard](https://aur.archlinux.org/packages/openboard) 56.60MiB
[cmake](https://www.archlinux.org/packages/extra/x86_64/cmake) 39.25MiB
[git](https://www.archlinux.org/packages/extra/x86_64/git) 38.36MiB
[intel-media-driver](https://www.archlinux.org/packages/community/x86_64/intel-media-driver) 34.99MiB
[grub](https://www.archlinux.org/packages/core/x86_64/grub) 32.53MiB
[zathura-djvu](https://www.archlinux.org/packages/community/x86_64/zathura-djvu) 27.23KiB
[zathura-pdf-poppler](https://www.archlinux.org/packages/community/x86_64/zathura-pdf-poppler) 23.22KiB
[ttf-monaco](https://aur.archlinux.org/packages/ttf-monaco) 79.00KiB
[zathura](https://www.archlinux.org/packages/community/x86_64/zathura) 563.38KiB
[rar](https://aur.archlinux.org/packages/rar) 1185.71KiB
[curl](https://www.archlinux.org/packages/core/x86_64/curl) 1647.57KiB
[ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts) 5.42MiB
[mathpix-snipping-tool](https://aur.archlinux.org/packages/mathpix-snipping-tool) 5.13MiB
[openssh](https://www.archlinux.org/packages/core/x86_64/openssh) 5.20MiB
[obs-studio](https://www.archlinux.org/packages/community/x86_64/obs-studio) 13.48MiB
[networkmanager](https://www.archlinux.org/packages/extra/x86_64/networkmanager) 15.36MiB
[r](https://www.archlinux.org/packages/extra/x86_64/r) 61.81MiB
https://aur.archlinux.org/packages/cadabra2
7.95 MiB cadabra2 http://cadabra.science
easystroke 1425.62 KiB http://easystroke.sourceforge.net/
anki 29.01 MiB https://ankisrs.net
github-desktop-bin 224.86 MiB https://desktop.github.com