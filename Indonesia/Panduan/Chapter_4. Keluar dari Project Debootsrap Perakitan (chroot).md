**[ 1 ]---------------------------------------------------------------------------------**  
Panduan      : Keluar dari Project Debootsrap Perakitan (chroot)  
Penjelasan   :  
Catatan      :  

Buka Terminal dan Ketik Perintah Berikut :  
32-Bit  
```bash
apt-get clean && apt-get autoremove && rm -rf /tmp/* ~/.bash_history && umount /proc && umount /sys && umount /dev/pts
exit
sudo umount ./root/dev
```

64-Bit  
```bash
apt-get clean && apt-get autoremove && rm -rf /tmp/* ~/.bash_history && umount /proc && umount /sys && umount /dev/pts
exit
sudo umount ./root/dev
```
