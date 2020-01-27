# Configuration Guide

## Purpose
The purpose of this document is a step-by-step setup guide for software development machines. In contrast to hard drive images, a guide allows each user to understand how their machine and IDEs work, preventing the emergence of configuration "black boxes". It also allows each user to customize things as they go.

## Windows Setup

### Create Windows Install Media
* Obtain a windows setup iso and a flash drive.
* At the command prompt, run `diskpart`
  * `list disk`
  * `select disk #` replacing `#` with the index of the USB flash drive.
  * `clean`
  * `create partition primary`
  * `select partition 1`
  * `format fs=ntfs quick`
  * `assign`
  * `exit`
* Copy the files from the windows iso to the flash drive.
* At command prompt run `X:\boot\bootsect.exe /nt60 X:`, replacing `X` with the drive letter of the flash drive.
  * You may run the above command with the `/force` flag if there is an issue getting exclusive access to drive.

### Install Windows
* If you are re-installing Windows on the same machine, you can skip entering a product key.
* Choose a custom install and delete all existing partitions.
* Choose an 'offline account' instead of a Microsoft account. This may be hidden in a corner after a 'Next' button that otherwise indicates you'd have to setup an account.
* Set most features to 'off' when prompted unless you need a specific feature.
* Run Windows Update.
* Set the correct time zone.
* Disable hibernation like `powercfg -h off`.
* Disable system restore.
* Disable remote assistance.

## Cygwin Setup

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
  * Set the following user environment variables: `HOME: %USERPROFILE%\home`
  * Create and use the following shortcut to access bash:
  * `C:\cygwin64\bin\bash.exe --login -i`
  * Start in `C:\Users\<User>\home`
  * To clear any outputs from the startup script, you can add `printf "\033c"` to the bottom of `~/.bash_profile`.
  * In `C:\cygwin64\etc\nsswitch.conf` include the line `db_home: /%H/home/` to ensure Cygwin uses the windows user profile as its home directory.

### emacs
 * Required packages: emacs, emacs-w32
  * Run `git config --global core.editor "emacs"`
  * Set the following user environment variables:
    * `VISUAL: emacs`
    * `EDITOR: $VISUAL`

### git
* Required packages: git, gitk, openssh
* Set git global settings.
  * Run `git config --global user.name "<Full Name>"`.
  * Run `git config --global user.email "<Email>"`.
* Create an ssh key for services such as github or bitbucket.
  * `cd ~/.ssh`
  * `ssh-keygen -t rsa -C "<Email>" -f id_rsa`
  * `chmod 400 id_rsa`
  * Copy the clipboard to your public key with `clip < id_rsa.pub`
  * Open your user configuration on your desired services and add the ssh key.
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
* To test your ssh connection, use `ssh` like `ssh -vT git@github.com`

### make
* Required packages: make

### tex
* Required packages: texlive, texlive-collection-latex

### x
* Required packages: xinit, xorg-server
* Set the following user environment variables: `DISPLAY :0`
* To start xwin automatically on launching Cygwin, add the following to `~/.bash_profile`:

```
# Start xwin
if ! ps | grep /usr/bin/xwin
then
  run xwin -multiwindow -noclipboard
fi
```

## Unity Setup
* Install Unity. It is reccomended to first install Visual Studio seperately rather than using the version that comes with the Unity installer.
* Set the script templates under *C:\Program Files\Unity\Editor\Data\Resources\ScriptTemplates* to conform to any coding standards.

## Visual Studio Setup
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
