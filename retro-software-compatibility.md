# Retro Software Compatibility

## Purpose
This guide discusses practical techniques for running older software on modern computers. It explains why compatibility problems happen in the first place and various practical solutions for solving them in different situations.

The following are discussed, with detailed guides
  * **Classic Mac**
  * **DOS**
  * **Windows 3.1**
  * **Windows 95/98**
  * **Windows XP**

The following are not currently covered
  * **Apple II** software
  * PowerPC **Mac OS X**
  * Intel **Mac OS X**
  * CD-ROM disc authentication and copy protection (especially late 90s to early 00s)

## What Software Depends On
A software program depends on what it needs to "talk to".

*Hardware* is the lowest level thing it can talk to. It consists of physical parts like CPUs, GPUs, mice, keyboards, cameras, printers, and more.

*Operating Systems* (*OS*) are one level above hardware. They manage the system and provide services to programs so that program developers don't have to reinvent the wheel for common things. Developers want to be able to say "draw the letter X" not "start at the top-left corner of the monitor and draw a white line at such and such angle..." Operating systems include **Linux**, **macOS**, and **Windows**.

*API*s (*Application Programming Interfaces*) are how services are provided to programs. Some are part of the OS while others are distributed separately. OS services tend to be generic things needed by many programs whereas separate APIs may provide specific things like 3D graphics. Examples of 3D graphics APIs include **DirectX**, **Metal**, and **Vulkan**.

Packages that provide large APIs, or bundles of related APIs, are sometimes referred to as software *libraries*. Game engines, such as **Unreal** and **Unity**, bundle multiple libraries and specialized APIs specific to game development. Technically, these packages are more than *just* APIs, but APIs are how programs talk to them. 

```
Software Program
    ↓
APIs / Libraries
    ↓
Operating System
    ↓
Hardware
```

These layers *are not rigid*. Software programs may skip over and talk to lower layers directly. For example: a **DOS** game might talk directly to the sound card.

Some layers may not exist on some systems. On early game consoles, games often handled low-level things on their own and ran somewhat directly on the hardware.

## Software Compatibility Solutions
Software program compatibility problems happen when they were written to work with a layer in a particular way but the layer has changed (or does not exist) on some system.

Sometimes it is possible to *run the program directly* on the desired system by applying *patches* (an update that replaces parts of the program) or by setting a particular *configuration* (to make the program avoid doing incompatible things if the rest of the things it needs to do are compatible).

*Compatibility layers* are programs that translate some or all of a program's operations and API calls into a form that is runnable on the desired system. Examples include **Proton** or **Wine**.

*Virtual machine*s (*VM*) are typically designed for apps that don't depend on "the behavior of particular hardware" but instead "depend on the behavior of a particular OS". They often have high proformance and focus on Compatibility with business apps rather than multimedia or games. Examples include **Hyper-V**, **VirtualBox** and **VMware Workstation**. **KVM** is a virtualization system on Linux but it is more of a "virtualization technology" that can be re-used by other projects and not a complete package.

*Emulators* simulate hardware. An emulator may simulate specific real-life hardware. Or it may simulate a single generic and predictable machine to avoid having to simulate the hundreds of variations among the machines that actually existed. Ideally, emulators let relevant OSes, APIs, and software programs run without any modifications just as they did on an original hardware. The more complex and accurate the hardware being simulated, the higher the CPU requirements of the emulator tend to be.

Often whatever is simplest is the best solution unless you have goals like to recreating a historic experience. Even "buy old hardware" should be considered as a solution for tricky or unsolved Compatibility problems.

## Mac Software

### Types of Mac Software
Mac hardware historically had fewer variations than PC. Apple has also historically been aggressive in dropping support for old platforms in order to promote a consistent, modern experience for all customers. In general, Apple tends not to provide long-term support for old software. However, because the breadth of hardware was smaller than that of the PC world, emulation developers had a more focused set of hardware to work against and emulation is very mature for old Macs.

Macs are divided into eras based on the CPU architecture used by the machine. Major software compatibility breaks happened during transitions from one CPU family to another. Each transition included some form of compatibility technology provided by Apple for a limited time.

*68k Macs* were the original Macs from 1984 to the mid-90s. These were built on Motorola 68000-series CPUs. They began with black-and-white, later introducing color. The OSes were **System 1** to **System 7** with limited support extending to **Mac OS 8**.

*PowerPC Macs* were introduced in 1994. The PowerPC CPU was a joint venture between Apple, IBM, and Motorola (the "AIM Alliance)". These span the late Classic Mac era through early Power Macs, PowerBooks, and iMacs. OSes were **System 7**, **Mac OS 8**, **Mac OS 9**, earlier versions of **Mac OS X**. In 1996, Apple bought Steve Jobs' company NeXT, eventually rehired him as CEO. Consequently, the OS **NeXSTEP**, rather than the earlier **System/Mac OS** line, was used as the starting point for developing **Mac OS X**. The release of **Mac OS X** represents a large OS break partway through this era.

*Intel Macs* were introduced in 2006 when Apple switched over to the same type of x86 CPU used by PCs. The OS continued to be **Mac OS X**, which was rebranded as **macOS** in 2016. As of 2026, Intel CPUs are still supported.

*Apple Silicon Macs* were introduced in 2020 when Apple moved to its own ARM-based processor, like the one it already uses for its phones. A goal of this was to make the hardware of **iOS** and **macOS** devices more similar so that developers can more often create one solution and use it on both.

### Mac Emulators
**Mini vMac** emulates early compact 68k Macs starting with the original "Macintosh" (later known as Macintosh 128K) thru the Macintosh 512K, Plus, SE, Classic. It prioritizes hardware accuracy and a historically authentic experience. **System 6** is a stable "final plateau" OS that can be run on this emulator whereas it may struggle with **System 7** just as the original hardware struggled. It has a reputation of being hard to use however that comes from the Macs it is emulating being harder to use in real-life than later systems, not the emulator itself.

**Basilisk II** emulates a powerful late-era 68k Mac similar to a Quadra, while **SheepShaver**, by the same developer, emulates a late-era PowerPC machine similar to a Power Mac. It prioritizes software compatibility and ease-of-use rather than realistically emulating specific hardware. These two emulators are excellent choices for software that is forgiving in terms of the hardware it can run on. **System 7** is a good plateau OS for either 68k or PowerPC software. For later PowerPC software, **Mac OS 9** (typically **Mac OS 9.0.4**) is often a good choice.

**SheepShaver** does not support beyond **Mac OS 9.0.4** because it does not implement the memory management unit used by later versions of **Mac OS 9** or by **Mac OS X**.

Development of **Mini vMac**, **Basilisk II**, and **SheepShaver** has mostly halted though **Mini vMac** has seen occasional updates as of 2026. All three are able to run on either **Mac**, **Linux**, and **Windows**.

> Recommendations:
> * Use **Mini vMac** for a historically accurate Mac.
> * Use **Basilisk II** for most 68k Mac software.
> * Use **SheepShaver** for most PowerPC era Classic Mac software.
> * Look elsewhere for **Mac OS X** software.

#### Mac Guide: Mini vMac (68k Mac running Mac OS 6.0.8)
* Links
  - [Site](https://www.gryphel.com/c/minivmac/)
  - [E-Maculation Forum](https://www.emaculation.com/forum/viewforum.php?f=7)
  - [E-Maculation Wiki](https://www.emaculation.com/doku.php/mini_vmac_setup)
  - [Github](https://github.com/minivmac)
* Download **Mini vMac** from its website.
* Obtain a ROM and put it in the same directory as the executable as the name `vMac.ROM`.
  - A good 68k Mac ROM is the final Macintosh Plus ROM revision which works well with **System 6.0.8**.
    - `4D1F8172 - Plus, 512Ke (r3) - 1.1-7.5.5`
* Obtain **System 6** install media. It should include two floppy disk images.
* You can prep the floppy disk images for use by the emulator using `ua608d`, a tool on the emulator's website.
  - Download from https://www.gryphel.com/c/minivmac/extras/ua608d/
  - Run the tool twice
    - `ua608d SSW_6.0.8-1.4MB_Disk1of2.sea.bin "System Startup"`
    - `ua608d SSW_6.0.8-1.4MB_Disk2of2.sea.bin "System Additions"`
    - Copy the resultant files (`System Startup` and `System Additions`) to the **Mini vMac** folder. These files do not have file extensions.
* Obtain an uninitialized disk image that you will use as the emulator's hard disk from the emulator's website.
   - https://www.gryphel.com/c/minivmac/extras/blanks/index.html
   - For example, in this archive, `112M.dsk` is a 112 MB disk.
* Run the emulator. It should show a floppy disk with a blinking question mark.
* Drag the files `System Startup` and then the unitialized `.dsk` file you chose from above onto the emulator window.
* Run **Installer** from the `System Startup` disk.
* When the installer asks for it, drag `System Additions` onto the emulator window (and then drag `System Startup` onto the window again when prompted).
* **Shut Down** and exit the emulator.
* When running the emulator, boot from your hard disk like
  - Start the emulator
  - When the floppy with a question mark appears, drag the `.dsk` file onto the emulator window.
* Install **Stuffit Expander 4.0.1** using the link on the emulator author's site. Mac software online is often packaged with this tool.
  - https://www.gryphel.com/c/sw/archive/stuffexp/index.html

#### Mac Guide: Basilisk II (68k Mac running Mac OS 7.5.3 or 7.6.1)
* Links
  - [Site](https://basilisk.cebix.net/)
  - [E-Maculation Forum](https://www.emaculation.com/forum/viewforum.php?f=6)
  - [E-Maculation Wiki](https://www.emaculation.com/doku.php/basiliskii_osx_setup)
  - [Github](https://github.com/cebix/macemu)
* Download **Basilisk II** following instructions from its website (which leads to a forum post), or by building it from scratch.
* Configure the emulator
  - **Volumes**
    - Choose an OS, obtain its install media and add a volume for the OS install disc.
    - Create a new volume of size `1000 MiB` like `MacOS753` or `MacOS761`.
    - If you want to give the emulator access to files on the outer machine, consider creating a small blank partition named `Swap` and set the drive letter to something like `Z:`. Then if you set **Mount Drives** to `Z` this prevents the emulator from touching your host machine's disk.
  - **Graphics/Sound**
    - **Window Refresh Rate**: `Dynamic`
    - **Width**: `1024`
    - **Height**: `768`
    - **Render Driver**: `Software`
    - **Vertical Sync (Software)**: `Checked`
  - **Memory/Misc**
    - **MacOS RAM Size**: `64`
    - **Mac Model ID**: `Quadra 900 (MacOS 8.x)`
    - **CPU Type**: `68040`
    - **ROM File**: `420DBFF3 - Quadra 700&900 & PB140&170.ROM`
* Install the OS
  - Start emulation.
  - Name your blank volume.
  - Install an OS from its instalation disc.
  - Shut down.
  - Remove the installation disc image from the list of configured volumes.
* Setup the OS
  - Under **Control Panels > Monitors**, set your display to color.
  - Install **Stuffit Expander 5.5** and **Disk Copy 6.3.3**. Mac Software online is often packaged using these tools.

#### Mac Guide: SheepShaver (PowerPC Mac running Mac OS 7.5.3 or 7.6.1, or 9.0.4)
* Links
  - [Site](https://sheepshaver.cebix.net/)
  - [E-Maculation Forum](https://www.emaculation.com/forum/viewforum.php?f=20)
  - [E-Maculation Wiki](https://www.emaculation.com/doku.php/sheepshaver_setup)
  - [Github](https://github.com/cebix/macemu)
* Download **SheepSaver** instructions from its website (which leads to a forum post), or by building it from scratch.
* Configure the emulator
  - **Volumes**
    - Choose an OS, obtain its install media and add a volume for the OS install disc.
    - Create a new volume of size `1000 MiB` (for **Mac OS 7**) or `2000 MiB` (for **Mac OS 9**) like `MacOS753` or `MacOS761` or `MacOS904`.
    - If you want to give the emulator access to files on the outer machine, consider creating a small blank partition named `Swap` and set the drive letter to something like `Z:`. Then if you set **Mount Drives** to `Z` this prevents the emulator from touching your host machine's disk.
  - **Graphics/Sound**
    - **Window Refresh Rate**: `Dynamic`
    - **Width**: `1280`
    - **Height**: `1024`
    - **Render Driver**: `Software`
    - **Vertical Sync (Software)**: `Checked`
  - **Memory/Misc**
    - **MacOS RAM Size**: `128`
    - **ROM File**: `79D68D63 - Power Mac G3 desktop (Gossamer)`
      - This [E-Maculation forum post](https://www.emaculation.com/forum/viewtopic.php?p=61384#p61384) documents ROMS that **SheepShaver** supports:
        - `6F5724C0 - Performa 6400 (Alchemy)`
        - `6E92FE08 - Power Mac 6500 (Gazelle)`
        - `78F57389 - Power Mac G3 (v3) (Gossamer)`
        - `79D68D63 - Power Mac G3 desktop (Gossamer)`
        - `960E4BE9 - Power Mac 7300 & 7600 & 8600 & - 9600 (v1) (TNT)`
        - `960FC647 - Power Mac 8600 & 9600 (v2) (TNT)`
        - `9630C68B - Power Mac 7200&7500&8500&9500 v2 - (TNT)`
        - `96CD923D - Power Mac 7200&7500&8500&9500 v1 (TNT)`
* Install the OS
  - Start emulation.
  - Name the blank volume.
  - **Mac OS 9** only: Format as **Mac OS Extended** which corresponds to HFS+.
  - Install the OS from its instalation disc.
  - **Mac OS 9** only: When the wizard displays **Click Start to install...**, click **Options...** and deselect **Update Apple Hard Disk Drivers**.
  - Shut down.
  - Remove the installation disc image from the list of configured volumes.
* Set up the OS
  - Start emulation.
  - **Mac OS 9** only: The **Mac OS Setup Assistant** pops up. You can run a few steps of it, but it will always hang at **Looking for Network Devices** so exit the wizard before that page and complete any configurations using the control panels manually. Or proceed to that page and hard reboot when it gets stuck.
  - **Mac OS 9** only: Sound may not work immediately after installation. If the Sound control panel does not show **Built-in** as an output device, try one or more of the following:
    - Re-mount the **Mac OS 9** installation CD and reboot.
    - Open the **Sound** control panel directly from **System Folder > Control Panels** rather than using the Apple menu shortcut.
    - Reboot **SheepShaver** after opening the **Sound** control panel.
    - When sound is working correctly, **Built-in** should appear as an output device. Selecting it and adjusting the volume should play a test sound.
  - Install **Stuffit Expander 5.5** and **Disk Copy 6.3.3**. Mac Software online is often packaged using these tools.

## Windows Software

### Types of Windows Software

In determining the strategy for running a piece of old **Windows** software the top three most important questions are:

* What is the **Windows** OS family the software was designed for?
* How many bits does the software have?
* Does the software rely on a particular 3D API or 3D hardware?

#### **Windows** Families
The **DOS** family includes the original **MS-DOS** and extends through versions of **Windows** up to **Windows 3.1**. **MS-DOS** (aka **DOS**) was originally a stand-alone text-based OS introduced in 1981. **Windows** was introduced in 1985 and is a graphical environment that runs on top of **DOS** meaning OS duties are split between **DOS** and **Windows**. **DOS** handles booting, loading programs, managing memory, and communicating with hardware while **Windows** provides ways to do graphics, sound, printing, and multitasking. Applications that run directly in **Windows** from this era are called *Windows applications*. Users may exit **Windows** and run pure **DOS** in order to run *DOS applications*.

The **Windows 9x** family includes **Windows 95**, **Windows 98**, and **Windows ME**. It spanned an era from 1995 to the early 2000s. These systems rely on **DOS** to start up the system. **Windows 9x** then loads and takes over most OS functions though **DOS** is still retained for use as a Compatibility layer.

The **Windows NT** family includes **Windows NT**, **Windows 2000**, **Windows XP**, and all subsequent versions of **Windows** including **Vista**, **7**, **8**, **10** and **11**. **NT** was built from scratch and was released in 1993. Its goals were to modernize **Windows** in terms of security, stability, and networking. It was initially marketed as a business-oriented OS. With the release of **Windows XP** in 2001, Microsoft ended the **9x** line and moved home and business users to **NT**.

#### Software Bitness
Bits are the size of the numbers a CPU is designed to work with. Larger bit sizes allow a CPU to address more memory (i.e. RAM) and process larger amounts of data at once. Software is written with assumptions about the bitness of the CPU and OS it will run on.

There are three software bitness categories for **Windows**: 16-bit, 32-bit, and 64-bit.

The transition from 16-bit to 32-bit occurred gradually during the DOS, Windows 9x, and early NT eras. The transition from 32-bit to 64-bit occurred gradually during the XP, Vista, and Windows 7 eras.

Modern versions of **Windows** are almost always 64-bit and remain highly compatible with 32-bit software. However, 16-bit software is no longer supported.

Additionally, one common complication is that the bitness of a program may differ from its installer. Some 32-bit applications may come with a 16-bit installer and the Compatibility solution is then to find a workaround for the installer. Once installed, the it may be possible to run the program normally.

#### 3D
In the first years after consumer 3D graphics cards went mainstream, roughly from 1996 to 2004, "how to do 3D" had not yet been completely standardized and many competing 3D technologies existed.

The issue regarding 3D compatibility is not "is the technology old", it is "did the technology lead anywhere." 

Programs built on technologies that evolved into today's graphics hardware, APIs, and game engines tend to have fewer compatibility issues on modern systems because even if tweaks are required, modern drivers, wrappers, and compatibility layers have a lineage to build on. Programs built on dead-end, highly hardware-specific, or custom 3D tech often have significant compatibility challenges.

#### Running Directly on Windows
Some old **Windows** software can run directly on modern systems. This works surprisingly well for old **Windows 2000** and **Windows XP** software (or any later versions of NT **Windows**) and for some **Windows 9x** software. Productivity applications and 2D software are more likely to work than 3D games.

Modern **Windows** includes a built-in compatibility mode. This is mostly behind-the-scenes configuration rather than a full Compatibility layer. Right-click on a program, click **Properties**, and go to the **Compatibility** tab. The effectiveness of these settings varies between applications. Compatibility mode may be updated as part of various **Windows** updates. Software that once failed may later work (and vice versa).

> Recommendations:
> * For **Windows 95**, **Windows 98**, and especially **Windows XP** or later software, try running the application on modern Windows normally. 
> * If that fails, try compatibility mode.
> * If that fails, try searching for compatability patches or special configurations specific to the desired piece of software.

#### Windows VMs
A VM is an option if the main compatibility issue is that your software needs a specific operating system. VMs on modern **Windows** are primarily designed to support current versions of **Windows** and **Linux** because there is little business demand for running very old operating systems. When they work, VMs can run software much faster than full hardware emulators because they do not need to emulate an entire PC.

Historically, VM software was a go-to solution for running **Windows XP**. However, support of **XP** has gradually declined as virtualization software and modern operating systems have moved on. **XP** is still easy to install on some VMs but features such as audio, graphics, and device integration may work imperfectly and require significant effort and experimentation to improve.

* **VirtualBox**: A free, stable solution from Oracle that continues to receive incremental updates. This is by far the easiest to set up and is your best bet for trying to run **XP** (although 3D acceleration is not generally achievable with **XP**). **VirtualBox** has a feature called **unattended install** which will install the OS for you from its installation media. This often works well but you may with to disable it and go through the set up manual if you encounter problems.

* **VMware Workstation Pro**: Historically the largest commercial desktop virtualization product. In 2024 it was released as freeware by its new owner Broadcom. It continues to recieve updates as of 2026. Although free, it is tough to download through Broadcom's labyrinthine website (which also requires account creation and registration). Older versions worked well with **XP**, but support has gradually declined. Issues such as audio distortion are common, and some users report needing to adjust advanced **VMware** security and compatibility settings to obtain acceptable performance.

* **Hyper-V**: Microsoft's successor to **Virtual PC**, introduced in the **Windows 7** era. It is available only on Pro and Server editions of **Windows** and focuses on server and business applications. It is not a separate program but a feature you can enable in **Windows** under **Turn Windows features on or off**. It is great for spinning up a modern OS for tech work but is not intended to run legacy desktop operating systems. If you attempt to set up an old OS, choose the **Generation 1** VM option and do not expect much documentation or community support.

> Recommendations: 
> * VMs are most useful for modern OSes but still may work for some Windows XP software.
>  Look elsewhere for solutions to run multimedia, 3D games, and very old software.
> * Try **VirtualBox** for a lightweight and easy VM.
> * Try **VMware Workstation** for a VM with more features.
> * Try **Hyper-V** for enterprise, server, tech work-related workloads.

#### Windows Emulators
**DOSBox** is one of the most actively developed PC emulators. Its goal is to simulate a generic DOS-era PC that can run as many different software programs as possible (especially games). When you download and run **DOSBox**, the OS *just runs* with no need to set one up yourself. **DOSBox** can be tricky as far as getting particular applications to work, requiring you to either edit text configuration files manually or to download a separate frontend that lets you configure using a UI. Often, you can look up configuration guides for popular apps and games. Many retro game re-releases on stores like GOG and Steam are running **DOSBox** under-the-hood. It can also run early Windows programs (aka thru Windows 3.1) although compatibility is less good than for pure DOS applications.

**PCEm** is an emulator whose goal is to emulate PC hardware at low level with high accuracy. It achieved this for **DOS** and **Windows** era PCs and was actively developed from 2007 to 2020. A successor project, begun in 2016, is **86Box**. **86Box** has aggressively expanded the range of hardware that can emulated and has also taken on other improvements.

The focus of **PCEm** and later **86Box** historically ended around the Pentium II era (when **Windows 9x** dominated). Pentium III and 4 systems have generally been outside of their project scope. Pentium III and 4 systems accompanied a rapid increase in PC hardware complexity and the rise of 3D tech. Accurately emulating this hardware requires substantially more work than earlier PC platforms, and emulating the increasingly fast CPUs would be very demanding. Because of this, there is a bit of an awkward Compatibility gap for late **Windows 98** and early **Windows XP** software, especially games built on dead-end 3D tech.

> Recommendations:
> * Try **DOSBox** first for almost any **DOS** program and for more simple **Windows 3.1** programs.
> * Try **86Box** for **DOS**, **Windows 3.1**, **Windows 95**, and **Windows 98** software, especially if you want to recreate the historic experience of setting up an old PC.
> * Try a VM for **Windows XP** software after you have already tried running it directly on modern **Windows** first.
> * Look elsewhere for solutions to run **Windows XP** or later programs. 

#### Windows Guide: 86Box (MS-DOS 6.22 and Windows 3.11 for Workgroups on a 486 CPU)

#### Hardware and OS Setup
* Links
  - [Site](https://86box.net/)
  - [Github](https://github.com/86Box/86Box)
* Download an **86Box** release as well as the **86Box ROM Set**.
  - Extract the ROM set into the same folder as the emulator, in a directory called `roms`.
* Set up a new machine using **New Machine**.
* Set the following hardware configuration:
  - **Machine**
    - **Machine Type**: `[1994] i486 (Socket 3 PCI)`
    - **Machine**: `[i420EX] Intel Classic/PCI ED`
    - **Memory**: `32 MB`
    - **CPU Type**: `Intel i486DX2 @ 66 MHz`
  - **Display**
    - **Video**: `[PCI] S3 Trio64`
  - **Input devices**
    - **Keyboard**: `AT Keyboard`
    - **Mouse**: `Microsoft Serial Mouse`
  - **Sound**
    - **Sound card 1**: `[ISA16] Sound Blaster 16`
    - **MIDI**: `Roland MT-32 (New) Emulation`
  - **Hard disks**
    - **File name**: (as desired)
    - **Type**: `518 MB (CHS: 1054, 16, 63)`
  - **Floppy & CD-ROM drives**
    - **Floppy**
      - `3.5" 1.44M`
    - **CD-ROMs**
      - `Bus: ATAPI`
      - `Speed: 8x`
* Install the OS.
  - Install **MS-DOS 6.22**.
    - Usually this is three 1.44 MB 3.5" disk images.
  - Install **Windows 3.11 for Workgroups** on top of **DOS**.
    - Usually this is eight 1.44 MB 3.5" disk images.
    - Express setup is OK.

#### Notes on Sound Hardware
* Historically, most users relied on a single sound card to do both synthesizer music (MIDI) and sound. The setup above is a premium configuration where the Sound Blaster can be used for both sound and MIDI, but the Roland MT-32 is available to handle MIDI for programs that support it.
* The Roland MT-32 was an expensive MIDI synthesizer popular with enthusiasts and game developers. Many classic DOS games include dedicated MT-32 support and are often considered to sound their best when using it. If you want a more typical mid-1990s setup, you can omit the MT-32 and use only the Sound Blaster.

#### Important Information for Using the Emulated System 
* Basic **DOS** commands and programs.
  - When navigating folders in **DOS** use `cd` to change directories like `cd C:\FOLDER\SUBFOLDER`.
  - To see what is in a directory, enter `dir`. To see only files with a particular name or file extension, wildcards can be used like `dir NAME*` for files starting with "Name", or `dir *.TXT` for files ending with `.TXT`.
  - To change to a different drive, type `A:`, `C:`, `D:`, etc.
  - Many installers require you to change to the directory of where the installer is located and then type `SETUP`, `SETUP.EXE`, `INSTALL`, `INSTALL.EXE`, etc.
  - To edit a file in **DOS** type the command `EDIT <FILE>`.
  - To copy all files in a directory to another directory, use `copy` like `copy C:\SOURCE\*.* C:\DEST\`.
    - You can copy just one file like `copy C:\SOURCE\FILE.TXT C:\DEST\FILE.TXT`
  - If a command prints a lot of text, add `| MORE` to the end of your command like `<command> | MORE` to page through the text.
  - When the system boots it enters **DOS**. Type `win` if you want to start **Windows**. To return to **DOS**, exit **Windows**.
* Basic **DOS** tips
  - You may reboot or turn off **DOS** anytime it is sitting at the command prompt doing nothing without harming the system. Unlike modern operating systems, **DOS** does not provide a restart or shutdown menu.
    - Reboots can be performed from the **86Box** **Action** menu. To power off the system, simply close **86Box**.
  - Files on a **DOS** system can get messy fast. Try to put things in organized folders like using `C:\DRIVERS\` for all your drivers.
* Basic **Windows** tips
  - In **Windows**, you may want to go to **Control Panel > Mouse** and reduce the **Mouse Tracking Speed** if it is too fast.
* **DOS** configuration files.
  - `CONFIG.SYS`: Loads low-level drivers and configures **DOS** itself. 
  - `AUTOEXEC.BAT`: Runs commands automatically when **DOS** starts.
  - These files are normally located in `C:\`. Whenever making a change to either of these, you must reboot for them to take effect.
  - Whenever you run a setup or program it is a good idea to inspect these files to see what the setup has changed or added.
  - If you put `REM` at the beginning of a line, such as `REM MSCDEX.EXE /D:MSCD001`, that line will be ignored. `REM` stands for "remark". This can be useful for troubleshooting or temporarily disabling a driver or startup program while testing alternatives.
* Basic **86Box** actions.
  - Press <kbd>Ctrl</kbd> + <kbd>End</kbd> to let your mouse escape being captured by the emulator window.
  - To share files with your host machine with the emulated system, look under the **86Box** **Media** file menu.
    - Choose **Media > CD-ROM > Folder...** and this presents a folder on the host system as a read-only virtual CD-ROM disk.
    - You may also mount floppy disk images or CD images under the **Media** menu.
    - It will be impossible for your system to use CDs until you install a CD-ROM driver. If the CD-ROM driver you have is in the form of files, instead of a floppy disk image, you will have to create a floppy disk image.
      - On **Windows** the shareware **WinImage** can be used to create floppy disk images.
      - On **macOS** and **Linux**, command-line tools such as `dd` and `mtools` can be used to create floppy disk images.
  - **DOS** cannot easily handle `zip` files. If you encounter a `.zip` file, unzip it on your host machine before trying to share the files inside it with the emulated system.

#### Setup Oak CD-ROM Universal ATAPI IDE Driver (`OAKCDROM.SYS`), a CD-ROM driver
* Usually, this comes in the form of a single file: `OAKCDROM.SYS`. Copy it to `C:\DRIVERS\OAKCDROM.SYS`.
* Edit `CONFIG.SYS` to add the line `DEVICE=C:\DRIVERS\OAKCDROM.SYS /D:MSCD001` to make sure **DOS** loads the driver.
* Edit `AUTOEXEC.BAT` to add the line `C:\DOS\MSCDEX.EXE /D:MSCD001` to make sure **DOS** uses the driver.
* The identifier `/D:MSCD001` must match between the two files.

#### Setup Microsoft Mouse Driver Version 8.2 (`MOUSE.COM`), a mouse driver
* Some distributions consist only of the file `MOUSE.COM`.
  - Copy it to `C:\DRIVERS\MOUSE.COM`
  - Edit `AUTOEXEC.BAT` to add the line `C:\DRIVERS\MOUSE.COM`
* Other distributions are in the form of a setup program. Run the setup and it will configure things automatically.
  - You can open `CONFIG.SYS` and `AUTOEXEC.BAT` to see what was changed.

#### Set up S3Trio64, a video driver
* This improves video in **Windows**. Most **DOS** programs talk to video hardware directly without a driver.
* From DOS, copy the file `S3WIN31.EXE` to `C:\DRIVERS\S3WIN31.EXE`.
* Run `S3WIN31.EXE` to extract the driver files.
* Enter **Windows** and run **Windows Setup**.
* Go to **Options > Change System Settings**, and under **Display** choose **Other Display**.
* Enter `C:\Drivers\S3Win31` as the OEM setup path.
* Choose the driver **S3 Trio64 1.61-03 1024x768 64K col SF**
  - SF and LF mean "small fonts" and "large fonts"
* I have seen weird popups where it asked me to insert the driver disk. I clicked through them all, went through **Windows Setup** again and selected the driver again, and it worked the second time.

#### Set up Creative Labs Sound Blaster 16AWE, a sound driver
* The driver package includes drivers for regular **Sound Blaster 16** as well as the **AWE** variant.
* From DOS run `Install.exe` and it will copy any appropriate files to your `C` disk. Default settings are OK.
* If you have trouble with the sound card later you can run `C:\SB16\DIAGNOSE`.

#### Dealing with DOS Out-of-memory issues
* DOS was originally designed to use only up to 1 MB of memory (although there were later techniques to exceed this). However, many **DOS** programs were written with the assumption that they would run within the first 1 MB of memory.
* DOS applications generally run in the first 640 KB of memory, called *conventional memory*. Drivers such as for the CD-ROM, mouse, and sound card also consume this limited space, causing some programs (especially games) to run out of the conventional memory. You might see this in the form of an "out of memory" error presented by the program.
* The address space between 640 KB and 1 MB is reserved for hardware and system functions.
* Some programs such as games need a lot of conventional memory. You can see what programs and drivers are currently running, and what types of memory they are consuming, by entering `mem /C`. 
* If you encounter memory problems, there are two common approaches, see below.

##### Memory-saving approach 1: Driver replacements
* This approach is commonly recommended by modern retro-computing guides. These drivers were designed to be smaller and more memory-efficient than many of the drivers that were commonly used during the DOS era. They could be run on real DOS hardware but were not part of a typical mainstream DOS setup.
* For a smaller CD-ROM driver, use **Acer CDROM Universal ATAPI IDE Driver** (`VIDE-CDD.SYS`)
  - This usually comes as an installer, rather than a single file.
  - Run `SETUP.EXE` and specify the install directory `C:\DRIVERS\ACERCD\`. It should configure your **DOS** configuration files for you.
* For a smaller mouse driver, use **CuteMouse** (`CUTEMOUSE.EXE`)
  - This comes as a single file, `CUTEMOUSE.EXE`, rather than with an installer.
  - Copy to `C:\DRIVERS\CTMouse.exe`
  - Add a line to `AUTOEXEC.BAT`: `C:\DRIVERS\CTMouse.exe`
* For a replacement of `MSCDEX` (the **DOS** program that allows applications to access CD-ROM drives through a CD-ROM driver) consider `SHSUCDX`
  - Download `SHSUCDX v3.09`
  - Copy `SHSUCDX.COM` to `C:\DRIVERS\SHSUCDX.COM`
  - To use this, edit `AUTOEXEC.BAT` and replace references to `MSCDEX.EXE` with `SHSUCDX.COM`.

##### Memory-saving approach 2: Traditional DOS Memory Management
* The 640 KB to 1 MB memory space is technically reserved but parts of it go unused and drivers (and other system programs) can be moved into this unused space in order to free up conventional memory for other applications.
* The technique of moving drivers into unused memory between 640 KB and 1 MB is called using *upper memory blocks* (UMBs).
* Most programs work fine with drivers loaded into UMBs, though issues can occur. Most commonly a driver may work normally in most cases but fail for particular programs. but fails for a particular program.
* You can see what programs and drivers are currently running, and what types of memory they are consuming, by entering `mem /C`. 
  - *Note which programs are using up conventional memory. If a program does not appear in the list, do not re-configure it to use UMBs. Some programs might run on startup to do minor testing and then exit without consuming any memory permanently*.
* Remember: whenever you make a change, you must reboot to see it take effect.
* Here is how to move drivers and programs into UMBs:
  - Step 1. Ensure DOS memory management is enabled.
    - In `CONFIG.SYS` you should see a line loading `HIMEM.SYS` like `DEVICE=C:\DOS\HIMEM.SYS`.
    - You should also see `DOS=HIGH`, which allows DOS to move part of itself out of conventional memory.
  - Step 2. Turn on UMB support.
    - In `CONFIG.SYS`, add `DEVICE=C:\DOS\EMM386.EXE NOEMS`.
    - Change `DOS=HIGH` to `DOS=HIGH,UMB`.
  - Step 3. Move device drivers to UMBs.
    - Look in `CONFIG.SYS` for device drivers. To move these to UMBs, change `DEVICE=` to `DEVICEHIGH=`.
    - If a driver stops working after being moved, change it back to `DEVICE=`. 
    - Do not move memory management drivers like `HIMEM`, or `EMM386` to `DEVICEHIGH`.
  - Step 4. Move startup programs to UMBs.
    - Look in `AUTOEXEC.BAT` for programs you might move to UMBs, especially some of the driver-related programs you may have installed earlier.
    - Change these to load into UMBs by changing lines like `C:\DRIVERS\CTMOUSE.EXE` TO `LH C:\DRIVERS\CTMOUSE.EXE`.
    - Again, if moving something to UMBs causes issues, simply move it back.

### Windows Guide: 86Box (Windows 98SE on a Pentium II-era CPU)

#### Hardware and OS Setup
* Links
  - [Site](https://86box.net/)
  - [Github](https://github.com/86Box/86Box)
* Download an **86Box** release as well as the **86Box ROM Set**.
  - Extract the ROM set into the same folder as the emulator, in a directory called `roms`.
* Set up a new machine using **New Machine**.
* Set the following hardware configuration:
  - **Machine**
    - **Machine Type**: `[1998] Socket 370`
    - **Machine**: `[i440BX] ASUS CUBX`
    - **Memory**: `128 MB`
    - **CPU Type**: `Intel Celeron (Mendocino)`
    - **Frequency**: `466`
  - **Display**
    - **Video**: `[AGP] 3dfx Voodoo3 3000`
  - **Input devices**
    - **Keyboard**: `AT Keyboard`
    - **Mouse**: `PS/2 Mouse`
  - **Sound**
    - **Sound card 1**: `PCI Sound Blaster PCI 128 (ES1373)`
  - **Hard disks**
    - **File name**: (as desired)
    - **Type**: `8192 MB (CHS: 16644, 16, 63)`
  - **Floppy & CD-ROM drives**
    - **Floppy**
      - `3.5" 1.44M`
    - **CD-ROMs**
      - `Bus: ATAPI`
      - `Speed: 32x`
* Install Windows 98 SE:
  - Usually this is a single CD-ROM `.iso` image. Mount this image using the **Media** menu in **86Box** and when prompted choose to run **Windows Setup** from the CD-ROM.
  - You can use most default options, but make sure that, when prompted, to select **Yes, enable large disk support**.
  - You may reboot several times in which case choose to boot from the setup CD-ROM each time you are prompted.
  - After the setup has copied the windows files and displays **Getting ready to run Windows for the first time** you should choose to boot from the hard drive instead when prompted.
  - You will need to enter a valid Windows 98 SE product key.
  - After setup is complete, unmount the setup CD.
* Install the **3DFX VooDoo 3 3000 AGP Video Card Drivers**.
* Install the **Sound Blaster PCI 128** drivers.
  - It may pop up a window asking you to register but you can cancel out of that.
* Install the **Intel Chipset Device Software** for the **ASUS CUBX** motherboard.
* You may want to install **DirectX 9.0c**, the final version for this OS.
  - **DirectX 6.1a** comes with **Windows 98 SE**.
* When you want to shut down **Windows**, click the **Start** menu on the bottom-left and choose **Shut Down**

#### Creating Data Hard Disk Images (`.vhd`)
* If you have a large folder greater than the capacity of most CD dics (which usually top out at 650 or 700 MB), then you may have trouble trying to mount that folder as a virtual CD.
* Instead, create a virtual hard disk and put your data on it, then add it to the configuration of the simulated system.
* In **Windows 11**
  - Press <kbd>Win</kbd> + <kbd>X</kbd> and select **Disk Management**.
  - **BE CAREFUL: this includes your host machine's actual disks, do not touch those.**
  - Select **Action > Create VHD**
  - Save the `.vhd` somewhere on your disk.
  - After it appears, right-click on the new disk, near the name of the disk, and click **Initialize**, and choose **MBR**.
  - Right-click the unallocated space and choose **New Simple Volume**, choose a drive letter, and format as **FAT32**.
  - Now you have a new virtual drive on your host machine where you can copy files.
  - When you are done copying files to the disk, go back to **Disk Management** right-click the disk and choose **Detach VHD**.
  - You may now add the disk to your **86Box** configuration.
* You can also use these on the **DOS** machine though the maximum size the `.vhd` may be is 2 GB on this system.
