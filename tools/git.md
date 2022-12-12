### Dotfiles
- Creating a dotfile git repo  
1. Intialize git and create a folder named ~/.cfg
```bash
git init --bare $HOME/.cfg
```
2. Put this in your .bashrc or .zsh to use `config` as a dotfiles alias.  
```bash
  alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'
```

3. Make sure to ignore the folder we're going use to clone.  
```bash
echo ".cfg" >> .gitignore
```
4. Set flag to not show untracked files  
```bash
config config --local status.showUntrackedFiles no
```
5. Replacing git with our newly created config alias we can version control our
  dotfiles.
```bash
config status
config add .bashrc
config commit -m "Added bashrc"
config push
```

config submodule add https://github.com/user/repo.git .path/to/repo  

config submodule update --remote --merge

- - -

### Basic commands
Intialize a git repository in the root of the folder.
```bash
git init
```
See which files git knows exist.
```bash
git status
```
Add a new file to the repo.
```bash
git add <file>
```
Create a commit with a message about the commit.
```bash
git commit -m <file>
```
Push the changes/commits to our repo.
```bash
git push -u origin main
```
