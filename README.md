# .dotfiles Installation and config patterns for Arch on WSL.
Warning: If you want to give these dotfiles a try, you should first fork this repository, review the code, and remove things you don’t want or need. Don’t blindly use my settings unless you know what that entails. Use at your own risk!
This Readme is just a description of what's happening in each step, the goal is to make this an automated proccess through script. 


## To clone this repository
```
git clone git@github.com:sglauber/.dotfiles.git
```


# Core
> These are the packages that I consider for me to work on arch

### Installing yay
```
pacman -S --needed git base-devel
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
```

### Installing ZSH
```
yay -S zsh
sudo chsh -s /bin/zsh curr_user
```

### Installing powerlevel10k
```shell
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/powerlevel10k
echo "source ~/powerlevel10k/powerlevel10k.zsh-theme" >>~/.zshrc
```

# Plugin manager ASDF managing node, python, kotlin all at once.
```
git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.9.0
echo "/opt/asdf-vm/asdf.sh" >> ~/.zshrc
```


# Rewritten in rust
These are linux packages that were rewritten in Rust, they bring a nicer look to ls, cat and diff respectivelly, this assumes that rust/cargo will be already installed

> Installing packages with cargo 
```
cargo install exa
cargo install --locked bat / pacman -S bat
cargo install git-delta
```

# Persistent SSH on WSL 
SSH on WSL keeps asking for passphrase (it may be cause of the missing sytemd).
The solution is to use a agent-manager just as keychain, it will handle the agent as soon as
the terminal session is open and will persist until the host machine is rebooted.

## Install keychain and add the agent to the shell configuration file
```shell
yay -S keychain
eval `keychain --quiet --eval --agents ssh keyid_here`
```