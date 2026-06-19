# Windows Guide

## Purpose
Tips for using Windows.

## Disabling Unwanted Programs
* Turn startup programs on or off
  1. Press <kbd>Windows Key</kbd>, type `task manager` and click on **Task Manager** on the search results.
  1. On the right, select **Startup apps**
  1. Here you can see the list of programs that automatically start when you sign in to **Windows**. See **Status** in the table to see which are **Enabled** or **Disabled**.
  1. You can disable startup apps that don't need to start right away using the Right-Click menu. (If you don't need it whatsoever, you can uninstall it instead, see **Uninstall Programs** in the guide below). This does not uninstall the app, it only stops it from launching automatically. Avoid disabling startup items if they're unsure what they do, especially security software or hardware utilities (audio, touchpad, graphics). Third-party apps (chat apps, game launchers, updaters, etc.) are safer candidates for disabling. Some apps start automatically so they can preload in the background. If you disable them from startup, they may take slightly longer to open when you use them later.
  1. If disabling a startup apps causes problems or strange behavior, you can use the Right-Click menu to **Enable** again upon startup.

## Freeing Disk Space
* Run Disk Cleanup
  1. Press <kbd>Windows Key</kbd>, type `disk cleanup`, click on **Disk Cleanup** on the search results.
  1. Pick the disk you want to free up space on, and click **OK**.
  1. Click the **Disk Cleanup** button.
  1. In the **Disk Cleanup** window, if there is a button that says **Clean up system files** click it to
  make sure you are cleaning up as much as possible. If the button is not there, move to the next step.
  1. Check what you want to clean up. *Do not* check any option in the list that says **Compress** but
  generally anything else is safe to check as long as you don't need it for some reason (e.g. you want to save some things in your **Downloads** folder). One finished, click **OK**
  1. At **Are you sure you want to permanently delete these files?** click **Delete Files**.
  1. The delete files progress bar will apear. This may tens of minutes (or longer) if there is a large
  amount of things to clean up, especially **Windows Update Cleanup**.
* Disable Hiberation
  * This turns off hibernation. Hibernation is an option that allows you to save the exact state of your
  computer and then turn it off. Personally, I don't use this: I either sleep my computer (most laptops
  enter this low-power mode when closing the lid) or shut down. If you don't want to use it, you can disable it. On some machines, this can make system startup slower.
  1. Press <kbd>Windows Key</kbd>, type `command prompt`, Right-Click on **Command Prompt** on the search results, and click **Run as Administrator**.
  1. Type `powercfg -h off` and press <kbd>Enter</kbd>.
  1. If you want to turn it back on, you can type `powercfg -h on` and press <kbd>Enter</kbd>.
* Cleanup or Disable System Restore
  * **System Restore** can consume several gigabytes of disk space. If you do not use restore points and need additional space, you can disable it or reduce the amount of disk space allocated to it. The tradeoff is that you lose the ability to restore the system to an earlier state after some software, driver, or configuration problems. If you wish to keep system restore on but believe that your PC is currently stable, you can delete old restore points while leaving the feature on to automatically create restore points going forward.
  1. Press <kbd>Windows Key</kbd>, type `system restore`, and click on **Create a Restore point** on the search results. You should be in the **System Properties** window on a tab called **System Protection**.
  1. See each drive that supports **System Restore**. Click **Configure...** on a drive.
  1. To delete all restore points, click **Delete** under **Disk Space Usage**. Do this even if you are going to disable the feature also.
  1. To disable the feature for the drive, check **Disable system protection** and click **OK** to close the window. You can now repeat for other drives.
* Uninstall Programs
  1. Press <kbd>Windows Key</kbd>, type `control panel`, Click on **Control Panel** on the search results.
  1. Look in the top right corner for **View By**. If the setting is **Category** change it to **Large Icons**.
  1. Click **Programs and Features**
  1. There is a **Size** column for the list of installed programs. You can click on this column to sort by size.
  1. Press <kbd>Windows Key</kbd>, type `settings`, and click on **Settings**. On the left-side menu, click **Apps**, and then click on **Installed Apps**. Here you can manage modern apps such as those downloaded from the **Microsoft Store** as well as normal apps. Sometimes the same programs are displayed as in **Programs and Features** are also displayed here but with more accurate size information.
* Remove Data
  1. You can use a program like * [Space Monger](https://archive.org/details/spcmn140_zip) — disk space usage visualization to visualize your hard drive and help you find large files you may be able to remove. 
