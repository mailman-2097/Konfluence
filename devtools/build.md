#  Kickstart nvim on Ubuntu WSL

## Constraints
- Snap packages don't work well hence building from source  
- Never override XDG vars

## Setup

```
curl -s https://ohmyposh.dev/install.sh | bash -s
mv 
rm -rf  .local/share/nvim/lazy/
mv ~/.config/nvim ~/.config/nvim_0

sudo apt-get install ninja-build gettext cmake unzip curl

<!-- https://github.com/sadikeey/nvim -->

git clone https://github.com/neovim/neovim.git
cd neovim
git branch -a
git checkout release-0.9
make CMAKE_BUILD_TYPE=Release
sudo make install

git clone https://github.com/nvim-lua/kickstart.nvim.git ~/.config/nvim

```

## Bespoke Tailoring

### init.lua
Modify init.lua.. which is like you index.html

### Customisations

1. Dashboard
1. Debugger

```

```

# LunarVim
```
sudo apt install python3-pip -y
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

LV_BRANCH='release-1.3/neovim-0.9' bash <(curl -s https://raw.githubusercontent.com/LunarVim/LunarVim/release-1.3/neovim-0.9/utils/installer/install.sh)

```

## AWS Azure SSO Tool
```bash
<!-- https://samltool.io/ -->

git clone https://github.com/aws-azure-login/aws-azure-login.git
mkdir ~/.npm-global
npm config set prefix '~/.npm-global'
export PATH=~/.npm-global/bin:$PATH
echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.bash_custom
source ~/.bash_profile

npm install -g aws-azure-login


Tenant Id: 05a0e69a-418a-47c1-9c25-9387261bf991
App Id URI: https://signin.aws.amazon.com/saml
userid: nishad.ks@det.nsw.edu.au

dnf install -y \
alsa-lib.x86_64 \
atk.x86_64 \
cups-libs.x86_64 \
gtk3.x86_64 \
ipa-gothic-fonts \
libXcomposite.x86_64 \
libXcursor.x86_64 \
libXdamage.x86_64 \
libXext.x86_64 \
libXi.x86_64 \
libXrandr.x86_64 \
libXScrnSaver.x86_64 \
libXtst.x86_64 \
pango.x86_64 \
xorg-x11-fonts-100dpi \
xorg-x11-fonts-75dpi \
xorg-x11-fonts-cyrillic \
xorg-x11-fonts-misc \
xorg-x11-fonts-Type1 \
dnf update nss -y

aws-azure-login --configure detnsw

aws-azure-login --profile detnsw


```