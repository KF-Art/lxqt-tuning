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

# Lockscreen

LXQt by default does not provides a lockscreen service, using instead <code>xscreensaver</code> (which is ugly for me). We will be using Betterlockscreen, which uses i3lock-color. For the moment I will only provide Void, OpenSUSE, Arch and FreeBSD installation steps. The rest of distros will come in the future.

## Install betterlockscreen

### Void Linux

    # xbps-install -S betterlockscreen

### Garuda and every Arch based distro with Chaotic AUR

    # pacman -S betterlockscreen

### Arch and derivatives (using Yay in this example)

    # yay -S betterlockscreen

### OpenSUSE
We will need to "manual" install Betterlockscreen, as it's not in the repositories. The first thing we need is to install <code>opi</code> (if not installed already), which allows us to install OBS software.

    # zypper refresh && zypper in opi

Proceed installing i3lock-color:

    $ opi i3lock-color

Install runtime dependencies:

    # zypper in ImageMagick xdpyinfo feh bc xrandr

Clone repository:

    $ git -C /tmp clone https://github.com/betterlockscreen/betterlockscreen

User install:

    $ /tmp/betterlockscreen/install.sh user

System install:

    # /tmp/betterlockscreen/install.sh system

### FreeBSD

Install runtime dependencies:

    # pkg install ImageMagick7 xdpyinfo feh i3lock-color xrandr

Clone repository:

    $ git -C /tmp clone https://github.com/betterlockscreen/betterlockscreen

User install:

    $ /tmp/betterlockscreen/install.sh user

System install:

    # /tmp/betterlockscreen/install.sh system

## Configure lockscreen background

Before we can use our new lockscreen, we need to set up a background:

    betterlockscreen -u /path/to/your/wallpaper.png

## Set keyboard shortcut

Now configure a shortcut to easily lock your screen. Go to Preferences -> LXQt Settings -> Keyboard Shortcuts, add a new one and set the command <code>betterlockscreen -l</code>. This also can be done at <code>~/.config/lxqt/globalkeyshortcuts.conf</code>. This example uses Super + L (requires restart LXQt):

    [Meta%2BL.40]
    Comment=Lock the screen
    Enabled=true
    Exec=betterlockscreen, -l

# Autolock and suspend

As you may noticed, even installing a lockscreen manager, it will not lock automatically. To do this, we will use <code>xidlehook</code>, which detects keyboard and mouse inactivity and then runs a desired command. XAutolock also exists, but it has the disadvantage of running the command even if we are watching videos, for example.

## Install Xidlehook

### Void Linux

Xidlehook is not at the repositories, but there is PR template which I used to build the package and upload it to GitHub. Also, there is a template available if you need to rebuild and/or update the package. Get your correspondant package for your architecture and libc. For this example I will use the x86_64 (glibc) package. All builds are <a href="https://github.com/KF-Art/xidlehook-void/releases">here</a>.

    $ wget https://github.com/KF-Art/xidlehook-void/releases/download/v0.10.0_1/xidlehook-0.10.0_1.x86_64.xbps

Next, index the new downloaded package and install it.

    $ xbps-rindex -a *.xbps
    # xbps-install -R . xidlehook
    
### Arch Linux and derivatives

If you use an Arch based distribution, then you are lucky. The package is already at AUR. For this example I will be using Yay, but feel free to use any AUR helper.

    $ yay -S xidlehook

## Build Xidlehook on distributions where is not available

From this point, all distributions require to manually build Xidlehook.

### OpenSUSE

First, install build dependencies:

    # zypper in libxcb-devel libXss-devel libpulse0 pkgconf-pkg-config rust cargo

### FreeBSD

Install build dependencies:

    # pkg install libxcb libXScrnSaver pulseaudio pkgconf devel/cargo

### Build

Build Xidlehook:

    $ cargo install xidlehook --bins

This will create two binaries at <code>~/.cargo/bin</code>. You can add this location to PATH, move them to another home location, or move them to <code>/usr/local/bin/</code> to use it at system level. In this case we will do the last one.

    $ cd $HOME/.cargo/bin/
    # cp ./* /usr/local/bin

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

If you find that the panel does not display correctly, create this script. I recommend to save it at <code>~/scripts</code> (you will need to install <code>psmisc</code> if your distro does not have it already):

    #!/bin/sh

    # ~/scripts/wait-panel.sh
    killall -q fluxbox
    sleep 1; fluxbox &

Make it executable:

    chmod u+x $HOME/scripts/wait-panel.sh

Then add an autostart entry at Preferences -> LXQt Settings -> Session Settings -> Autostart, and choose your recently created script, marking the "wait for tray" option. Alternatively, you can create the entry manually:
    
    # $HOME/.config/autostart/wait-panel.desktop
    [Desktop Entry]
    Exec=~/scripts/wait-panel.sh
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

### Panel and Desktop integration

To integrate well the panel and PCManFM-Qt's Desktop, add this to <code>~/.fluxbox/apps</code>:

    [app] (name=LXQt Panel) (class=lxqt-panel)
        [Layer]       {4}
    [end]

    [app] (class=pcmanfm-qt) (@_NET_WM_WINDOW_TYPE=_NET_WM_WINDOW_TYPE_DESKTOP)
        [layer]       {12}
    [end]


### Manual Tiling

As I said before, the main reason why I use LXQt with Fluxbox, is the ability to easily configure the manual tiling. With this, we will be able to tile or snap our windows just pressing Super + Arrows or Numeric Pad. Paste this at <code>~/.fluxbox/keys</code>:

    ### MANUAL TILING ###
    
    # Move with Super + Arrows:
    Mod4 Up  :MacroCmd {ResizeTo 100% 50%} {MoveTo 0 0 Top}
    Mod4 Down :MacroCmd {ResizeTo 100% 50%} {MoveTo 0 0 Bottom}
    Mod4 Left  :MacroCmd {ResizeTo 50% 100%} {MoveTo 0 0 Left}
    Mod4 Right :MacroCmd {ResizeTo 50% 100%} {MoveTo 0 0 Right}

    # Reduce size and center:
    Mod4 KP_5 :MacroCmd {ResizeTo 60% 70%} {MoveTo 0 0 Center}

    # Simple cross tiling, move to corners:
    Mod4 KP_7  :MacroCmd {ResizeTo 50% 50%} {MoveTo 0 0 TopLeft}
    Mod4 KP_9 :MacroCmd {ResizeTo 50% 50%} {MoveTo 0 0 TopRight}
    Mod4 KP_1  :MacroCmd {ResizeTo 50% 50%} {MoveTo 0 0 BottomLeft}
    Mod4 KP_3 :MacroCmd {ResizeTo 50% 50%} {MoveTo 0 0 BottomRight}

    # Move to the center of every border:
    Mod4 KP_8  :MacroCmd {ResizeTo 50% 50%} {MoveTo 0 0 Top}
    Mod4 KP_6 :MacroCmd {ResizeTo 50% 50%} {MoveTo 0 0 Right}
    Mod4 KP_4  :MacroCmd {ResizeTo 50% 50%} {MoveTo 0 0 Left}
    Mod4 KP_2 :MacroCmd {ResizeTo 50% 50%} {MoveTo 0 0 Bottom}

### Workspace management (optional)

If like me, you usually work with a lot of workspaces, then I recommend you to configure them also. You can leave the defaults, or configure your own shortcuts at <code>~/.fluxbox/keys</code>. This is an example of mines:

    # change to a specific workspace
    Alt 1 :Workspace 1
    Alt 2 :Workspace 2
    Alt 3 :Workspace 3
    Alt 4 :Workspace 4
    Alt 5 :Workspace 5
    Alt 6 :Workspace 6
    Alt 7 :Workspace 7
    Alt 8 :Workspace 8
    Alt 9 :Workspace 9
    Alt 0 :Workspace 10

    # send the current window to a specific workspace
    Alt Shift 1 :SendToWorkspace 1
    Alt Shift 2 :SendToWorkspace 2
    Alt Shift 3 :SendToWorkspace 3
    Alt Shift 4 :SendToWorkspace 4
    Alt Shift 5 :SendToWorkspace 5
    Alt Shift 6 :SendToWorkspace 6
    Alt Shift 7 :SendToWorkspace 7
    Alt Shift 8 :SendToWorkspace 8
    Alt Shift 9 :SendToWorkspace 9
    Alt Shift 0 :SendToWorkspace 10

Also, if you need more or less workspaces, define them at <code>~/.fluxbox/init</code> (replace the names by the ones you prefer):

    session.screen0.workspaces:	5
    session.screen0.workspaceNames:	1,2,3,4,5,6,7,8,9,10,
