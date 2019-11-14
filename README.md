# Overwiew

i3expo is an simple and straightforward way to get a visual impression of all your
current virtual desktops that many compositing window managers use.  It's not a
very powerful approach, but a very intuitive one and especially fits workflows
that use lots of temporary windows or those in which the workspaces are mentally
arranged in a grid.

i3expo emulates that function within the limitations of a non-compositing window
manager. By listening to the IPC, it takes a screenshot whenever a window event
occurrs. Thanks to an extremely fast C library, this produces negligible
overhead in normal operation and allows the script to remember what state you
left a workspace in.

The script is run as a background process and reacts to signals in order to open
its UI in which you get an overview of the known state of your workspaces and
can select another with the mouse or keyboard.

This is based on the work of David Reis, found on [Gitlab](https://gitlab.com/d.reis/i3expo)

Example output:
![Sample](img/ui.png)

# Installation

## Instructions for Arch Linux:
Install dependencies with pipman:
```
pipman -S timing
pipman -S pyxdg
```

Clone, build and install package
```
curl https://raw.githubusercontent.com/mihalea/i3expo/master/PKGBUILD -o PKGBUILD
makepkg -csi
```


## Manual installation

Clone, build and install
```
git clone https://github.com/mihalea/i3expo
cd i3expo
python setup.py install
```

Compile `prtscn.c`  and copy files to `/usr/share/i3expo`:

```
gcc -shared -O3 -Wall -fPIC -Wl,-soname,prtscn -o prtscn.so prtscn.c -lX11
mkdir /usr/share/i3expo
cp defaultconfig /usr/share/i3expo/defaultconfig
cp prtscn.so /usr/share/i3expo/prtscn.so
```
# Usage



A default config can be copied to `~/.config/i3expo/config` by running `i3expod --copy-config`

For the other options, `None` or invalid values will usually
(when `ConfigParser` throws a `ValueError`) be interpreted as "use the default".
Colors can be specified by using their PyGame names or in #fff or #ffffff hex.

Use `i3expo -s` to show the i3expo UI, or `i3expo -u` to reload the config file.

Navigate the UI with the mouse or with they keyboard using the arrow
keys, Return and Escape.

# Limitations

Since it works by taking screenshots, the application cannot know workspaces it
hasn't seen yet. Furthermore, the updates are less continuous than you might be
used to if you're coming from a compositing WM where they can happen live and in
the background.

# Credit

Stackoverflow user JHolta for the screenshot library to be found in this thread:
https://stackoverflow.com/questions/69645/take-a-screenshot-via-a-python-script-linux
