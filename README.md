# Setup HyperJS + Oh My Zsh on WSL2 with Personal Preferences

This guide helps you set up HyperJS and Oh My Zsh on Windows Subsystem for Linux 2 (WSL2) with custom configurations.

## Prerequisites

- **Windows 10 Version 1903 or higher**, or **Windows 11**.
- **Administrator privileges** on your Windows system.

## Steps

### 1. Enable WSL2 and Virtual Machine Platform

Open Command Prompt as Administrator and run:

```sh
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

Restart your computer.

### 2. Install Linux Kernel Update Package

Download and install the Linux kernel update package from [this link](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi).

### 3. (Optional) Install Docker

If you want Docker, download Docker Desktop from [this link](https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe?utm_source=docker&utm_medium=webreferral&utm_campaign=dd-smartbutton&utm_location=module&_gl=1*hp8qi9*_gcl_au*MTA2OTIxMDc4OC4xNzIzMzIwODk0*_ga*MTA5NDcxMDEzNy4xNzIzMzIwODk0*_ga_XJWPQMJYHQ*MTcyMzMyMDg5NC4xLjEuMTcyMzMyMDkxNi4zOC4wLjA).

### 4. Set WSL Default Version to 2

Open Command Prompt or PowerShell and run:

```sh
wsl --set-default-version 2
```

### 5. Install Ubuntu from Microsoft Store

1. Open Microsoft Store and search for "Ubuntu".
2. Install your preferred version (e.g., Ubuntu 22.04 LTS).

### 6. Configure Ubuntu

1. Launch Ubuntu from the Start menu.
2. Create a new user and password.

   **Optional:** To avoid password prompts for `sudo` commands, edit the sudoers file:

   ```sh
   sudo nano /etc/sudoers
   ```

   Add the following line:

   ```
   yourusername ALL=(ALL:ALL) NOPASSWD:ALL
   ```

   Save and exit (Ctrl + O, Enter, Ctrl + X).

3. Update and upgrade Ubuntu:

   ```sh
   sudo apt update
   sudo apt upgrade
   ```

### 7. Install Oh My Zsh

1. Install Zsh and Powerline fonts:

   ```sh
   sudo apt install zsh
   sudo apt install powerline fonts-powerline
   ```

2. Set Zsh as the default shell:

   ```sh
   chsh -s /bin/zsh
   ```
   Then restart your terminal
   If prompted to select a configuration file, press `q`.

3. Install Oh My Zsh:

   ```sh
   sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
   ```

4. Restart the terminal.

### 8. Configure Oh My Zsh Plugins

**Syntax Highlighting:**

1. Install the plugin:

   ```sh
   git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
   ```

2. Edit `~/.zshrc` and add `zsh-syntax-highlighting` to the plugins list:

   ```sh
   plugins=( [plugins...] zsh-syntax-highlighting)
   ```

3. Restart the terminal.

**Auto Suggestions:**

1. Install the plugin:

   ```sh
   git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
   ```

2. Edit `~/.zshrc` and add `zsh-autosuggestions` to the plugins list:

   ```sh
   plugins=( [other plugins...] zsh-autosuggestions)
   ```

3. Restart the terminal.

**Spaceship Prompt:**

1. Install Spaceship prompt:

   ```sh
   git clone https://github.com/spaceship-prompt/spaceship-prompt.git "$ZSH_CUSTOM/themes/spaceship-prompt" --depth=1
   ```

2. Create a symlink:

   ```sh
   ln -s "$ZSH_CUSTOM/themes/spaceship-prompt/spaceship.zsh-theme" "$ZSH_CUSTOM/themes/spaceship.zsh-theme"
   ```

3. Edit `~/.zshrc` to set Spaceship as the theme:

   ```sh
   ZSH_THEME="spaceship"
   ```

4. Add custom Spaceship settings to `~/.zshrc` under the #User settings section:

   ```sh
   LS_COLORS=$LS_COLORS:'ow=01;34:' ; export LS_COLORS

   SPACESHIP_PROMPT_ORDER=(
     user          # Username section
     dir           # Current directory section
     host          # Hostname section
     git           # Git section (git_branch + git_status)
     hg            # Mercurial section (hg_branch  + hg_status)
     exec_time     # Execution time
     line_sep      # Line break
     jobs          # Background jobs indicator
     exit_code     # Exit code section
     char          # Prompt character
   )

   SPACESHIP_USER_SHOW="always" # Shows System user name before directory name

   SPACESHIP_PROMPT_ADD_NEWLINE=false
   # SPACESHIP_PROMPT_SEPARATE_LINE=false # Make the prompt span across two lines
   # SPACESHIP_DIR_TRUNC=1 # Shows only the last directory folder name

   SPACESHIP_CHAR_SYMBOL_SUCCESS='❯'
   SPACESHIP_CHAR_SYMBOL_FAILURE='❯'
   SPACESHIP_CHAR_SUFFIX=" "
   ```

5. Restart the terminal.

### 9. Install and Configure Hyper Terminal

1. Download and install Hyper from [their website](https://hyper.is/).

2. Open Hyper and install the following plugins:

   ```sh
   hyper install hyper-custom-controls
   hyper install hyper-omni-theme
   hyper install hyperborder
   ```

3. Modify Hyper's configuration:

   - Open Hyper's settings (`Ctrl + ,`).
   - Update `shell` and `shellArgs`:

     ```json
     shell: 'wsl.exe',
     shellArgs: ['-d', 'Ubuntu-22.04'],
     ```

   - Set `showHamburgerMenu` to `false`:

     ```json
     showHamburgerMenu: false
     ```

4. Save the configuration and restart Hyper.

## Enjoy Your Custom Terminal

You now have a stylish and functional terminal setup with HyperJS and Oh My Zsh on WSL2. Enjoy the enhanced terminal experience!

Feel free to adjust configurations according to your preferences. For additional support, refer to the documentation of each tool or their respective communities.
