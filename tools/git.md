## Dotfiles

#### Creating a dotfiles git repo

1. Intialize git and create a folder named ~/.cfg

```bash
$ git init --bare $HOME/.cfg
```

2. Put this in your .bashrc or .zsh to use `config` as a dotfiles alias.

```bash
$ alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'
```

3. Make sure to ignore the folder we're going use to clone.

```bash
$ echo ".cfg" >> .gitignore
```

4. Set flag to not show untracked files

```bash
$ config config --local status.showUntrackedFiles no
```

5. Replacing git with our newly created config alias we can version control our
   dotfiles.

```bash
$ config status
$ config add .bashrc
$ config commit -m "Added bashrc"
$ config push
```

#### Installing onto a new system

1. Avoid weird behaviour/recursion issues when .cfg tries to track itself

```bash
$ echo ".cfg" >> .gitignore
```

2. Clone the repo

```bash
$ git clone --bare <remote-git-repo-url> $HOME/.cfg
```

3. Set up the alias 'config'

```bash
$ alias config='/usr/bin/git --git-dir=<path to .cfg’s Git directory> --work-tree=$HOME'
alias config='git --git-dir=$HOME/.cfg --work-tree=$HOME'
```

4. Set local configuration into .cfg to ignore untracked files

```bash
$ config config --local status.showUntrackedFiles no
```

5. Checkout

```bash
$ config checkout
```

git symbolic-ref refs/remotes/origin/HEAD refs/remotes/origin/main
git branch -u origin/branchName
or
git branch --set-upstream-to=origin/master main
git update-ref refs/heads/master origin/master

You can also set it with a push
git push -u origin master
git push --set-upstream origin master

#### Use git subtree to sync other repos into dotfiles

1. First make sure dotfiles is up-to date or commit/push/reset all changes
   otherwise this error message will show: `Working tree has modifications.  Cannot add.`

```bash
$ config reset --hard origin/main
```

Also NOTE: the prefix (subdirectory in which you will add the subtree) cannot already exist therefore delete/backup locally.

2. Add the repo's file path and it's remote url:  
   NOTE: Can use the `--squash` flag to omit storing of entire history of subproject into main repo but if used then the flag will always have to be used with the given repo/subtree and it's commands

```bash
$ config subtree add --prefix /path/to/file <remote-git-repo-url> <branch>
# Example:
$ config subtree add --prefix .config/nvim https://github.com/srdusr/nvim.git main --squash
```

3. Update to sync/show any changes into dotfiles (upstream repo):

```bash
$ config subtree pull --prefix /path/to/file <remote-git-repo-url> main
```

4. Finally push onto remote repository:

```bash
$ config push
```

5. Optional aliases to put into .gitconfig:

```bash
[alias]
  sba ="!f() { git subtree add --prefix $2 $1 main; }; f"
  sbu ="!f() { git subtree pull --prefix $2 $1 main; }; f"
  # Or use --squash if prefered
  sba ="!f() { git subtree add --prefix $2 $1 main --squash; }; f"
  sbu ="!f() { git subtree pull --prefix $2 $1 main --squash; }; f"
# Example:
$ config sbu https://github.com/srdusr/nvim.git .config/nvim #--squash
```

---

## Basic commands

Intialize a git repository in the root of the folder:

```bash
$ git init
```

See which files git knows exist:

```bash
$ git status
```

Add a new file to the repo:

```bash
$ git add <file>
```

Create a commit with a message about the commit:

```bash
$ git commit -m <file>
```

Make main branch

```bash
$ git branch -M main
```

Add remote server repository

```bash
$ git remote add origin https://github.com/srdusr/grimoire.git
```

> NOTE: To remove server: `git remote remove origin` or change url `git remote set-url origin git://new.url.here`
> Push the changes/commits onto repo:

```bash
$ git push -u origin <branch>
```

Fetch the most recent changes/commits from the remote branch/repository
> NOTE: make sure to checkout to the desired branch first, example: `git checkout main`
```
$ git fetch origin
```
or 
```
$ git fetch origin main:refs/remotes/origin/main
```

Reset the local main branch to remote repository aka...  
Delete the most recent commit, destroying the work you've done:

```bash
$ git reset --hard origin/main
```

Delete the most recent commit, keeping the work you've done:

```bash
$ git reset --soft origin/<branch>
```

Allow unrelated histories when two unrelated projects are merged/unaware of each
other's existence:

```bash
$ git pull origin <branch> --allow-unrelated-histories
```

Diff between commits

```
$ git log
$ git diff (checkout_id):file.txt file.txt
or
$ git diff <commit_id1> <commit_id2>
or
$ git difftool <commit_id1> <commit_id2>

```

If the top commit is pointed to by HEAD then you can do something like this:

commit1 -> HEAD
commit2 -> HEAD~1
commit3 -> HEAD~2

Diff between the first and second commit:

git diff HEAD~1 HEAD

Diff between first and third commit:

git diff HEAD~2 HEAD

Diff between second and third commit:

git diff HEAD~2 HEAD~1

---

#### Miscellaneous

Find out size of a repo before cloning it

```bash
$ curl -s https://api.github.com/repos/{orgname/username}/{repo_name} | jq '.size' | numfmt --to=iec --from-unit=1024

```

---

#### Trouble-shooting

fatal: ambiguous argument 'origin': unknown revision or path not in the working tree

```bash
$ git fetch origin main:refs/remotes/origin/main
```

---
