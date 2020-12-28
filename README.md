Four Leaves ISO
===============

<div align="center">
  <img alt="LaTeX" height="360px" vspace="" hspace="25" src="syslinux/splash-fourleaves.png">
</div>

Esta imagen debe [copiarse](https://github.com/jsamr/bootiso) en una memoria USB
(de preferencia de 8GB o más de almacenamiento).

Instalación de la herramienta [`archiso`](https://gitlab.archlinux.org/archlinux/archiso)
-----------------------------------------------------------------------------------------

```console
~ » yay -Sy archiso
~ » git clone --filter=blob:none --depth=1 git@github.com:four-leaves/four-leaves-iso.git
~ » sudo mkarchiso -v -w /archiso-tmp -o . four-leaves-iso
```

Estructura del directorio `/usr/share/archiso/configs`
------------------------------------------------------

```
├── baseline
│   ├── airootfs
│   ├── efiboot
│   ├── packages.x86_64
│   ├── pacman.conf
│   ├── profiledef.sh
│   └── syslinux
└── releng
    ├── airootfs
    │   ├── etc
    │   ├── root
    │   └── usr
    ├── efiboot
    ├── packages.x86_64
    ├── pacman.conf
    ├── profiledef.sh
    └── syslinux
38 directories
```

> **Consejo**:
> 
> Use la extensión [octotree](https://www.octotree.io) para visualizar
> los subdirectorios en la página del repositorio.

Nos enfocaremos en estudiar el perfil `releng` que está en `/usr/share/archiso/configs/releng`.
Como vimos en el diagrama de árbol de arriba, este comprende tres directorios:
`airootfs`, `efiboot`,  y `syslinux`. Veamos ahora en más detalle junto con los
archivos contenidos allá.

```
├── airootfs
│   ├── etc
│   │   ├── hostname
│   │   ├── locale.conf
│   │   ├── localtime -> /usr/share/zoneinfo/UTC
│   │   ├── mkinitcpio.conf
│   │   ├── mkinitcpio.d
│   │   │   └── linux.preset
│   │   ├── modprobe.d
│   │   │   └── broadcom-wl.conf
│   │   ├── motd
│   │   ├── passwd
│   │   ├── resolv.conf -> /run/systemd/resolve/stub-resolv.conf
│   │   ├── shadow
│   │   ├── ssh
│   │   │   └── sshd_config
│   │   ├── systemd
│   │   │   ├── journald.conf.d
│   │   │   │   └── volatile-storage.conf
│   │   │   ├── logind.conf.d
│   │   │   │   └── do-not-suspend.conf
│   │   │   ├── network
│   │   │   │   ├── 20-ethernet.network
│   │   │   │   └── 20-wireless.network
│   │   │   └── system
│   │   │       ├── choose-mirror.service
│   │   │       ├── dbus-org.freedesktop.network1.service -> /usr/lib/systemd/system/systemd-networkd.service
│   │   │       ├── dbus-org.freedesktop.resolve1.service -> /usr/lib/systemd/system/systemd-resolved.service
│   │   │       ├── etc-pacman.d-gnupg.mount
│   │   │       ├── getty@tty1.service.d
│   │   │       │   └── autologin.conf
│   │   │       ├── livecd-alsa-unmuter.service
│   │   │       ├── livecd-talk.service
│   │   │       ├── multi-user.target.wants
│   │   │       │   ├── choose-mirror.service -> ../choose-mirror.service
│   │   │       │   ├── iwd.service -> /usr/lib/systemd/system/iwd.service
│   │   │       │   ├── livecd-talk.service -> /etc/systemd/system/livecd-talk.service
│   │   │       │   ├── pacman-init.service -> ../pacman-init.service
│   │   │       │   ├── reflector.service -> /usr/lib/systemd/system/reflector.service
│   │   │       │   ├── systemd-networkd.service -> /usr/lib/systemd/system/systemd-networkd.service
│   │   │       │   └── systemd-resolved.service -> /usr/lib/systemd/system/systemd-resolved.service
│   │   │       ├── network-online.target.wants
│   │   │       │   └── systemd-networkd-wait-online.service -> /usr/lib/systemd/system/systemd-networkd-wait-online.service
│   │   │       ├── pacman-init.service
│   │   │       ├── reflector.service.d
│   │   │       │   └── archiso.conf
│   │   │       ├── sockets.target.wants
│   │   │       │   └── systemd-networkd.socket -> /usr/lib/systemd/system/systemd-networkd.socket
│   │   │       ├── sound.target.wants
│   │   │       │   └── livecd-alsa-unmuter.service -> ../livecd-alsa-unmuter.service
│   │   │       └── systemd-networkd-wait-online.service.d
│   │   │           └── wait-for-only-one-interface.conf
│   │   └── xdg
│   │       └── reflector
│   │           └── reflector.conf
│   ├── root
│   │   └── customize_airootfs.sh
│   └── usr
│       └── local
│           ├── bin
│           │   ├── choose-mirror
│           │   ├── Installation_guide
│           │   └── livecd-sound
│           └── share
│               └── livecd-sound
│                   └── asound.conf.in
├── efiboot
│   └── loader
│       ├── entries
│       │   ├── archiso-x86_64-linux.conf
│       │   └── archiso-x86_64-speech-linux.conf
│       └── loader.conf
├── packages.x86_64
├── pacman.conf
├── profiledef.sh
└── syslinux
    ├── archiso_head.cfg
    ├── archiso_pxe.cfg
    ├── archiso_pxe-linux.cfg
    ├── archiso_sys.cfg
    ├── archiso_sys-linux.cfg
    ├── archiso_tail.cfg
    ├── splash.png
    └── syslinux.cfg

29 directories, 55 files
```

## `airootfs`

## `efiboot`

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

# Paquetes de la versión lite

## Internet

- [networkmanager](https://www.archlinux.org/packages/extra/x86_64/networkmanager) 15.36MiB
- [firefox](https://www.archlinux.org/packages/extra/x86_64/firefox) 187.79MiB
- [brave-bin](https://aur.archlinux.org/packages/brave-bin) 241.53 MiB

## Utilidades

- [`yay`](https://aur.archlinux.org/packages/yay) 7.97MiB
- [`linux-firmware`](https://www.archlinux.org/packages/core/any/linux-firmware) 514.04MiB
- [`intel-media-driver`](https://www.archlinux.org/packages/community/x86_64/intel-media-driver) 34.99MiB
- [`nvidia-utils`](https://archlinux.org/packages/extra/x86_64/nvidia-utils) MiB
- [openssh](https://www.archlinux.org/packages/core/x86_64/openssh) 5.20MiB
- [`rar`](https://aur.archlinux.org/packages/rar) 1185.71KiB
- [`p7zip`](https://archlinux.org/packages/extra/x86_64/p7zip) 6.09 MiB
- [curl](https://www.archlinux.org/packages/core/x86_64/curl) 1647.57KiB
- [`httpie`](https://archlinux.org/packages/community/any/httpie) MiB
- [`curlie`](https://archlinux.org/packages/community/x86_64/curlie) MiB
- [`pdfarranger`](https://archlinux.org/packages/community/any/pdfarranger) 279.30 KiB

## Desarrollo

- [`git`](https://www.archlinux.org/packages/extra/x86_64/git) 38.36MiB
- [`github-cli`](https://archlinux.org/packages/community/x86_64/github-cli) 19.22 MiB
- [`cmake`](https://www.archlinux.org/packages/extra/x86_64/cmake) 39.25MiB
- [`docker`](https://www.archlinux.org/packages/community/x86_64/docker) 264.44MiB
- [`act`](https://aur.archlinux.org/packages/act) 15.38 MiB
- [`gitlab-runner`](https://archlinux.org/packages/community/x86_64/gitlab-runner) 44.10 MiB
- [`github-actions-bin`](https://aur.archlinux.org/packages/github-actions-bin) 197.57 MiB
- [`mongodb-bin`](https://aur.archlinux.org/packages/mongodb-bin) 128.49MiB
- [`mongodb-tools-bin`](https://aur.archlinux.org/packages/mongodb-tools-bin) 85.91MiB

## Documentos y textos

- [`nano`](https://archlinux.org/packages/core/x86_64/nano) 2.26 MiB
- [`emacs-lucid`](https://aur.archlinux.org/packages/emacs-lucid) 126.96MiB
- [`vscodium-bin`](https://aur.archlinux.org/packages/vscodium-bin) 238.55MiB
- [`visual-studio-code-bin`](https://aur.archlinux.org/packages/visual-studio-code-bin) 245.00 MiB
- [`zathura`](https://www.archlinux.org/packages/community/x86_64/zathura) 563.38KiB
- [`zathura-djvu`](https://www.archlinux.org/packages/community/x86_64/zathura-djvu) 27.23KiB
- [`zathura-pdf-poppler`](https://www.archlinux.org/packages/community/x86_64/zathura-pdf-poppler) 23.22KiB

# Paquete de la versión completa

## Ciencia

- [`racket`](https://www.archlinux.org/packages/community/x86_64/racket) 457.36MiB
- [`rstudio-desktop-bin`](https://aur.archlinux.org/packages/rstudio-desktop-bin) 487.40MiB
- [`octave`](https://www.archlinux.org/packages/community/x86_64/octave) 64.20 MiB
- [`mathpix-snipping-tool`](https://aur.archlinux.org/packages/mathpix-snipping-tool) 5.13MiB
- [`kotlin`](https://archlinux.org/packages/community/any/kotlin) MiB
- [`rust`](https://archlinux.org/packages/extra/x86_64/rust) 491.00 MiB
- [`sagemath`](https://www.archlinux.org/packages/community/x86_64/sagemath) 416.59MiB
- [`julia`](https://www.archlinux.org/packages/community/x86_64/julia) 198.22MiB
- [`fricas`](https://aur.archlinux.org/packages/fricas) 145.99MiB
- [`r`](https://www.archlinux.org/packages/extra/x86_64/r) 61.81MiB
- [`miniconda3`](https://aur.archlinux.org/packages/miniconda3) 387.19MiB
- [`python-poetry`](https://archlinux.org/packages/community/any/python-poetry) 1889.34 KiB
- [`cadabra2`](https://aur.archlinux.org/packages/cadabra2) 7.95 MiB
- [`texlive-core`](https://www.archlinux.org/packages/extra/any/texlive-core) 396.52MiB

## Otros

- [`ffmpeg`](https://archlinux.org/packages/extra/x86_64/ffmpeg) 32.37 MiB
- [`blender`](https://archlinux.org/packages/community/x86_64/blender) 286.24 MiB
- [`inkscape`](https://www.archlinux.org/packages/extra/x86_64/inkscape) 154.70 MiB
- [`openboard`](https://aur.archlinux.org/packages/openboard) 56.28MiB
- [`xournalpp`](https://archlinux.org/packages/community/x86_64/xournalpp) 4.24 MiB
- [`xdman`](https://aur.archlinux.org/packages/xdman) 81.94 MiB
- [`mat2`](https://archlinux.org/packages/community/any/mat2) 265.20 KiB
- [`imagine-git`](https://aur.archlinux.org/packages/imagine-git) 181.61 MiB
- [`okular`](https://archlinux.org/packages/extra/x86_64/okular) 15.80 MiB
- [`mariadb`](https://archlinux.org/packages/extra/x86_64/mariadb) MiB
- [`postgresql`](https://archlinux.org/packages/extra/x86_64/postgresql) MiB
- [`github-desktop-bin`](https://aur.archlinux.org/packages/github-desktop-bin) 224.86 MiB
- [`easystroke`](https://aur.archlinux.org/packages/easystroke) 1425.62 KiB
- [`anki`](https://archlinux.org/packages/community/x86_64/anki) 29.01 MiB
- [`languagetool`](https://archlinux.org/packages/community/any/languagetool) 288.96 MiB
- [`jabref`](https://aur.archlinux.org/packages/jabref) 211.91 MiB
- [`noto-fonts`](https://www.archlinux.org/packages/extra/any/noto-fonts) 91.19MiB
- [`ttf-monaco`](https://aur.archlinux.org/packages/ttf-monaco) 79.00KiB
- [`otf-san-francisco`](https://aur.archlinux.org/packages/otf-san-francisco) 7.06 MiB
- [`texlive-fontsextra`](https://www.archlinux.org/packages/extra/any/texlive-fontsextra) 1202.02MiB
- [`ttf-ms-fonts`](https://aur.archlinux.org/packages/ttf-ms-fonts) 5.42MiB

## Comunicaciones

- [`telegram-desktop`](https://www.archlinux.org/packages/community/x86_64/telegram-desktop) 43.41MiB
- [`discord`](https://archlinux.org/packages/community/x86_64/discord) 171.34 MiB
- [`whatsdesk-bin`](https://aur.archlinux.org/packages/whatsdesk-bin) 174.00 MiB
- [`signal-desktop`](https://archlinux.org/packages/community/x86_64/signal-desktop) 318.37 MiB
- [`element-desktop`](https://archlinux.org/packages/community/x86_64/element-desktop) 28.18 MiB
- [`criptext-bin`](https://aur.archlinux.org/packages/criptext-bin) 310.40 MiB
- [`zoom`](https://aur.archlinux.org/packages/zoom) 177.93 MiB

## Multimedia

- [svp](https://aur.archlinux.org/packages/svp) 37.85 MiB
- [obs-studio](https://www.archlinux.org/packages/community/x86_64/obs-studio) 13.48MiB
