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
-----------------------------------

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

2. Clone to a second host and confirm sync
==============================================================================


3. Add new vcsh repos
============================

