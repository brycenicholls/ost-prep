

lsblk
parted /dev/vdx print
parted /dev/vdd mklabel msdos mkpart primary xfs 1Mb 1G
mkfs.xfs /dev/vdx1
