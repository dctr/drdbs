dctr's rdiff-backup script
==========================

This script started as my personal backup script, but as it is getting more general and versatile, i decided to put it on github.

Installation
============

1. Put /bin and /etc on your disk
---------------------------------

- */usr/local/bin* and */usr/local/etc*, or
- *~/.local/bin* and *~/.local/etc*

**Note:** At the moment, etc has to be in the same folder as bin, as files are included via *../etc/...*,

2. Adapt drdbs.conf
-------------------

drdbs.conf is well documented. Adjust it to your needs.


3. Adapt drdbs.exclude
----------------------

This is the most important part: Select, what you want to include or exclude in your backup.

1. drdbs.exclude uses rdiff-backup's globbing syntax (basic part explained below)
2. The script includes */* to provide complete relative paths
3. To human logic, the file is interpreted in reverse order

### Syntax

- Lines starting with *-* mean "exclude".
- Lines starting with *+* mean "include"
- \* matches anything but "/", therefore \* means "ONE folder (or file)"
- \*\* matches "/" too, so \*\*/foo means "any file foo in any folder of any nesting depth"

### Creating your own config

As the backup starts at */* and you usually only want to backup selected folders (but not e.g. */dev*), building you own exclude should start with the following line.

    - **

As the file is interpreted in reverse order, any further includes have to be made above that line.

    + /home
    - **

You can place an exlude above an include to make an exception for this include

    - /home/eve
    + /home
    - **

This would backup all home folders, but not Eve's .

You can find an example drdbs.exclude in the etc directory of this repository.