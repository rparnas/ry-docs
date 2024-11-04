# Configuration Guide

## Purpose
The purpose of this document is a step-by-step setup guide for software development machines. In contrast to hard drive images, a guide allows each user to understand how their machine and IDEs are setup, preventing the emergence of configuration "black boxes". It also allows each user to customize things as they go.

## Windows

### Create Windows Install Media
* Download the latest Windows Media Creation Tool and use it to set up a bootable USB drive.

### Install Windows
* Choose a custom install and delete all existing partitions.
* Set most features to 'off' when prompted unless you need a specific feature.
* Windows Setup will require you to login with a Microsoft account.

### Setup Windows
* If you wish to log into the system with a local account, rather than the default Microsoft account linked account, create a local account then delete the linked account.
* You may create a folder at `%userprofile%\home` which is usually `C:\Users\<username>\home` to be your `home` folder as opposed to using the user profile directly. This allows you to backup your home folder leaving out the junk various Windows programs tend to accumulate and place in the user folder.
* If using a custom home directory you may want to move the Desktop folder to be a subdirectory of home. Righ-click on `Desktop` in File Explorer and select `Properties`. You may move the Desktop's location on the `Location` tab.
* Run Windows Update.
* Set the correct time zone.
* Disable hibernation like `powercfg -h off`.
* Disable system restore.
* Disable remote assistance.

## Setup Boot Menu
* If you are installing multiple OS, you can manipulate the boot menu with `bcedit`.
* `bcedit /set {name} description "Description"` sets the description
* `bcedit /displayorder {name0} {name1}` sets the menu order
* `bcedit /default {name0}` sets the default entry
* `bcedit /timeout <seconds>` sets how long to wait before the boot manager selects the default entry.

## Cygwin

### Cygwin
* Copy the Cygwin installer `setup-x86_64.exe` to `C:\cygwin64-install\`.
* Run `setup-x86_64.exe`.
  * Choose `Install from Internet`.
  * Leave the root directory `C:\cygwin64\`.
  * Leave the package directory as `C:\cygwin64-install\`.
  * Choose your packages. **Look ahead in this document to see packages you may need**.
  * Set the following user environment variables: `HOME: %USERPROFILE%\home`
  * Ensure `Terminal` is set as the default terminal application
    - Open `Terminal`
    - Go to `Settings`
    - Under "Default Terminal Application" set "Windows Terminal"
  * Add a profile for cygwin
    - Open `Terminal`, go to `Settings` and click `Add a new profile`
    - Create a new empty profile
    - Set the name to "Cygwin"
    - Set the command line to `C:\cygwin64\bin\bash.exe --login -i`
    - Set the starting directory `%USERPROFILE%\home`
    - You may want to use one of the icons at `C:\cygwin64\`
  * To clear any outputs from the startup script, you can add `printf "\033c"` to the bottom of `~/.bash_profile`.
  * In `C:\cygwin64\etc\nsswitch.conf` include the line `db_home: /%H/home/` to ensure Cygwin uses the windows user profile as its home directory.

### emacs
 * Required packages: emacs, emacs-w32
  * Set the following user environment variables:
    * `VISUAL: emacs`
    * `EDITOR: $VISUAL`

### git
* Required packages: git, gitk, openssh
* Set git global settings.
  * Run `git config --global core.editor "emacs"`
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

## Visual Studio
* Download the Visual Studio Community installer from https://visualstudio.microsoft.com/downloads/
* When first running Visual Studio you will be asked to choose `Development Settings`. Choose `Visual C#`. If you need to change this later you can go to **Tools->Import and Export Settings...** and then choose **Reset all settings** on the wizard.
* In Visual Studio, set the following options under **Tools->Options**: 
  * Under **Environment->Documents** check **Reload modified files unless there are unsaved changes**
  * Under **Tools->Options->Text Editor->All Languages->Tabs** choose
    * **Indenting**: Smart
    * **Tab size**: 2
    * **Indent size**: 2
    * Check **Insert Spaces**. 
* If you have trouble with line endings, download and install [Strip 'em](http://www.grebulon.com/software/stripem.php) to automatically normalize line endings in Visual Studio whenever a file is saved.
* Log into an appropriate Microsoft account.
