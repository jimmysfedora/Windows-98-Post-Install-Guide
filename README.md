# Windows 98 Second Edition Install Guide

This is a refresher containing a condensed set of instructions to get your bare metal install of Windows 98 installation working.

Hardware Tips:
- Tweak BIOS settings to your liking before installing Windows.

- If you are having errors booting into floppy and CD media, reset the BIOS settings.

- Keep partition size under what OS and hardware can support.
  - It is recommended to have a 32GB partition but Windows 95 OSR 2.5, 98, 98SE & ME supports up to 137GB partitions natively.

- If you are experiencing hardware instabilities such as being unable to run at full CPU clock speed, first check motherboard capacitors they probably need replacement. If you don't want to do that, install Windows 9x without ACPI by forcing APM mode with ```setup.exe /p i```

- Instead of configuring boot loader for dual booting, it is easier to have a single operating systems on their own separate drive.
	- Most BIOSes will load the first operating it sees from top-down Primary Master IDE 0 → Primary Master Slave IDE 1 → Secondary Master IDE 2 → Secondary Slave IDE 3.
	- If you want to boot into another drive despite having multiple drives connected on your IDE cables, you will have to mark the IDE channels the drives are on as NOT INSTALLED.
	- BIOS → IDE HDD AUTO-DETECTION → UNUSED DRIVES → MARK AS NOT INSTALLED

- If sound doesn't work in some games it can be because some Windows games use WDM drivers instead of VXD drivers.

- Note on audio drivers: VXD drivers will perform better in DOS games, and you can reboot into MS-DOS with VXD drivers. WDM drivers work only on DOS games running on Windows, but will work with Windows games. However, you won't be able to reboot into MS-DOS with working sound with WDM drivers installed. WDM drivers generally perform worse than VXD drivers but provide more compatibility with Windows and DOS games. For general use you will have to decide to choose WDM or VXD audio drivers based on the games that you play. TLDR; WDM drivers are the best for compatibility, while sacrificing performance.

# Recommended BIOS Settings:
```
- LOAD SETUP DEFAULTS - LOADS PERFORMANCE SETTINGS
- LOAD BIOS DEFAULTS - ONLY FOR TROUBLESHOOTING
- ADJUST TIME
- BOOT ORDER - AS NECESSARY
- USB KB/MOUSE LEGACY - KEYB + MOUSE (IF USING ONE)
- PnP AWARE OS - ON
- PRIMARY GRAPHICS ADAPTER - AGP (IF RUNNING AGP VIDEO CARD)
- COMPLIANCE WITH O/S - YES (CHANGE TO NO TO FORCE APM INSTALL)
- UNUSED PORTS (SERIAL, PARALLEL, etc) - DISABLED (FREES UP INTERRUPTS)
- ONBOARD AC’97, LEGACY AUDIO & SOUND BLASTER - DISABLE IF NOT USING ONBOARD AUDIO
- FSB SPEED - (ADJUST AS NECESSARY) - FOR ME I HAVE A PENTIUM III 1000MHZ AND IT RUNS GREAT AT A FSB OF 133MHZ.
- VOLTAGE - (ADJUST AS NECESSARY FOR PROCESSOR)
- IDE HDD AUTO DETECTION - SELECT TO REFRESH DRIVES
```

## Pre-Installation Procedures

- Make sure the hard drive is **not** set as a slave to the CD-ROM.

- **GoTek Floppy Emulator (a must have for storing multiple floppy disk images on a single USB stick)** - https://www.philscomputerlab.com/gotek-floppy-emulator.html

- I use [SeaTools](https://www.seagate.com/support/downloads/seatools/seatools-legacy-support/) and
  [WD Data Lifeguard Tools](https://www.philscomputerlab.com/western-digital.html) to format partitions
  instead of using `fdisk` for quicker formats.
  - Note: By not using `fdisk`, you won’t get sector checks like you would when creating and formatting
    partitions with `fdisk`.

#### If installing on Seagate Hard Drives

- Use **SeaTools** to reset the disk size or cap the partition to **32 GB**.
- Then use
  [Seagate DiscWizard Starter Edition](https://www.philscomputerlab.com/seagate.html)
  to configure the rest of the drive.

#### If installing on Western Digital Hard Drives

- Insert the **EZ-Drive** floppy diskette.
  - If you encounter boot floppy errors:
    - Reset BIOS settings
    - Set the CPU to the lowest processor speed
    - Physically disconnect other drives
    
# Basic CLI Commands: 
- ```cd``` - Change directory.
- ```cd\``` - Goes back to previous directory.
- ```dir``` - Shows every file in the directory.
- ```dir /p``` - Loads all the files one screenful at a time.
- ```dir /w``` - Loads information widefully.
- ```copy *.* c:\``` - Common way to copy files. 
- ```format a: /u``` - Low level format floppy diskettes.
- ```format c: /q /u /s``` - Use this command if you cannot format drive after using fdisk on it. Go to the CD-ROM, cd into win98 folder, and run the command.
- Resetting HDD to factory settings: [https://www.youtube.com/watch?v=rGSjWwTy1Rg](https://www.youtube.com/watch?v=rGSjWwTy1Rg)

# Standard Installation Procedures:
- Boot with Windows 98 Second Edition Boot Disk
  
- Start computer with CD-ROM support

- Make directory on C: drive with “md win98”

- Go to CD-ROM and ```cd``` into win98 folder

- Run ```copy *.* C:\win98``` (copies installation files to hard drive directly and Windows won't nag you to insert disk when updating drivers)

- Go to C drive and run ``setup.exe``
  - ``setup.exe /p i`` ("/p i" parameter bypasses the reporting the existence of a Plug and Play BIOS during setup).
  
  - Running ``setup.exe /p j`` ("/p j" parameter forces Windows to use ACPI/PnP. Which is useful if having a newer ACPI BIOS not recognized)

- Add or remove Windows features (the less the better for stability)

# Post install housekeeping

- Verify DMA Mode is turned on for storage device & CD-ROM in Device Manager
  - If OS is unstable, disable DMA mode.

- Set sound output for devices in multimedia to the highest sample rate conversion quality.

- Set file system in Settings → System → Performance → File System → Network Server

- Remove network login prompt by going to ```Settings → Network → Change Primary Network Logon to Windows Logon```

- If you didn't set a Windows password, it should boot into the desktop directly.

- Install motherboard chipset drivers, graphics drivers, sound drivers. 

# Graphics Drivers
- Installing the latest DirectX version your graphics card supports is recommended, but you may want to stick to installing DirectX 7.0a for more period correct games.

- Installing the latest drivers isn't always the greatest idea. For example, I used to run a Radeon 9500 Pro on the latest 6.2 Cataylst driver. Then, I had issues with a black screen whenever I loaded a game. So I downgraded to an older driver (4.14) and my games loaded finally.

- NVIDIA Users: Version 45.23 drivers are considered the defacto version for the best overall driver.
- ATI/Radeon: Any drivers from 2002-2004 is good enough - https://www.philscomputerlab.com/radeon-9x-drivers.html

# Optional 9x Updates
- It is generally recommended to not install the latest Windows updates to prevent clutter. But for some reason if your having trouble running some newer apps, you can try to install newer updates.

- **Windows 98 SE Update CD** - https://archive.org/details/w98se-upd-r1
  - An unofficial package containing only the offical updates ever released for Windows 98 SE. 

- **Windows ME Update CD** - https://archive.org/details/wmeupd-r2
  - An unofficial package containing only the offical updates ever released for Windows ME. 

# Windows 9x Tips:
- If having issues with USB drives, try formatting within Windows 9x.
- If burning disks make sure burn speed is slow like 10X and verifying the content is burnt in ISO 9660 file system.
- If dual booting XP and Windows 98 and using EZ-Drive, make sure FAT32 partition for Windows 98 is smaller than the NTFS partition for XP.
- https://www.reddit.com/r/windows98/comments/1d26gr7/here_is_a_actual_network_sharing_fix_for_windows/

## Recommended Software & Websites
- **3DMark** (benchmark software) - https://www.philscomputerlab.com/futuremark-3dmark.html

- **DAMEON Tools** (ISO mounting) - https://www.philscomputerlab.com/daemon-tools-windows-98.html

- **Diskeeper 6.0** (disk defrag tool use only if running actual hard drives) - https://winworldpc.com/product/diskeeper/60

- **ImgBurn** (CD Burning software) - https://www.imgburn.com/

- **Legacy DirectX Versions** - https://falconfly.vogonswiki.com/directx.html

- **MemTest86** (test RAM sticks for errors) - https://www.memtest86.com/index.html

- **Norton Ghost 2003** (backup recovery software) - https://archive.org/details/norton_ghost_2003/

- **Phil's Computer Lab** - https://www.philscomputerlab.com/

- **USB Driver** (usb device support) - https://www.philscomputerlab.com/windows-98-usb-storage-driver.html

- **Windows Installer 2.0** - https://archive.org/details/instmsi   

- **WinImage** (disk image software) - https://winworldpc.com/product/winimage/61

- **WinWorldPC** (OS repository) - https://winworldpc.com/library/operating-systems

**Hardware Specific:**


- **Audigy 2 ZS Drivers** - https://www.vogons.org/viewtopic.php?f=62&t=71449

- **VIA Chipset Tweaks** - https://www.georgebreese.com/net/software/

**Optional:**
- **86Box** (Machine emulator to run on modern machines) - https://86box.net/

- **Windows CD Emulator** (ISO mounting for modern machines)- https://wincdemu.sysprogs.org/download/

**Game Perhiphals:**
- **Sidewinder 3D Pro Drivers** - https://www.vogons.org/viewtopic.php?t=6318

**Not recommended (use with caution):**
- **Legacy Update** (online updates for Win9x, Win 2000, WinXP, Vista, 7, etc) - https://legacyupdate.net/

- **Windows Update Restored** (sister website of Legacy Update mainly caters towards Win9x) - http://windowsupdaterestored.com/ 

# Windows Keys
- **Windows 95** - ``29696-OEM-0015933-60761``

- **Windows 98 SE** - ``G2FGT-6HYRW-X2W2C-RT7HW-RF7WX``

- **Windows 98 SE OEM** - ``DKRBQ-TXYCX-6K4GD-4CPJ7-C6B26``

- **Windows ME** - ``TH3RK-MQC86-YX3PH-8DC4R-RKQ72``

# References
- https://www.vogons.org/viewtopic.php?f=61&t=52119
- https://www.vogons.org/viewtopic.php?p=1034545
