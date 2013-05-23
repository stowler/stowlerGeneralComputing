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
4. type "echo $PATH" and notice that the install prepended /opt/local paths to the front of $PATH
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

	curl wget tmux tree htop imagemagick
	
And for OS X only you will also want these:

	getopt tmux-pasteboard
	
	# ...and then follow these instructions: 
	To enable tmux-MacOSX-pasteboard add following line to ~/.tmux.conf replacing
	'bash' with your actual shell:
	set-option -g default-command "/opt/local/bin/reattach-to-user-namespace bash"


# R and Rstudio
R is the way and the light. It is a complete statistics analysis language supported by a universe of active statisticians and developers. Rstudio is a graphical integrated development environment for the R lanuage.

## Install on OS X Mountain/Lion:

1. [download R]( http://cran.stat.ucla.edu/bin/macosx/) (precompiled binary of R base packages)
2. install R from the download
3. [download Rstudio Desktop](http://www.rstudio.com/ide/download/desktop) (precompiled binary)
4. install Rstudio Desktop from downloaded .dmg file
 

## Install on ubuntu linux:

See http://cran.r-project.org/bin/linux/ubuntu/README.html

	sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E084DAB9
	# add to /etc/apt/sources.list:
	# deb http://cran.stat.ucla.edu/bin/linux/ubuntu precise/
	sudo apt-get update
	sudo apt-get install r-base r-base-dev
	
Then download the rstudio [.deb installation file from the rstudio website](http://www.rstudio.com/ide/download/desktop). Install by double-clicking on it, and after installation it should appear in Applications -> Development -> Rstudio .

## Install on linux (debian 7.0 wheezy neurodebian virtual machine):

Based on the [CRAN installation instructions for debian](http://cran.r-project.org/bin/linux/debian/) .

First get the key:

    sudo gpg --keyserver pgp.mit.edu --recv-key 381BA480
    sudo gpg -a --export 381BA480 > /tmp/jranke_cran.asc
    sudo apt-key add /tmp/jranke_cran.asc

...then add these lines to /etc/apt/sources.list :

    deb http://cran.stat.ucla.edu/bin/linux/debian wheezy-cran3/
    deb-src http://cran.stat.ucla.edu/bin/linux/debian wheezy-cran3/

...and install binaries:

    sudo apt-get update
    sudo apt-get install r-base r-base-dev r-recommended r-mathlib
    sudo apt-get install r-cran-rodbc r-cran-rsprng
    sudo apt-get install libx11-dev libglu1-mesa-dev libxml2-dev libopenmpi-dev
    sudo apt-get install cdbs debhelper tcl-tclreadline tk8.5-dev
    sudo apt-get install -y openjdk-7-jdk icedtea-7-plugin
    sudo update-java-alternatives -l
    sudo update-java-alternatives -s java-1.7.0-openjdk-i386
    sudo R CMD javareconf

...and configure in R:

    sudo R --no-save
    update.packages(ask=FALSE)
    install.packages('Rcmdr', dependencies=TRUE)
    install.packages('JGR', dependencies=TRUE)
    install.packages('Deducer', dependencies=TRUE)
    install.packages('DeducerExtras', dependencies=TRUE)
    install.packages('DeducerRichOutput', repos = 'http://R-Forge.R-Project.org', dependencies=TRUE)

...and test:

    sudo R --no-save
    library(Rcmdr)
    library(JGR)
    JGR()
    library(Deducer)
