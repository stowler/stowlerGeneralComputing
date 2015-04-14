setupBasicScriptingEnvironment.md
===================================

All of my scripts and documentation assume that these resources have been installed. Below is a reasonable order for installation along with some of my install and config notes. 



1 Install Xcode (OS X only)
==============================
It's useful to install Xcode first, as it is needed for other packages like git and macports. Here's how I do it in OS X 10.10 Yosemite:

1. Install Xcode via Mac App Store.
1. Open Xcode and allow additional components to install if prompted.
1. From the terminal run `sudo xcodebuild -license`.
1. From the terminal run `sudo xcode-select --install` to install Apple's [Developer Command Line Tools.](https://developer.apple.com/downloads/index.action)



2 Install MacVim (OS X only)
==============================================

Install MacVim (and its command-line version mvim) immediately for something more reliable than built-in vim:

   - Download MacVim from http://code.google.com/p/macvim/
   - Uncompress and move `MacVim.app` to `/Applications/`
   - Install `mvim` from the download:
   
      ```bash
      sudo mkdir -p /usr/local/bin
      sudo mv ~/Downloads/MacVim-*/mvim /usr/local/bin/
      which mvim
      mvim #...should open MacVim as GUI
      ```

   - Set aside OS X native `vi` and `vim`:

      ```bash
      # Native vim in your path is probably /usr/bin/vim, and 
      # /usr/bin/vi is probably just a symlink to /usr/bin/vim:
      which vim
      which vi
      # Let's look at the native vim version just for fun:
      /usr/bin/vim --version
      # ...and now let's get it out of the way:
      sudo mv /usr/bin/vim /usr/bin/vim_from_apple
      ```

   - Set these new symlinks for `vi` and `vim`. Calling them will open `mvim` in terminal mode:
 
      ```bash
      sudo ln -s /usr/local/bin/mvim /usr/local/bin/vi
      sudo ln -s /usr/local/bin/mvim /usr/local/bin/vim
      # ...and confirm that we're using macvim:
      ls -al /usr/local/bin/mvim /usr/local/bin/vi*
      which vim
      vim --version
      # to get more information on symlinking, open MacVim and type ":h mvim"
      # :h macvim can be used to get general information about MacVim
      ```

   - I also like to set these symlinks for `view` (read-only mode) and `vimdiff` (side-by-side diff mode):
 
      ```bash
      sudo ln -s /usr/local/bin/mvim /usr/local/bin/view
      sudo ln -s /usr/local/bin/mvim /usr/local/bin/mview
      sudo ln -s /usr/local/bin/mvim /usr/local/bin/gview
      sudo ln -s /usr/local/bin/mvim /usr/local/bin/vimdiff
      sudo ln -s /usr/local/bin/mvim /usr/local/bin/mvimdiff
      sudo ln -s /usr/local/bin/mvim /usr/local/bin/gvimdiff
      ```



3 Install iTerm2 (OS X only)
=============================================
I prefer [iTerm2][] to the OS X default terminal.

1. [Download](http://iterm2.com/downloads.html) the most recent iTerm2 stable release.
1. Uncompress the download and move iTerm.app to Applications.
1. Open iTerm2. Select Edit -> Preferences -> General -> "Load preferences from a custom folder or URL", and specify the folder `~/.iterm2`
1. If you make changes to iTerm2 preferences that you want syncronized to other hosts via VCSH (see above), be sure to click "Save Settings to Folder" to export the updated settings into the VCSH-managed `~/.iterm2`. This must be done after each change or set of changes that you want to propogate. (The active preferences are stored in `~/Library/Preferences/com.googlecode.iterm2.plist`).


[iTerm2]: http://iterm2.com/


4 Install MacPorts (OS X only)
==============================================

Though modern OS X has a number of useful \*nix tools pre-installed, sometimes they are missing or outdated. Macports provides an easy way to install these tools.

Here's how I install Macports On OS X Mavericks:

1. Confirm that the [macports prequisites](http://www.macports.org/install.php) are installed:
	1. Install [Xquartz.](http://xquartz.macosforge.org/)
	1. Logout and log back in to activate Xquartz.
	1. Install Xcode via Mac App Store (see above).
	1. Install Xcode's Command Line Developer Tools (see above).
2. [Download and install macports](http://www.macports.org/install.php) from the .pkg package installer specific for your version of OS X.
3. Confirm the install worked: open a NEW terminal window, type `echo $PATH`. Notice that the install prepended `/opt/local` paths to the front of your previous `$PATH`.
4. Confirm that you can [update macports](http://guide.macports.org/#using.common-tasks) and [install a package](http://guide.macports.org/#using.port.install):
	5. `sudo port -v selfupdate`
	6. `sudo port upgrade outdated`
	7. `sudo port install htop`
5. There's no point in having Spotlight index macport files, so omit `/opt/local` from Spotlight via System Preferences -> Spotlight -> Privacy.



5 Install git
===============================

Git is a system used to install and manage software repositories. It has both GUI and command-line interfaces, though I recommend you learn to use the more flexible command-line interface.

## Remember to set git preferences!
Regardless of OS, remember to set some basic git preferences after installation. For me that looks like:

```bash
git config --global user.name "Stephen Towler"
git config --global user.email "stowler@gmail.com"
git config --global color.ui auto
# ...you can list all of your environment's git settings with:
git config --list
# ...and specific git settings with git config <key>, for example:
git config user.email
```

## Install git on OS X Yosemite:

OS X 10.10 Yosemite comes with git already available in your `$PATH` as `/usr/bin/git`. At the time of writing that's git version 1.9.3 (Apple Git-50). However, installing the macports version allows you to track a more current version of git:

```bash
# upate the local ports tree:
sudo port -v selfupdate

# list the available variants for git:
port variants git

# install git with osxkeychain compatibility:
sudo port install git +credential_osxkeychain +doc
# ...at the time of writing my command also included +python27

# the install worked if you get an osxkeychain usage message in response to this command:
git credential-osxkeychain

# enable os x keychain to store your username and password when connecting to a remote server  
git config --global credential.helper osxkeychain
```

If you don't want to install macports or use the OS X default git, there are other options:

1) The GitHub GUI client for OS X also installs a command-line git client for OS X. [Just download the GitHub GUI client](http://mac.github.com/) and allow it to install the command-line client when it prompts you at the end. 
2) If you don't want to install the GUI client you could follow [these instrucitons](https://help.github.com/articles/set-up-git#platform-mac) instead.

Regardless of which version of git you use, remember to set your user preferences after installation (see above).

## Install git on debian/ubuntu linux:

```bash
sudo apt-get install git
```

Remember to set your user preferences after installation (see above).
	


6 Install and sync VCSH and MR
=============================================
Follow [my instructions][] to install [VCSH][] and [MR][], and sync existing MR-managed repos to the new host. I use these packages to keep my dotfiles and git repositories synchronized among hosts.

[VCSH]: https://github.com/RichiH/vcsh
[MR]: http://myrepos.branchable.com
[my instructions]: https://github.com/stowler/stowlerGeneralComputing/blob/master/docs/setupVCSH.md#2-clone-to-a-new-host-and-test-operations


7 Confirm important dotfiles
==================================

I use individual VCSH repositories to sync and track my most important dotfiles:

```bash
$ vcsh list
mr
vcsh-sdt-bash
vcsh-sdt-tmux
vcsh-sdt-vim
```

The VCSH repo called `vcsh-sdt-bash` is where I manage my shell-related dotfiles:

```bash
$ vcsh list-tracked vcsh-sdt-bash
/Users/stowler/.aliases
/Users/stowler/.bash_profile
/Users/stowler/.bash_prompt
/Users/stowler/.bashrc
/Users/stowler/.exports
/Users/stowler/.extra
/Users/stowler/.gitignore.d/vcsh-sdt-bash
/Users/stowler/.path
```

In this arrangement, `.bash_profile` has a line that sources all of the other dotfiles in that repo.  
path,bash_prompt,exports,aliases,functions,extra


## dotfiles sourced directly from mathiasbynens
I source these directly from the [mathiasbynens dotfiles repo][]. The `.bash_profile` sources all of the other files. 

TBD: how do I bootstrap from the repo to my homedir and watch for changes?

### .aliases
This provides smart aliasing of ls, as well as a number of other aliases like `afk` and `...`.

### .bash_profile
In addition to setting a number of shell options, this file also has a line that sources all of the other dotfiles in my vcsh-sdt-bash repo.

### .bashrc
This file mostly just displaces an existing .bashrc

### .exports
Exports reasonable values for environmental variables like EDITOR, HIST\*, LANG, and GREP_OPTIONS
TBD: pull out my content



## dotfiles adapted from mathiasbynens

### .bash_prompt
This is my custom-edited version of the original from the [mathiasbynens dotfiles repo][]

## dotfiles and settings managed through .extra
As a way of adding custom commands and configs without forking mathiasbynens, I've added some of my own customizations to .extra, which is the last file sourced by .bash_profile


## .path
.path isn't in the vcsh-sdt-bash file list above because its config is pretty machine specific. Excerpted from https://github.com/mathiasbynens/dotfiles/blob/master/README.md :

>   If ~/.path exists, it will be sourced along with the other files, before any feature testing (such as detecting which version of ls is being used) takes place.

This means that `.path` isn't particularly useful for things like `$FSLDIR/data/standard`, since the values of $FSLDIR isn't defined in `.exports` until *after* `.path` is sourced.



[mathiasbynens dotfiles repo]: https://github.com/mathiasbynens/dotfiles

	
8 Install general command-line utilities
============================================


Install these utilities. If you don't know why now, you will. This will take negligable time on debian/ubuntu linux, but about 2.5 of macports compiling on a 2.8 GHz i5 iMac.

Each of these packages can be installed on debian/ubuntu linux by typing:

	sudo apt-get install [name(s) of the package(s)]
	
...and on OS X via Macports:

	sudo port install [name(s) of the package(s)]

Below is a list of the package names to substitute into the commands above (no square brackets when you actually type/paste these package names into your install command above:)

	curl wget tmux tree htop slurm imagemagick
	
And for OS X only you will also want these:

	getopt tmux-pasteboard
	
...and then, for OS X only, follow these instructions in the top of the default .tmux.conf: 

	# To enable tmux-MacOSX-pasteboard add following line to ~/.tmux.conf replacing
	'bash' with your actual shell:
	set-option -g default-command "/opt/local/bin/reattach-to-user-namespace bash"



9 Install R and Rstudio
============================

R is the way and the light. It is a complete statistics analysis language supported by a universe of active statisticians and developers. Rstudio is a graphical integrated development environment for the R lanuage.

## Install R and Rstudio on OS X Mavericks:

1. [Download R]( http://cran.stat.ucla.edu/bin/macosx/) as precompiled binary of R base packages.
2. Install R from the download .pkg file.
3. [Download Rstudio Desktop](http://www.rstudio.com/ide/download/desktop) as a precompiled binary.
4. Install Rstudio Desktop from downloaded .dmg file.

To upgrade R or Rstudio Desktop just follow the same instructions. They are both generally good about finding your existing install and either migrating everything over to the new version or warning you if there is going to be trouble.
 

## Install R and Rstudio on ubuntu linux:

See http://cran.r-project.org/bin/linux/ubuntu/README.html

	sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E084DAB9
	# add to /etc/apt/sources.list:
	# deb http://cran.stat.ucla.edu/bin/linux/ubuntu precise/
	sudo apt-get update
	sudo apt-get install r-base r-base-dev
	
Then download the rstudio [.deb installation file from the rstudio website](http://www.rstudio.com/ide/download/desktop). Install by double-clicking on it, and after installation it should appear in Applications -> Development -> Rstudio .



## Install R and Rstudio on Neurodebian 7.2.0 wheezy virtual machine:

For a neurodebian wheezy virtual machine (VM) installed and updated using 
[these instructions](http://j.mp/setupNeurodebianVM), a working installation of R can be added with the following steps. These instructions are based on the 
[CRAN installation instructions for installing R on Debian 7.0 / 7.2.0 wheezy](http://cran.r-project.org/bin/linux/debian/).
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
