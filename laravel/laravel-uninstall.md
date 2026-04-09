**NOTE:** Tested on a system with Linux Mint.

## Uninstall Node.js
```
rm -rf "$HOME/.nvm"

nano ~/.bashrc
```
Remove anything similar to the following three lines:

- `export NVM_DIR="$HOME/.nvm"`
- `[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"`
- `[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"`
```
source ~/.bashrc
```

## Uninstall raw PHP and Composer 
**NOTE:** Ignore if PHP, Composer and Laravel installer wasnt from [PHP NEW](https://php.new/).

```
# to remove php
sudo apt purge php php-curl php-dom php-mbstring php-mysql php-sqlite3 php-xml php-zip unzip
sudo apt autoremove --purge

# to remove composer binary
sudo rm /usr/local/bin/composer

# to remove global composer packages (i.e. laravel)
rm -rf ~/.config/composer
rm -rf ~/.composer # for older systems

nano ~/.bashrc
```
Remove anything similar to the following line:
- `export PATH="$HOME/.config/composer/vendor/bin:$PATH"`

```
source ~/.bashrc

# to remove composer cache
rm -rf ~/.cache/composer
```

## Uninstall [PHP NEW](https://php.new/)

### Official script
```
~/.config/herd-lite/bin/uninstall_herd_lite
```

### Manual approach
```
rm -rf ~/.config/herd-lite
```

Edit the following files according to the next instructions
```
nano ~/.bashrc
nano ~/.bash_profile
nano ~/.profile
```

Remove any lines containing:
- `.config/herd-lite/bin`
- `PHP_INI_SCAN_DIR`

Specifically, remove lines like:
- `export PATH="$HOME/.config/herd-lite/bin:$PATH"`
- `export PHP_INI_SCAN_DIR="$HOME/.config/herd-lite/bin:$PHP_INI_SCAN_DIR"`

```
source ~/.bashrc
```
