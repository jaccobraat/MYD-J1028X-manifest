# MYD-J1028X-manifest

Documentation: 
https://www.nxp.com/docs/en/user-guide/UG10081_LLDP_6.1.55_2.2.0.pdf

Modified LS1028ARDB from:
https://github.com/nxp-qoriq/yocto-sdk

> mkdir bin  
> curl http://commondatastorage.googleapis.com/git-repo-downloads/repo  > bin/repo  
> chmod a+x bin/repo


> git config --global user.email "you@example.com"  
> git config --global user.name "Your Name"  

> bin/repo init -u https://github.com/jaccobraat/myd-j1028x-manifest  -b mickledore -m myd-j1028x-6.1.55-2.2.0.xml  
> bin/repo sync  

> . board-setup-env  

### atf & u-boot
> bitbake qoriq-atf  
> cd tmp/deploy/images/ls1028amyd  

### make sure to check correct sd device! 
use flex-installer to prepare sdcard then install:

> sudo dd if=atf/bl2_sd.pbl of=/dev/sdd bs=512 seek=8  
> sudo dd if=atf/fip_uboot.bin of=/dev/sdd bs=512 seek=2048  

### kernel & boot image
> bitbake linux-qoriq  
> bitbake generate-boottgz  
> tar -zxf boot_ls1028amyd_lts_6.1.tgz  -C <mount point partition 1>  

### userland
> bitbake ls-image-main