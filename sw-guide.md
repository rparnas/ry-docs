# Program Guide

## Purpose
This document is a list of go-to software for various purposes.

## Antivirus
* [AdwCleaner](https://www.malwarebytes.com/adwcleaner/)
* [Malwarebytes](https://www.malwarebytes.com/)
* [Spywareblaster](https://www.brightfort.com/spywareblaster.html)
* [Rkill](https://www.bleepingcomputer.com/download/rkill/)

## Freeing Hard Drive Space
* Run Disk Cleanup
  1. Go to **My Computer**, right-click the hard drive you want to free up space on, and click **Properties**.
  1. Click the **Disk Cleanup** button.
  1. In the *Disk Cleanup* window, if there is a button that says **Clean up system files** click it to
  make sure you are cleaning up as much as possible. If the button is not there, move to the next step.
  1. Check what you want to clean up. *Do not* check any option in the list that says *Compress* but
  generally check everything else. One finished, click **K**
  1. At *Are you sure you want to peremantely delete these files?* click **Delete Files**.
  1. The delete files progress bar will apear. This may tens of minutes (or longer) if there is a large
  amount of things to clean up, especially "Windows Update Cleanup".
* Disable Hiberation
  * This turns off "Hibernation". Hibernation is an option that allows you to save the exact state of your
  computer and then turn it off. Personally, I don't use this: I either sleep my computer (most laptops
  enter this low-power mode when closing the lid) or shut down.
  1. Press **Windows-Key + R** to open the run popup.
  1. At the run popup type **cmd** and they press **CTRL + Shift + Enter** to open the command prompt with
  Administrator privlages.
  1. Type **powercfg -h off** and press **Enter**.
* Disable System Restore
  * System Restore keeps old copies of things like the registry in case a weird program or driver causes something to break. I've never found it useful.
  1. Go to the **Control Panel**.
  1. Look in the top right corner for *View By*. If the setting is *Category* change it to **Large Icons**.
  1. Click **System** and then click **System protection** in the links on the upper left.
  1. On the *System* window, select your main hard drive and click **Configure...**
  1. Under *Restore Settings* at the top, check the **Disable system protection** radio button.
  1. Under *Disk Space Usage* at the bottom, click the **Delete** button.
  1. Click *Apply* and then **OK** to close the window.
* Uninstall Programs
  1. Go the **Control Panel**
  1. Look in the top right corner for *View By*. If the setting is *Category* change it to **Large Icons**.
  1. Click **Programs and Features**
  1. There is a *Size* column for the list of installed programs. You can click on this column to sort by size.
 

## Hard Drive Erasure
* [Eraser](https://eraser.heidi.ie/)
