---
layout: post
title: Linux setup guide
---

## Install basic utilities
```
sudo apt-get install vim git curl zsh tmux tree
```

## Set up shell, dotfiles, theme

ZSH
```
zsh
chsh -s $(which zsh)
sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)
```

Dotfiles and shell scripts
```
git clone https://github.com/erikr/dotfiles.git  
cd dotfiles && sh generate_symlinks.sh
```

Vundle
```
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim  
vim +PluginInstall +qall
```

TypeWritten ZSH theme
```
git clone git@github.com:reobin/typewritten.git $ZSH_CUSTOM/themes/typewritten
ln -s "$ZSH_CUSTOM/themes/typewritten/typewritten.zsh-theme" "$ZSH_CUSTOM/themes/typewritten.zsh-theme"  
```

ZSH syntax highlighting
```
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting  
rm -rf zsh-syntax-highlighting
```

## Anaconda and environments
```
wget https://repo.anaconda.com/archive/Anaconda3-2019.10-Linux-x86_64.sh
sh Anaconda3
source ~/anaconda3/bin/activate
```
No need to run `conda init zsh`. My `.zshrc` sets paths.

## SSH
Install some stuff
```
sudo apt install openssh-server
sudo systemctl status ssh
sudo ufw allow ssh
```

From your local machine, add your public key to the remote machine's authorized keys:
```
cat ~/.ssh/id_rsa.pub | ssh b@B 'cat >> ~/.ssh/authorized_keys'
```

## For local use

Set up Solarized Dark for the terminal
```
git clone https://github.com/aruhier/gnome-terminal-colors-solarized.git  
cd gnome-terminal-colors-solarized  
./install.sh  
cd && rm -rf gnome-terminal-colors-solarized
```

Install [JetBrains Mono font](https://www.jetbrains.com/lp/mono/)

Install Dropbox
https://www.dropbox.com/install-linux  
> Waiting for the app to ask for the link code never works. Instead, log in at dropbox.com/login.

## For `mithril`:

Edit grub
```
sudo vim /etc/default/grub
--verbose debug nomodeset
```

Create mount points for HDDs, and mount on startup:
```
sudo \mkdir /media/8tb  
sudo \mkdir /media/2tb  
sudo -E vim /etc/fstab  
/dev/sda1 /media/8tb ext4 defaults 0 0
/dev/sdb1 /media/2tb ext4 defaults 0 0
```

Set up CIFS and SMB mount to external servers
```
sudo apt-get install cifs-utils  
sudo \mkdir /media/mad3  
```
Mount scripts are at `~/dotfiles/mount-mad3.sh`

