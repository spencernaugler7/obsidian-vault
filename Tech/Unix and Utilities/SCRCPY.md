
First Keep screen on when usb is connected. ^[source: [adb link](https://varunbarad.com/blog/keep-android-screen-on-when-usb-connected)]

```bash
adb shell svc power stayon usb
```

Basic Usage

```bash
scrcpy --video-codec=h265 --max-size=1920 --keyboard=uhid
```

Shortcuts
- right-click triggers `BACK` (or `POWER` on)
- middle-click triggers `HOME`
- the 4th click triggers `APP_SWITCH`
- the 5th click expands the notification panel

Advanced Usage

Record the device camera in H.265 at 1920x1080 (and microphone) to an MP4 file:
```bash
scrcpy --video-source=camera --video-codec=h265 --camera-size=1920x1080 --record=file.mp4
```

Control the device without mirroring by simulating a physical keyboard and mouse (USB debugging not required):
```bash
scrcpy --otg
```
