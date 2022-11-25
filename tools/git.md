## Dotfiles
- Intialize git and create a folder named ~/.cfg
```bash
git init --bare $HOME/.cfg
```
- Put this in your .bashrc or .zsh to use `config` as a dotfiles alias.  
```bash
  alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'
```

- Make sure to ignore the folder we're going use to clone.  
```bash
echo ".cfg" >> .gitignore
```
- Set flag to not show untracked files  
```bash
config config --local status.showUntrackedFiles no
```
- Replacing git with our newly created config alias we can version control our
  dotfiles.
```bash
config status
config add .bashrc
config commit -m "Added bashrc"
config push
```
config submodule add https://github.com/user/repo.git .path/to/repo  

config submodule update --remote --merge
