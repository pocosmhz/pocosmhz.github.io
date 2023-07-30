---
layout: single
status: publish
title: "A retro battlestation: Making of (II)"
tags: [retro]
comments: true
author: manuel_molina
author_profile: true
categories: []
published: true
date: '2023-03-25 19:40:56 +0100'
date_gmt: '2023-03-25 19:40:56 +0100'
excerpt_separator: <!--more-->
---
I was not really very happy with my experience using Windows XP at the end of my [previous post]({% post_url 2023-03-18-retrobattlestation-making-of %}).

Thus, I'll try to go for a real, updated operating system.
<!--more-->
Of course, due to the limitations of the hardware, the choices are limited:
- Linux. Not possible with current distributions, due to the minimum RAM required.
  - [Arch Linux](https://archlinux.org/) requires 512 MBytes RAM to begin with. Also, only available for x86-64 architecture.
  - [Debian GNU/Linux](https://www.debian.org/). Although it's available for 32-bit PCs, it asks for 485 MBytes RAM for standard installation.
- [NetBSD](https://www.netbsd.org/). It's an option, indeed. It will work.
> NetBSD 9.3 runs on all i486 or later PC-compatible systems with 1 to 32 processors. The minimal configuration for a full, standard installation is 32MB of RAM and 250MB of disk space.
- [FreeBSD](https://www.freebsd.org). This is another good candidate, widely maintained, and *might* fit with the hardware requirements. Processor-wise, it's ok. However, memory-wise could be a bit tight. Also, I've read that installing on something under 1 GB RAM is not recommended.
- [OpenBSD](https://www.openbsd.org/). This is the secure version and ... why not?

# OpenBSD installation media
You can get `install72.iso` for i386 architecture from [here](https://cdn.openbsd.org/pub/OpenBSD/7.2/i386/install72.img)

# Installation
Let's install version 7.2. This laptop has not option to boot from USB drive.
Once we boot into the *physical* CD-ROM I toasted, we get this:
```
CD-ROM: 82
Loading /7.2/I386/CDBOOT
probing: pc0 com0 apm pci mem[639K 95M a20=on]
disk: fd0 hd0+* cd0
>> OpenBSD/i386 CDBOOT 3.44
boot>
```

## Boot
We go ahead by hitting enter and then the boot process starts.
```
Welcome to the OpenBSD/i386 7.2 installation program.
(I)nstall, (U)pgrade, (A)utoinstall or (S)hell?
```

As we want to use full disk encryption for security reasons, we'll follow the [corresponding section](https://www.openbsd.org/faq/faq14.html#softraidFDE) of their FAQ, and select *(S)hell*.

## Full disk encryption
However, the tutorial there assumes you're partitioning the whole disk for OpenBSD. As I'm doing a dual-boot, we'll do slight changes to the process, as detailed in [this Reddit post](https://www.reddit.com/r/openbsd/comments/m0b7wt/comment/gq7088o/)
```
# cd /dev
# sh MAKEDEV wd0
# fdisk -e wd0
Enter 'help' for information
wd0: 1>
```
We ask for `print` to see what is the first available partition. It is 1, as we only have one busy (0).

```
wd0: 1> edit 1
            Starting          Ending        LBA Info:
 #: id      C   H   S -       C   H   S [      start:        size ]
------------------------------------------------------------------------------
 1: 00      0   0   0 -       0   0   0 [          0:           0 ] unused
 Partition id ('0' to disable) [01 - FF] [00] (? for help)
```
We select `A6` as the partition type.
```
Do you wish to edit in CHS mode? [n]
```
We continue without CHS mode (default).
```
Partition offset [0 - 39070079]: [0] 10490446
Partition size [1 - 28579634]: [1] 28579634
```
Now we save the changes by quitting this way:
```
wd0*: 1> quit
Writing MBR at offset 0.
```
Once we save the partition table, we must edit OpenBSD partition and add `a` partition type (RAID) with:
```
# disklabel -E wd0
Label editor (enter '?' for help at any prompt)
wd0> a a
offset: [10490446]
size: [28579634]
FS type: [RAID]
wd0* > q
Write new label?: [y]
```
Let's create the encrypted disk:
```
# bioctl -c C -l wd0a softraid0
New passphrase: XXXXX
Re-type passphrase: XXXXX
sd0 at scsibus1 targ 1 lun 0: <OPENBSD, SR CRYPTO, 006>
sd0: 13954MB, 512 bytes/sector, 28579106 sectors
softraid0: CRYPTO volume attached as sd0
# cd /dev
# sh MAKEDEV sd0
```
Exit the shell and then continue with installation.

## Installation part 2
- Select `I` for *(I)nstall*
- Choose your keyboard layout: `es`
- Enter hostname: `toshi01`

It's time now for an initial network configuration.

### Network configuration
PCMCIA card 3COM 3CXE589DT is installed, and will be available for the following stage:
```
Available network interfaces are: ep0 vlan0
Which network interface do you wish to configure? (or 'done') [ep1]
IPv4 address for ep1? (or 'autoconf' or 'none') [autoconf]
IPv6 address for ep1? (or 'autoconf' or 'none') [none]
Available network interfaces are: ep0 vlan0
Which network interface do you wish to configure? (or 'done') [done]
Using DNS domainname my.domain
Using DNS nameservers at 192.168.18.1
```

### Root user account
When requested, issue the password for `root` user.
```
Password for root account? (will not echo)
Password for root account? (again)
Start sshd(8) by default? [yes]
```

### X Window System
We'll be asked about X Window System:
```
Do you expect to run the X Window System? [yes]
Do you want the X Window System to be started by xenodm(1) [no]
Change the default console to com0? [no]
```

### User configuration and timezone
```
Setup a user? (enter a lower-case loginname, or 'no') [no] manuelmc
Full name for user manuelmc? [manuelmc] Manuel Molina
Password for user manuelmc? (will not echo)
Password for user manuelmc? (again)
WARNING: root is targeted by password guessing attacks, pubkeys are safer.
Allow root ssh login? (yes, no, prohibit-password) [no]
What timezone are you in? ('?' for list) [Europe/Madrid]
```

### Disk partitioning
Bear in mind that we're going to partition the encrypted disk `sd0`:
```
Available disks are: wd0 sd0.
Which disk is the root disk? ('?' for details) [wd0] sd0
MBR has invalid signature; not showing it.
Use (W)hole disk or (E)dit the MBR? [whole]
Setting OpenBSD MBR partition to whole sd0...done.
The auto-allocated layout for sd0 is:
#                size           offset  fstype [fsize bsize   cpg]
  a:           293.1M               64  4.2BSD   2048 16384     1  # /
  b:           191.2M           600256    swap
  c:         13954.6M                0  unused
  d:           348.9M           991936  4.2BSD   2048 1638      1  # /tmp
  e:           452.0M          1706464  4.2BSD   2048 1638      1  # /var

  f:          1786.1M          2632096  4.2BSD   2048 1638      1  # /usr
  g:           469.8M          6290080  4.2BSD   2048 1638      1  # /usr/X11R6
  h:          1453.2M          7252288  4.2BSD   2048 1638      1  # /usr/local
  i:          1557.2M         10228416  4.2BSD   2048 1638      1  # /usr/src
  j:          5234.5M         13417600  4.2BSD   2048 1638      1  # /usr/obj
  k:          2168.6M         24137760  4.2BSD   2048 1638      1  # /home
Use (A)uto layout, (E)dit auto layout, or create (C)ustom layout? [a] E
```
We're going to edit this, as I feel I won't have enough swap space.
```
Label editor (enter '?' for help at any prompt)
sd0> d d
sd0*> d e
sd0*> d f
sd0*> d g
sd0*> d h
sd0*> d i
sd0*> d j
sd0*> d k
sd0*> c b
Partition b is currently 391664 sectors in size, and can have a maximum
size of 27978850 sectors.
size: [391664] 783328
sd0*> a
partition: [d]
offset: [1383584]
size: [27195522] 714528
FS type: [4.2BSD]
mount point: [none] /tmp
sd0*> a
partition: [e]
offset: [2098112]
size: [26480994] 925632
FS type: [4.2BSD]
mount point: [none] /var
sd0*> a
partition: [f]
offset: [3023744]
size: [25555362] 3657984
FS type: [4.2BSD]
mount point: [none] /usr
sd0*> a
partition: [g]
offset: [6681728]
size: [21897378] 962208
FS type: [4.2BSD]
mount point: [none] /usr/X11R6
sd0*> a
partition: [h]
offset: [7643936]
size: [20935170] 2976128
FS type: [4.2BSD]
mount point: [none] /usr/local
sd0*> a
partition: [i]
offset: [10620064]
size: [17959042] 3189184
FS type: [4.2BSD]
mount point: [none] /usr/src
sd0*> a
partition: [j]
offset: [13809248]
size: [14769858] 10720160
FS type: [4.2BSD]
mount point: [none] /usr/obj
sd0*> a
partition: [k]
offset: [24529408]
size: [4049698]
FS type: [4.2BSD]
mount point: [none] /home
sd0*> q
Write new label?: [y]
```
Partition slices are created now. Once done, we'll continue
```
Available disks are: wd0.
Which disk do you wish to initialize? (or 'done') [done]
```

### Software set installation
The temporary mount points for installation are mounted now.
```
Let's install the sets!
Location of sets? (cd0 disk http or 'done') [cd0]
Pathname to the sets? (or 'done') [7.2/i386]

Select sets by entering a set name, a file name pattern or 'all'. De-select
sets by prepending a '-', e.g.: '-game*'. Selected sets are labelled '[X]'.
    [X] bsd           [X] comp72.tgz    [X] xbase72.tgz   [X] xserv72.tgz
    [X] bsd.rd        [X] man72.tgz     [X] xshare72.tgz
    [X] base72.tgz    [X] game72.tgz    [X] xfont72.tgz
Set name(s) (or 'abourt' or 'done') [done]
Directory does not contain SHA256.sig. Continue without verification? [no] yes
```
Now it's time to install all the sets. It will take about 25 minutes.

After all sets are copied, we get:
```
Location of sets? (cd0 disk http or 'done') [done]
Time appears wrong.  Set to 'Sat Mar 25 22:48:57 CET 2023'? [yes]
Saving configuration files... done.
Making all device nodes... done.
fw_update: added none; updated none; kept none
Relinking to create unique kernel... done.

CONGRATULATIONS! Your OpenBSD install has been successfully completed!

When you login to your new system the first time, please read your mail
using the 'mail' command.

Exit to (S)hell, (H)alt or (R)eboot? [reboot]
```
At this point we can:
- Reboot. We can boot from the freshly installed OpenBSD by typing this at the OpenBSD Install CD-ROM boot prompt:
   ```
   b sr0a:/bsd
   ```
   We'll be requested to enter the encryption password.
- Exit to a shell, where we will gather the required data to build a dual boot system together with Windows XP.

## Dual boot
Following [this guide](https://cromwell-intl.com/open-source/multiboot-windows-openbsd/) for Windows 7 or [this one](https://www.aleph0.com/computing/openbsd/dualboot/) for Windows XP, we will need a copy of the OpenBSD Partition Boot Record or PBR, the boot block from the partition holding OpenBSD.

From a shell, we will mount an external device where we'll save it:
```
toshi01# dd if=/dev/rwd0a of=/mnt/openbsd.pbr bs=512 count=1
1+0 records in
1+0 records out
512 bytes transferred in 0.011 secs (45491 bytes/sec)
toshi01# umount /mnt
```
**Be aware!** We're copying the PBR from the physical drive, container of the encrypted drive. That is, from `/dev/rwd0a` instead of `/dev/rsd0a`.

And now under Windows XP:
```
C:\>md boot
C:\>copy e:\openbsd.pbr c:\boot
        1 archivos copiados.
```
Open the Start Menu, right-click on My Computer, and choose “Properties”. Click on the “Advanced” tab, click the “Settings” button under “Startup Recovery”, and under “System Startup” click “Edit”. Add `C:\boot\openbsd.pbr="OpenBSD"` to the end of the file, and save it.

Now you can reboot. You'll be automatically offered a boot menu.

As the hardware clock will be set by Windows XP, we have to add an offset to the current time on OpenBSD. According to the [FAQ](https://www.openbsd.org/faq/faq10.html#OpenNTPD), we must do:
```
toshi01# echo "kern.utc_offset=-120" >> /etc/sysctl.conf
```

# Post installation
After having a booting system, we'll take care of initial configuration steps.

## Disabling double encryption of swap space
OpenBSD encrypts swap space by default. As we have opted for a full disk encryption, we're encrypting this content twice.

In order to prevent that (which makes no real sense), we're going to add a `sysctl` setting and reboot the system:
```
toshi01# echo "vm.swapencrypt.enable=0" >> /etc/sysctl.conf
toshi01# sync ; shutdown -r now
```

## X Window configuration

### startx
Let's try to start X Window as `root` user just for testing purposes:
```
toshi01# startx
...
xinit: giving up
xinit: unable to connect to X server: Connection refused
xinit: server error
xauth: (argv):1:  bad display name "toshi01.my.domain:0" in "remove" command
```
Not much luck here.
Let's check the logs:
```
toshi01# grep EE /var/log/Xorg.0.log
	(WW) warning, (EE) error, (NI) not implemented, (??) unknown.
[  6296.734] (EE) Failed to load module "s3virge" (module does not exist, 0)
[  6297.060] (EE) VESA(0): Specified fbbpp (24) is not a permitted value
[  6297.064] (EE) Screen(s) found, but none have a usable configuration.
[  6297.065] (EE)
[  6297.065] (EE) no screens found(EE)
[  6297.066] (EE)
[  6297.066] (EE) Please also check the log file at "/var/log/Xorg.0.log" for additional information.
[  6297.066] (EE)
[  6297.084] (EE) Server terminated with error (1). Closing log file.
```
This laptop has a S3 ViRGE MX graphics card, whose X video driver was [removed](https://www.openbsd.org/faq/upgrade66.html) from packaged X Window distribution in OpenBSD 6.6, on October 2019.

We can either:
- Build Xenocara from scratch: Continue reading [here](https://github.com/openbsd/xenocara/blob/master/README). **Spoiler:** It's no longer possible as the `s3virge` driver has been sent to the *attic* (deleted, in CVS terms) in their [current CVS tree](https://cvsweb.openbsd.org/cgi-bin/cvsweb/~checkout~/xenocara/driver/xf86-video-s3virge/).
- Use the [Generic VESA video driver](https://man.openbsd.org/vesa.4), which is a totally valid option for an old and only 2D accelerated video card.

### X config file
We need to set up a default `bpp` of 16 to being able to start up this.
The command-line equivalent is:
```
toshi01# startx -- -depth 16
```
And now it looks better:
![FVWM first view](/assets/images/2023-03-25-retrobattlestation-making-of-part-2/fvwm.png)

By the way, the screenshot was taken thanks to the [script](https://thorstenzoeller.com/screenshots-on-openbsd/) and directions from [Thorsten Zöller](https://thorstenzoeller.com/).

So, I need a valid depth + mode configuration. I took a sample one from [here](https://askubuntu.com/a/108564). Let's commit this single change as a default configuration for the sake of the test. Our Xorg config file looks like this:
```
toshi01# cat /etc/X11/xorg.conf
Section "Device"
    Identifier    "Configured Video Device"
EndSection

Section "Monitor"
    Identifier    "Configured Monitor"
    HorizSync       30.0-62.0
    VertRefresh     50.0-70.0
EndSection

Section "Screen"
    Identifier    "Default Screen"
    Monitor        "Configured Monitor"
    Device        "Configured Video Device"
    DefaultDepth    16
    SubSection "Display"
        Depth    16
        Modes     "800x600"
    EndSubSection
EndSection
```

### IceWM configuration
We look for a [X window manager](https://en.wikipedia.org/wiki/X_window_manager) with lower memory impact.
My choice is [IceWM](https://en.wikipedia.org/wiki/IceWM) instead of the default [fvwm](https://en.wikipedia.org/wiki/FVWM). Besides resource usage, there is the factor that it is being maintained.
We have to install it first:
```
toshi01# pkg_add -v icewm
Update candidates: quirks-6.42 -> quirks-6.42
quirks-6.42 signed on 2023-03-21T19:31:22Z
icewm-2.9.9:libao-1.2.0p1: ok
icewm-2.9.9:graphite2-1.3.14: ok
icewm-2.9.9:lzo2-2.10p2: ok
icewm-2.9.9:png-1.6.37p0: ok
icewm-2.9.9:xz-5.2.5p2: ok
icewm-2.9.9:sqlite3-3.39.3: ok
icewm-2.9.9:bzip2-1.0.8p0: ok
icewm-2.9.9:libffi-3.4.2: ok
icewm-2.9.9:python-3.9.16: ok
icewm-2.9.9:pcre-8.44: ok
icewm-2.9.9:glib2-2.72.4p2: ok
icewm-2.9.9:cairo-1.17.6: ok
icewm-2.9.9:harfbuzz-5.2.0: ok
icewm-2.9.9:fribidi-1.0.12: ok
icewm-2.9.9:pango-1.50.10: ok
icewm-2.9.9:libogg-1.3.5: ok
icewm-2.9.9:libvorbis-1.3.7: ok
icewm-2.9.9:lame-3.100p1: ok
icewm-2.9.9:flac-1.3.4p0: ok
icewm-2.9.9:mpg123-1.30.1: ok
icewm-2.9.9:opus-1.3.1: ok
icewm-2.9.9:libsndfile-1.1.0: ok
icewm-2.9.9:desktop-file-utils-0.26: ok
icewm-2.9.9:lz4-1.9.4: ok
icewm-2.9.9:zstd-1.5.2: ok
icewm-2.9.9:jpeg-2.1.3v0: ok
icewm-2.9.9:tiff-4.4.0p2: ok
icewm-2.9.9:libxml-2.10.3: ok
icewm-2.9.9:shared-mime-info-2.2: ok
icewm-2.9.9:gdk-pixbuf-2.42.9p0: ok
icewm-2.9.9:libid3tag-0.15.1bp5: ok
icewm-2.9.9:giflib-5.2.1: ok
icewm-2.9.9:imlib2-1.4.10p0: ok
icewm-2.9.9:librsvg-2.54.5: ok
icewm-2.9.9: ok
Running tags: ok
```

Now let's set up IceWMm as our window manager for my user:

```
toshi01$ echo "exec icewm-session" > $HOME/.xsession
```

### xenodm configuration
We enable and start `xenodm` with:
```
toshi01# rcctl enable xenodm
toshi01# rcctl start xenodm ; exit
```
And here we have the session login window!
![xenodm login](/assets/images/2023-03-25-retrobattlestation-making-of-part-2/toshi01-xenodm.png)

### Configure a different IceWM theme
TBD

## syspatch
For supported versions of OpenBSD, the easiest way to get the latest security patches is to use the `syspatch` utility.

By default, a `cron` will be run executing `syspatch -c` command wich will retrieve a list of available patches. The list will be mailed to the root user.
```
toshi01# syspatch -c
001_x509
002_asn1
003_ukbd
004_expat
005_pixman
007_unwind
008_pfsync
009_xserver
011_gpuinv
012_acme
013_tcp
014_libxpm
017_sshd
018_x509
019_xserver
020_smtpd
021_wscons
022_resolv
023_bgpd
```
To apply the patches, run the command without the `-c` option:
```
toshi01# syspatch
Get/Verify syspatch72-001_x509.tgz 100% |***************| 11887 KB    00:25
Installing patch 001_x509
Get/Verify syspatch72-002_asn1.tgz 100% |***************| 11887 KB    00:25
Installing patch 002_asn1
Get/Verify syspatch72-003_ukbd.tgz 100% |***************| 30265       00:00
Installing patch 003_ukbd
Get/Verify syspatch72-004_expat.tgz 100% |**************|   584 KB    00:01
Installing patch 004_expat
Get/Verify syspatch72-005_pixman.tgz 100% |*************|   665 KB    00:01
Installing patch 005_pixman
Get/Verify syspatch72-007_unwind.tgz 100% |*************|   463 KB    00:01
Installing patch 007_unwind
Get/Verify syspatch72-008_pfsync.tgz 100% |*************|   306 KB    00:00
Installing patch 008_pfsync
Get/Verify syspatch72-009_xserver... 100% |*************|  4100 KB    00:08
Installing patch 009_xserver
Get/Verify syspatch72-011_gpuinv.tgz 100% |*************|   185 KB    00:00
Installing patch 011_gpuinv
Get/Verify syspatch72-012_acme.tgz 100% |***************| 38894       00:00
Installing patch 012_acme
Get/Verify syspatch72-013_tcp.tgz 100% |****************|   454 KB    00:01
Installing patch 013_tcp
Get/Verify syspatch72-014_libxpm.tgz 100% |*************| 98832       00:00
Installing patch 014_libxpm
Get/Verify syspatch72-017_sshd.tgz 100% |***************|  1434 KB    00:03
Installing patch 017_sshd
Get/Verify syspatch72-018_x509.tgz 100% |***************| 11886 KB    00:25
Installing patch 018_x509
Get/Verify syspatch72-019_xserver... 100% |*************|  4098 KB    00:08
Installing patch 019_xserver
Get/Verify syspatch72-020_smtpd.tgz 100% |**************|   315 KB    00:00
Installing patch 020_smtpd
Get/Verify syspatch72-021_wscons.tgz 100% |*************| 54153       00:00
Installing patch 021_wscons
Get/Verify syspatch72-022_resolv.tgz 100% |*************|  8753 KB    00:18
Installing patch 022_resolv
Get/Verify syspatch72-023_bgpd.tgz 100% |***************|   190 KB    00:00
Installing patch 023_bgpd
Relinking to create unique kernel... done; reboot to load the new kernel
Errata can be reviewed under /var/syspatch
```
So now we're rebooting.

After reboot, we can check that we do have a new kernel in place:
```
toshi01# dmesg | head -4
OpenBSD 7.2 (GENERIC) #7: Sat Feb 25 14:06:23 MST 2023
    root@syspatch-72-i386.openbsd.org:/usr/src/sys/arch/i386/compile/GENERIC
real mem  = 100220928 (95MB)
avail mem = 81539072 (77MB)
```

For the sake of speed, we're going to disable library reordering upon boot, caused by [ASLR](https://en.wikipedia.org/wiki/Address_space_layout_randomization) (Address space layout randomization):
```
toshi01# rcctl disable library_aslr
```
This allows a boot time of 1min 50 sec before we get the login prompt.

# Misc utilities
I've also installed a couple utilities I find useful. VNC and RDP remote clients, a text email client and an IRC client.
```
toshi01# pkg_add -V mutt irssi tigervnc freerdp
```
Also, I'll try to check which of these web browsers am I able to run here:
```
toshi01# pkg_add -V dillo netsurf
quirks-6.42 signed on 2023-04-06T19:19:25Z
dillo-3.0.5p5:pcre2-10.37: 2/6
dillo-3.0.5p5:libpsl-0.21.1: 3/6
dillo-3.0.5p5:wget-1.21.3: 4/6
dillo-3.0.5p5: 5/6
netsurf-3.10p3:libnspsl-0.1.6: 6/16
netsurf-3.10p3:libnsgif-0.2.1p0: 7/16
netsurf-3.10p3:libwapcaplet-0.4.3: 8/17
netsurf-3.10p3:libparserutils-0.2.4p0: 9/18
netsurf-3.10p3:hubbub-0.3.7: 10/18
netsurf-3.10p3:libdom-0.4.1: 11/18
netsurf-3.10p3:libcss-0.9.1: 12/18
netsurf-3.10p3:libnsutils-0.1.0: 13/18
netsurf-3.10p3:libnsbmp-0.1.6: 14/18
netsurf-3.10p3:libutf8proc-2.4.0p0: 15/18
netsurf-3.10p3:dconf-0.40.0: 16/21
netsurf-3.10p3:adwaita-icon-theme-42.0: 17/21
netsurf-3.10p3:atk-2.38.0: 18/23
netsurf-3.10p3:at-spi2-core-2.44.1: 19/23
netsurf-3.10p3:at-spi2-atk-2.38.0: 20/23
netsurf-3.10p3:gtk+3-3.24.34: 21/23
netsurf-3.10p3:libnslog-0.1.3: 22/23
netsurf-3.10p3: 23/23
Running tags: ok
New and changed readme(s):
	/usr/local/share/doc/pkg-readmes/gtk+3
```
For text editing, I found [WordGrinder](http://cowlark.com/wordgrinder/index.html), which is great if you only want to *write*:
```
toshi01# pkg_add -V wordgrinder
```
Also, let's have a nice editor as well:
```
toshi01# pkg_add -V vim-9.0.0192-no_x11-ruby
```
Let's have some music as well:
```
toshi01# pkg_add -V xmms2 mikmod
```

# Additional configuration

## doas
`doas` is the replacement of `sudo` in OpenBSD. In order to configure it for our personal user to be able to run tasks as `root`, we can create a simple configuration here:

1. Create the `doas.conf` file:
    ```
    toshi01# echo "permit persist :wheel" >> /etc/doas.conf
    ```
    This way we allow the password to be requested only once.

2. Allow our user to be part of `wheel` group:
    ```
    toshi01# usermod -G wheel manuelmc
    ```

Now we're able to do tasks as `root` user:
```
toshi01$ ls /root
ls: root: Permission denied
toshi01$ doas ls /root
doas (manuelmc@toshi01.my.domain) password: XXXXXX
.Xdefaults       .cshrc           .forward         .mikmod_playlist .profile         .ssh
.config          .cvsrc           .login           .mikmodrc        .sndio
```

## Modem configuration
Although I'm not going to configure a [ppp](https://en.wikipedia.org/wiki/Point-to-Point_Protocol) access right now, I'd like to confirm whether the integrated modem works or not:
```
toshi01# dmesg | grep "^com. at"
com0 at isa0 port 0x3f8/8 irq 4: ns16550a, 16 byte fifo
com1 at isa0 port 0x2f8/8 irq 3: ns8250, no fifo
com4 at pcmcia1 function 0 "3Com Megahertz, 3CXM756/3CCM756" port 0x3e8/8: ns16550a, 16 byte fifo
```
The first COM port belongs to the RS232C connector in the back of the laptop. The second one is a [softmodem](https://en.wikipedia.org/wiki/Softmodem), also known as *winmodem*, and won't work under OpenBSD :man_shrugging: .

Thus, I inserted a [3Com Megahertz](https://www.usr.com/en-support/product/?prod=3cxm756) modem PCMCIA card, which indeed works:
```
toshi01# cu -s 115200 -l /dev/cua04
Connected to /dev/cua04 (speed 115200)
ati0
5601

OK
ati3
TK206, V.90 Modem
Regulatory revision 1.1


OK

[EOT]
```

# Wrap up
As a proof of concept, it was *fun*. However, nowadays is really hard to use this computer for more things than a remote teminal (screen+keyboard+SSH).

Just for any minimal browsing capabilities you would need more horsepower. And I don't even think on anything close to JavaScript.

Let me show you the final image of it:
![final layout](/assets/images/2023-03-25-retrobattlestation-making-of-part-2/IMG20230325184519.jpg)
