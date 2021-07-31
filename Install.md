# FreeBSD Post Install Config

## Add Primary user

- Create an user and add them to the 'wheel' group
- Login as `root`
- Install `sudo`
- Run `visudo` and uncomment the first `%wheel`

## Install packages offline

```shell
mkdir /dist
mount -t cd9660 /dev/da0 /dist
env REPOS_DIR=/dist/packages/repos pkg install <package-name> # Replace `<package-name>` with the package you want to install.
```

## Install a Desktop Eevironment
- Install `xorg` and  `gnome3` or `x11/kde5` offline
- Install `x11/sddm` if chose `x11/kde5`
- For KDE / GNOME Edit `/etc/fstab` and add `proc   /proc   procfs   rw 0  0`
    

## System Configuration
- Edit `/etc/rc.conf` to load required settings. Sample `rc.conf` contains required configurations for Nvidia and KDE / GNOME
    ### Nvidia GPU only
    - Install `x11/nvidia-driver x11/nvidia-xconfig x11/nvidia-settings` for Nvidia GPUs.
    - Add/Edit `/usr/local/etc/X11/xorg.conf.d/driver-nvidia.conf` to match the `driver-nvidia.conf` in the repo
    ### Optional
    - Autogenerate `xorg` config.
        ```shell
        Xorg -configure
        cp /root/xorg.conf.new /usr/local/etc/X11/xorg.conf
        ```

