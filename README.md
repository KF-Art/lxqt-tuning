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
  
Debian and Ubuntu:

    # apt update && apt install qt5-style-kvantum{,l10n}
  
Fedora:

    # dnf install kvantum
    
 ## Install Graphite Kvantum theme
 
 I will be using Vinceliuice's Graphite themes, but you can choose any that you want.
 
    git -C /tmp clone https://github.com/vinceliuice/Graphite-kde-theme
    cp -r /tmp/Graphite-kde-theme/Kvantum/Graphite $HOME/.config/Kvantum
    
 This theme is tricky, because if we want another color scheme than the default, it must be changed manually. It is sufficient to use any "find & replace" tool, but we are using Sed via CLI. Also, I'm assuming that the dark variant is the chosen one.
    
    # Change to blackness color scheme.
    sed -i 's/#2c2c2c/#0f0f0f/g' $HOME/.config/Kvantum/Graphite/GraphiteDark.{kvconfig,svg}
    
    # Accent color (optional)
    # Replace the #4DB6AC (Teal) accent color by the one you prefer.
    sed -i 's/#e0e0e0/#4DB6AC/g' $HOME/.config/Kvantum/Graphite/GraphiteDark.svg
    
    # Only do this if some menus text look weird with the new accent color.
    sed -i 's/text.focus.color=#dfdfdf/text.focus.color=white/g' $HOME/.config/Kvantum/Graphite/GraphiteDark.kvconfig
   
