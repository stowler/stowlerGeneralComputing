setupBasicScriptingEnvironment.md
===================================

All of my scripts and documentation assume that these resources have been installed.



# MacPorts (Apple OS X only)

Though modern OS X has a number of useful *nix tools pre-installed, sometimes they're missing or outdated. Macports provides an easy way to install these tools.

## Install Macports On Mountain Lion:

1. confirm that the [prequisites](http://www.macports.org/install.php) are installed per the macports webpage
 * install [Xquartz](http://xquartz.macosforge.org/)
 * logout and log back in to active Xquartz
 * install Xcode via Mac App Store
 * run xcodebuild -license
 * install [Command Line Developer Tools](https://developer.apple.com/downloads/index.action)
2. [download](http://www.macports.org/install.php) and [install](http://www.macports.org/install.php#pkg) macports
3. open a NEW terminal window
4. notice that the install edited (/etc/bash_profile? ~/.profile? something else?) to add /opt/local paths to the front of $PATH
5. sudo port -v selfupdate
6. sudo port install [package name]



# Git

Git is used to install and manage software repositories. It has both GUI and command-line interfaces, though I just use the CLI.

## Install git / github on OS X Mountain/Lion:

The Github GUI client also installs the command-line git client. [Download it](http://mac.github.com/) and allow it to install the command-line client when it prompts you at the end. Alternatively you could follow [these instrucitons](https://help.github.com/articles/set-up-git#platform-mac)

## Install git on debian/ubuntu linux:
	sudo apt-get install git
	
	
# General command-line utilities

Install these. If you don't know why now, you will.

Each of these packages can be installed on debian/ubuntu linux by typing:

	sudo apt-get install [name(s) of the package(s)]
	
...and on OS X via Macports:

	sudo port install [name(s) of the package(s)]

These are the package names to substitute into the commands above (no square quotes when you actually type/paste this:)

	sed awk cut wc bc getopt curl wget tmux tee tree htop
	
And for OS X only you will also want to:

	sudo port install tmux-pasteboard
	
	
	
