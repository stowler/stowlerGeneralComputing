# Configure a Basic Scripting Environment

_Most of my scripts and documentation are written assuming that the following resources have been installed. Below is a reasonable order for installation along with some of my install and configuration notes._

Contents
=================

  * [OS X only: Install XQuartz](#os-x-only-install-xquartz)
  * [OS X only: Install Xcode](#os-x-only-install-xcode)
  * [OS X only: Install MacVim](#os-x-only-install-macvim)
  * [OS X only: Install iTerm2](#os-x-only-install-iterm2)
  * [OS X only: Install MacPorts](#os-x-only-install-macports-)
  * [Install or upgrade git](#install-or-upgrade-git)
  * [Install and sync VCSH and MR](#install-and-sync-vcsh-and-mr)
  * [Confirm important dotfiles](#confirm-important-dotfiles)
  * [Solarized-ize the terminal](#solarized-ize-the-terminal)
  * [Install general command-line utilities](#install-general-command-line-utilities)
  * [Install R](#install-r-)
  * [Install Matlab](#install-matlab)

OS X only: Install XQuartz
===============================

Install the most recent version of [XQuartz](http://xquartz.macosforge.org/). After installation activate XQuartz by logging out and then logging back in.


OS X only: Install Xcode
==============================
Xcode is needed to install later packages like git and macports. Here's how I install Xcode in in OS X 10.10 Yosemite:

1. Install Xcode via Mac App Store.
1. Open Xcode and allow additional components to install if prompted.
1. From the terminal run `sudo xcodebuild -license`.
1. From the terminal run `sudo xcode-select --install` to install Apple's [Developer Command Line Tools.](https://developer.apple.com/downloads/index.action)
1. Add FileMerge to the dock:
`dockutil --add '/Applications/Xcode.app/Contents/Applications/FileMerge.app'`


OS X only: Install MacVim
==============================================

Install MacVim (and its command-line version `mvim`) for access to many more features than the vim shipped with OS X:

   - Download MacVim from http://code.google.com/p/macvim/
   - Uncompress and move `MacVim.app` to `/Applications/`
   - Add to Dock drag-and-drop:
   `dockutil --add '/Applications/MacVim.app'`
   - Install `mvim` from the download:
   
      ```bash
      sudo mkdir -p /usr/local/bin
      sudo mv ~/Downloads/MacVim-*/mvim /usr/local/bin/
      which mvim
      mvim #...should open MacVim as GUI
      ```

   - Set aside OS X native `vi` and `vim`:

      ```bash
      # Native vim in the existing path is probably /usr/bin/vim, and 
      # /usr/bin/vi is probably just a symlink to /usr/bin/vim:
      which vim
      which vi
      # Let's look at the native vim version just for fun:
      /usr/bin/vim --version
      # ...and now let's get it out of the way:
      sudo mv /usr/bin/vim /usr/bin/vim_from_apple
      ```

   - Create new symlinks for `vi` and `vim`. Calling them will open `mvim` in terminal mode:
 
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

   - I also like to create these symlinks for `view` (read-only mode) and `vimdiff` (side-by-side diff mode):
 
      ```bash
      sudo ln -s /usr/local/bin/mvim /usr/local/bin/view
      sudo ln -s /usr/local/bin/mvim /usr/local/bin/mview
      sudo ln -s /usr/local/bin/mvim /usr/local/bin/gview
      sudo ln -s /usr/local/bin/mvim /usr/local/bin/vimdiff
      sudo ln -s /usr/local/bin/mvim /usr/local/bin/mvimdiff
      sudo ln -s /usr/local/bin/mvim /usr/local/bin/gvimdiff
      ```



OS X only: Install iTerm2
=============================================
I prefer [iTerm2][] to the OS X default terminal. Installing and configuring iTerm2:

1. [Download](http://iterm2.com/downloads.html) the most recent iTerm2 stable release.
1. Uncompress the download and move iTerm.app to Applications.
1. Open iTerm2. Select Edit -> Preferences -> General -> "Load preferences from a custom folder or URL", and specify the folder `~/.iterm2`
1. If you make changes to iTerm2 preferences that you want synchronized to other hosts via VCSH (see below), be sure to click "Save Settings to Folder" to export the updated settings into the VCSH-managed `~/.iterm2`. This must be done after each change or set of changes that you want to propagate. (The active preferences are stored in `~/Library/Preferences/com.googlecode.iterm2.plist` by default).


[iTerm2]: http://iterm2.com/



OS X only: Install MacPorts 
==============================================

Though modern OS X has a number of useful \*nix tools pre-installed, sometimes they are missing or outdated. Macports provides an easy way to install these tools.

Here's how I install Macports On OS X Mavericks:

1. Confirm that the [macports prequisites](http://www.macports.org/install.php) are installed.
2. [Download and install macports](http://www.macports.org/install.php) from the `.pkg` package installer that matches your version of OS X.
3. Confirm the install worked: open a NEW terminal window, type `echo $PATH`. Notice that the install prepended `/opt/local` paths to the front of the previous `$PATH` entries.
4. Confirm that you can [update macports](http://guide.macports.org/#using.common-tasks) and [install a package](http://guide.macports.org/#using.port.install):
	5. `sudo port -v selfupdate`
	6. `sudo port upgrade outdated`
	7. `sudo port install htop`
5. There's no point in having Spotlight index macport files, so omit `/opt/local` from Spotlight via System Preferences -> Spotlight -> Privacy.



Install or upgrade git
===============================

[Git](https://git-scm.com) is a system used to install and manage software repositories. It has both GUI and command-line interfaces, though I recommend you learn to use the more flexible command-line interface. I also recommend that you use the same version of git on each of your platforms when possible, preferably by upgrading to a recent version. You can check the installed version of git with `git --version`. 

NB: At the time of writing I'm using version 2.4.3, and have found that versions in the 1.x series are incompatible with some current utilities, including [VCSH and MR](https://github.com/stowler/stowlerGeneralComputing/blob/master/docs/setupVCSH.md).

## Remember to set git preferences!
Regardless of OS, remember to set some basic git preferences after installation. I like to do this in `~/.extra`, which I source from `.bash_profile`:

```bash
git config --global user.name "Stephen Towler"
git config --global user.email "stowler@gmail.com"
git config --global color.ui auto
# ...you can list all of the environment's git settings with:
#        git config --list
# ...and specific git settings with git config <key>, for example:
#        git config user.email
```

## Upgrade git on OS X Yosemite:

OS X 10.10 Yosemite comes with git already available in the `$PATH` as `/usr/bin/git`. At the time of writing that's git version 2.3.2 (Apple Git-55).  Installing the macports version allows you to use a more current version of git. 

```bash
# confirm that the macports folder appears earlier in the $PATH than /usr/bin/ :
echo $PATH

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

1) The GitHub GUI client for OS X also installs a command-line git client for OS X. [Just download the GitHub GUI client](https://mac.github.com/) and allow it to install the command-line client when it prompts you at the end. 
2) If you don't want to install the GUI client you could follow [these instructions](https://help.github.com/articles/set-up-git#platform-mac) instead.

Regardless of which version of git you use, remember to set your user preferences after installation (see above).

## Upgrade git on Ubuntu
**UPDATED: 20150817**

Ubuntu 14.04 and earlier ship with git versions < 2, and benefit from upgrading. If the stock version of git is already installed, begin by removing it:

```bash
sudo apt-get remove git
```

Now add the [official git PPA](https://launchpad.net/~git-core/+archive/ubuntu/ppa) to your apt sources and install git:

```bash
sudo apt-add-repository ppa:git-core/ppa
sudo apt-get update
sudo apt-get install git
```

## Upgrade git on CentOS 6.6:

CentOS versions 6.6 and earlier ship with git versions < 2, and benefit from upgrading. If the stock version of git is already installed, begin by removing it:

```bash
sudo yum remove git
```

Next install the prerequisites for compiling git:

```bash
sudo yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel gcc perl-ExtUtils-MakeMaker
```

Download, extract, and compile a more modern release of git source:

```bash
wget https://www.kernel.org/pub/software/scm/git/git-2.4.3.tar.gz
tar -zxvf git-2.4.3.tar.gz 
cd git-2.4.3
make prefix=/usr/local/git all
sudo make prefix=/usr/local/git install
```

Add this new git to your `$PATH`. I do this via `$HOME/.extra_local`, but in more conventional environments you'll probably want to add it to the end of `$HOME/.bash_profile`:

```bash
echo 'export PATH=/usr/local/git/bin:$PATH' >> $HOME/.bash_profile
```

Remember to set your user preferences after installation (see above).
	


# Install and sync VCSH and MR
**UPDATED: 20150818**

I use [VCSH][] and [MR][] to keep my dotfiles and git repositories synchronized among hosts. If you haven't already initialized a set of VCSH/MR repositories for yourself, you could follow [my instructions][] to do so on an existing host where you already have dotfiles and repositories worth tracking.

After [installing][] the VCSH and MR executables on a new host, I [synchronize][] all of my existing MR/VCSH-tracked repositories to that new host with two commands:


```bash
vcsh clone https://github.com/stowler/mr.git mr
mr update
```

[VCSH]: https://github.com/RichiH/vcsh
[MR]: http://myrepos.branchable.com
[my instructions]: https://github.com/stowler/stowlerGeneralComputing/blob/master/docs/setupVCSH.md#2-clone-to-a-new-host-and-test-operations
[installing]: https://github.com/stowler/stowlerGeneralComputing/blob/master/docs/setupVCSH.md#1-install-vcsh-and-mr
[synchronize]: https://github.com/stowler/stowlerGeneralComputing/blob/master/docs/setupVCSH.md#3-sync-to-a-new-host


# Confirm important dotfiles

I use individual VCSH repositories to sync and track my most important dotfiles:

```bash
$ vcsh list
mr
vcsh-sdt-bash
vcsh-sdt-iterm2
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


## dotfiles sourced directly from mathiasbynens
I source these directly from the [mathiasbynens dotfiles repo][]. The `.bash_profile` sources all of the other files. 

TBD: how do I bootstrap from the repo to my homedir and watch for changes?

### .aliases
This provides smart aliasing of ls, as well as a number of other aliases like `afk` and `...`.

### .bash_profile
In addition to setting a number of shell options, this file also has a line that sources all of the other dotfiles in my vcsh-sdt-bash repo.

### .bashrc
This file mostly just displaces a system's default (and usually empty) `.bashrc`.

### .exports
Exports reasonable values for environmental variables like EDITOR, HIST\*, LANG, and GREP_OPTIONS

*TBD: pull out my content*



## dotfiles adapted from mathiasbynens

### .bash_prompt
This is my custom-edited version of the original from the [mathiasbynens dotfiles repo][]

## dotfiles and settings managed through .extra
As a way of adding custom commands and configs without forking mathiasbynens, I've added some of my own customizations to `.extra`, which is the last file sourced by `.bash_profile`


## .path
`.path` isn't in the vcsh-sdt-bash file list above because its config is pretty machine specific. Excerpted from https://github.com/mathiasbynens/dotfiles/blob/master/README.md :

>   If ~/.path exists, it will be sourced along with the other files, before any feature testing (such as detecting which version of ls is being used) takes place.

This means that `.path` isn't particularly useful for things like `$FSLDIR/data/standard`, since the values of $FSLDIR isn't defined in `.exports` until *after* `.path` is sourced.

*TBD: add `.extra_local`*


[mathiasbynens dotfiles repo]: https://github.com/mathiasbynens/dotfiles



Solarized-ize the terminal
==============================

The [solarized color palette](http://ethanschoonover.com/solarized) produces legible color-coding of text in a number of environments. [I use it within vim](https://github.com/stowler/vcsh-sdt-vim/blob/master/.vimrc) for [syntax highlighting](http://ethanschoonover.com/solarized/img/screen-shell-dark.png), but it is also helpful to have it available in the terminal for [color-coded `ls` output](https://raw.githubusercontent.com/seebi/dircolors-solarized/master/img/dircolors.256dark.png). The steps for configuring the terminal to use the solarized palette vary depending on the specific terminal emulator and environment. Below are my notes on terminal environments where I use it.

## OS X Yosemite: iTerm2

In OS X I use [iTerm](http://iterm2.com) instead of the built-in terminal, and I have added Solarized Dark to my [iTerm2 config](https://github.com/stowler/vcsh-sdt-iterm2/tree/master/.iterm2). This iTerm2 palette is included in the [official solarized repository](https://github.com/altercation/solarized), and can be installed according to the instructions in its README file:

```bash
git clone git://github.com/altercation/solarized.git
less solarized/iterm2-colors-solarized/README.md 
```

## CentOS 6.6: gnome-terminal and dircolors

At the moment the official solarized repository doesn't contain a configuration for gnome terminal, but a third party is maintaining the [Gnome Terminal Colors Solarized repository](https://github.com/Anthony25/gnome-terminal-colors-solarized). Clone that repository and run its interactive install script:

```bash
git clone https://github.com/Anthony25/gnome-terminal-colors-solarized.git
cd gnome-terminal-colors-solarized
./install.sh
```

With that completed, you just need to give bash its color scheme for color-coded `ls` output. This can be done by installing the [Solarized Color Theme for GNU ls](https://github.com/seebi/dircolors-solarized):

```bash
git clone https://github.com/seebi/dircolors-solarized.git
cd dircolors-solarized
cp dircolors.256dark ${HOME}/.dircolors
echo 'eval `dircolors ${HOME}/.dircolors`' >> ${HOME}/.bash_profile

```



# Install general command-line utilities


Install these utilities. If you don't know why now, you will. This will take negligible time on debian/ubuntu linux, but about 2.5 hours of macports compiling on a 2.8 GHz i5 iMac.

Each of these packages can be installed on debian/ubuntu linux by typing:

	sudo apt-get install [name(s) of the package(s)]
	
...and on OS X via Macports:

	sudo port install [name(s) of the package(s)]

Below is a list of the package names to substitute into the commands above (no square brackets when you actually type/paste these package names into the install command above:)

	curl wget tmux tree htop slurm parallel imagemagick
	
And for OS X only you will also want these:

	getopt tmux-pasteboard openssh +ssh_copy_id

## export ssh public key to remote hosts

Enable password-less ssh logins to a remote host from your trusted secure client:

```bash
# generate your public/private rsa key pair:
$ ssh-keygen
# ...just keep pressing the enter key...don't enter a password

# export your public key to a remote host to which you would like to have passwordless access:
$ ssh-copy-id user@remotehost.something

# now you should be able to ssh to the remote host as before, but you won't be
# prompted for a password:
$ ssh user@remotehost.something

```

## configure tmux

For OS X only, follow these instructions in the top of the default .tmux.conf: 

	# To enable tmux-MacOSX-pasteboard add following line to ~/.tmux.conf replacing
	'bash' with your actual shell:
	set-option -g default-command "/opt/local/bin/reattach-to-user-namespace bash"



Install R 
============================

R is the way and the light. It is a complete statistics analysis language supported by a universe of active statisticians and developers. Rstudio is a graphical integrated development environment for the R language.

## Install R and Rstudio on OS X Mavericks:

1. [Download R]( http://cran.stat.ucla.edu/bin/macosx/) as precompiled binary of R base packages.
2. Install R from the download .pkg file.
3. [Download Rstudio Desktop](http://www.rstudio.com/ide/download/desktop) as a precompiled binary.
4. Install Rstudio Desktop from downloaded .dmg file.

To upgrade R or Rstudio Desktop just follow the same instructions. They are both generally good about finding existing versions and either migrating everything over to the new version or warning you if there is going to be trouble.
 

## Install R and Rstudio on ubuntu linux:
**UPDATED: 20150818**

If R has already been installed from the default apt sources it is probably out-of-date or will be soon, and should be replaced by packages from the R CRAN repos. 

First confirm the location of currently installed R libraries:

```
$ sudo R --no-save
> .libPaths()
[1] "/usr/local/lib/R/site-library" "/usr/lib/R/site-library"
[3] "/usr/lib/R/library"
```

Next uninstall the existing R packages that are registered with apt:

```bash
$ sudo apt-get autoremove r-base r-base-core r-base-dev r-doc-html
# ...after which you may want to run aptitude to detect and resolve any conflicts created by that command
```

Then uninstall the existing R packages that weren't registered with apt:

```bash
# (this command will vary depending on the output of .libPaths() above)
$ sudo rm -fr /usr/local/lib/R/site-library /usr/lib/R/site-library /usr/lib/R/library

```


With that fresh start, follow the R Ubuntu [README](http://cran.r-project.org/bin/linux/ubuntu/README.html) to add the official R ubuntu apt source and `r-base` and `r-base-dev`:

```bash
# add the secure apt key to your system:
$ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E084DAB9

# add this line to /etc/apt/sources.list for 14.04 Trusty, or modify for your ubuntu release per the README
# deb http://cran.stat.ucla.edu/bin/linux/ubuntu trusty/
$ sudo apt-get update

# install the base R packages:
$ sudo apt-get install r-base r-base-dev
```

Update the installed packages from within R:

```
$ sudo R --no-save
> update.packages(ask=FALSE)
> q()
```

Because 3D operations and GUI toolkits can be touchy, it is helpful to install and test `rgl` and `Rcmdr` before adding any other R packages. Start by installing dependencies from apt sources:

```bash
 # rgl dependencies from apt sources:
 $ sudo apt-get install xserver-xorg-dev libx11-dev libglu1-mesa-dev mesa-utils glew-utils

 # Rcmdr dependencies from apt sources:
 # (you could apt-get install r-cran-rjava, but may be better to just install
 # its deps instead:)
 $ sudo apt-get install default-jre default-jdk unixodbc-dev
 $ sudo R CMD javareconf

 # RcmdrPlugin.HH dependencies from apt sources:
 $ sudo apt-get install libgmp-dev libmpfr-dev

```
<!-- 
What about dependencies from previous documentation:
tk-dev ? tk8.5-dev ? tclreadline ? libopenmpi-dev ? libxml2-dev ?
-->

Finally, compile and install these sentinal packages from within R: `rgl`, `car`, `Rcmdr`, and `RcmdrPlugin.HH`. I use these packages in my work, but have also found that they are good at surfacing R installation problems:

```bash
$ sudo R --no-save
> install.packages('rgl',            dependencies=TRUE, repos='http://cran.stat.ucla.edu')
> install.packages('car',            dependencies=TRUE, repos='http://cran.stat.ucla.edu')
> install.packages('XLConnect',      dependencies=TRUE, repos='http://cran.stat.ucla.edu')
> install.packages('Rcmdr',          dependencies=TRUE, repos='http://cran.stat.ucla.edu')
> install.packages('RcmdrPlugin.HH', dependencies=TRUE, repos='http://cran.stat.ucla.edu')
> q()
```

With installation complete, [test R 3D and GUI toolkits][].


To install Rstudio, just download the rstudio [.deb installation file from the rstudio website](http://www.rstudio.com/ide/download/desktop). Install by double-clicking on it, and after installation it should appear in Applications -> Development -> Rstudio . (TBD: CLI version)




## Install R and Rstudio on Neurodebian 7.2.0 wheezy virtual machine:
**UPDATED: 20150818**
**TBD: re-write to match or incorporate Ubuntu section**

For a neurodebian wheezy virtual machine (VM) installed and updated using 
[these instructions](http://j.mp/setupNeurodebianVM), a working installation of R can be added with the following steps. These instructions are based on the 
[CRAN installation instructions for installing R on Debian 7.0 / 7.2.0 wheezy](http://cran.r-project.org/bin/linux/debian/).
Because of the transition from the 2.x R series to 3.x, special care must me taken to install
a minimum of pre-compiled 3.x binaries, followed by compiling current packages from source.

First get the key for the R 3.x backports:

```bash
$ sudo gpg --keyserver pgp.mit.edu --recv-key 381BA480
$ sudo gpg -a --export 381BA480 > /tmp/jranke_cran.asc
$ sudo apt-key add /tmp/jranke_cran.asc
```

...and add these lines to `/etc/apt/sources.list` :

    deb http://cran.stat.ucla.edu/bin/linux/debian wheezy-cran3/
    deb-src http://cran.stat.ucla.edu/bin/linux/debian wheezy-cran3/


## Test R 3D and GUI toolkits
**UPDATED: 20150823**

Test R, including its 3D and GUI toolkits. None of these should produce errors:

```bash
$ sudo R --no-save
> library(rgl)
> demo(rgl)
> library(car)
> library(Rcmdr)
# mouse:
#     1) Tools -> Load Rcmdr plug-ins... -> RcmdrPlugin.HH
#     2) Data -> Data in packages -> Read data set from an attached package... -> PACKAGE: datasets, DATA SET: mtcars
#     3) Data set: mtcars
#     4) Graphs -> 3d graph -> 3d scatterplot... (HH). DV: mpg, IVs: disp, hp.
#     5) Graphs -> 3d graph -> "Open new 3D grahics window", "Identify observations with mouse", "Show surface grid lines" 
#
# ...or the CLI version of steps 2-5:
> data(mtcars, package="datasets")
> scatter3dHH(mtcars$disp, mtcars$mpg, mtcars$hp, fit="linear", bg="white", grid=TRUE, squares=FALSE, xlab="disp", ylab="mpg", zlab="hp")
> Identify3d(mtcars$disp, mtcars$mpg, mtcars$hp, labels=row.names(mtcars))
> q()
```

[test R 3D and GUI toolkits]: #test-r-3d-and-gui-toolkits

# Install Matlab
**UPDATED: 20150822**

Usually I direct download direct from [Matlab](http://www.mathworks.com/). At installation I select these toolboxes to support neuroimaging apps (2.3 GB download, 5.5 GB install) :

- bioinformatics toolbox
- database toolbox
- image processing toolbox
- matlab coder
- matlab compiler
- matlab compiler SDK
- parallel computing toolbox
- signal processing toolbox
- statistic and machine learning toolbox

Once Matlab is installed, the command `ver` entered at the Matlab prompt will output a list of installed toolboxes.

## install matlab on linux
**UPDATED: 20150822**

This is the post-download install procedure I use on all flavors of linux:

```bash
$ cd ~/Downloads
$ mkdir installMatlab
$ cd installMatlab
$ unzip ../matlab_R2015a_glnxa64.zip
$ sudo ./install
# I like to install to /opt/MATLAB/${matlabVersion}, like /opt/MATLAB/R2015a
# and then I allow the installer to create symbolic links in its default /usr/local/bin
```

## install matlab on OS X

_TBD: basically the same as linux but I need to confirm that and write up during my next install_

# Install a grid engine

Sometimes you'll be running software that can use a scheduler like Sun Grid Engine or Son of Grid Engine to perform parallel processing across multiple cores of a single host, or even multiple nodes in a cluster.

At the moment my choice of examples below is mostly driven by what works for FSL, which is the primary scheduler-enbabled neruoimaging package I use. (Lazily consolidating my notes here as I deploy new installs).

## Install gridengine on Ubuntu 14.04


## Install son of gridengine

TBD

## Install torque

TBD

## Install condor

TBD
