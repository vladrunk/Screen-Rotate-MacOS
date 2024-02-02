# Screen Rotate MacOS
A file for Automator on MacOS Sonoma for rotating the screen using hotkeys through Services.

## Instructions 

1) Install [HomeBrew](https://brew.sh/)
2) Install [displayplacer](https://github.com/jakehilborn/displayplacer) 
```bash
brew install jakehilborn/jakehilborn/displayplacer
```

3) Import `Screen rotate.workflow` to Automator. Do not close Automator. In `#6 | Rotate if id and degree are selected` you will need to change the commands for your monitor.

### Prepare config for 0 degree rotate
4) Choose Apple menu  > System Settings, then click Displays  in the sidebar. Click the pop-up menu next to Rotation on the right and choose 0 degrees (Standart or Default) to rotate the image on your display. Confirm.
5) Run in Terminal command `displayplacer list`   
  Command output example:
```bash
Persistent screen id: 37D8832A-2D66-02CA-B9F7-8F30A301B230
Contextual screen id: 1
Serial screen id: s4251086178
Type: MacBook built in screen
Resolution: 1800x1169
Hertz: 120
Color Depth: 8
Scaling: on
Origin: (0,0) - main display
Rotation: 0 - rotate internal screen example (may crash computer, but will be rotated after rebooting): `displayplacer "id:37D8832A-2D66-02CA-B9F7-8F30A301B230 degree:90"`
Enabled: true
Resolutions for rotation 0:

Persistent screen id: 9362C902-B9BA-46AA-8A5D-EB924502E126
Contextual screen id: 3
Serial screen id: s810299979
Type: 27 inch external screen
Resolution: 2560x1440
Hertz: 75
Color Depth: 7
Scaling: off
Origin: (1800,-271)
Rotation: 0
Enabled: true
Resolutions for rotation 0:

Execute the command below to set your screens to the current arrangement. If screen ids are switching, please run `displayplacer --help` for info on using contextual or serial ids instead of persistent ids.

displayplacer "id:37D8832A-2D66-02CA-B9F7-8F30A301B230 res:1800x1169 hz:120 color_depth:8 enabled:true scaling:on origin:(0,0) degree:0" "id:9362C902-B9BA-46AA-8A5D-EB924502E126 res:2560x1440 hz:75 color_depth:7 enabled:true scaling:off origin:(1800,-271) degree:0"
```

6) My external monitor, which I want to rotate with a hotkey, has the ID = `9362C902-B9BA-46AA-8A5D-EB924502E126`    

7) From the last line of the command `displayplacer list` output (step 4), copy   
```bash
"id:9362C902-B9BA-46AA-8A5D-EB924502E126 res:2560x1440 hz:75 color_depth:7 enabled:true scaling:off origin:(1800,-271) degree:0"
```

  Transform it into a string     
```bash
"id:$screen_id res:2560x1440 hz:75 color_depth:7 enabled:true scaling:off origin:(1800,-271) degree:$degree"
```

  Run `brew info displayplacer` to get path where stored bin. Example output (we need line 4):
```bash
==> jakehilborn/jakehilborn/displayplacer: stable 1.4.0, HEAD
macOS command line utility to configure multi-display resolutions and arrangements. Essentially XRandR for macOS.
https://github.com/jakehilborn/displayplacer
/opt/homebrew/Cellar/displayplacer/1.4.0 (5 files, 93KB) *
  Built from source on 2024-02-02 at 00:04:07
From: https://github.com/jakehilborn/homebrew-jakehilborn/blob/HEAD/Formula/displayplacer.rb
==> Options
--HEAD
	Install HEAD version
```

  Replace line 10 in the Shell `#6 | Rotate if id and degree are selected` in file `Screen rotate.workflow` with a line like this template:   
```bash
/opt/homebrew/Cellar/displayplacer/1.4.0/bin/displayplacer "id:$screen_id res:2560x1440 hz:75 color_depth:7 enabled:true scaling:off origin:(1800,-271) degree:$degree"
```

### Prepare config for 90 degree rotate
8) Choose Apple menu  > System Settings, then click Displays  in the sidebar. Click the pop-up menu next to Rotation on the right and choose 90 degrees to rotate the image on your display. Confirm.  
9) Run in Terminal command `displayplacer list`   
  Command output example:
```bash
Persistent screen id: 37D8832A-2D66-02CA-B9F7-8F30A301B230
Contextual screen id: 1
Serial screen id: s4251086178
Type: MacBook built in screen
Resolution: 1800x1169
Hertz: 120
Color Depth: 8
Scaling: on
Origin: (0,0) - main display
Rotation: 0 - rotate internal screen example (may crash computer, but will be rotated after rebooting): `displayplacer "id:37D8832A-2D66-02CA-B9F7-8F30A301B230 degree:90"`
Enabled: true
Resolutions for rotation 0:

Persistent screen id: 9362C902-B9BA-46AA-8A5D-EB924502E126
Contextual screen id: 3
Serial screen id: s810299979
Type: 27 inch external screen
Resolution: 1440x2560
Hertz: 75
Color Depth: 7
Scaling: off
Origin: (1800,-1391)
Rotation: 90
Enabled: true
Resolutions for rotation 90:

Execute the command below to set your screens to the current arrangement. If screen ids are switching, please run `displayplacer --help` for info on using contextual or serial ids instead of persistent ids.

displayplacer "id:37D8832A-2D66-02CA-B9F7-8F30A301B230 res:1800x1169 hz:120 color_depth:8 enabled:true scaling:on origin:(0,0) degree:0" "id:9362C902-B9BA-46AA-8A5D-EB924502E126 res:1440x2560 hz:75 color_depth:7 enabled:true scaling:off origin:(1800,-1391) degree:90"
```

10) My external monitor, which I want to rotate with a hotkey, has the ID = `9362C902-B9BA-46AA-8A5D-EB924502E126`
11) From the last line of the command `displayplacer list` output (step 9), copy   
```bash
"id:9362C902-B9BA-46AA-8A5D-EB924502E126 res:1440x2560 hz:75 color_depth:7 enabled:true scaling:off origin:(1800,-1391) degree:90"
```

  Transform it into a string     
```bash
"id:$screen_id res:1440x2560 hz:75 color_depth:7 enabled:true scaling:off origin:(1800,-1391) degree:$degree"
```

  Replace line 12 in the Shell `#6 | Rotate if id and degree are selected` in file `Screen rotate.workflow` with a line like this template:   
```bash
/opt/homebrew/Cellar/displayplacer/1.4.0/bin/displayplacer "id:$screen_id res:1440x2560 hz:75 color_depth:7 enabled:true scaling:off origin:(1800,-1391) degree:$degree""
```

12) Save file `Screen rotate.workflow`
13) Choose Apple menu  > System Settings, click Keyboard  in the sidebar, then click Keyboard Shortcuts on the right. Click Services, then select `Screen rotate` and set hotkey for it.
14) Done.

![Preview](https://github.com/vladrunk/Screen-Rotate-MacOS/assets/37048171/880c0540-ae00-4bdc-b018-6decfebfd65c)
