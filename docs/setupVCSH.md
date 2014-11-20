These are my provisional notes on how to get started using VCSH and MR to manage your dotfiles.


I followed a combination of the [vcsh author documentation][] and [this Nov 2013 Linux Journal article.][] My initial host was a debian wheezy 7.4.0 VM (no backports).

[vcsh author documentation]: https://github.com/RichiH/vcsh/tree/master/doc
[this Nov 2013 Linux Journal article.]: http://www.linuxjournal.com/content/manage-your-configs-vcsh



1. One-time only: installation and initial push of vcsh and mr
=========================================================



1.1. Download and install vcsh and mr
----------------------------------------

If git isn't already installed on your computer, [download and install](https://github.com/stowler/stowlerGeneralComputing/blob/master/docs/setupBasicScriptingEnvironment.md#git) git before following the rest of these instructions.

Once git is installed, choose a parent directory into which you will clone the git repos for [vcsh](https://github.com/RichiH/vcsh) and [mr](http://myrepos.branchable.com):

```bash
mkdir ${HOME}/src.upstream.gitRepos
```


Clone the [vcsh repository](https://github.com/RichiH/vcsh) and make it available system-wide:

```bash
cd ${HOME}/src.upstream.gitRepos
git clone git://github.com/RichiH/vcsh.git
sudo mkdir -p /usr/local/bin
sudo ln -s ${HOME}/src.upstream.gitRepos/vcsh/vcsh /usr/local/bin/
ls -l /usr/local/bin # ...which should show /usr/local/bin/vcsh as a symlink
```



Clone the [myrepos repository](http://myrepos.branchable.com) and make it available system-wide:
```bash
cd ${HOME}/src.upstream.gitRepos
git clone git://myrepos.branchable.com/myrepos
cd myrepos
sudo make install
# ...this installs the executable /usr/bin/mr and its supporting files
```



1.2. Create and push your first vcsh repo
-------------------------------------------

After you confirm that your `~/.vimrc` and `~/.vim/` exist, initialize a vcsh repo for vim configuration:
```bash
cd ${HOME}
vcsh init vcsh-sdt-vim
# …which produces ~/.config/vcsh if it didn’t already exist, and specifically
# for this repo it produces ~/.config/vcsh/repo.d/vcsh-sdt-vim.git/
```

Add your vim files to the repo and commit:
```bash
vcsh vcsh-sdt-vim add ${HOME}/.vimrc ${HOME}/.vim
vcsh vcsh-sdt-vim commit -m 'Initial commit of my vim configuration'
```

Now create your vim repo on the github website, which will give you the remote origin.
When complete, configure the local repo for that origin and push it:
```bash
vcsh vcsh-sdt-vim remote add origin https://github.com/stowler/vcsh-sdt-vim.git
vcsh vim push -u origin master
```



1.3. Customize and push the vcsh mr template
--------------------------------------------------

Clone the vcsh mr template:
```bash
vcsh clone git://github.com/RichiH/vcsh_mr_template.git mr
ls ${HOME}/.config/mr/available.d/
# ...should just show mr.vcsh and zsh.vcsh
```

Add the vcsh vim repo to mr by adapting mr's newly downloaded zsh.vcsh template: 
```bash
cd ${HOME}/.config/mr/available.d
mv zsh.vcsh vcsh-sdt-vim.vcsh
# edit ~/.config/mr/available.d/vcsh-sdt-vim.vcsh to say:
[${HOME}/.config/vcsh/repo.d/vcsh-sdt-vim.git]
checkout = vcsh clone https://github.com/stowler/vcsh-sdt-vim.git vcsh-sdt-vim
```

Do the same for `mr.vcsh`:
```bash
# edit ~/.config/mr/available.d/mr.vcsh to point to github:
[${HOME}/.config/vcsh/repo.d/mr.git]
checkout = vcsh clone https://github.com/stowler/mr.git mr
```

At the moment mr is only setup to sync the mr.vcsh repo. Add a symlink to tell mr to sync the vim repo as well:
```bash
cd ${HOME}/.config/mr/config.d/
ls -l #…should just see link to mr.vcsh
ln -s ../available.d/vcsh-sdt-vim.vcsh vcsh-sdt-vim.vcsh
```

Now create your mr repo on the github website, which will give you the remote origin.
When complete, configure the local repo for that origin and push it to github:
```bash
cd ${HOME}/.config
vcsh enter mr
ls #…one of the directories should be mr
git add mr
git commit -m ‘initial commit’
# before init and push, notice that the original origin persists:
git remote show origin
# ...so remove it:
git remote rm origin
# ...and replace it with the new origin from the github repo you just created in the browser:
git remote add origin https://github.com/stowler/mr.git
git push -u origin master
```



2. Clone to a new host and test operations
=============================================


2.1. Sync your VCSH/MR repos to a new host
-----------------------------------------
1. Install VCSH and MR per section 1.1 above.
2. VCSH clone your MR configs via `vcsh clone https://github.com/stowler/mr.git mr` , which creates:
   ```bash
   ~/.config/
   ~/.config/git/ignore # TBD: not really, as of 20141028. Fix this.

   ~/.config/mr/
   ~/.config/mr/available.d/*.vcsh
   ~/.config/mr/config.d/*.vcsh

   ~/.config/vcsh/
   ~/.config/vcsh/repo.d/mr.git/

   ~/.mrconfig
   ```

3. Update all mr-registered repos: `mr update`

4. `ls -al ~/.config/mr/*.d/` to confirm that any vcsh repos that should be active for this host are linked from `~/.config/mr/available.d/*.vcsh` to `~/.config/mr/config.d/`



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


3. Add an existing (non-vcsh) repo to .mrconfig
====================================================
MR can also sync non-vcsh repos so that you have the same repos available on all of your hosts.

1. Clone an existing non-vcsh repo to somewhere reasonable (e.g., `$HOME/src.upstream.gitRepos` or `$HOME/src.mywork.gitRepos`):
   ```bash
   cd $HOME/src.upstream.gitRepos
   git clone git://github.com/altercation/solarized.git
   ```

2. Register the repo into `~/.mrconfig`:
   ```bash
   cd $HOME/src.upstream.gitRepos/solarized
   mr register
   cat $HOME/.mrconfig #...should show the new repos's entry at the end of .mrconfig
   ```

3. Via `vcsh`, commit and push the `.mrconfig` changes:
   ```bash
   vcsh enter mr
   git status #...should show modified .mrconfig
   git add .mrconfig
   git commit -m 'added upstream repo: solarized'
   git push -u origin master
   exit # ...exiting the vcsh repo
   ```


4. Add and test new vcsh repo
============================

On second host, confirm that mr is current (`mr update`), and if so add .tmux as a second repo.

4.1. Add new vcsh repo
------------------------

1. Name the vcsh repo:        `repoName=vcsh-sdt-tmux`
1. Create config file:        `cp ${HOME}/.config/mr/available.d/vcsh-sdt-vim.vcsh ${HOME}/.config/mr/available.d/$repoName.vcsh`
1. Edit the new .vcsh file to reflect `$repoName`
1. Create symlink:            `cd ${HOME}/.config/mr/config.d; ln -s ../available.d/$repoName.vcsh $repoName.vcsh`
1. Add new .vcsh to mr repo   `vcsh mr add ${HOME}/.config/mr/available.d/$repoName.vcsh`
1. Init the new repo:         `vcsh init $repoName`
1. Setup ignores:             `vcsh write-gitignore $repoName`
1. Add the repo's first file: `vcsh $repoName add -f ${HOME}/.tmux.conf` 
1. Commit the new repo:       `vcsh $repoName commit -m "initial commit for $repoName"`
1. Create the new repo on the github website, which will give you the remote origin.  
1. Add new repo origin:       `vcsh $repoName remote add origin https://github.com/stowler/$repoName.git`
1. Push the new repo:         `vcsh $repoName push -u origin master`
1. Use a web browser to confrim that github reflects the push.
1. Commit the change to mr:   `vcsh enter mr; git commit -m 'added vcsh-sdt-tmux'; git push -u origin master; exit`
1. Use a web browser to confirm that github reflects the push.
1. Optional: should every host have this vcsh repo active per config.d link? If so:
   ```bash
   cd ${HOME}/.config/mr/config.d
   vcsh enter mr
   git add -f vcsh-sdt-tmux.vcsh
   git commit -m 'added symlink mr/config.d/vcsh-sdt-tmux.vcsh'
   git push -u origin master
   exit
   ```

1. Then VCSH [made need some help with gitignore](https://github.com/RichiH/vcsh/issues/126) (TBD: remove this step if this bug has been fixed):
   ```bash
   repo=myRepoName
   vcsh write-gitignore $repo
   vcsh $repo add -f .gitignore.d/$repo
   vcsh write-gitignore $repo
   vcsh $repo add .gitignore.d/$repo
   vcsh $repo commit -m "Add/update gitignore.d/$repo"
   vcsh push $repo -u origin master
   ```



4.2. Test: does other host receive the new repo?
--------------------------------------------


