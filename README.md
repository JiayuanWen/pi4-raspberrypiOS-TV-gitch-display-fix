### Devices:
* Sony Bravia KDL-42EX440 LCD TV
* Raspberry Pi 4 Model B (2GB)
    * OS: Raspberry Pi OS (Raspbian) 11 bullseye


### Problem:
When connecting Pi 4 to TV via Micro-HDMI to HDMI, the display is glitched and flashes all over the place.

### Solution:
Some TV models might send incorrect information to Pi 4's mini-HDMI, causing Pi 4 to get confused of the TV's specs (such as supported resolutions, ratio, etc). We want Pi 4 to ignore TV's information and use a manually determined one instead.
1. Find a way to access your system file in Pi (either via SSH, use secondary PC monitor, or plug your Pi's SDcard to a working PC and access the partition where `/boot` is located) 
2. Edit `config.txt` in your `/boot` system folder as a super user. Ex: `$ sudo nano /boot/config.txt` 
3. Add the following lines: `hdmi_ignore_edid=0xa5000080`, `hdmi_force_hotplug=1`
4. Refer to [Raspberry Pi's official document on HDMI Mode](https://www.raspberrypi.com/documentation/computers/config_txt.html#hdmi_group), add these two lines: `hdmi_group=x`, `hdmi_group=y`. Replace `x` and `y` with value suitable to your TV. 
5. Connect your Pi's HDMI to TV, turn both on. If you see black border around the UI (aka desktop size is incorrect despite the display being set correctly), keep reading.
6. Refer to [Raspberry Pi's official document on Overscan](https://www.raspberrypi.com/documentation/computers/config_txt.html#overscan_left), add these four lines: `overscan_left=x`, `overscan_right=x` `overscan_top=y`, `overscan_botton=y`. 
7. Adjust the `x` and `y` value.
8.  Connect your Pi's HDMI to TV, turn both on. If you see black border around the UI (aka desktop size is incorrect despite the display being set correctly), repeat step 6-8 until you're satisfy with your UI size.

<sup>*Note: Raspberry Pi's official document might change in the future, if linkd lead you to confusing places/sections, feel free to post an [Issue] to notify me (https://github.com/JiayuanWen/pi4-raspberrypiOS-TV-gitch-display-fix/issues).<sup>
