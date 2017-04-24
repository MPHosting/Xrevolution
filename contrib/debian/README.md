
Debian
====================
This directory contains files used to package xrevd/xrev-qt
for Debian-based Linux systems. If you compile xrevd/xrev-qt yourself, there are some useful files here.

## xrev: URI support ##


xrev-qt.desktop  (Gnome / Open Desktop)
To install:

	sudo desktop-file-install xrev-qt.desktop
	sudo update-desktop-database

If you build yourself, you will either need to modify the paths in
the .desktop file or copy or symlink your xrev-qt binary to `/usr/bin`
and the `../../share/pixmaps/xrev128.png` to `/usr/share/pixmaps`

xrev-qt.protocol (KDE)

