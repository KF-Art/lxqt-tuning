# lxqt-tuning
Personal tuning for the LXQt desktop to make it more beautiful.

# Overview
LXQt desktop is relatively easy to tune up, but for some reason a lot of people think that is horrible and cannot be customized. Today I'm here to prove that is not true. To summarize, we will use Kvantum, <code>picom-jonaburg-fix</code>, <code>xidlehook</code>, Graphite themes, Reversal icons, Roboto fonts and Betterlockscreen.

# Desktop themes
The first thing we'll do is to install a well-looking Kvantum theme. First you will need, obviously, to install Kvantum.

## Install Kvantum

Void Linux:

    # xbps-install -S kvantum
    
Arch Linux and Manjaro:

    # pacman -S kvantum-qt5
    
FreeBSD:

    # pkg install kvantum-qt5
  
OpenSUSE:

    # zypper in kvantum-manager{,lang}
  
Debian and Ubuntu 20.04+:

    # apt update && apt install qt5-style-kvantum{,-l10n}
    
Ubuntu 18.04 and previous:
    
    # add-apt-repository ppa:papirus/papirus
    # apt update && apt install qt5-style-kvantum{,-l10n}
  
Fedora:

    # dnf install kvantum
    
 ## Install Graphite Kvantum theme
 
 I will be using Vinceliuice's Graphite themes, but you can choose any that you want.
 
    git -C /tmp clone https://github.com/vinceliuice/Graphite-kde-theme
    cp -r /tmp/Graphite-kde-theme/Kvantum $HOME/.config/Kvantum
    
 Open Kvantum Manager and select our new installed theme. Also, you can do it via CLI (if the file already exists):
 
    sed -i 's/theme=/#theme=/g' $HOME/.config/Kvantum/kvantum.kvconfig
    echo "theme=GraphiteDark" | tee -a $HOME/.config/Kvantum/kvantum.kvconfig
    
 Now go to Preferences -> Appearance -> Qt Style and change it to <code>kvantum-dark</code>. Alternatively, you can change it at <code>~/.config/lxqt/lxqt.conf</code> modifying these lines (you will need to restart LXQt):
 
    [Qt]
    style=kvantum-dark
    
    [General]
    theme=system
    
  ### Change color scheme (optional)
    
 This theme is tricky, because if we want another color scheme than the default, it must be changed manually. It is sufficient to use any "find & replace" tool, but we are using Sed via CLI. Also, I'm assuming that the dark variant is the chosen one.
    
    # Change to blackness color scheme.
    sed -i 's/#2c2c2c/#0f0f0f/g' $HOME/.config/Kvantum/Graphite/GraphiteDark.{kvconfig,svg}
    sed -i 's/#3c3c3c/#0f0f0f/g' $HOME/.config/Kvantum/Graphite/GraphiteDark.svg
    
    # Accent color (optional)
    # Replace the #4DB6AC (Teal) accent color by the one you prefer.
    sed -i 's/#e0e0e0/#4DB6AC/g' $HOME/.config/Kvantum/Graphite/GraphiteDark.svg
    
    # Only do this if some menus text look weird with the new accent color.
    sed -i 's/text.focus.color=#dfdfdf/text.focus.color=white/g' $HOME/.config/Kvantum/Graphite/GraphiteDark.kvconfig

## Install Graphite GTK theme

In order to preserve the desktop consistency, we'll also be using the GTK variant of Graphite. I'm choosing the blackness version too. Change the theme color scheme by the one you prefer or use <code>all</code> to install all of them. The <code>rimless</code> parameter is to avoid the color border in apps like Firefox.

    git -C /tmp clone https://github.com/vinceliuice/Graphite-gtk-theme
    cd /tmp/Graphite-gtk-theme
    ./install.sh --theme teal --tweaks black rimless -d $HOME/.local/share/themes
    
Now we need to go to Preferences -> LXQt Settings -> Appearance, check the "Set GTK themes" option and select the recently installed theme.

# Icon theme

There is a lot of beautiful icon themes, but I will focus on two: Reversal and Tela. Feel free to install any icon theme that you want.

## Reversal icon theme

    git -C /tmp clone https://github.com/yeyushengfan258/Reversal-icon-theme
    cd /tmp/Reversal-icon-theme
    ./install.sh green # by default install all variants

## Tela icon theme

    git -C /tmp clone https://github.com/vinceliuice/Tela-icon-theme
    cd /tmp/Tela-icon-theme
    ./install.sh manjaro -c # use -a to install all variants


