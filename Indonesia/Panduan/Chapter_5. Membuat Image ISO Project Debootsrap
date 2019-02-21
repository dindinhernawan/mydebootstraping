**[ 1 ]---------------------------------------------------------------------------------**  
Panduan      : Menghapus filesistem.squashfs jika sebelumnya membuat filesistem.squashfs  
Penjelasan   :  
Catatan      : Jika Pertama kali membuat iso lewatkan perintah dibawah ini  
Buka Terminal dan Ketik Perintah Berikut :
```bash
sudo rm /home/$(whoami)/Project/dvd32/casper/filesystem.squashfs 
```
**[ 2 ]---------------------------------------------------------------------------------**  
Panduan      :   Membuat Folder Kerangka dvd32 Pertama kali.  
Penjelasan   :  
Catatan      : jika sudah buat lewatin saja  
Buka Terminal dan Ketik Perintah Berikut :  
```bash
cd /home/$(whoami)/Project/dvd32
sudo mkdir casper .disk isolinux
sudo cp /home/$(whoami)/Project/root32/boot/vmlinuz-4.4.0-21-generic /home/$(whoami)/Project/dvd32/casper/vmlinuz
sudo cp /home/$(whoami)/Project/root32/boot/initrd.img-4.4.0-21-generic /home/$(whoami)/Project/dvd32/casper/initrd.lz
cd /home/$(whoami)/Project/dvd32/isolinux/ 
sudo wget -c https://github.com/dindinG41TR3/panduan-debootstraping/raw/master/Indonesia/Modul/isolinux/isolinux.bin
sudo cp /usr/lib/syslinux/modules/bios/Idllinux.c32 /home/$(whoami)/Project/dvd32/isolinux/
sudo cp /boot/memtest86+.bin dvd32/casper/memtest
```

```bash
cd /home/$(whoami)/Project/dvd32/
cat > README.diskdefines << "EOF"
#define DISKNAME  Xenta OS
#define TYPE  binary
#define TYPEbinary  1
#define ARCH  i386
#define ARCHi386  1
#define DISKNUM  1
#define DISKNUM1  1
#define TOTALNUM  0
#define TOTALNUM0  1
EOF
```
```bash
cd /home/$(whoami)/Project/dvd32/.disk
sudo echo "base_installable" > base_installable
sudo echo "full_cd/single" > cd_type
sudo echo "Xenta OS 1.3" > info
sudo echo "http://www.xentaos.org/" > release_notes_url
```
```bash
cd /home/$(whoami)/Project/dvd32/isolinux
cat > isolinux.cfg << "EOF"
DEFAULT live
LABEL live
  menu label ^Start Xenta OS 1.3 LTS Console Edisi
  kernel /casper/vmlinuz
  append boot=casper initrd=/casper/initrd.lz --
DISPLAY isolinux
EOF
```
```bash
cd /home/$(whoami)/Project/dvd32/isolinux
cat > isolinux << "EOF"
*******************************************************************************
 \XXXXXXXXXXXXXXXXXXXXXXXXXXX  
   \XXXXXXXXXXXXXXXXXXXXXXXXX  WELLCOME TO XENTA OS 1.3 AROK CONSOLE EDISI
     \XXXXXXXXXXXXXXXXXXXXXXX  
       \XXXXXXXXXXXXXXXXXXXXX  OS          : Xenta OS
        /XXXXXXXXXXXXXXXXXXXX  Arch        : i386
       /XXXXXXXXXXXXXXXXXXXXX  Versi       : 1.3 LTS
      /XXX/\XXXXXXXXXXXXXXXXX  Codename    : Arok
     /XX/  /XXX\XXXXXXXXXXXXX  Edisi       : Console
    /X/   /XXXXXXXXXXXXXXXXXX  
    /    /XXXXXXXXX\XXXXXXXXX  Website      : http://www.xentaos.org/
        /XXXXXX/ \XXXXXXXXXXX  Facebook     : Xenta OS
       /XXXXXX/   /XXXXXXXXXX  Youtube      : Xenta OS
      /XXXXX/    /XXX/XXXXXXX  Twitter      : @xentaos
     /XXX/      /XX/  \XXXXXX  IRC Channel (freenode) #xentaos
    /XX/       /X/     \XXXXX  
   /X/         /         \XXX  
   /                       \X  
                               
*******************************************************************************
EOF
```

# [ 3 ]---------------------------------------------------------------------------------
#      Panduan      :   Membuat List Paket & Info live sistem
#      Penjelasan   :
#                       * 
#      Catatan      :
#                       * 
# Buka Terminal dan Ketik Perintah Berikut :
cd /home/$(whoami)/Project/
sudo chroot root32 dpkg-query -W --showformat='${Package} ${Version}\n' | sudo tee dvd32/casper/filesystem.manifest
sudo cp -v dvd32/casper/filesystem.manifest dvd32/casper/filesystem.manifest-desktop
sudo su
printf $(sudo du -sx --block-size=1 root32 | cut -f1) > dvd32/casper/filesystem.size
exit

# [ 4a ]---------------------------------------------------------------------------------
#      Panduan      :   Membuat Filesistem.squashfs STANDAR COMPRESS
#      Penjelasan   :
#                       * 
#      Catatan      :
#                       * 
# Buka Terminal dan Ketik Perintah Berikut :
cd /home/$(whoami)/Project/
sudo mksquashfs root32 ./dvd32/casper/filesystem.squashfs

# [ 4b ]---------------------------------------------------------------------------------
#      Panduan      :   Membuat Filesistem.squashfs HIGH COMPRESS
#      Penjelasan   :
#                       * 
#      Catatan      :
#                       * 
# Buka Terminal dan Ketik Perintah Berikut :
cd /home/$(whoami)/Project/
sudo mksquashfs root32 dvd32/casper/filesystem.squashfs -b 1048576 -comp xz -Xdict-size 100%

# [ 5 ]---------------------------------------------------------------------------------
#      Panduan      :   Membuat md5sum iso
#      Penjelasan   :
#                       * 
#      Catatan      :
#                       * 
# Buka Terminal dan Ketik Perintah Berikut :
cd /home/$(whoami)/Project//dvd32
find -type f -print0 | sudo xargs -0 md5sum | grep -v isolinux/boot.cat | sudo tee MD5SUMS

# [ 6 ]---------------------------------------------------------------------------------
#      Panduan      :   Membuat ISO Rilis 
#      Penjelasan   :
#                       * 
#      Catatan      :
#                       * 
# Buka Terminal dan Ketik Perintah Berikut :
cd /home/$(whoami)/Project/ 
sudo mkisofs -r -V "xentaos-1.3lts-console-i386" -cache-inodes -J -l -b isolinux/isolinux.bin -c isolinux/boot.cat -no-emul-boot -boot-load-size 4 -boot-info-table -o ./xentaos-1.3lts-console-i386.iso dvd32
sudo chmod 777 xentaos-1.3lts-console-i386.iso

# [ 7 ]---------------------------------------------------------------------------------
#      Panduan      :   Membuat ISOHybrid
#      Penjelasan   :
#                       * 
#      Catatan      :
#                       * 
# Buka Terminal dan Ketik Perintah Berikut :
cd /home/$(whoami)/Project/
isohybrid xentaos-1.3lts-console-i386.iso

# [ 8a ]---------------------------------------------------------------------------------
#      Panduan      :   Membuat MD5sum
#      Penjelasan   :
#                       * 
#      Catatan      :
#                       * 
# Buka Terminal dan Ketik Perintah Berikut :
cd /home/$(whoami)/Project/
md5sum xentaos-1.3lts-console-i386.iso > xentaos-1.3lts-console-i386.iso.md5sum

# [ 8b ]---------------------------------------------------------------------------------
#      Panduan      :   Membuat SHA1sum
#      Penjelasan   :
#                       * 
#      Catatan      :
#                       * 
# Buka Terminal dan Ketik Perintah Berikut :
cd /home/$(whoami)/Project/
sha1sum xentaos-1.3lts-console-i386.iso > xentaos-1.3lts-console-i386.iso.sha1sum

# [ 8c ]---------------------------------------------------------------------------------
#      Panduan      :   Membuat SHA2sum
#      Penjelasan   :
#                       * 
#      Catatan      :
#                       * 
# Buka Terminal dan Ketik Perintah Berikut :
cd /home/$(whoami)/Project/
sha2sum xentaos-1.3lts-console-i386.iso > xentaos-1.3lts-console-i386.iso.sha2sum
