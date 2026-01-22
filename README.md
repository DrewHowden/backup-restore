# backup
*backup* is a simple bash script that takes selected directories, and puts them in an encrypted .7z archive, which can easily be copied to external media or cloud storage.

This script is meant to be run as a **regular user**.

Dependencies:
- `p7zip`
    - Can be installed on Debian/Ubuntu (and derivatives) with `sudo apt install p7zip`

Installation:
1. Replace `INSERT_DIRECTORIES_TO_BE_BACKED_UP_HERE` with directores under your home directory to be backed up (e.g. `~/Documents ~/Pictures ~/Videos` etc.)
    - NOTE: The directories specified here need to be at the root of your home folder.
2. Make any other customizations required
    - For example, to back up `.config/autostart`, add `mkdir ~/backup/home/.config` and `cp -r ~/.config/autostart` in the appropriate places (read the comments within the script for guidance on where to put these commands)
3. After you are finished making the required modifications, move the script to `/usr/local/bin` with `sudo mv backup /usr/local/bin`, with your working directory set to the directory you saved this script in
    - HINT: Use the "Open in Terminal" function in your file manager, while in the directory you saved this script in
4. Finally, mark this script as executable with `chmod +x /usr/local/bin/backup`

Usage:
1. Just type `backup` in a Terminal window
2. You will be prompted to create a password for your encrypted backup (7z does not prompt you to confirm your password, so **make sure you get this right the first time!**)
3. It does the rest!
4. After this script is done, you will see a file called `backup.7z` on your desktop. Make sure you can open this file, using the password you created, before copying it to external storage

# restore
*restore* is the companion script to *backup*. It unarchives the encrypted backup created by *backup*, and puts all the files in the right places.

This script is meant to be run as a **regular user, with the ability to sudo**.

Installation:
1. Make any customizations required
    - For example, if you had *backup* back up files or directories outside your home directory, you will need to add additional `cp` commands to tell *restore* where to put these files
2. Place this script on any external media (or cloud storage) where you copied backup.7z to, and mark it as Executable

Usage:
1. To restore your backup from backup.7z, open a Terminal window, switch to the directory where your backup.7z file is stored, then type `./restore`
    - NOTE: This script needs to be in the same directory as backup.7z, which must be your working directory when running this script
    - HINT: Use the "Open in Terminal" function in your file manager, while in the directory with your backup
2. If restoring from cloud storage, you may need to download your backup.7z file and this script from your cloud storage to your local machine (be sure to mark this script as Executable)
3. You will be prompted for the password used to encrypt your backup
4. It does the rest!

You can also have this script call other scripts or commands to further reconfigure your system, like:

# app-install
*app-install* automatically installs packages of your choosing. This is a great way to get back up and running after a reinstall!
This script also installs Flatpak for you by default.

NOTE: This script is written with a Ubuntu system in mind. As such, by default, it assumes `apt` is your package manager, and that `snapd` is installed. If you are not on Ubuntu, you will need to tweak this script to suit your distribution.

This script is meant to be run as a **regular user, with the ability to sudo**.

Installation:
1. Put the names of the packages you want to install where `# Put packages to install here` is
    - Also replace `apt install` with your distribution's package manager if necessary
2. Put the Application IDs of the Flatpaks you want to install where `# Put Flatpaks to install here (e.g. com.spotify.Client)` is
    - If you don't want Flatpaks, remove `flatpak` from the `apt install` line, and delete all `flatpak` lines
3. Put the names of the Snaps you want to install where `# Put Snaps to install here` is
    - NOTE: If `snapd` is not installed by default on your distribution, either install it from the package manager in step 1, or if you don't want Snaps, delete all `snap` lines
4. Put the names of pre-installed packages you want to remove where `# Put pre-installed packages to remove here` is
    - If there are no pre-installed packages to be removed, delete this line
5. Put the names of pre-installed Snaps you want to remove where `# Put pre-installed Snaps to remove here` is
    - If you are not on Ubuntu, or there are no pre-installed Snaps to remove, delete this line
6. After you are finished making the required modifications, move the script to `/usr/local/bin` with `sudo mv app-install /usr/local/bin`, with your working directory set to the directory you saved this script in
    - HINT: Use the "Open in Terminal" function in your file manager, while in the directory you saved this script in
    - NOTE: If this script is in `/usr/local/bin`, *backup* will automatically back this script up by default, and *restore* will automatically restore it here and mark it as executable by default, along with anything else in `/usr/local/bin`
7. Finally, mark this script as executable with `chmod +x /usr/local/bin/app-install`

Usage:
1. Just run `app-install` in a Terminal window (or call it with another script, like *restore*)
2. It does the rest!
3. After this script is finished running, it will ask you if you would like to reboot the system. If you answer `y`, the system reboots, otherwise the script simply exits
