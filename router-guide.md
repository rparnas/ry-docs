# Router

## Purpose
Information about settings on my router. I use these ASUS models:

- RT-AC86U (Wi-Fi 5)
- RT-AX86U (Wi-Fi 6)
- RT-BE86U (Wi-Fi 7)

## Configuration

- **Traffic Analyzer**
  - **Statistic:** **ON**
    - Slight performance hit but if something goes wrong this can help a lot to analyze any rogue devices.
- **Wireless**
  - **General > Wireless Mode:** **Disable 11b**
    - Removes support for 802.11b (1999-era) devices, reducing airtime overhead. 
  - **WPS > Enable WPS:** **Off**. 
    - Disables an alternative non-password method for connecting to the router.
  - **Professional > Bluetooth Coexistence:** **Enable**
    - Helps the 2.4 GHz radio better coexist with Bluetooth.
  - **Professional > Roaming assistant:** **Disable**
    - Let clients decide when the signal is so weak they want to disconnect. Turning this setting on makes more sense when your network has multiple access points.
  - **Professional > Multi-User MIMO:** **Enabled**
    - Feature on Wi-Fi 5+ only, where the router uses multiple antennas to communicate with multiple compatible devices simultaneously.
  - **Professional > OFDMA/802.11ax MU-MIMO:** **DL/UL OFDMA + MU-MIMO**
    - Feature on Wi-Fi 6+ only, where the router intelligently divides the channel into smaller pieces so multiple compatible devices can communicate at the same time.
  - **Professional > Universal Beamforming:** **Disable**
    - Attempts to focus the transmitted signal toward older devices that don't explicitly support beamforming. Seems better to just communicate with such devices normally.
- **IPv6** 
  - **Connection type**: **Disable**
    - Doesn't necessarily cause issues but seems unecessary for now.
- **Administration**
  - **System > Basic Config > Enable Reboot Scheduler:** **Yes**
    - Consider setting a weekly reboot, for example at 3:00am Sunday.
  - **Firmware upgrade > Auto Firmware Upgrade:** **On**
    - Set a Preferable Upgrade Time like 02:00am.
    - Automatically upgrades firmware.
