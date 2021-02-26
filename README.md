Dude
====

The `dude` tool (**d**isk **u**sage **d**eep **e**xaminer) may be used for
listing the biggest directories or files deep in file system hierarchie of
given path list.  While `du` does a perfect job finding disk space used on the
first level like

    du -cshx *

or in deeper levels like

    du -achHx * | sort -rn | head -n 30

, both results leave either deep information or good overview to be desired. In
an attempt to provide a quick overview where in the filesystem the big guys
hang around, the `dude`  script has been written. 

For example, calling

    dude /var/lib

displays 12 file system entries like:

     51.6M /var/lib/rpm
     45.0M .... /var/lib/rpm/Packages
      2.6M .... /var/lib/rpm/Basenames
     31.1M /var/lib/sss
     25.3M .... /var/lib/sss/mc
     10.5M ........ /var/lib/sss/mc/initgroups
      8.4M ........ /var/lib/sss/mc/passwd
      6.3M ........ /var/lib/sss/mc/group
      5.8M .... /var/lib/sss/db
     16.3M /var/lib/yum/yumdb
      6.2M /var/lib/yum/yumdb/p
      2.6M /var/lib/yum/yumdb/l
    102.3M total

In this example, all entries < `2.6 MiB` are not displayed. Directories which
are parents of displayed sub-entries are shown only if their content size (size
minus displayed sub-entries) is bigger than this limit. 


`dude` does not cross filesystem mounts. This allows for fast check of e.g. `/`
filesystem without stepping into virtual kernel filesystems or network mounts.

Symbolic links are not followed if not specified on command line, directly.

Sparse files (e.g. `/var/log/lastlog` are displayed with the size they have on
disk, not the apparent bloated size.
    

Usage
-----

This script has been successfully tested under CentOS, Debian and macOS, both
python2.7 and python 3.6.

As a short reference, call 

    dude -h

Besides tree view, `dude` offers sorted lists of given length - human readable 

    dude -ln 50 

... or for parsing by e.g. monitoring scripts:

    dude -pn 50


Installation
------------

You can clone this repository or directly pull this script into
`/usr/local/bin`:

    curl -L  https://raw.githubusercontent.com/sternmotor/dude/master/dude >
/usr/local/bin/dude chmod 0755 /usr/local/bin/dude

If `curl` is not available, use `wget`:

    wget https://raw.githubusercontent.com/sternmotor/dude/master/dude -O
/usr/local/bin/dude chmod 0755 /usr/local/bin/dude

Thats it, see "Usage" section.


TODO
----
* better example for file systems tree
* exclude virtual drive and network mounts, 
    * include mount local drives (/dev devices)
    * maintain fs list ext[234], btrfs , zfs, reiserfs, jfs, xfs, vfat, ntfs-3g, apfs , exfat, fat
    * /sbin/udevadm info --query=all --name=sdX | grep ID_BUS
