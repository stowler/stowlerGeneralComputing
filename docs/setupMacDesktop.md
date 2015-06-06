setupMacDesktop.md
====================


- Security
   - System Prefs -> FileVault -> turn on filevault2 whole-disk encryption
   - System Prefs -> Security & Privacy -> General -> require password immediately after sleep or screensaver
   - lock down all sharing
   - turn off guest account

- TBD: set hostname (get from Evernote note?)


- Install on macs for which I'm the only admin:
   - 1password (from MAS)
   - Dropbox (not MAS)
   - Evernote (not MAS)
      - TBD: exclude evernote from spotlight?


- Dictation and Speech:
   - TBD


- HCI
   - remap caps lock to control key
      - System Prefs -> Keyboard -> Keyboard -> Modifier Keys
   - speed-up mouse/trackpad
   - set mouse/trackpad secondary click
   - Dock: add ScreenSaverEngine:
     - `/System/Library/Frameworks/ScreenSaver.framework/Versions/A/Resources/ScreenSaverEngine`
   - Dock: add Mission Control 
      - `/Applications/Mission Control`
   - Zoom:
      - System Prefs -> Accessibility -> Zoom
         - Use keyboard shortcuts to zoom
         - Use scroll gesture with modifier keys to zoom: Control
         - Smooth Images
         - (Unchecked) Zoom follows keyboard focus
         - zoomstyle: Fullscreen
         - options: screen images moves only when the pointer reaches an edge
    - Spaces:
         - Syste Prefs -> disable "Automatically rearrange spaces based on most recent use"


- uncomplicate:
   - disable automatic spelling correction
      - System Prefs -> Keyboard -> Text -> uncheck "correct spelling automatically"
   - disable transparency
      - System Prefs -> Accessibility -> Reduce Transparency
   - Safari -> Preferences -> General 
      - Safari opens with all windows from last session
      - New Windows Open With Empty Page
      - New Tabs Open With Empty Page
      - Top sites show 6 sites (turn off all?)
      - UNCHECK Open "safe" files after downloading
   - disable handoff?

- Safari extensions: 
   - TBD

- Services:
   - TBD

- Automator:
   - TBD

- applescript:
   - TBD


Install Apps From Mac App Store
===========================

- GUI tweaks:
   - Moom
   - PopClip
   - Memory Clean
   - ScreenSharingMenulet
   - iHash
   - CleanMyDrive by MacPaw

- disk & file utilities:
   - Disk Map by FIPLAB
      - remember to turn on hidden files and system files
   - The Duplicate Finder by Rocky Sand Studio
   - EasyFind by DEVONtechnologies
   - Blackmagic Disk Speed Test

- network utilities:
   - WiFi Explorer by adriangranados
   - ForkLift by Binary Nights

- development:
   - Dialog Maker by Birkett
   - SQLPro for SQLite Read-Only by Hakinsoft

- neuro apps:
   - MRIcro (not MRIcro Viewer or MRIcroX)

- other apps:
   - Mental Case 2
      - point sync at Dropbox and turn it on, wait for complete sync, then spot-check
   - Keynote
   - Pages
   - Numbers
   - iBooks
   - iBooks Author
   - iMovie
   - Kindle


Install Apps from non-MAS packages
=======================

istat?

- [Emory's F5 BIG-IP VPN client](http://it.emory.edu/vpntools/)
- [Matlab](http://www.mathworks.com/) (2 GB download, 5.5 GB install)
   - database toolbox
   - image processing toolbox
   - matlab coder
   - matlab compiler
   - matlab compiler SDK
   - signal processing toolbox
   - statistic and machine learning toolbox
- [Chrome Beta](https://www.google.com/chrome/browser/beta.html)
- [VMware Fusion Pro](http://www.vmware.com/products/fusion/fusion-evaluation.html)
- [Skitch](https://evernote.com/skitch/)
- [MacVim](https://github.com/macvim-dev/macvim/releases)
- [Skype](http://www.skype.com/en/download-skype/skype-for-computer/)
- [Marked 2](http://marked2app.com/)
- [Iterm2](http://iterm2.com)
- [Go2Shell](http://zipzapmac.com/Go2Shell)


Install External Hardware Support from non-MAS Packages
========================================================
- ScanSnap
- Garmin Express
- Sleepyhead
- Shuttle Pro v2
- printer drivers
