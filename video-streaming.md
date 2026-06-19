# Streaming Video

## Purpose
Notes for streaming, especially to achieve high-quality real-time streaming with multiple viewers. 

## Method: Direct Streaming via OBS Stream -> SRS (running on WSL) -> Web Browser
This method is useful if you have enough bandwidth to directly host a stream to your participants. This guide requires opening ports on your router and exposing SRS to the public internet, so it is intended for limited hobbyist use rather than as a permanent setup. When you are not streaming, make sure to disable any port-forwarding rules you created on your router.

### Step 1: Setup WSL (Windows Subsystem for Linux) and Docker Desktop
* To install **WSL**, run `wsl --install`.
* Add a Linux distribution such as **Ubuntu** by searching `Ubuntu` in the **Microsoft Store**.
* Install **Docker Desktop** from the Microsoft Store.
* Once **Docker Desktop** is installed, run it and go to **Settings > Resources > WSL Integration**. **Ensure Enable integration with additional distros** is checked for the distro you chose earlier.
* Test that **Docker** works by opening a command prompt for your Linux distro
  * `sudo docker run --rm hello-world` (you may have to wait a few moments until **Docker** is fully started for this to work).
* Optionally, allow users to run docker without **sudo**
  * `sudo usermod -aG docker $USER`
  * `newgrp docker`
  * `docker run --rm hello-world`

### Step 2: Setup SRS (Simple Realtime Server)
* This uses *WebRTC for Live Streaming* as described by the [SRS Getting Started guide](https://ossrs.net/lts/en-us/docs/v6/doc/getting-started).
* Run **SRS** like this, replacing `<LAN-IP>` with your LAN IP address (this can be obtained from **ipconfig** in **Windows** or from your router's admin page).
```
CANDIDATE="<LAN-IP>"
docker run --rm -it -p 1935:1935 -p 1985:1985 -p 8080:8080 \
    --env CANDIDATE=$CANDIDATE -p 8000:8000/udp \
	ossrs/srs:5 ./objs/srs -c conf/rtmp2rtc.conf
```

### Step 3: Setup Port-forwarding
* On your router, add the following port-forwarding rules. Also add these as **Inbound** rules in the **Windows Firewall**.
  * `SRS-WHEP`: `TCP, port 1985`
  * `SRS-WebRTC-UDP`: `UDP, port 8000`
  * `SRS`: `TCP, port 8080`
* The rule named **SRS-WHEP** is for control/signalling, **SRS-WebRTC-UDP** is for the audio/video stream, **SRS** is for the built-in web server.
* You may additionally forward `SRS-RTMP`: `TCP, port 1935` if you to stream **OBS** from an external machine to **SRS**.

### Step 4: Setup OBS
* Go to **Settings > Stream**
  * Set the **Service** to **Custom...**
  * Set **Server** to `rtmp://127.0.0.1/live` and **Stream Key** to `livestream`
* Go to Output
  * Set an **Audio Encoder** and set a **Video Encoder** which takes advantage of your graphics card.
  * **Rate Control**: `CBR`
  * **Bitrate:** `6000` (You can experiment with bitrate depending on how reliable your stream is).
  * **Keyframe Interval:** `1`
  * **Preset:** `Quality`
  * **Profile:** `High`
  * **Max B-Frames:** `0`
* Set up a video source, and when you are ready to stream click **Start Streaming** under **Controls** in the main window.
 
### Step 5: Running the Stream
* Go the built-in **SRS** web page at `http://<WAN-IP>:8080/players/rtc_player.html` replacing `<WAN-IP>` with your internet-facing IP.
* On that page enter `webrtc://<WAN-IP>/live/livestream` and click the button.

## Method: RTC Software Streaming via OBS Virtual Webcam -> Real-time Communication Software (such as Discord or Zoom)
This method is useful if you have limited upload bandwidth. Streaming using a virtual webcam has an advantage in video quality, video and audio stability and required bandwidth as opposed to streaming using screen share.

Using this method, any remaining quality bottlenecks seems to be dependent on the communication software's server (e.g. **Discord**, **Zoom**). For example, on **Discord** audio quality is generally poor except at the highest paid "boost levels".

When using a virtual webcam to stream, you may wish to stream from one computer while joining the stream as a participant from another computer (especially given the inconvenience of having to change chat application settings when switching from streaming back to everyday usage). Otherwise, see some workarounds below to do everything on the same machine. 

In **Discord**, **Zoom** and other conferencing applications, the video preview of the **OBS** virtual webcam will be horizontally flipped on the local machine only.

### Step 1: Setup VB-Cable
* A virtual audio input device is required to pass along the audio from the virtual **OBS**-based webcam. This is because many communication applications can only take audio from devices listed explicitly under *Control Panel \ Sound \ Recording**.
* Download the [VB-CABLE Virtual Audio Device](https://vb-audio.com/Cable/) and run the installer as an administrator.
* Go to both **Control Panel \ Sound \ Playback**. 
  * If a **VB-Audio** device is not visible, right-click the empty space in the device list and click **Show Disabled Devices** to see the disabled **VB-Audio** device then right-click the disabled **VB-Audio** device and choose **Enable**.
  * The **VB-Cable** installer may have changed the **Default Device** and or the **Default Communication Device** to itself. You may want to revert it back by right-clicking the appropriate device and clicking **Set as the Default Device** and **Set as the Default Communication Device** respectively.
  * Similarly ensure there is an enabled** VB-Audio** device under **Control Panel > Sound > Recording** (and revert any defaults as desired).

### Step 2: Setup OBS
* Under **File > Settings** on the **Audio** tab, ensure that **Advanced \ Monitoring Device** is set to the **VB-Audio** device.
* Right-click the **Audio Mixers** and choose **Advanced Audio Properties**. Ensure that under the **Monitoring** column, the **VLC** audio source is set to **Monitor Only**.
* On the **Audio Mixers** list you may wish to disable other audio sources.
* On the **Video Preview**, you should right-click the **VLC** video feed and choose **Resize output (source size)**.
* Set up a video source, and when you are ready to stream click **Start Virtual Camera** under **Controls** in the main window.

### Step 3 (Optional): Additional OBS Setup for Engaging in the Stream as a Participant While Also Hosting the Stream
* To speak on the stream, add your microphone to the **OBS** Studio audio mixer.
* Under the **Audio Properties**, under the **Monitor** column, choose **Monitor Only** for this device.
* To listen to the audio being streamed from your virtual web cam, go to **Control Panel > Sound** and select the **Recording** tab. Right-click on the **VB-Audio** *Cable Output* device and select properties. On the **Listen** tab, check **Listen to this device**.

### Step 4: Setup Discord
* In **Discord**, go to the **User Settings Page** (gear icon)
  * Under **Voice & Video**:
    * Ensure your **Input Device** is set to **VB-Audio**.
    * Turn off **Automatically determine input sensitivity** and set the sensitivity threshold to the minimum value (*-100 dB*).
  * Under *Video Settings*:
    * Set **Camera** to **OBS Virtual Camera**.
  * Under **Advanced** ensure that the following are disabled:
    * **Noise Suppression**
    * **Echo Cancellation**
    * **Noise Reduction**
    * **Advanced Voice Activity** (if it is not already greyed-out).
    * **Automatic Gain Control**

## Appendix: Using VLS as a Source in OBS
* Ensure that [VLC](https://www.videolan.org/vlc/) and [OBS Studio](https://obsproject.com/) are installed. The bittage of both applications must match (i.e. both must be either 32-bit or 64-bit).
* In **OBS** Studio, right-click the **Sources** in the list and choose **Add > VLC Video Source**.
* Choose the settings from the **VLC Video Source** as desired, including adding the video files to be streamed to the playlist. The playlist and other settings can be changed at any time by double-clicking on the source in the sources list.
* The **OBS VLC plugin** is limited in its ability to control which audio and or subtitles are displayed. You may want to simply create a version of your media file with only the single desired audio and (and single desired subtitle track if applicable). If using subtitles you may want to set the **Fored Track** flag to **Yes**. Use [MKVToolNix](https://mkvtoolnix.download/) to do this. The executables are Windows are hosted [here](https://www.fosshub.com/MKVToolNix.html).
