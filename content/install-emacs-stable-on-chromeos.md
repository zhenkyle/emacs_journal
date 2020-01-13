+++
title = "Install Emacs stable release on Chrome OS"
date = 2020-01-11T15:00:00Z
+++

What I want is to install the stable version of Emacs on my ChromeBook.The most recent stable version of Emacs is 26.3 now, the most recent version of Chrome OS is 79 now, recent Debian version on Chrome OS 79's Linux enviroment is Strech now.

Install Emacs stable release on Arch Linux is a piece of cake, because Arch linux is a rolling release, you are always up to update.
Install Emacs on Debian/Ubuntu unstable is also easy, there are lots of prebuild newer version packages you can install directliy. However, As Chrome OS 79, the Crostini Linux enviroment is still at `stretch` , the `oldstable` release, install stable release of Emacs on Chrome OS require some extra work.

I spend some time searching for prebuilt stable Emacs (26.3) on Debian oldstable (stretch) on EmacsWiki and Debian sites without lucky, so that means I have to build my Emacs 26.3 myself. There are 3 ways to do this, orderd by recommendations priority.

1. use Debian backport method if the version of software required is in newer version of Debian
    Debian Wiki says this way won't mess up with your package system.

2. use Ubuntu PPA port to Debian method if the version of required is in Ubuntu PPA
3. build directly from sources

Because Emacs 26.3, which is what I needed, is on Debian unstable (sid), so I decided to do a Simple Backport Creation, following this [Guide][1]. After some tweak, I built and installed it with success, in case I will needed to do this again, there some gotcha to be remembered.

1. The `rmadison` command is from `packaging-dev`, you can use it to check which version is available in Debian archive.

1. Before started, uninstall all packages whose name begin with `emacs` and `emacsen` witch `apt purge`\, if you install old version of emacs before.

2. In order to download emacs source form `sid`, you need to add these lines to your `source.list`
    ```
    deb http://deb.debian.org/debian sid main non-free
    deb-src http://deb.debian.org/debian sid main non-free
    ```
    Only add the second line will not will. Then do
    ```
    apt update
    ```
    And then download source with 
    ```
    apt source -t sid emacs
    ```
    After that and before building, delete these lines form your `source.list` and do `apt update` again. This is important, or else you will build your emacs on wrong debian version. Remember we want to build Emacs on Strech version.
    
3. `fakeroot debian/rules binary` require a lot time, it can be safely skipped.

4. In my enviroment, I need `emacsen-common` package to sucessful install `emacs`, and also need `emacs-common-non-dfsg` for Emacs Info document, which is from `non-free` channel.

5. To install a deb file under current path, you need to prefix it with `./`

6. I need to specify all deb files in order to successful install, which is
```
apt install ./emacs_*_*.deb ./emacs-common_*_*.deb \
./emacs-bin-common_*_*.deb ./emacs-gtk_*_*.deb
```


7. Backup these deb files to some place, you can reinstall it someday without rebuild

8. In order to make text bigger, add `sommeiler -X --dpi=175` to `/usr/share/application/emacs.desktop`'s `Exe` section.

9. In order to see all fonts in Emacs Hello file with `C-h h`, I need to install these fonts
    ```
    apt install -t stretch-backport fonts-noto fonts-noto-cjk
    ```
	Note: strech-backport channel's fonts is newer than strech channel's.


After all these steps, I can happily play with emacs stable release on my ChromeBook now :-)

[1]: https://wiki.debian.org/SimpleBackportCreation

