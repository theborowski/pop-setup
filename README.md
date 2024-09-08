# pop_os 22.04 setup

## install & set `zsh` as the default shell

```sh
sudo apt install zsh
zsh --version
chsh -s $(which zsh)
```
* Logout and back in to apply change of default shell.
* When configuring the .zshrc file, choose an empty option, `ohmyzsh` will replace it.
* Check installation okay with `$SHELL --version`.

## install `ohmyzsh`

https://github.com/ohmyzsh/ohmyzsh/

basic installation option
```sh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

* Remove the backup `.zshrc` file the installation made with `rm .zshrc.pre-oh-my-zsh`.

## install `pure` prompt for `zsh`

* clone the `pure` repo
```sh
mkdir -p "$HOME/.zsh"
git clone https://github.com/sindresorhus/pure.git "$HOME/.zsh/pure"
```

* Add the path of the cloned repo to `$fpath` in `$HOME/.zshrc` and load the prompt.
```sh
# .zshrc
fpath+=($HOME/.zsh/pure)
autoload -U promptinit; promptinit
prompt pure
```

## install `dracula` theme for `zsh`

```sh
cd "$HOME/.zsh"
git clone https://github.com/dracula/zsh.git
mv zsh dracula

# link the theme
ln -s "$HOME/.zsh/dracula/dracula.zsh-theme" "$HOME/.oh-my-zsh/themes/dracula.zsh-theme"
```

## install `dracula` for `gnome` terminal

https://draculatheme.com/gnome-terminal

```sh
sudo apt-get install dconf-cli
```

```sh
mkdir -p .terminal
git clone https://github.com/dracula/gnome-terminal
cd gnome-terminal
./install.sh
```

## configure `git`

### set the default branch as `main`
```sh
git config --global init.defaultBranch main
```

### set the user email config
```sh
git config --global user.email "email@domain.com"
git config --global core.editor "vim"
```

## install `pyenv`

get the basic dependencies setup
```sh
sudo apt update; sudo apt install build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev curl git \
libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev
```
install `pyenv`
```sh
curl https://pyenv.run | bash
```

## `toshy`

https://github.com/RedBearAK/toshy

```sh
mkdir -p "$HOME/.toshy"
cd "$HOME/.toshy"
```

Then follow the instructions at https://github.com/RedBearAK/toshy?tab=readme-ov-file#how-to-install.


## install `kitty`

```sh
curl -L https://sw.kovidgoyal.net/kitty/installer.sh | sh /dev/stdin
```

### setting up the desktop icon

Haven't gotten the below instructions to work for getting the desktop icon setup so I just installed `kitty` from the pop shop.

```sh
# Create symbolic links to add kitty and kitten to PATH (assuming ~/.local/bin is in
# your system-wide PATH)
ln -sf ~/.local/kitty.app/bin/kitty ~/.local/kitty.app/bin/kitten ~/.local/bin/
# Place the kitty.desktop file somewhere it can be found by the OS
cp ~/.local/kitty.app/share/applications/kitty.desktop ~/.local/share/applications/
# If you want to open text files and images in kitty via your file manager also add the kitty-open.desktop file
cp ~/.local/kitty.app/share/applications/kitty-open.desktop ~/.local/share/applications/
# Update the paths to the kitty and its icon in the kitty desktop file(s)
sed -i "s|Icon=kitty|Icon=$(readlink -f ~)/.local/kitty.app/share/icons/hicolor/256x256/apps/kitty.png|g" ~/.local/share/applications/kitty*.desktop
sed -i "s|Exec=kitty|Exec=$(readlink -f ~)/.local/kitty.app/bin/kitty|g" ~/.local/share/applications/kitty*.desktop
# Make xdg-terminal-exec (and hence desktop environments that support it use kitty)
echo 'kitty.desktop' > ~/.config/xdg-terminals.list
```

### change the theme 

```sh
kitten themes
```

### update `kitty.conf`

press ctrl + shift + f2 to open the kitty config.

```
font_size 10
map ctrl+alt+right next_tab
map ctrl+alt+left previous_tab
```