Odroid U2/3 - Arch Linux - Mali/xorg-server-dsd Patch
=====================================================
This is  fork of gripped's repo odroid-u2-pkgbuilds, i made this to try and update the PKGBUILD's and keep them moving with Arch, the orignal README will be left in the repo for reference, the other libs are still available, i made this repo for cleanliness/order/my own sanity and it only includes packages i am working on.

Most of these packages arent needed any more due to ones provided in the official repo, the problem i run into is odroid-libgl conflicts with mesa-libgl but doesnt provide all the functionality and breaks/crashes alot ! To get around this i copied a PKGBUILD from a pull request for odroid-libgl which removes the conflict of mesa-libgl so they can be installed side by side, you will find that in the odroid-libgl-mali folder.

Install/Build Instructions
==========================
There are 2 methods for installation which i will outline below.

Method 1
--------
Edit your pacman.conf file and add my repo :
```
sudo nano /etc/pacman.conf
```
Then add these lines to the end of the file :
```
[odroidu]
SigLevel = Never
Server = http://odroidxu.leeharris.me.uk/u2
```
Save and exit before then updating pacman :
```
sudo pacman -Syu
```
Then install packages in the normal way :
```
sudo pacman -S odroid-libgl-mali xorg-server-dsd
```
You will need to edit your /etc/xorg.conf, mine has this :
```
# X.Org X server configuration file for xfree86-video-mali

Section "Device"

  Identifier "Mali-Fbdev"

  Driver   "armsoc"

  Option   "fbdev"           "/dev/fb1"

  Option  "DriverName"      "exynos"

EndSection



Section "Screen"

  Identifier   "Mali-Screen"

  Device       "Mali-Fbdev"

  DefaultDepth 24 

EndSection



Section "DRI"

  Mode 0666

EndSection
```
Method 2
--------
To install simply build the package with the `PKGBUILD` and `makepkg -s` and then install the resulting `pkg.tar.xz` file with pacman. The packages i recommend you install are :
```
odroid-libgl-mali           (official repo = odroid-libgl - conflicts with mesa-libgl)
xorg-server-dsd             (official repo = xorg-server)
```
You will also need these packages from the official repos (amongst others) :
```
linux-odroid-u2
xf86-video-armsoc-odroid
xf86-video-fbturbo-git
xf86-video-fbdev
mesa-libgl
```
How to Build/Install
--------------------
Change directory to where you want to clone the repo :
```
$ cd git
```
Then clone the repo :
```
$ git clone https://github.com/hreikin/odroid-arch-pkgbuilds
```
Then change directory into the file you wish to install, for example odroid-libgl-mali :
```
$ cd odroid-libgl-mali
```
Then take a look at the 'PKGBUILD' to check everything is ok with nano before running 'makepkg -s' :
```
$ nano PKGBUILD
$ makepkg -s
```
Once 'makepkg' finishes it will create a 'pkg.tar.xz' file (maybe more than 1!) which can be installed with pacman like so :
```
$ sudo pacman -U odroid-libgl-mali-r4p0-1-armv7h.pkg.tar.xz
$ sudo pacman -U odroid-libgl-mali-r4p0-1-armv7h.pkg.tar.xz
```
Once you have all the files installed you need to edit your '/etc/xorg.conf' mine has :
```
# X.Org X server configuration file for xfree86-video-mali

Section "Device"

  Identifier "Mali-Fbdev"

  Driver   "armsoc"

  Option   "fbdev"           "/dev/fb1"

  Option  "DriverName"      "exynos"

EndSection



Section "Screen"

  Identifier   "Mali-Screen"

  Device       "Mali-Fbdev"

  DefaultDepth 24 

EndSection



Section "DRI"

  Mode 0666

EndSection
```
