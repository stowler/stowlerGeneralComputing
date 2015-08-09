# Provisioning New Macs

_These are the steps I follow when provisioning a new mac for myself.
TBD: Should be mostly correct, but update for Yosemite and edit/format._

Contents
=================

  * [Configure security](#configure-security)
  * [Configure network](#configure-network)
  * [Configure the dock](#configure-the-dock)
  * [Configure spaces](#configure-spaces)
  * [Configure safari](#configure-safari)
  * [Configure mouse/trackpad](#configure-mousetrackpad)
  * [Configure keyboard, spelling, shortcuts](#configure-keyboard-spelling-shortcuts)
  * [Configure services, applescript, and automator](#configure-services-applescript-and-automator)
  * [Configure dictation and speech](#configure-dictation-and-speech)
  * [Install sensitive apps](#install-sensitive-apps)
  * [Install apps from mac app store](#install-apps-from-mac-app-store)
  * [Install apps from outside MAS](#install-apps-from-outside-mas)
  * [Install development environment](#install-development-environment)
  * [Install neuroimaging environment](#install-neuroimaging-environment)
  * [Install external hardware support](#install-external-hardware-support)

# Configure security

- System Prefs -> FileVault -> turn on filevault2 whole-disk encryption
- System Prefs -> Security & Privacy -> General -> require password immediately after sleep or screensaver
- lock down all sharing
- turn off guest account
- set a hotcorner for screensaver and apply password immediately


# Configure network 

The point-and-click way to set computer name is "System Preferences -> Sharing ", but that's not very reliable so I use the commands below. 

(One guide to OS X hostname weirdness: http://ilostmynotes.blogspot.com/2012/03/computername-vs-localhostname-vs.html)
```bash
# Each of these values can also be queried by substituting "--get" for "--set":
newHostName="hal"
sudo scutil --set ComputerName "${newHostName}"
sudo scutil --set HostName "${newHostName}"
sudo scutil --set LocalHostName "${newHostName}"
# This value can also be queried by substituting "read" for "write":
sudo defaults write /Library/Preferences/SystemConfiguration/com.apple.smb.server NetBIOSName -string "${newHostName}"
```


# Configure the dock

Install [dockutil](https://github.com/kcrawford/dockutil) and configure initial dock:
```bash
# temporary location for dockutil as this is likely to occur early in setup
# before source directories are established:
cd ~/Downloads
git clone https://github.com/kcrawford/dockutil.git
sudo cp dockutil/scripts/dockutil /usr/local/bin/
# remove default items from the dock, but don't restart the dock yet:
dockutil --remove all --no-restart
# add items to dock but wait until the end to restart the dock:
dockutil --add '/System/Library/Frameworks/ScreenSaver.framework/Versions/Current/Resources/ScreenSaverEngine.app' --no-restart
dockutil --add '/Applications/Mission Control.app' --no-restart
dockutil --add '/Applications/System Preferences.app' --no-restart
dockutil --add '~/Downloads' --view grid --display folder
```

# Configure spaces

- System Prefs -> disable "Automatically rearrange spaces based on most recent use"


# Configure safari

- Safari -> Preferences -> General 
   - Safari opens with all windows from last session
   - New Windows Open With Empty Page
   - New Tabs Open With Empty Page
   - Top sites show 6 sites (turn off all?)
   - UNCHECK Open "safe" files after downloading (helps with .tar.gz and .tgz files)

- To avoid Java-based security risks: Safari -> Preferences -> Security -> uncheck "Enable Java"

- To disable Safari auto-correct of typed words: Safari -> Edit -> spelling and grammar
   - untick ‘check spelling while typing’ to get rid of the red underlines when you mis-spell words
   - untick ‘correct spelling automatically’ to stop safari from replacing words it thinks are incorrect.
- TBD: disable handoff?
- Safari extensions: 
   - [Evernote web clipper](http://evernote.com/webclipper/)
   - [1password](https://agilebits.com/onepassword/extensions)

# Configure mouse/trackpad

- speed-up mouse/trackpad
- set mouse/trackpad secondary click
- Zoom:
  - System Prefs -> Accessibility -> Zoom
     - Enable access for assisstive devices
     - Use keyboard shortcuts to zoom
     - Use scroll gesture with modifier keys to zoom: Control
     - Smooth Images
     - (Unchecked) Zoom follows keyboard focus
     - zoomstyle: Fullscreen
     - options: screen images moves only when the pointer reaches an edge

# Configure keyboard, spelling, shortcuts 

- Caps lock is pretty useless, so turn it into a Control key:
  `System Preferences -> Keyboard -> Modifier Keys`
- Disable aggressive system-wide auto-correction, which is frequently wrong:
  `System Preferences -> Language and Text -> Text ->` untick "Correct Spelling Automatically", along with any annoying symbol/text substitions
- For some apps (like Safari), you may have to disable in that app. To enable or disable auto-correct on an app by app basis, you need to be in an active text field (for example, in Safari you could go to Google and click to put the cursor in the search field). From there, navigate to Edit/Spelling and Grammar and then check or uncheck 'Correct Spelling Automatically.'
- Enable system-wide shortcuts:
  `System Preferencess -> Keyboard -> Keyboard Shortcuts -> Application Shortcuts -> All Applications`
   - New Email With Selection: SHIFT+COMMAND+M
   - Hover dict in Safari etc:     default is Ctrl-Command-D
      - can disable but can add additional shortcut in Services -> Searching -> Look Up in Dictionary



- uncomplicate:
   - disable automatic spelling correction
      - System Prefs -> Keyboard -> Text -> uncheck "correct spelling automatically"
   - disable transparency
      - System Prefs -> Accessibility -> Reduce Transparency

# Configure services, applescript, and automator
TBD

# Configure dictation and speech
TBD


# Install sensitive apps 

_These apps contain personal information or credentials, so I only install them on computers for which I am the sole admin:_

- 1password (from MAS)
- Dropbox (not MAS)
- Evernote (not MAS)
   - TBD: exclude evernote from spotlight?

# Install apps from mac app store

## MAS storage utilities

- Blackmagic Disk Speed Test
- The Duplicate Finder by Rocky Sand Studio
- EasyFind by DEVONtechnologies
- CleanMyDrive
- Disk Map by FIPLAB
  - `dockutil --add '/Applications/Disk Map.app'`
  - remember to turn on hidden files and system files

## MAS network utilities

- WiFi Explorer by adriangranados
- ForkLift by Binary Nights

## MAS GUI tweaks

- Moom
- PopClip
- Memory Clean
- ScreenSharingMenulet
- iHash
- CleanMyDrive by MacPaw

## MAS development

- Dialog Maker by Birkett
- SQLPro for SQLite Read-Only by Hakinsoft

## MAS neuroimaging 

- MRIcro (not MRIcro Viewer, not MRIcroX)

## MAS miscellaneous apps

- Mental Case 2
   - point sync at Dropbox and turn it on, wait for complete sync, then spot-check
- Keynote
- Pages
- Numbers
- iBooks
- iBooks Author
- iMovie
- Kindle


# Install apps from outside MAS


- [Emory's F5 BIG-IP VPN client](http://it.emory.edu/vpntools/)
- [Chrome Beta](https://www.google.com/chrome/browser/beta.html)
- [VMware Fusion Pro](http://www.vmware.com/products/fusion/fusion-evaluation.html)
- [Skitch](https://evernote.com/skitch/)
- [Skype](http://www.skype.com/en/download-skype/skype-for-computer/)
- [Marked 2](http://marked2app.com/)
- [github-markdown-toc.go](https://github.com/ekalinin/github-markdown-toc.go#precompiled-binaries) (add to precompiled binary to /usr/local/bin)
- [Go2Shell](http://zipzapmac.com/Go2Shell)
- [iStat Menus](https://bjango.com/mac/istatmenus/)
- [Papers 2.7.3](http://www.papersapp.com/mac/)


# Install development environment

I maintain a [separate document](https://github.com/stowler/stowlerGeneralComputing/blob/master/docs/setupBasicScriptingEnvironment.md) describing how I configure a base development environment, which include MacVim, iTerm2, Xcode, VCSH, and more.

# Install neuroimaging environment

I maintain a [separate document](https://github.com/stowler/brainwhere/blob/master/docs/setupNeuroimagingEnvironment.md) describing how I configure stand-alone neuroimaging environments.

# Install external hardware support

- ScanSnap
- Garmin Express
- Sleepyhead
- Shuttle Pro v2
- printer drivers


