# luky-borg-backup
Automated backup scripts using Borg Backup, systemd and optionally Nextcloud/ownCloud/STACK.

This will backup the source files and folders of your choice to a [Borg](https://borgbackup.readthedocs.io/en/stable/) repository of your choice and optionally synchronize the repository with one of your cloud storage locations (based on [Nextcloud](https://nextcloud.com/), [ownCloud](https://owncloud.org/) or [STACK](https://www.transip.nl/stack/).
You can (and should) run it daily and for now it will keep 7 daily, 4 weekly, 12 monthly and unlimited yearly archives of your source files.

# Installation

## Arch Linux
For Arch Linux, an [installation package is available in the AUR](https://aur.archlinux.org/packages/luky-borg-backup/) which includes all needed dependencies.
> Please also check and install the optional dependencies for more functionality

## Manual
For a manual installation:
1. Install `borg` on your system
1. Copy `luky-borg-backup.conf` to folder `/etc`.
   > **This should only be done the first time**
1. Copy `luky-borg-backup.service` and `luky-borg-backup.timer` to folder `/etc/systemd/system` or `/usr/lib/systemd/system`.
1. Copy `luky-borg-backup` to folder `/usr/bin`

# Configuration
File `/etc/luky-borg-backup.conf` contains all configuration options of the backup script.
The file is rather self-explanatory, but here are some hints:
* At least `REPOSITORY` and `SOURCES` should be defined.
* To prevent manual intervention for filling in your repository password interactively, you can define `BORG_PASSPHRASE`.

Of course, prior to using `luky-borg-backup` for the `REPOSITORY` as defined in `/etc/luky-borg-backup.conf`, you should setup the repository by i.e.:
```bash
borg init -e keyfile <repository>
```

## Running every night at 04:00
To run the script every night at 04:00, you can enable and start the related timer by:
```bash
systemctl enable luky-borg-backup.timer
systemctl start luky-borg-backup.timer
```
