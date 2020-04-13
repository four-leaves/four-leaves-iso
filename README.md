Four Leaves
===========

En caso de no poder instalar el programa [archiso](https://wiki.archlinux.org/index.php/Archiso),
puede guardar la imagen [ArchTeXlive](https://sourceforge.net/projects/archtexlive/)
en un usb (de preferencia de 8GB o más de almacenamiento) y ejecutar
siempre con usuario `root`.

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

> Consejo:
> 
> Use la extensión [octotree](https://www.octotree.io) para visualizar los subdirectorios en la página del repositorio.

Nos enfocaremos en estudiar el perfil releng en `archiso/configs/releng`.

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