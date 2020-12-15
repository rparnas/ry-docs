# Streaming

## Video Streaming
Streaming using a virtual webcam has an advantage in video quality, video and audio stability and bandwidth required (as opposed to streaming using screen share). This setup should be used with a reasonably fast computer or with a video card that supports hardware video encoding in VBS.

If using the virtual webcam to stream to Discord the reamaining issues are:
* Audio quality. This seems to be very limited except perhaps on high server boost levels. However, as long as voice-specific audio processing is turned off, the audio does not seem worse than with Discord screen share.
* Video picture quality is very good, but the number of frames being shown still appears lower than the original material, giving it a low frame rate look. **TODO: Determine if this is actually an issue with the stream participant**.

The above issues could perhaps be addressed by also hosting the stream itself (instead of sending it to Discord). However, this would require enough bandwidth to multiplex the stream to all participants. Or an alternative streaming host/chat application could be used.

When using a virtual webcam to stream you may wish to stream from one computer while joining the stream as a participant from another computer (especially for the inconvienece of changing voice settings back if you switch to using discord directly for microphone audio again). Otherwise see the steps below to do everything on the same machine. Note that in Discord and many other conferencing applications, the video preview of the OBS virtual webcam will be horizontally flipped on the local machine only.

### Setup Virtual Audio
* A virtual audio input device is required to pass along the audio from a virtual OBS-based webcam. This is because many communication applications can only take audio from devices listed explicitly under *Control Panel \ Sound \ Recording*.
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
* Right-click the *Audio Mixers* and choose  *Advanced Audio Properties*. Ensure that under the *Monitoring* column, the VLC audio source is set to *Monitor Only*.
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
    
### Additional Setup to Host the Stream and Engage in the Stream as a Participant from One Computer 
* To speak on the stream add your microphone to the OBS Studio audio mixer. Under the *Audio Properties*, under the *Monitor* column, choose *Monitor Only* for this device.
* **TODO: How to listen to the audio of the video being streamed (without also hearing your own microphone).**
* To view the streamed video in full-screen, right-click on the video preview in OBS Studio and choose *Full Screen Projector (Preview)*.
