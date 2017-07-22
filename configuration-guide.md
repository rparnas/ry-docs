# Configuration Guide

## Purpose
The purpose of this document is a step-by-step setup guide for software development machines. In contrast to hard drive images, a guide allows each team member to understand how their machine and IDEs work, preventing the emergence of configuration "black boxes". It also allows each member to customize things as they go.

## OSX: Git Setup
* Set git global settings.
  * Run `git config --global user.name "<Full Name>"`.
  * Run `git config --global user.email "<Email>"`.
* Create an ssh key for github.
  * `ssh-keygen -t rsa -C "<Email>`
  * `eval "$(ssh-agent -s)"`
  * `ssh-add`

## Windows: OS Setup
This is valid for Windows 7, 8, 8.1 or 10.

### Create a Windows Install Disk
* Obtain a windows setup iso file and a USB thumb drive.
* At the command prompt, run `diskpart`
  * `list disk`
  * `select disk 2` replacing `2` with the index of the USB thumb drive.
  * `clean`
  * `create partition primary`
  * `select partition 1`
  * `format fs=ntfs quick`
  * `assign`
  * `exit`
* Copy the files from the windows image to the flash drive.
* At the command prompt run `E:\boot\bootsect.exe /nt60 E:`, replacing `E` with the drive letter of the USB disk.

### Install Windows
* Delete existing partitions through custom setup.
* Do not use express settings. Use customized settings.
  * Click no for discovering devices. Set every setting to off except for the do not track cookie and windows update.
* When you get to setting up your Microsoft account, click create a new account. From there, you should be able to find a button letting you create a local account only.
* Run Windows Update and get all the latest critical updates.
* Set the correct time zone.

## Windows: Cygwin

### Cygwin
* Copy the Cygwin installer `setup-x86_64.exe` to `C:\cygwin64-install\`.
* Run `setup-x86_64.exe`.
  * Choose to install from the internet.
  * Leave the root directory as `C:\cygwin64\`.
  * Set the local package directory to `C:\cygwin64-install\`.
  * Choose your packages. This document recommends the following, and you can read ahead to see what they are used for. You can always change your packages later if needed.
    * emacs
    * emacs-w32
    * git
    * gitk
    * make
    * openssh
    * texlive
    * texlive-collection-latex
    * xinit
    * xorg-server 
  * Set the following user environment variables: `HOME: %USERPROFILE%`
  * Create and use the following shortcut to access bash:
  * `C:\cygwin64\bin\bash.exe --login -i`
  * Start in `C:\Users\<User>\`
  * To clear any outputs from the startup script, you can add `printf "\033c"` to the bottom of `~/.bash_profile`.

### emacs
 * Required packages: emacs, emacs-w32
  * Run `git config --global core.editor "emacs"`
  * Set the following user environment variables:
    * `VISUAL: emacs`
    * `EDITOR: $VISUAL`

### git (and Github)
* Required packages: git, gitk, openssh
* Set git global settings.
  * Run `git config --global user.name "<Full Name>"`.
  * Run `git config --global user.email "<Email>"`.
* Create an ssh key for github.
  * `cd ~/.ssh`
  * `ssh-keygen -t rsa -C "<Email>" -f ./id_rsa`
  * `chmod 400 ~/.ssh/id_rsa`
  * Copy the clipboard to your public key with `clip < ~/.ssh/id_rsa.pub`
  * Open your gethub user configuration and add the ssh key.
  * To make sure your ssh-agent is ready to go whenver you run Cygwin, copy the following into `~/.bash_profile`:

```
# Start ssh-agent
# Query the agent for available keys.
# If none are found, try to load the agent config from a file.
# If it still can't connect to the agent, start a new ssh-agent.
ssh-add -l
if [ "$?" == 2 ]; then
  test -r ~/.ssh-agent && \
    eval "$(<~/.ssh-agent)"
  ssh-add -l
  if [ "$?" == 2 ]; then
    (umask 066; ssh-agent > ~/.ssh-agent)
    eval "$(<~/.ssh-agent)"
    ssh-add ~/.ssh/id_rsa
  fi
fi
```

### make
* Required packages: make

### tex
* Required packages: texlive, texlive-collection-latex

### x
* Required packages: xinit, xorg-server
* Set the following user environment variables: `DISPLAY :0`
* To start xwin automatically on launching Cygwin, add the following to `~/.bash_profile`:

```
if ! ps | grep /usr/bin/xwin
then
  run xwin -multiwindow -noclipboard
fi
```

## Windows: Unity
* Install Unity. It is reccomended to first install Visual Studio seperately rather than using the version that comes with the Unity installer.
* Set the script templates under *C:\Program Files\Unity\Editor\Data\Resources\ScriptTemplates* to conform to any coding standards.

## Windows: Visual Studio
* For each visual studio you need to install, start with the oldest first.
* It is recommended that you download a complete Visual Studio setup rather than installing from the web. To do this, acquire the web installer and run the installer with the argument `/layout`. For example: `vs_community__8b6e245420ae4e408ba8397154f28d5e.exe /layout`.
* During the install, you will be asked to choose development settings. Choose `Visual C#`. If you forget to do this, it can be changed later by going to **Tools->Import and Export Settings...** and then choosing **Reset all settings** on the wizard.
* In Visual Studio, set the following options under **Tools->Options**: 
  * Under **Environment->Documents** check **Reload modified files unless there are unsaved changes**
  * Under **Tools->Options->Text Editor->All Languages->Tabs** choose
    * **Indenting**: Smart
    * **Tab size**: 2
    * **Indent size**: 2
    * Check **Insert Spaces**. 
* If you have trouble with line endings, download and install [Strip 'em](http://www.grebulon.com/software/stripem.php) to automatically normalize line endings in Visual Studio whenever a file is saved.
* If using a recent version of Visual Studio, make sure to log into an appropriate Microsoft account.
