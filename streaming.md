# Streaming

## Video Streaming via Discord

### Setup Virtual Audio

* A virtual audio input device is required to pass along the audio from a virtual OBS-based webcam to Discord. This is because Discord can only take audio from devices listed explicitly under *Control Panel \ Sound \ Recording*.
* Download the [VB-CABLE Virtual Audio Device](https://vb-audio.com/Cable/) and run the installer as an administrator.

* Go to both *Control Panel \ Sound \ Playback*. 
  * If a VB-Audio device is not visible right-click the empty space in the device list and click *Show Disabled Devices* to see the disabled VB-audio device. Right-click the disabled AB-Audio device and choose *Enable*. 
  * The VB-Cable installer may have changed the *Default Device* and or the *Default Communication Device* to itself. You may want to revert it back by right-clicking the appropriate device and clicking *Set as the Default Device* and *Set as the Default Communication Device* respectively.
  * Similarly ensure there is an enabled VB-Audio device under *Control Panel \ Sound \ Recording* (and revert any defaults as desired).

### Setup Virtual Webcam

* Ensure that [VLC](https://www.videolan.org/vlc/) and [OBS Studio](https://obsproject.com/) are installed.
* In OBS Studio, right-click the *Sources* list and choose *Add > VLC Video Source*. 
  * Choose the settings from the VLC Video Source as desired, including adding the video files to be streamed to the playlist. The playlist and other settings can be changed at any time by double-clicking on the source in the sources list.
* Under *File > Settings* on the *Audio* tab, ensure that *Advanced \ Monitoring Device* is set to the VB-Audio device.
  * You may additionally want to set up your output bitrates on the *Outputs* tab under *Streaming*. For 1080p resolution a *Video Bitrate* of 4000 Kbps or greater and an *Audio Bit Rate* of 320 are good rules of thumb. 
  * Right-click the *Audio Mixers* and choose  *Advanced Audio Properties*. Ensure that under the *Monitoring* column, the VLC audio source is set to either *Monitor Only* or *Monitor and Output* depending on whether you want to send the audio to the monitor only or if you also want to listen to the audio from your VLC source directly from OBS.
* On the *Audio Mixers* list you may wish to disable other audio sources.
* On the Video Preview, you should right-click the VLC video feed and choose *Resize output (source size)*.
* When you are ready to stream click *Start Virtual Camera* under *Controls* in the main window.

### Setup Discord

* In Discord, go to the *User Settings Page*.
  * Under *Voice & Video*:
    * Ensure your *Input Device* is set to VB-Audio.
    * Turn off *Automatically determine input sensitivity* and set the sensitivity threshold to the minimum value (-100 dB).
  * Under *Video Settings*:
    * Set *Camera* to the OBS Virtual Camera.
  * Under *Advanced* ensure that the following are disabled:
    * Noise Suppression
    * Echo Cancellation
    * Noise Reduction
    * Advanced Voice Activity (disable if it is not already greyed-out).
    * Automatic Gain Control
