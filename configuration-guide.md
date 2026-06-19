# Configuration Guide

## Purpose
The purpose of this document is a step-by-step setup guide for software development machines. In contrast to hard drive images, a guide allows each user to understand how their machine is setup instead of configuration being a "black box". It also allows users to customize as they go.

## Windows

### Create Windows Install Media
* Download the latest **Windows Media Creation Tool** and use it to set up a bootable USB drive.

### Install Windows
* Choose a custom install and delete all existing partitions.
* Set most features to **off** when prompted unless you need a specific feature.
* **Windows Setup** will require you to login with a Microsoft account.

### Setup Windows
* If you wish to log into the system with a local account, rather than the default Microsoft account linked account, create a local account then delete the linked account.
* You may create a folder at `%userprofile%\home` which is usually `C:\Users\<username>\home` to be your `home` folder as opposed to using the user profile directly. This allows you to backup your home folder leaving out the junk various Windows programs tend to accumulate and place in the user folder.
* If using a custom home directory you may want to move the Desktop folder to be a subdirectory of home. Right-click on **Desktop** in **File Explorer** and select **Properties**. You may move the desktop's location using the **Location** tab.
* Run **Windows Update**.
* Set the correct time zone.
* Disable hibernation like `powercfg -h off`.
* Disable system restore.
* Disable remote assistance.

## Windows Boot Menu
* If you are installing multiple copies of **Windows**, you can manipulate the boot menu using **bcedit**.
* `bcedit /set {name} description "Description"` sets the description
* `bcedit /displayorder {name0} {name1}` sets the menu order
* `bcedit /default {name0}` sets the default entry
* `bcedit /timeout <seconds>` sets how long to wait before the boot manager selects the default entry.

## Cygwin on Windows

### Cygwin
* Copy the **Cygwin** installer `setup-x86_64.exe` to `C:\cygwin64-install\`.
* Run `setup-x86_64.exe`.
  * Choose **Install from Internet**.
  * Leave the root directory `C:\cygwin64\`.
  * Leave the package directory as `C:\cygwin64-install\`.
  * Choose your packages. **Look ahead in this document to see packages you may need**.
  * Set the following user environment variables: `HOME: %USERPROFILE%\home`
* Ensure **Terminal** is set as the default terminal application
  - Open **Terminal**
  - Go to **Settings**
  - Under **Default Terminal Application** set **Windows Terminal**
* Add a profile for **cygwin**
  - Open **Terminal**, go to **Settings** and click **Add a new profile**
  - Create a new empty profile
  - Set the name to `Cygwin`
  - Set the command line to `C:\cygwin64\bin\bash.exe --login -i`
  - Set the starting directory `%USERPROFILE%\home`
  - You may want to use one of the icons at `C:\cygwin64\`
* To clear any outputs from the startup script, you can add `printf "\033c"` to the bottom of `~/.bash_profile`.
* In `C:\cygwin64\etc\nsswitch.conf` include the line `db_home: /%H/home/` to ensure **Cygwin** uses the **Windows** user profile as its home directory.

By default this will update the title every command as you navigate directories, etc. If you want to add the ability to set a custom title for an open terminal tab, replace that line with ... and then whenever you wish to set a permanent title for a tab, run the command `export TAB_TITLE "MyTitle"`.

### emacs
 * Required packages: **emacs**, **emacs-w32**
  * Set the following user environment variables:
    * **VISUAL**: `emacs`
    * **EDITOR**: `$VISUAL`

### git
* Required packages: **git**, **gitk**, **openssh**
* Set **git** global settings.
  - Run `git config --global core.editor "emacs"`
  - Run `git config --global user.name "<Full Name>"`.
  - Run `git config --global user.email "<Email>"`.
* Create an ssh key for services such as **Bitbucket**, **GitHub**.
  - `cd ~/.ssh`
  - `ssh-keygen -t rsa -C "<Email>" -f id_rsa`
  - `chmod 400 id_rsa`
  - Copy the clipboard to your public key with `clip < id_rsa.pub`
  - Open your user configuration on your desired services and add the ssh key.
  - To make sure **ssh-agent** is ready to go whenver you run **Cygwin**, copy the following into `~/.bash_profile`:
```
start_ssh_agent() {
  local agent_file="$HOME/.ssh/ssh-agent.env"

  # Already connected to a working agent
  if ssh-add -l >/dev/null 2>&1; then
    return
  fi

  # Try saved agent environment
  if [ -r "$agent_file" ]; then
    . "$agent_file"

    if ssh-add -l >/dev/null 2>&1; then
      return
    fi
  fi

  # Start new agent
  mkdir -p "$HOME/.ssh"
  (umask 077; ssh-agent > "$agent_file")
  . "$agent_file"

  ssh-add "$HOME/.ssh/id_rsa"
}

start_ssh_agent
```
* To test your ssh connection, use `ssh` like `ssh -vT git@github.com`

### make
* Required packages: **make**

### tex
* Required packages: **texlive**, **texlive-collection-latex**

### x
* Required packages: **xinit**, **xorg-server**
* Set the following user environment variables: **DISPLAY**: `:0`
* To start **xwin** automatically on launching **Cygwin**, add the following to `~/.bash_profile`:

```
start_xwin() {
  if ! ps | grep '[x]win' >/dev/null; then
    run xwin -multiwindow -noclipboard
  fi
}

start_xwin
```

## Visual Studio
* Download the **Visual Studio** from https://visualstudio.microsoft.com/downloads/
* When first running **Visual Studio** you will be asked to choose **Development Settings**. Choose **Visual C#**.
  - If you need to change this later you can go to **Tools > Import and Export Settings...** and then choose **Reset all settings** on the wizard.
* In Visual Studio, set the following options under **Tools > Options**: 
  - Under **Environment > Documents** check **Reload modified files unless there are unsaved changes**
  - Under **Tools > Options > Text Editor > All Languages > Tabs** choose
    - **Indenting**: **Smart**
    - **Tab size**: `2`
    - **Indent size**: `2`
    - Check **Insert Spaces**. 
* Log into an appropriate Microsoft account if desired.
