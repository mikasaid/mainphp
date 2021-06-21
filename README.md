:octocat: Hi there! Thanks for visiting!
This is my personal configuration for my favorite openbox window manager and some applications too.I hope you understand everything here. 😉
Here are some details about my setup

Window Manager • Openbox 🎨 4 changable mode!
Shell • Zsh 🐚 with oh my zsh framework! optional
Terminal • URxvt, Termite available
Openbox Menu • OBmenu-generator
Panel • Tint2 🍧 material icon font!
Compositor • Picom 🍩 rounded corners!
Notify Daemon • Dunst 🍃 minimalism!
Application Launcher • Rofi 🚀 blazing fast!
File Manager • Thunar 🔖 customized sidebar & icon!
Music Player • Mpd + Ncmpcpp, Spotify 🎑 riced!
GUI & CLI IDE/Text Editor • Geany, Neovim
🎁 Changelogs
normal
v3.0
v3.1
v3.2 latest
🌸 Setup
This is step-by-step how to install these .files for automatic setup OpenboxWM custom environment.

Introduction of Linux Rice
Please read this and/or this.
Installation (dependencies)
Customize your choice about dependencies below, this is my complete setup as I use single OS, single OpenboxWM with my preference utility application. In fact, what is in the column is a minimal recommendation.

Detailed environment
Please refer to wiki/Detailed-Environment.

Warning!
This configuration is highly dependent to bash, sed, and coreutils.
Assume that you are using sudo or doas. Installation feels like LFS? 😆

Attention!

Rofi must be above version 1.6.x, so for Debian-based you may need to compile manually from source. - issue
If your Linux distribution repository only contains pure rxvt-unicode without patch for wide unicode and others, an example is on Arch Linux which provides pure rxvt-unicode and rxvt-unicode-patched version in the AUR repository. The problem is that the urxvt in the AUR hasn't been updated yet, and the link for the urxvt source-code for that version has been removed from the original link. Therefore, use rxvt-unicode from the main repo of each linux distribution that you use. Debian is different (already patched). - issue
You may want to use polkit-gnome instead of lxsession / lxpolkit. Because, currently the lxsession in Gentoo/Linux is really bad (dependency hell).
Debian & Ubuntu (and all based distributions)
sudo apt install rsync python psmisc x11-utils imagemagick ffmpeg wireless-tools openbox pulseaudio
alsa-utils brightnessctl nitrogen dunst tint2 gsimplecal rofi qt5-style-plugins lxpolkit xautolock
rxvt-unicode xclip scrot thunar thunar-archive-plugin thunar-volman ffmpegthumbnailer tumbler
viewnior mpv mpd mpc ncmpcpp pavucontrol parcellite neofetch w3m w3m-img htop playerctl xsettingsd
oh-my-zsh & plugins optional
picom
obmenu-generator

Arch Linux (and all based distributions)
Make sure your AUR Helper is yay or paru.

yay -S rsync python psmisc xorg-xprop xorg-xwininfo imagemagick ffmpeg wireless_tools openbox 

pulseaudio pulseaudio-alsa alsa-utils brightnessctl nitrogen dunst tint2 gsimplecal rofi 

qt5-styleplugins lxsession xautolock rxvt-unicode-patched xclip scrot thunar thunar-archive-plugin 

thunar-volman ffmpegthumbnailer tumbler viewnior mpv mpd mpc ncmpcpp pavucontrol parcellite 

neofetch w3m htop picom-git obmenu-generator gtk2-perl playerctl xsettingsd
oh-my-zsh & plugins optional

Another Linux Distribution

Optional: betterdiscord, geany + geany plugins, gimp, nano + nano syntax highlighting, neovim, spotify, termite, xfce4-power-manager.

Installation (dotfiles)
Are all directories required? 🤔
Please refer to wiki/Detailed-Environment.

Most of .files
You can clone or download as a archive. After that put all files in the dotfiles folder to user's home directory.

Assume you are cloning in the /Documents directory for example.

cd /Documents/ && git clone https://github.com/owl4ce/dotfiles.git
I recommend with rsync.

rsync -avxHAXP --exclude '.git*' --exclude 'LICENSE' --exclude '*.md' dotfiles/ ~/
Explanation

Options	Function
-a	all files, with permissions, etc..
-v	verbose, mention files
-x	stay on one file system
-H	preserve hard links (not included with -a)
-A	preserve ACLs/permissions (not included with -a)
-X	preserve extended attributes (not included with -a)
-P	show progress
--exclude	exclude files matching PATTERN
Differences

cp is for duplicating stuff and by default only ensures files have unique full path names.
rsync is for synchronising stuff and uses the size and timestamp of files to decide if they should be replaced. It has many more options and capabilities than cp.
I recommend to not deleting dotfiles folder after cloning from this repository, because to make upgrades easier. Read the update section.

Icons
Note
pushd is same as cd, but can return back to the first directory (checkpoint).

pushd ~/.icons/ &&
    tar -Jxvf Papirus-Custom.tar.xz && tar -Jxvf Papirus-Dark-Custom.tar.xz &&
    sudo ln -vs ~/.icons/Papirus-Custom /usr/share/icons/Papirus-Custom &&
    sudo ln -vs ~/.icons/Papirus-Dark-Custom /usr/share/icons/Papirus-Dark-Custom &&
popd
Why I need to link icons to user system resources? 🤔
That's needed by dunst in order to display most of icon from notification that spawned by application.

Refresh Font Cache
fc-cache -rv
Root Privileges with SUID
brightnessctl
others if needed
For brightnessctl, I recommend adding users to video group.

sudo chmod u+s $(command -v brightnessctl)
The step you are waiting for
The final step is login into openbox-session, basically login from display manager you use such as lightdm, gdm, etc.

Note
Make sure the sh symlinks to bash, as it's very dependent on bash.

[ "$(readlink /bin/sh)" != "bash" ] && sudo ln -vfs bash /bin/sh
If you are using ~/.xinitrc without display manager, simply add

Systemd Linux Distribution

exec openbox-session
Init-Freedom Linux Distribution

exec dbus-launch --exit-with-session openbox-session
Then you can proceed to user's configuration. Explore!

Additional
Suggested replacement commands

ls ➜ exa
~/.zshrc

...
134 alias ls="exa -lgh --icons --group-directories-first"
135 alias la="exa -lgha --icons --group-directories-first"

...

cat ➜ bat
Suggestion for tiling users



I recommend compiling it from source. Then put zentile binary your PATH, for example in ~/.local/bin/

<div class="highlight highlight-source-shell position-relative" data-snippet-clipboard-copy-content="# To run in the background (detached)
zentile &!
To kill (or pkill)
killall zentile
" style="box-sizing: border-box; position: relative !important; margin-bottom: 16px; color: rgb(201, 209, 217); font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji"; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(13, 17, 23); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial;">

# To run in the background (detached)

zentile &!

# To kill (or pkill)

killall zentile

Update
Since I recommend using rsync from start, the easiest way is to list the files that will not be updated to avoid changing personal files with files in this repository. First, update local repository with git repository.

Remember where you cloned this repository.
For example, from the start we assumed that it was in /Documents.

cd /Documents/ &&

pushd dotfiles/ && git pull && popd
Then list the files excluded by rsync (PATTERN). For example,
/Documents/owl4ce_drsyncexc

.git*

LICENSE

*.md

*.joy

BetterDiscord

geany

GIMP

gtk-3.0

config.conf

nvim

autostart

environment

tray

shared

sidebar

termite

Thunar

xfconf

.fonts

.nothing

.mpd

.gtkrc-2.0

.zshrc

.nanorc

.Xresources

.xsettingsd
Use find command to check PATTERN,

find dotfiles/ -iname 'PATTERN'
and whatever the file is. Next, of course is rsync.

rsync -avxHAXP --exclude-from /Documents/owl4ce_drsyncexc dotfiles/ /
User's configuration
SLiM Themes optional

See
Chromium-based Web Browser suggested

See
Spotify - Spicetify Theme suggested

See
Telegram Desktop suggested

See
Capitaine Cursors Theme suggested

See
Touchpad tap-to-click (libinput) optional
/etc/X11/xorg.conf.d/30-touchpad.conf

Section "InputClass"

Identifier "touchpad"

Driver "libinput"

MatchIsTouchpad "on"

Option "Tapping" "on"

Option "TappingButtonMap" "lmr"

EndSection
More information.

User's Preferences required
/.owl4ce_var
Manage all your settings there. I hope all comments there are easy to understand. ^^

User's Tray Icons
/.config/openbox/tray
An example is turning on nm-applet, because by default I don't use it and use networkmanager_dmenu instead.

How about battery indicator?
Because on the tint2 panel I turned off battery status. Alternatively, install xfce4-power-manager and enable system tray icon in xfce4-power-manager-settings.

Remove hashtags for all your needs, then relogin openbox-session.

Warning! Putting a tray here means that when switching Visual Mode, the program will be restarted.

1 #

2 # This tray will restart after switching modes

3 # Please add "&" after command

4 #

5 # ---

6

7 parcellite &

8 #nm-applet &

9 #xfce4-power-manager &
Available Default Apps
/.scripts/default-apps/list

Terminal: urxvt termite
Lockscreen: anything
Music Player: mpd spotify
File Manager: anything
1 terminal="urxvt"

2 lockscreen="slimlock"

3 musicpl="mpd"

4 filemanager="thunar"
Neovim
/.config/nvim/
You know what to do with Vim-plug.

MPD Music Directory
/.mpd/mpd.conf

<div class="highlight highlight-source-haproxy-config position-relative" data-snippet-clipboard-copy-content="...
6 music_directory "~/Music"

...
" style="box-sizing: border-box; position: relative !important; margin-bottom: 16px;">

...

6 music_directory     "~/Music"


...

Ncmpcpp Music Directory
Auto connect with MPD.

How to use ncmpcpp albumart? (URxvt)
It's easy, put album|cover|folder|artwork|front.jp?g|png|gif|bmp into folder with song album. Recommended image size is 500px ( 1:1 ) or more. See keybinds

Audio Server optional
/.config/openbox/autostart

This is optional for Linux distributions that don't use systemd as their init, actually pulseaudio can be triggered from increasing-decreasing audio volume.
QT Themer (env var) optional
/.config/openbox/environment
This is optional if you're having issues like blind text with background from Mechanical Theme (Fleon GTK), as it basically uses plugins (QT5 to GTK2). Remove gtk2 after the equal sign, then relogin openbox-session.

<div class="highlight highlight-source-haproxy-config position-relative" data-snippet-clipboard-copy-content="...
7 # Use qt5-styleplugins for QT Themes
8 export QT_QPA_PLATFORMTHEME=gtk2

...
" style="box-sizing: border-box; position: relative !important; margin-bottom: 16px;">

...

7 # Use qt5-styleplugins for QT Themes

8 export QT_QPA_PLATFORMTHEME=gtk2


...

Neofetch Image
~/.config/neofetch/config.conf

<div class="highlight highlight-source-haproxy-config position-relative" data-snippet-clipboard-copy-content="...
641 # Image Source
642 #
643 # Which image or ascii file to display.
644 #
645 # Default: 'auto'
646 # Values: 'auto', 'ascii', 'wallpaper', '/path/to/img', '/path/to/ascii', '/path/to/dir/'
647 # 'command output (neofetch --ascii "$(fortune | cowsay -W 30)")'
648 # Flag: --source
649 #
650 # NOTE: 'auto' will pick the best image source for whatever image backend is used.
651 # In ascii mode, distro ascii art will be used and in an image mode, your
652 # wallpaper will be used.
653 #image_source="auto"
654 #image_source="${HOME}/.config/neofetch/images/arch.png"
655 #image_source="${HOME}/.config/neofetch/images/arch_dark.png"
656 #image_source="${HOME}/.config/neofetch/images/artix.png"
657 #image_source="${HOME}/.config/neofetch/images/bedrock.png"
658 #image_source="${HOME}/.config/neofetch/images/gentoo.png"
659 #image_source="${HOME}/.config/neofetch/images/gentoo_dark.png"
660 #image_source="${HOME}/.config/neofetch/images/lofi.png"
661 image_source="${HOME}/.config/neofetch/images/sakura.png"
662 #image_source="${HOME}/.config/neofetch/images/ubuntu.png"
663 #image_source="${HOME}/.config/neofetch/images/ubuntu_dark.png"
664 #image_source="${HOME}/.config/neofetch/images/void.png"
665 #image_source="${HOME}/.config/neofetch/images/void_dark.png"

...
" style="box-sizing: border-box; position: relative !important; margin-bottom: 16px;">

...

641 # Image Source

642 #

643 # Which image or ascii file to display.

644 #

645 # Default:  'auto'

646 # Values:   'auto', 'ascii', 'wallpaper', '/path/to/img', '/path/to/ascii', '/path/to/dir/'

647 #           'command output (neofetch --ascii "$(fortune | cowsay -W 30)")'

648 # Flag:     --source

649 #

650 # NOTE: 'auto' will pick the best image source for whatever image backend is used.

651 #       In ascii mode, distro ascii art will be used and in an image mode, your

652 #       wallpaper will be used.

653 #image_source="auto"

654 #image_source="${HOME}/.config/neofetch/images/arch.png"

655 #image_source="${HOME}/.config/neofetch/images/arch_dark.png"

656 #image_source="${HOME}/.config/neofetch/images/artix.png"

657 #image_source="${HOME}/.config/neofetch/images/bedrock.png"

658 #image_source="${HOME}/.config/neofetch/images/gentoo.png"

659 #image_source="${HOME}/.config/neofetch/images/gentoo_dark.png"

660 #image_source="${HOME}/.config/neofetch/images/lofi.png"

661 image_source="${HOME}/.config/neofetch/images/sakura.png"

662 #image_source="${HOME}/.config/neofetch/images/ubuntu.png"

663 #image_source="${HOME}/.config/neofetch/images/ubuntu_dark.png"

664 #image_source="${HOME}/.config/neofetch/images/void.png"

665 #image_source="${HOME}/.config/neofetch/images/void_dark.png"


...
See Images
📝 Notes
Color Scheme

owl4ce.color-scheme

Nord Color Palette compatible


💬
Widget? We don't do that here. My main philosophy in building this is as a minimal replacement for Desktop Environment without any desktop decoration e.g icons and widgets, but it can be adapted to taste of user with an overall theme based on one color palette and can be easily switched between Mechanical-Eyecandy. I admit, the downside is that it relies heavily on the GNU/Linux operating system since bashism is not POSIX-compliant to other shell. Most of the size of this repository is large due to wallpapers, icons, and git caches.Please don't underrate, I've configured them all since April 2020 and have been stuDYING them since October 2019. Awesome open-source. If you support it, star it or make a PR. Or if there is a problem with configuration (please check previous issues if any) you can make an issue here. Also if you want a discussion.Thank you!Feel free to modify.. under GPL-3.0Why openbox? Really a perfect next-gen window manager, easily configurable, and less resources usage.Openbox isn't dead, but completed features.
 



💝 Tip Jar
If you enjoy my dotfiles and would like to show your appreciation, you may want to tip me here. It is never required but always wholeheartedly appreciated.

Thank you from the bottom of my heart! 💗

BTC: 3DrjWyd6Xgv4tKoL56mPtoQX4fL4LbR7zf
ETH: 0x818fC9B82548C1020ed7370DFeb04BCbADc59191
🎊 Credits / Thanks
Inspiration and resources

Elena
Adhi Pambudi
Fikri Omar
Nanda Oktavera
Rizqi Nur Assyaufi
Muktazam Hasbi Ashidiqi
Galih Wisnuaji
Ghani Rafif
Aditya Shakya
?
Knowledge and other resources

Digital Synopsis
Wiki @ Openbox
Pango Markup @ Gnome
Custom Environment @ ArchWiki
Recommended Applications @ Gentoo Wiki
Pure Bash Bible
Stark's Color Scripts
Notify Send (bash)
NetworkManager Dmenu
URxvt Manual
URxvt Resize Font
URxvt Tabbed Extended
Showing Album Cover in Ncmpcpp
Complete List of GitHub Markdown Emoji Markup
Many GNU/Linux and Unix forums.
Contributors

Ekaunt - Better promptmenu

HopeBaron - Termite config

Justin Faber - Rofi matched lines indicator



Made with contributors-img.

Softwares

Geany - The Flyweight IDE
GIMP - GNU Image Manipulation Program
Gpick - Advanced Color Picker
Gucharmap - GNOME Character Map
Themix - GUI Theme Designer
Tint2conf, etc.
Our local linux community Linuxer Desktop Art and @dotfiles_id, also r/unixporn.

© All artist who make icons, illustrations, and wallpapers.

The original source that I found:

Gladient Icons
桜
桜セイバー沖田総司
沖田総司![1](https://user-images.githubusercontent.com/58392246/122732714-c1a2ad00-d2a6-11eb-87f5-70ed92af8971.jpg)
![203545512_858046784833573_3538112098952761558_n](https://user-images.githubusercontent.com/58392246/122732719-c2d3da00-d2a6-11eb-883c-7e7b934a63e1.jpg)
![featured_channel](https://user-images.githubusercontent.com/58392246/122732721-c36c7080-d2a6-11eb-84ee-7350754a92a2.jpg)
![karakter-pecinta-warna-hitam](https://user-images.githubusercontent.com/58392246/122732724-c4050700-d2a6-11eb-8037-6e6c06eed6c7.jpg)
![shRgEdj](https://user-images.githubusercontent.com/58392246/122732725-c4050700-d2a6-11eb-984c-eb82c37d5845.png)
