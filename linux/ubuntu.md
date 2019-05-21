## Apt / Fix bad packages

If 

    sudo apt-get install -f

is failing due to broken dependencies and I cannot uninstall the packages using those dependencies through apt, then use dpkg to remove them:

    sudo dpkg -r gdal proj

After that you may be able to then use the package manager and re-install dependencies:

    sudo apt-get update
    sudo apt-get install -f

## Fix lost menu bar/launcher on Ubuntu 16/unity

Worked for me on Ubuntu 16.04:

```
sudo apt-get update
sudo apt-get install --reinstall ubuntu-desktop
sudo apt-get install unity
sudo shutdown -r now
```

## Reset a user's password

```
sudo passwd USERNAME
```

## Install ntp (keep time synchronized)

```
sudo apt-get install ntp
```

## Mount drive

```
# show block ids
sudo blkid

# make target directory
sudo mkdir /data

# temporary mount
sudo mount /dev/sda1 /data

# permanent mount
sudo vi /etc/fstab
# add a new line using the uuid from the blkid command as the identifier
UUID=fc791832-7c90-45b5-9648-4aad36e9fd0a       /data   ext4    defaults        0       2
```

## Set vim as default editor

```
vi ~/.bashrc

# add to file
export VISUAL=vim
export EDITOR="$VISUAL"
```
