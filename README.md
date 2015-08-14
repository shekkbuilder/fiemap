\# fiemap
fiemap ioctl() example by Colin Ian King (2010). gpl2 license.

Small example:

root@trout:~/nlitend/dev/fiemapxz# ls -li
total 32
3550986 -rwxr-xr-x 1 root root 21032 Feb  4 17:47 fiemap
3550710 -rw-r--r-- 1 root root  3257 Feb  4 17:44 fiemap.c
3550985 -rw-r--r-- 1 root root    97 Feb  4 17:44 Makefile

root@trout:~/nlitend/dev/fiemapxz# ./fiemap Makefile
File Makefile has 1 extents:
\#    Logical          Physical         Length           Flags
0:    0000000000000000 0000000d8c1cd000 0000000000001000 0001

convert the hex and divide by pagesize:

root@trout:~/nlitend/dev/fiemapxz# printf '%d\n' 0x0000000d8c1cd000
58185273344
root@trout:~/nlitend/dev/fiemapxz# getconf PAGESIZE
4096
root@trout:~/nlitend/dev/fiemapxz# echo "58185273344 / 4096"|bc
14205389

WALLAH!

root@trout:~/nlitend/dev/fiemapxz# debugfs /dev/sda1
debugfs 1.42.9 (4-Feb-2014)
debugfs:  icheck 14205389
Block    Inode number
14205389    3550985

which is the inode number for Makefile.

root@trout:~/nlitend/dev/fiemapxz# ls -li Makefile
3550985 -rw-r--r-- 1 root root 97 Feb  4 17:44 Makefile

--+
