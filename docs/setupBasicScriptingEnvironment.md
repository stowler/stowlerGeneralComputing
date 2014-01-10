setupBasicScriptingEnvironment.md
===================================

All of my scripts and documentation assume that these resources have been installed.



# MacPorts (Apple OS X only)

Though modern OS X has a number of useful *nix tools pre-installed, sometimes they're missing or outdated. Macports provides an easy way to install these tools.

## Install Macports On OS X Mavericks:

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



## Install on linux (Debian 7.2.0 wheezy neurodebian virtual machine):

For a neurodebian wheezy virtual machine (VM) installed and updated using 
[these instructions](http://j.mp/setupNeurodebianVM), a working installation of R can be added with the following steps. These instructions are based on the 
[CRAN installation instructions for installing R on Debian 7.0 wheezy](http://cran.r-project.org/bin/linux/debian/).
Because of the transition from the 2.x R series to 3.x, special care must me taken to install
a minimum of pre-compiled 3.x binaries, followed by compiling current packages from source.

First get the key for the R 3.x backports:

    sudo gpg --keyserver pgp.mit.edu --recv-key 381BA480
    sudo gpg -a --export 381BA480 > /tmp/jranke_cran.asc
    sudo apt-key add /tmp/jranke_cran.asc

...and add these lines to `/etc/apt/sources.list` :

    deb http://cran.stat.ucla.edu/bin/linux/debian wheezy-cran3/
    deb-src http://cran.stat.ucla.edu/bin/linux/debian wheezy-cran3/

...and install the R base and dependencies from the backports repository:

    sudo apt-get update
    sudo apt-get install r-base r-base-dev

Update the installed packages via CRAN:

    sudo R --no-save
    update.packages(ask=FALSE)
    q()

Because 3D operations and GUI toolkits can be touchy, it is sometimes helpful to install and test rgl and Rcmdr before adding any other R packages:

    sudo R --no-save
    install.packages('rgl', dependencies=TRUE)
    install.packages('car', dependencies=TRUE)
    install.packages('Rcmdr', dependencies=TRUE)
    install.packages('RcmdrPlugin.HH', dependencies=TRUE)
    q()
    
Reboot the Neurodebian VM to settle any graphics dependencies that were installed with those packages.

Test R, including its 3D and GUI toolkits. None of these shold produce errors:

    sudo R --no-save
    library(rgl)
    demo(rgl)
    library(car)
    library(Rcmdr)
    (mouse:) Tools -> Load Rcmdr plug-ins... -> RcmdrPlugin.HH
    (mouse:) Data -> Data in packages -> Read data set from an attached package... -> PACKAGE: datasets, DATA SET: mtcars
    (mouse:) Data set: mtcars
    (mouse:) Graphs -> 3d graph -> 3d scatterplot... (HH). DV: mpg, IVs: disp, hp.
    (mouse:) Graphs -> 3d graph -> Identify observations with mouse...
    ...or the CLI version of those last two:
    data(mtcars, package="datasets")
    scatter3dHH(mtcars$disp, mtcars$mpg, mtcars$hp, fit="linear", bg="white", grid=TRUE, squares=FALSE, xlab="disp", ylab="mpg", zlab="hp")
    identify3d(mtcars$disp, mtcars$mpg, mtcars$hp, labels=row.names(mtcars))
