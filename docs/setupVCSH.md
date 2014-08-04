These are my provisional notes on how to get started with VCSH. 


I followed a combination of the [vcsh author documentation](https://github.com/RichiH/vcsh/tree/master/doc) and [this Nov 2013 Linux Journal article.](http://www.linuxjournal.com/content/manage-your-configs-vcsh) My inital host was a debian wheezy 7.4.0 VM (no backports).


1. Installation and first push of vcsh and mr
==================================================

If git's global config options haven't been set, do so before anything else:
```
git config --global user.name “Stephen Towler”
git config --global user.email stowler@gmail.com
```



1.1. Download and install vcsh and mr
----------------------------------------

Choose a location for your initial vcsh and mr checkouts :

```
mkdir -p ~/work/git
```



Clone vcsh and make it available system-wide:
```
cd ~/work/git
git clone git://github.com/RichiH/vcsh.git
sudo ln -s ~/work/git/vcsh/vcsh /usr/local/bin/
```



Clone myrepos and make it available system-wide:
```
cd ~/work/git
git clone git://myrepos.branchable.com/ myrepos
cd myrepos
sudo make install
```



1.2. Create and push your first vcsh repo
-------------------------------------------

After you confirm that your `~.vimrc` and `~/.vim/` exist, initialize a vcsh repo for vim:
```
cd ~
vcsh init vcsh-sdt-vim
# …which produces ~/.config/vcsh if it didn’t already exist, and specifically
# for this repo it produces ~/.config/vcsh/repo.d/vcsh-sdt-vim.git/
```

Add your vim files to the repo and commit:
```
vcsh vcsh-sdt-vim add ~/.vimrc ~/.vim
vcsh vcsh-sdt-vim commit -m 'Initial commit of my vim configuration'
```

Now create the repo on the github website, which will give you the remote origin.
When complete, configure the local repo for that orign and push it:
```
vcsh vcsh-sdt-vim remote add origin https://github.com/stowler/vcsh-sdt-vim.git
vcsh vim push -u origin master
```



1.3. Customize mr template and push the results
--------------------------------------------------

Clone the vcsh/mr template:
```
vcsh clone git://github.com/RichiH/vcsh_mr_template.git mr
ls ~/.config/mr/available.d/
# ...should just show mr.vcsh and zsh.vcsh
```

Rename the template's zsh.vcsh and edit it to reflect the vim repo you just created:
```
cd ~/.config/mr/available.d
mv zsh.vcsh vcsh-sdt-vim.vcsh
# edit ~/.config/mr/available.d/vcsh-sdt-vim.vcsh to say:
\[$HOME/.config/vcsh/repo.d/vcsh-sdt-vim.git\]
checkout = vcsh clone https://github.com/stowler/vcsh-sdt-vim.git vcsh-sdt-vim
```

Do the same for `mr.vcsh`:
```
# edit ~/.config/mr/available.d/mr.vcsh to point to github:
\[$HOME/.config/vcsh/repo.d/mr.git\]
checkout = vcsh clone https://github.com/stowler/mr.git mr
```

At the moment mr is only setup to sync the mr.vcsh repo. Add a symlink to tell mr to sync the vim repo:
```
cd ~/.config/mr/config.d/
ls -l #…should just see link to mr.vcsh
ln -s ../available.d/vcsh-sdt-vim.vcsh vcsh-sdt-vim.vcsh
```

Now create the mr repo on the github website, which will give you the remote origin.
When complete, configure the local repo for that origin and push it to github:
```
cd ~/.config
vcsh enter mr
ls #…one of the directories should be mr
git add mr
git commit -m ‘initial commit’
# before init and push, notice that the original origin persists:
git remote show origin
# ...so remove it:
git remote rm origin
# ...and replace it with the new origin from the github repo you just created on-line:
git remote add origin https://github.com/stowler/mr.git
git push -u origin master
```



2. Clone to a second host and test operations
=============================================


2.1. Clone vcsh and mr to second host
----------------------------------------
1. Install vcsh and mr (see section 1.1 above)
2. `vcsh clone https://github.com/stowler/mr.git mr` (adds `mr` and `vcsh` directories to `~/.config`)
3. `mr update`



2.2. Test: does editing an existing file work?
--------------------------------------------
1. Manually confirm that the second host received the most up-to-date .vimrc
1. Make some trivial edit to second host's .vimrc
1. `mr diff` to confirm that the second host's mr sees the edit
1. Commit and push from second host: `mr commit -m "trivial test edits on second host"`
1. Use a web browser to confirm that github reflects the commit.
1. On original (first) host run `mr update`. Manually confirm that the host received the edits.



2.3. Test: does adding a new file work?
------------------------------
TBD


2.4. Test: does removing a file work?
-----------------------------
TBD


2.5. Test: does renaming a file work?
-----------------------------
TBD


2.6. Test: does moving a file work?
-----------------------------
TBD



3. Add and test new vcsh repo
============================

On second host, confirm that mr is current (`mr update`), and if so add .tmux as a second repo.

3.1. Add new vcsh repo
------------------------

1. Name the vcsh repo:        `repoName=vcsh-sdt-tmux`
1. Create config file:        `cp ~/.config/mr/available.d/vcsh-sdt-vim.vcsh ~/.config/mr/available.d/$repoName.vcsh`
1. Edit the new .vcsh file to reflect $repoName
1. Create symlink:            `cd ~/.config/mr/config.d; ln -s ../available.d/$repoName.vcsh $repoName.vcsh`
1. Add new .vcsh to mr repo   `vcsh mr add ~/.config/mr/available.d/$repoName.vcsh`
1. Init the new repo:         `vcsh init $repoName`
1. Setup ignores:             `vcsh write-gitignore $repoName`
1. Add the repo's first file: `vcsh $repoName add -f ~/.tmux.conf` 
1. Commit the new repo:       `vcsh $repoName commit -m "initial commit for $repoName"`
1. Create the new repo on the github website, which will give you the remote origin.  
1. Add new repo origin:       `vcsh $repoName remote add origin https://github.com/stowler/$repoName.git`
1. Push the new repo:         `vcsh $repoName push -u origin master`
1. Use a web browser to confrim that github reflects the push.
1. Commit the change to mr:   `vcsh enter mr; git commit -m 'added vcsh-sdt-tmux'; git push -u origin master; exit`
1. Use a web browser to confirm that github reflects the push.

Optional: should every host have this vcsh repo active per config.d link? If so:

```
cd ~/.config/mr/config.d
vcsh enter mr
git add -f vcsh-sdt-tmux.vcsh
git push -u origin master
exit
```

3.2. Test: does other host receive the new repo?
--------------------------------------------


