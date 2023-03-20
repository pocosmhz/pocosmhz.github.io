---
layout: single
status: publish
title: "A retro battlestation: Making of (I)"
tags: [retro]
comments: true
author: manuel_molina
author_profile: true
categories: []
published: true
date: '2023-03-18 16:40:56 +0100'
date_gmt: '2023-03-18 16:40:56 +0100'
excerpt_separator: <!--more-->
---
A couple years ago I received an old laptop that was already old by then.

<figure style="width: 404px">
  <a href="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/toshiba-desktop.jpg"><img src="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/toshiba-desktop.jpg" alt="Toshiba Satellite 2540CDS laptop"/></a>
  <figcaption>Toshiba Satellite 2540CDS</figcaption>
</figure> 

Let's figure out how could I bring back some life to it.
<!--more-->

A brief list of the [full specifications](https://support.dynabook.com/support/staticContentDetail?contentId=638175&isFromTOCLink=false) for this laptop is:

| --------- | ---------------- |
| Processor | AMD K6-2 333 MHz with 3D technology|
| Integrated coprocessor | Yes |
| Processor cache | 64KB: (32KB code; 32KB data) |
| L2 cache | Yes: 512KB |
| PCI BUS (v.2.1) | (32-bit, 33 MHz) PC Card Slots, Graphics Controller, HDD, CD-ROM, FDD |
| ISA BUS | 16-bit, 8.25 MHz BIOS, Sound chip, KBC |
| Supported standards APM (v.1.2) | ACPI; PnP (v.1.0a); VESA (v.2.0); DPMS; DCC2B; DMI (v.2.0) |
| MEMORY | 64Mbit EDO DRAM, 60ns, 3.3V Standard 32 MB ; Maximum 160 MB |
| VIDEO | Memory: 16Mbit SGRAM, 3.3V 2 MB Speed 83 MHz |
| Controller Chip | S3 Virge MX 3D graphics controller |
| Video resolutions | From 640 x 480 16.7M colors (Smaller Image) up to 1280 x 1024 256 colors (Virtual Display Mode) |
| Ports | ECP parallel port ; DB9 serial port ; 1x USB 1.1 ; PS/2 external keyboard/mouse port ; IR port ; 2x PCMCIA slots |
| Storage | 1x FDD ; 1x internal and serviceable 2.5 inch IDE drive ; Toshiba 24x CD-ROM drive |

# Software recovery CD-ROM
In order to start from scratch, I counted on the Toshiba Recovery CD-ROM (Spanish version), which you can find [here](https://archive.org/details/S254SPC1).

That CD is used to optionally wipe the hard drive, and then reinstall the following software:
- [Windows 98](https://en.wikipedia.org/wiki/Windows_98)
- [Microsoft Works 4.5a](https://en.wikipedia.org/wiki/Microsoft_Works#Works_for_Microsoft_Windows) office suite.
- Toshiba utilities

## Recovery process
The recovery process is very straight-forward. Once you boot with the recovery CD you have:

<figure style="width: 496px" class="align-center">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/HDDMENU.BMP" alt="Recovery mode selection menu"/>
</figure> 

You have three options:
1. Full recovery (wipe and reinstall).
2. Standard recovery (only reinstall).
9. Exit.

When we move forward, you'll see several reboots between stages (partition creation, formatting, etcetera).
<figure style="width: 496px" class="align-center">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/toshi_progress.bmp" alt="Recovery progress dialog"/>
</figure> 

After content is copied to hard drive, you'll go through a standard Windows 98 installation:
<figure style="width: 400px" class="align-center">
  <a href="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/win98-keyboard-selection.jpg">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/win98-keyboard-selection.jpg" alt="Keyboard selection"/></a>
</figure> 

Also, I took the chance to install a PCMCIA network card and test it:
<figure style="width: 400px" class="align-center">
  <a href="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/win98-pcmcia-eth-driver.jpg">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/win98-pcmcia-eth-driver.jpg" alt="3com driver install"/></a>
</figure> 

## Notes
There are several drawbacks if you try to use the software outside the designed configuration.
- Software has been superseded by newer one. I only took the necessary steps to make sure no needed firmware patch was missing. Otherwise, you can go ahead without it.
- The recovery media is a bootable [El Torito](https://en.wikipedia.org/wiki/Microsoft_Works#Works_for_Microsoft_Windows) CD-ROM. Although you can have access to the 1.4 MByte bootable diskette inside (file name is `W98S321P.SPA`), the two main software packages are to be decompressed by a proprietary utility called `F3DCHK.EXE`, which is tied to a hardware signature. It won't work in a different hardware or virtualized environment. Believe me, I've tried :wink: . You can read further [here](https://superuser.com/questions/664340/how-to-reinstall-oem-windows-98-se-on-an-old-toshiba-desktop).

<figure style="width: 400px" class="align-center">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/NO_TOSPC.BMP" alt="Not a Toshiba PC warning"/>
</figure> 

# Hard drive replacement
I replaced the original hard drive (which died), with another one with 3 GBytes capacity.

However, as it's so little space, I've bought another one, which is 20 GBytes and, by the way, it happens to be a Toshiba drive.
<figure style="width: 400px" class="align-center">
  <a href="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/ide-disk-drives.jpg">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/ide-disk-drives.jpg" alt="2.5 inch IDE hard drives"/></a>
  <figcaption>Old and new hard drive</figcaption>
</figure>

# Windows XP installation
As more modern drivers should have appeared for pretty much everything related to this laptop, I opted for upgrading it.

I replaced the hard drive and installed Windows XP SP2 with an installation media and OEM license that I kept over here.

## Initial installation
The CD-ROM unit was not able to read the Windows XP SP3 installation media I burnt, without errors. Fortunately the CD-ROM unit was instead able to read the original installation media with Windows XP SP2.
<figure style="width: 400px" class="align-center">
  <a href="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/winxp-install-text-1.png">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/winxp-install-text-1.png" alt="Windows XP installation start"/></a>
</figure>
After about half an hour of content copy:
<figure style="width: 400px" class="align-center">
  <a href="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/winxp-copy-text-1.png">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/winxp-copy-text-1.png" alt="Windows XP file copy"/></a>
</figure>
... Finally, we're about to finish the text installation stage:
<figure style="width: 400px" class="align-center">
  <a href="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/winxp-reboot-text-1.png">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/winxp-reboot-text-1.png" alt="Windows XP text restart"/></a>
</figure>
and restart:
<figure style="width: 400px" class="align-center">
  <a href="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/winxp-booting.png">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/winxp-booting.png" alt="Windows XP graphic boot"/></a>
</figure>
Another half an hour of this:
<figure style="width: 400px" class="align-center">
  <a href="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/winxp-install-graph-1.png">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/winxp-install-graph-1.png" alt="Windows XP graphic install"/></a>
</figure>
And we're done!

## License activation
Once the installation is complete, Windows XP will put a lot of emphasis on you to activate the license. However, you can't activate the license online anymore.
<figure style="width: 400px" class="align-center">
  <a href="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/winxp-activation-1.PNG">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/winxp-activation-1.PNG" alt="Windows XP activation second screen"/></a>
</figure>
So I went ahead and called to the free toll number in Spain (+34 900 150 889). An automated process let you do it without any human interaction. Something that is a bit creepy twenty something years after the release of the product :sweat_smile: ...
<figure style="width: 400px" class="align-center">
  <a href="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/winxp-activation-2.PNG">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/winxp-activation-2.PNG" alt="Windows XP activation second screen"/></a>
</figure>

I succeeded and it ended up like this:
<figure style="width: 422px" class="align-center">
  <a href="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/mipc.PNG">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/mipc.PNG" alt="My PC properties dialog"/></a>
  <figcaption>System properties</figcaption>
</figure>
<figure style="width: 407px" class="align-center">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/cpu-z.PNG" alt="CPU-Z report"/>
  <figcaption>CPU-Z report</figcaption>
</figure>

## Service Pack 3
Now it's time to install the latest official Service Pack for Windows XP: SP3:

It can be downloaded from [here](https://www.catalog.update.microsoft.com/Search.aspx?q=KB936929).
<figure style="width: 400px" class="align-center">
  <a href="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/winxp-sp3-install.png">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/winxp-sp3-install.png" alt="Windows XP SP3"/></a>
</figure>

## Unofficial SP4
After publishing SP3, there have been a lot of individual patches that Microsoft have not packaged or compiled together.
There have been several unofficial initiatives to gather all of them in an automated way.

We have several options.

### English version
If you happen to use the English version of the product Windows XP, you're lucky.

We have the one, big Unofficial SP4.
It can be downloaded from:
- [RyanVM Update Pack](https://ryanvm.net/forum/viewtopic.php?f=5&t=10321&sid=7293a71674fa8221649f5a0056a0f836). Main download site.
- [Major Geeks website](https://www.majorgeeks.com/files/details/windows_xp_service_pack_4_unofficial.html). This is an interesting website for legacy computing, by the way.

In these two sites you can see the details.

### Spanish version
However, if like myself, you're installing the Spanish version of Windows XP, you're not so lucky. The previously mentioned *Unofficial SP4* will refuse to install in a different language.
<figure style="width: 423px" class="align-center">
  <a href="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/windows_xp_sp4.png">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/windows_xp_sp4.png" alt="Windows XP SP3"/></a>
</figure>
Thus we have this one, smaller, that could do the trick for some patches.
Downloaded from:
- [Luciano Aibar's Unofficial SP4](https://www.lucianoaibar.com/?q=windows-xp-service-pack-4)

<figure style="width: 400px" class="align-center">
  <a href="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/sp4install.PNG">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/sp4install.PNG" alt="Windows XP SP4 install"/></a>
</figure>

## WSUS offline update
On top of the two previously suggested packs, I discovered another updater: [WSUS offline update](https://www.wsusoffline.net/). It's a tool for building update sets so you can batch update any Windows host without being online. It ranges from the old Windows 98 to the latest version of Windows.

<figure style="width: 400px" class="align-center">
  <a href="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/wsusoffline-legacy-generator.PNG">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/wsusoffline-legacy-generator.PNG" alt="WSUS Offline Update generator app"/></a>
  <figcaption>WSUS Offline Update generator app</figcaption>
</figure>

Let's try to gather the remaining patches in a more structured way.

### Last Windows XP compatible version

In [this blog post](https://dellwindowsreinstallationguide.com/wsus-offline-update/obtaining-the-latest-service-packsbuilds-of-internet-explorer/patching-windows-xp-fully-using-the-wsus-offline-update/) I found that the latest version that supported Windows XP was [9.2.1](http://download.wsusoffline.net/wsusoffline921.zip). 

That version was published on May 2014, though. There are further implications which we'll try to solve later on.

### wget is not working
Once we start to download patches, I noticed something was off:

<figure style="width: 400px" class="align-center">
  <a href="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/wsusoffline-unsupported-scheme.PNG">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/wsusoffline-unsupported-scheme.PNG" alt="Unsupported scheme for wget"/></a>
</figure>

Since the release of this version of WSUS Offline, Microsoft kept original download links but added a 302 redirection. The reason is to enable HTTPS download of such patches.

Let's replace `wget` utility as it is not able to download from HTTPS resources.
I was unable to find a Windows XP compatible compiled version with SSL support in the [official site](https://gnuwin32.sourceforge.net/packages/wget.htm).

I decided to download newer versions of WSUS Offline in search of such utility, which could have been the shortest path. However, they included the same version as I suppose it was fair until some months / years later.
The next version of `wget` found in later versions only worked, in turn, in later versions of Windows. Sad news.

I did further research and found this website, [Eternally Bored](https://eternallybored.org/misc/wget/), where Jernej Simončič provides several utilities compiled for Win32.

Of all versions available there, the only one I manage to get working was [version 1.19.2](https://eternallybored.org/misc/wget/releases/old/wget-1.19.2-win32.zip).

With that I was able to download content from secure sites, *however*, the root certificate list was so old that current Microsoft SSL certificates were not accepted.

Let's not verify the certificate either. In order to do that, we have to create a properties file so when `wget.exe` is run, it won't check if the cert is valid.

File should be called `.wgetrc` and will contain one single line:

```
check_certificate = off
```

In case of doubt, you can create `wgetrc` as well, with the same content. Location of the file is supposed to be the home directory of the user. I put it there and also in the same folder as the executable. It worked.

That way I was able to automatically download and install .NET Framework patches and some other things.

### Installer utility
Once you've downloaded all the files with the Generator utility, you have a working folder named `client` that includes the Installer.
<figure style="width: 400px" class="align-center">
  <a href="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/wsusoffline-installer.PNG">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/wsusoffline-installer.PNG" alt="WSUS Offline Update Installer"/></a>
</figure>
Run it and wait some minutes.

## Additional manual patches installation
There are some utilities that I had to manually download and add, as *WSUS offline update* is no longer able to fetch from Microsoft resources. Here are the relevant log lines:

```
18/03/2023  8:58:07,67 - Warning: Download of http://www.download.windowsupdate.com/msdownload/update/v3/static/trustedr/en/rootsupd.exe failed
18/03/2023  8:58:07,67 - Warning: Download of http://download.microsoft.com/download/0/E/6/0E60F1EB-4E0A-4D3A-B4D1-20D9D405499A/rvkroots.exe failed
18/03/2023  9:11:58,01 - Warning: Download of http://download.microsoft.com/download/0/c/6/0c609742-5507-49fb-b028-a00701f13197/WindowsXP-KB953356-x86-ENU.exe failed
18/03/2023  9:11:58,01 - Warning: Download of http://download.microsoft.com/download/2/6/1/261fca42-22c0-4f91-9451-0e0f2e08356d/WindowsXP-KB942288-v3-x86.exe failed
18/03/2023  9:24:51,91 - Warning: Download of http://download.microsoft.com/download/8/F/E/8FE8D835-0775-454B-B0AD-A4DA125F7DBF/WindowsXP-KB969084-x86-esn.exe failed
18/03/2023  9:24:51,91 - Warning: Download of http://download.microsoft.com/download/9/e/0/9e03bc7d-9f0f-4095-af2f-e8207b1457fe/wmp11-windowsxp-x86-ES-ES.exe failed
```

They belong to the following packages and can be downloaded from the links:
- First two are Root Certificate Updates and Revoked Certificates Updates. They're no longer there.
  - I found [this thread](https://msfn.org/board/topic/175170-root-certificates-and-revoked-certificates-for-windows-xp/page/3/#comment-1110568) that mentions an automatic updater for these. I downloaded version 1.6 but it started giving me errors. I added the RegEdit file provided. Same.
  - I learn to install [this package](https://www.microsoft.com/es-es/download/details.aspx?id=6315) from the same forum. File is `WindowsServer2003-KB340178-SP2-x86-ESN.msi` . Not helpful.
  - However, I found [this other thread](https://msfn.org/board/topic/183352-proxhttpsproxy-and-httpsproxy-in-windows-xp-for-future-use/) where, on section 11.2.4 I was able to download an offline updater that was up to date (February 2023).
  - After downloading `rootsupd.exe` and running it, I managed to browse several pages and IE8 accepted the certificates as valid!
- [KB953356 Update for Windows XP](https://www.catalog.update.microsoft.com/Search.aspx?q=KB953356). We're supposed to install this patch to prevent non-intel computers from continuously restart after installing SP3. Oops! I already did, so ... :wink:
- [KB942288-v3 Windows Installer 4.5 redistributable](https://support.microsoft.com/es-es/topic/windows-installer-4-5-est%C3%A1-disponible-bf06be18-3e0a-d5eb-4549-b482f67e1c46) That link was a dead end. After several broken links from Microsoft, and thanks to [Abuelo Informático](https://www.abueloinformatico.es/verprogramas.php?id=775&nombre=Windows%20Installer&cat=Componentes%20y%20librerias) (Computer Grandpa), I was able to reach [this link](https://www.microsoft.com/es-es/download/details.aspx?id=8483#filelist) from where I found another dead end :sad: . I finally found the file in [one SourceForge project](https://sourceforge.net/projects/vietnam-ldi/files/Software/Windows%20Installer%204.5/Windows%20Installer_WindowsXP-KB942288-v3-x86.exe/download?use_mirror=kumisystems&download=&failedmirror=jaist.dl.sourceforge.net).
- [KB969084 Remote desktop update for Windows XP](https://www.catalog.update.microsoft.com/Search.aspx?q=969084)
- Windows Media Player 11 for Windows XP. As I was unable to find a *reliable* link, I suggest to install the latest compatible version of [VLC player for Windows](https://www.videolan.org/vlc/download-windows.wa.html). At the time of this writing, it is 3.0.18.

### Internet Explorer 8
This was the last version of Microsoft's browser that was compatible with Windows XP.

WSUS Offline was unable to download it, because it's no longer on Microsoft website.

On Archive.org you can find [its old download page](https://web.archive.org/web/20100424031002/http://www.microsoft.com/downloads/details.aspx?FamilyID=341c2ad5-8c3d-4347-8c03-08cdecd8852b&displaylang=es), but it's not usable, as the binaries are not cached there.

I was unable to find any official source for the main installer. I found [this unofficial source](http://www.zonavirus.com/descargas/descargar-internet-explorer-8.asp) and downloaded it. **Do it at your own risk**.
<figure style="width: 400px" class="align-center">
  <a href="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/ie8install.PNG">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/ie8install.PNG" alt="IE8 installation welcome screen"/></a>
</figure>

After the main installation, you can still go ahead and install [KB2879017](https://www.microsoft.com/es-es/download/details.aspx?id=40390) from the official site. It was published on October 2013.

And on top of that, you can still go further and install the last cumulative patch, [KB4018271](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4018271).

Finally you end up with a working browser, that has a recent set of root and revoked certificates, but lacks:

- Later security patches
- Optimized and new technology
- Most important: Cryptographic protocols newer than TLS 1.0. Almost no web server nowadays negotiates something like that.
<figure style="width: 400px" class="align-center">
  <a href="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/ie8install_finished.PNG">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/ie8install_finished.PNG" alt="You can reboot your system now"/></a>
  <figcaption>You can reboot your system now</figcaption>
</figure>

### Microsoft Security Essentials
I was able to download the software from **here** but it's worthless in this case.
The reason is that this laptop has not enough RAM for allowing the installation. Thus, it fails with an error.
<figure style="width: 400px" class="align-center">
  <a href="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/seccenter.PNG">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/seccenter.PNG" alt="Antivirus warning disabled"/></a>
</figure>
Because of that, we'll disable the warning about antivirus protection in Secury Center.

# Common utilities
Let's add some utilities here. However, and before I move on in order to recommend certain up-to-date software versions, let's talk about the elephant in the room :grimacing: .

## SSE2 support
This particular laptop's CPU **does not** support [SSE2 instruction set](https://en.wikipedia.org/wiki/SSE2).

That means that you can get random execution errors if you try to run recent versions of Windows applications. Even if they are known to work with Windows XP, bear in mind that SSE2 enabled CPUs appeared on year 2000 and Windows XP official support ended on 2014, although some companies continued using it.

That said, I'll use two very valuable resources to suggest previous versions of some products, instead of the latest ones, for the sake of functionality:
- [Last versions of Windows applications that do not require SSE2](http://matejhorvat.si/en/unfiled/nosse2.htm)
- [Windows programs and utilities for pre-SSE2 processors](http://birdbird.org/electronics/sse2/windows-without-sse2.html)

Please see my final conclusions at the end of the post.

## Adding IOmega Zip 100 drive
For the sake of having massive storage, I'm installing this parallel port Zip 100 drive.

I have [this installation media](https://archive.org/details/iomegaware_202208) together with the Zip 100 drive I bought in the previous century.

However there are newer versions, like 2.8 [here](https://archive.org/details/iomega-iomegaware-usb-drivers) or 4.0.3 that you can get from [this web](http://dosdays.co.uk/topics/Manufacturers/iomega_downloads.php). I installed that last one.
<figure style="width: 400px" class="align-center">
  <a href="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/iomegaware-setup.PNG">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/iomegaware-setup.PNG" alt="IomegaWare Setup"/></a>
  <figcaption>PuTTY MSI installation</figcaption>
</figure>
Drawbacks:

- Parallel port Iomega Zip 100 drive only works on Windows nowadays.
- No chance I can get it to work on Linux, as no current distribution fits in this computer.

## Mozilla Firefox
The last version with Windows XP Support, according to [this article](https://mzl.la/3BXx1GL) is [52.9.0esr](https://ftp.mozilla.org/pub/firefox/releases/52.9.0esr/win32/es-ES/Firefox%20Setup%2052.9.0esr.exe)

*However*, if your computer is not SSE2 compliant, Mozilla [said](https://support.mozilla.org/en-US/questions/1226034) that you should use version [45.9.0esr](http://archive.mozilla.org/pub/firefox/releases/45.9.0esr/win32/).
<figure style="width: 400px" class="align-center">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/ff-install.PNG" alt="Mozilla Firefox install"/>
</figure>
That version crashed upon start. If we look at the aformentioned SSE2 resources, we must try version [48.0.2](https://ftp.mozilla.org/pub/firefox/releases/48.0.2/win32/es-ES/Firefox%20Setup%2048.0.2.exe). Release date was August 24, 2016.

Same happened with 47.0.2 and 46.0.1. :sad:

I saw [this question](https://support.mozilla.org/es/questions/841446) and I wondered if I was even able to run version 5, released on July 11th, 2011.

It worked, and was a progress from IE8, but not really usable.

I also tried version [10.0.12esr](https://ftp.mozilla.org/pub/firefox/releases/10.0.12esr/win32/es-ES/Firefox%20Setup%2010.0.12esr.exe), dated January 2013.

Some pages work, and some other just throw you a `ssl_error_no_cypher_overlap` error, for obvious reasons.

I might continue working on the last compatible version but only if I'm bored enough.

## PuTTY
<figure style="width: 400px" class="align-center">
  <a href="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/PuTTY-install.PNG">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/PuTTY-install.PNG" alt="PuTTY MSI installation"/></a>
  <figcaption>PuTTY MSI installation</figcaption>
</figure>
I tried current version, 0.78, but it crashed after installation.

As per the SSE restrictions mentioned above, I downloaded [version 0.70](https://the.earth.li/~sgtatham/putty/0.70/w32old/putty.zip), which is the very last that will work.

If you have time, you can bother with downloading the [whole MSI installer](http://web.archive.org/web/20180715141520/https://the.earth.li/~sgtatham/putty/latest/w32/putty-0.70-installer.msi) for that version. Be aware that:
- You're supposed to have admin privileges
- No matter what, you could get the *Installation Directory Must Be On A Local Hard Drive* error ...
- As seen [here](https://www.thefreewindows.com/19928/fix-error-installation-directory-local-hard-drive/), running `cmd.exe` with Admin privileges and then doing `msiexec /i putty-0.70-installer.msi WIXUI_DONTVALIDATEPATH="1"` should do the trick.

## BitVise SSH client
Latest version of this client is not working. Even the installer throws an error. I'm suspicious about the same SSE issue, so I won't push it anymore.
It was recommended on PuTTY's website.

## MobaXterm
<figure style="width: 400px" class="align-center">
  <a href="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/mobaxterm-install.PNG">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/mobaxterm-install.PNG" alt="MobaXterm MSI installation"/></a>
  <figcaption>MobaXterm MSI installation</figcaption>
</figure>
[MobaXterm](https://mobaxterm.mobatek.net/) is another classic, as it allows you to work with X-Window applications from other UNIX hosts, by exporting their display.

I installed latest version, which is [23.0](https://download.mobatek.net/2302023012231703/MobaXterm_Installer_v23.0.zip). However, it starts but shows errors.

I opted for downloading an older (about 2019), [portable version 12.3](https://download.mobatek.net/1232019093005654/MobaXterm_Portable_v12.3.zip).

More errors coming from this executable. As with Firefox, I might continue working on earlier versions if it were worth it.

# Wrap up

The main conclusion I reached after all this work are:
- **It is not worth it**.
- Only if you really have to run a very specific app, might be worth it.
- At specific use cases you might need to update the firmware of certain card or device, and the updater only runs on Windows XP. Might be another case.

<figure style="width: 400px" class="align-center">
  <a href="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/winxp_closing.png">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/winxp_closing.png" alt="Bye, bye!"/></a>
</figure>

To be continued ... :wink:

<figure style="width: 500px" class="align-center">
  <a href="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/openbsd72install.png">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/2023-03-18-retrobattlestation-making-of/openbsd72install.png" alt="OpenBSD 7.2 install"/></a>
</figure>