Dude DiskUsageDeepExaminer
===========================

Tool for finding biggest directories in given path list. While `du` does a perfect job finding disk space used on the first level like

    du -cshx *

or in deeper levels like

    du -achHx * | sort -rn | head -n 30

, both results leave either deep information or good overview to be desired. In an attempt to provide a quick overview where in the filesystem the big guys hang around, the `dude`  script has been written. 

For example, calling

    dude /var/lib

display 25 lines, minimum entry size 1.2M like:

    181.8M /var/lib/rpm
    168.1M .... /var/lib/rpm/Packages
      5.8M .... /var/lib/rpm/Basenames
      3.1M .... /var/lib/rpm/Providename
      1.9M .... /var/lib/rpm/Dirnames
      1.3M .... /var/lib/rpm/__db.003
     30.1M /var/lib/sss
     24.1M .... /var/lib/sss/mc
      9.9M ........ /var/lib/sss/mc/initgroups
      8.0M ........ /var/lib/sss/mc/passwd
      6.1M ........ /var/lib/sss/mc/group
      6.0M .... /var/lib/sss/db
      2.0M ........ /var/lib/sss/db/cache_idm.xtrav.de.ldb
      1.5M ........ /var/lib/sss/db/timestamps_idm.xtrav.de.ldb
      1.2M ........ /var/lib/sss/db/sssd.ldb
      1.2M ........ /var/lib/sss/db/config.ldb
     15.7M /var/lib/yum
      8.7M .... /var/lib/yum/history
      4.5M ........ /var/lib/yum/history/2017-09-11
      1.3M ............ /var/lib/yum/history/2017-09-11/7/saved_tx
      4.1M ........ /var/lib/yum/history/history-2017-09-11.sqlite
      6.7M .... /var/lib/yum/yumdb
      1.7M ........ /var/lib/yum/yumdb/l
      3.6M /var/lib/mlocate/mlocate.db
    231.8M total

`dude` does not cross filesystem mounts. This allows for fast check of e.g. `/` filesystem without stepping into virtual kernel filesystems or network mounts.

Symbolic links are not followed if not specified on command line, directly.
    

Usage
-----

As a short reference, call 

    dude -h

Besides tree view, `dude` offers sorted lists of given length - human readable 

    dude -ln 50 

... or for parsing by e.g. monitoring scripts:

    dude -pn 50


Installation
------------

You can clone this repository or directly pull this script into `/usr/local/bin`:

    curl -L  https://raw.githubusercontent.com/sternmotor/dude/master/dude > /usr/local/bin/dude 
    chmod 0755 /usr/local/bin/dude

If `curl` is not available, use `wget`:

    wget https://raw.githubusercontent.com/sternmotor/dude/master/dude -O /usr/local/bin/dude
    chmod 0755 /usr/local/bin/dude

Thats it, see "Usage" section.
