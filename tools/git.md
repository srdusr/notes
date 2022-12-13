## Dotfiles
#### Creating a dotfile git repo  
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
#### Installing onto a new system  
  1. Avoid weird behaviour/recursion issues when .cfg tries to track itself  
  ```bash
  echo ".cfg" >> .gitignore
  ```
  2. Clone the repo
  ```bash
  git clone <remote-git-repo-url> $HOME/.cfg
  ```
  3. Set up the alias 'config'  
  ```bash
  alias config='/usr/bin/git --git-dir=<path to .cfg’s Git directory> --work-tree=$HOME'
  ```
  4. Set local configuration into .cfg to ignore untracked files  
  ```bash
  config config --local status.showUntrackedFiles no
  ```
  5. Checkout  
  ```bash
  config checkout
  ```
#### Use submodules to sync other repos into dotfiles  
  1. Add a submodule to dotfiles  
  ```bash
  config submodule add https://github.com/user/dotfiles.git .path/to/dotfiles  
  ```
  2. Update submodules to sync to dotfiles  
  ```bash
  config submodule update --init --recursive  
  ```
  3. Config push  
  ```bash  
  config push  
  ```
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
