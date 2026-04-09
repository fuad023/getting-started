**NOTE:** Tested on a system with Linux Mint.

## Install [VSCodium](https://linuxcapable.com/how-to-install-vscodium-on-linux-mint/)
```
# to import gpg key
curl -fsSL https://gitlab.com/paulcarroty/vscodium-deb-rpm-repo/raw/master/pub.gpg | sudo gpg --dearmor -o /usr/share/keyrings/vscodium-archive-keyring.gpg

# to add repo
cat << EOF | sudo tee /etc/apt/sources.list.d/vscodium.sources
Types: deb
URIs: https://download.vscodium.com/debs
Suites: vscodium
Components: main
Architectures: amd64 arm64
Signed-By: /usr/share/keyrings/vscodium-archive-keyring.gpg
EOF

# to install
sudo apt update
# apt-cache policy codium # ignore
sudo apt install codium
codium --version
```

### Uninstall vscodium [optional]
```
sudo apt purge codium
sudo apt autoremove --purge
sudo rm /etc/apt/sources.list.d/vscodium.sources # vscodium repo
sudo rm /usr/share/keyrings/vscodium-archive-keyring.gpg # gpg key
sudo apt update
rm -rf ~/.config/VSCodium ~/.vscode-oss # user config files
```

## Install Postman
- Goto https://gist.github.com/prrao87/114933c4638a4f77aa3d4b2c5a3b2477
- Follow the procedure

### Uninstall Postman [optional]
```
sudo rm /usr/bin/postman # symlink
sudo rm -rf /opt/Postman # application directory
sudo rm /usr/share/applications/postman.desktop # desktop entry
rm -rf ~/.config/Postman ~/.cache/Postman ~/.local/share/Postman # user config data
```

## Install DBeaver

### Manual
- goto https://dbeaver.io/download/
- download and install the community edition, or

### Terminal-based
```
sudo add-apt-repository ppa:serge-rider/dbeaver-ce
sudo apt update
sudo apt install dbeaver-ce
```

### Uninstall DBeaver [optional]
```
sudo apt purge dbeaver-ce
sudo apt autoremove --purge
# sudo rm /etc/apt/sources.list.d/serge-rider-ubuntu-dbeaver-ce-*.list # does the same as the following command
sudo add-apt-repository --remove ppa:serge-rider/dbeaver-ce
sudo apt update
rm -rf ~/.local/share/DBeaverData ~/.config/DBeaverData # user config files
```

## Install MySQL Workbench
- Goto https://dev.mysql.com/downloads/workbench/
- Select ubuntu linux 24.4 64-bit
- Download NOT the dbgsym one

Open the .deb file using file manager and install it, or

### Use terminal
```
sudo dpkg -i mysql-workbench-community_8.0.46-1ubuntu24.04_amd64.deb
# will throw some dependency missing errors, to fix them

sudo apt --fix-broken install
sudo dpkg -i mysql-workbench-community_8.0.46-1ubuntu24.04_amd64.deb # ran it again
```
