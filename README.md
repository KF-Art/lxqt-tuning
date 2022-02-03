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
  
OpenSUSE:

    # zypper refresh && zypper in kvantum-manager{,lang}
  
Debian and Ubuntu 20.04+:

    # apt update && apt install qt5-style-kvantum{,-l10n}
    
Ubuntu 18.04 and previous:
    
    # add-apt-repository ppa:papirus/papirus
    # apt update && apt install qt5-style-kvantum{,-l10n}
  
Fedora:

    # dnf install kvantum

FreeBSD:

    # pkg install kvantum-qt5
    
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
    ./install.sh manjaro # use -a to install all variants

## Apply icon theme

Go to Preferences -> LXQt Settings -> Appearance -> Icons Theme and choose the one you installed. This also can be done manually at <code>~/.config/lxqt/lxqt.conf</code> (Requires restart LXQt):

    [General]
    icon_theme=your_icon_theme

# Install well-looking fonts

It is important to use a pretty font, because it will make our desktop look more beautiful and elegant. 

## UI font

In this case I recommend Roboto, which is on almost all distributions, is well-looking and elegant.

Void Linux:

    # xbps-install -S fonts-roboto-ttf

Arch Linux, Manjaro and derivatives:

    # pacman -S roboto-ttf

OpenSUSE:

    # zypper refresh && zypper in google-roboto-fonts

Debian, Ubuntu and derivatives:

    # apt update && apt install fonts-roboto

Fedora:

    # dnf install google-roboto-fonts

FreeBSD:

    # pkg install fonts-roboto-ttf

## Monospace font

Currently, my favorite monospace font is JetBrains Mono NL. So, we will install it. This process will be universal for all distributions. You can use any font you like, of course.

First, fetch the font itself:

    mkdir /tmp/JetBrains-Mono && cd /tmp/JetBrains-Mono
    wget https://github.com/JetBrains/JetBrainsMono/releases/download/v2.242/JetBrainsMono-2.242.zip
    unzip JetBrainsMono-2.242.zip

Now, the installation path will vary between GNU/Linux and FreeBSD. 

    #GNU/Linux
    sudo cp -r fonts /usr/share

    #FreeBSD
    sudo cp -r fonts /usr/local/share

Finally, update the font cache and list.

    fc-cache -fv; fc-list

## Apply UI font

Go to Preferences -> LXQt Settings -> Appearance -> Font, and select out new installed font at "Font name". Also, adjust the size accordingly to your screen. Do the same process for PCManFM-Qt desktop, doing right click -> Desktop Preferences -> Select font (I recommend to change the wallpaper also).

Alternatively, you can do this at <code>~/.config/lxqt/lxqt.conf</code> and </code>~/.config/pcmanfm-qt/lxqt</code>, respectively (requires restart LXQt):

    # ~/.config/lxqt/lxqt.conf
    [Qt]
    font="Roboto,11,-1,5,50,0,0,0,0,0"


    # ~/.config/pcmanfm-qt/lxqt
    [Desktop]
    Font="Roboto,10,-1,5,50,0,0,0,0,0,Regular"

# Window Manager
The window manager is one of the most important things in our desktop environment, so we must customize it too. The main focus will be the default WM, Openbox; but also I'll include instructions to integrate it with Fluxbox, and maybe in the future, i3wm.

## Openbox

### Install a theme

The chosen theme is Licorice, from Sweet Tastes Themes. We'll make some changes to adapt and integrate with Graphite color scheme, and enable window title (if wanted). First we need to clone the theme repository, and copy it to our home directory.
    
    git -C /tmp clone https://www.opencode.net/ju1464/Sweet_Tastes_Themes.git
    cp -r /tmp/Sweet_Tastes_Themes/Licorice ~/.local/share/themes

Next, we will change the color scheme in order to keep the desktop consistency with our installed theme:

    obtheme=$HOME/.local/share/themes/Licorice/openbox-3/themerc
    sed -i 's/#282828/#0f0f0f/g' $obtheme
    sed -i 's/#464141/#0f0f0f/g' $obtheme
    sed -i 's/window.inactive.label.text.color: #0f0f0f/window.inactive.label.text.color: #ffffff/g' $obtheme
    sed -i 's/window.active.label.text.color: #0f0f0f/window.active.label.text.color: #ffffff/g' $obtheme
    
### Apply theme and change fonts

Go to Preferences -> Openbox Settings, and select the Licorice theme, also go to Fonts section and change them all to Roboto, or your preferred font. This also can be done at <code>~/.config/openbox/rc.xml</code>.

## Fluxbox

It would appear strange use Fluxbox instead of Openbox on LXQt, but is has a lot of potential for our LXQt desktop. Mainly on the point of configuring manual tiling (which I didn't get to work at Openbox). First, of course, install Fluxbox:

Void Linux:

    # xbps-install -S fluxbox

Arch Linux, Manjaro and derivatives:

    # pacman -S fluxbox

OpenSUSE:

    # zypper refresh && zypper in fluxbox

Debian, Ubuntu and derivatives:

    # apt update && apt install fluxbox

FreeBSD:

    # pkg install fluxbox

Once installed, copy the example configuration to your home directory. Commonly, into GNU/Linux distributions is located at <code>/usr/share/fluxbox</code> and into FreeBSD <code>/usr/local/share/fluxbox</code>:

    # GNU/Linux
    cp -r /usr/share/fluxbox $HOME/

    # FreeBSD
    cp -r /usr/local/share/fluxbox

Before we change the window manager at our environment, we must hide the Fluxbox's panel (called toolbar), to avoid conflicts with LXQt's panel:

    echo "session.screen0.toolbar.visible:	false" | tee -a "$HOME/.fluxbox/init"

I recommend to set a shortcut to open Fluxbox configuration and other to restart it, in case you need them (Alt + L and Alt + Shift + R, respectively):

    fluxkeys=$HOME/.fluxbox/keys
    echo "Mod1 L :RootMenu" | tee -a $fluxkeys
    echo "Mod1 Shift R :Restart" | tee -a $fluxkeys

Go to Preferences -> LXQt Settings -> Session Settings and change the window manager to Fluxbox. After that logout. 

### Panel fix

If you find that the panel does not display correctly, then create add an autostart entry at Preferences -> LXQt Settings -> Session Settings -> Autostart (you will need to install <code>psmisc</code> if your distro does not have it already) with the following command: <code>killall -q fluxbox; sleep 1; fluxbox</code>, marking the "wait for tray" option. Alternatively, you can create the entry manually:

    # $HOME/.config/autostart/wait-panel.desktop
    [Desktop Entry]
    Exec=killall -q fluxbox; sleep 1; fluxbox
    Name=Wait for panel
    Type=Application
    Version=1.0
    X-LXQt-Need-Tray=true

This will restart Fluxbox once the panel is fully loaded.

### Install Sierra Dark theme

I made a fork theme which adapts well with Graphite color scheme. First, clone the repository:

    git -C $HOME/.fluxbox/styles/ clone https://github.com/KF-Art/Sierra-Dark-Fluxbox

Now we need to change our current theme. This can be done using our previously defined shortcut (Alt + L), then go to Advanced Settings -> Fluxbox -> User Styles, and select our new theme; or via CLI with Sed:

    fluxconf=$HOME/.fluxbox/init
    sed -i 's/session.styleFile:/#session.styleFile:/g' $fluxconf
    echo "session.styleFile:      ~/.fluxbox/styles/Sierra-Dark-Fluxbox" | tee -a $fluxconf

After that, restart Fluxbox with our previously defined shortcut (Alt + Shift + R) to apply all the changes correctly.
