# my_config
```bash
sudo apt update && sudo apt -y upgrade

sudo apt install -y git curl xclip luarocks tmux zsh
```
Installing some crazy fonts.
```bash
sudo apt install fonts-powerline
wget https://github.com/ryanoasis/nerd-fonts/releases/latest/download/Meslo.zip
unzip Meslo.zip -d ~/.fonts
fc-cache -fv
```

Installing zsh and powerlevel10 
```bash
git clone --depth=1 https://github.com/ohmyzsh/ohmyzsh.git ~/.oh-my-zsh
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
sed -i 's/^ZSH_THEME=.*/ZSH_THEME="powerlevel10k\/powerlevel10k"/' ~/.zshrc
```
Configuring powerlevel10
```bash
echo "⚡ Installing Zsh Plugins..."
ZSH_CUSTOM=${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}
[[ ! -d "$ZSH_CUSTOM/plugins/zsh-autosuggestions" ]] && git clone https://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
[[ ! -d "$ZSH_CUSTOM/plugins/zsh-syntax-highlighting" ]] && git clone https://github.com/zsh-users/zsh-syntax-highlighting $ZSH_CUSTOM/plugins/zsh-syntax-highlighting

sed -i 's/^plugins=(git)/plugins=(git zsh-autosuggestions zsh-syntax-highlighting)/' ~/.zshrc
dock
if [[ -f ~/.p10k.zsh ]]; then
    sed -i 's/^typeset -g POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=.*/typeset -g POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(os_icon user dir vcs ros2 docker)/' ~/.p10k.zsh
else
    echo "~/.p10k.zsh not found. Run 'p10k configure' to generate it."
fi
```

Installing neovim and NvChad based config
```bash
curl -LO https://github.com/neovim/neovim/releases/latest/download/nvim-linux-x86_64.tar.gz
sudo rm -rf /opt/nvim
sudo tar -C /opt -xzf nvim-linux-x86_64.tar.gz
echo  "export PATH="$PATH:/opt/nvim-linux-x86_64/bin"" >> ~/.zshrc 
git clone https://github.com/anubhav-dogra/nvim_config.git ~/.config/nvim
```
Do this at this end
start `zsh` as well `nvim` to configure at the end. 

### Troubleshooting
```bash
# to set up clang-format in nvim if :MasonInstall clang-format fails:
ln -sf /usr/bin/clang-format ~/.local/share/nvim/mason/bin/clang-format                                 INT
mkdir -p ~/.local/share/nvim/mason/packages/clang-format
touch ~/.local/share/nvim/mason/packages/clang-format/MASON
echo "/usr/bin/clang-format" > ~/.local/share/nvim/mason/packages/clang-format/exec
chmod +x ~/.local/share/nvim/mason/packages/clang-format/exec
```

