**[ 1 ]---------------------------------------------------------------------------------**  
Panduan      : Menghapus filesistem.squashfs jika sebelumnya membuat filesistem.squashfs  
Penjelasan   :  
Catatan      : Jika Pertama kali membuat iso lewatkan perintah dibawah ini  
Buka Terminal dan Ketik Perintah Berikut :
```bash
sudo rm /home/$(whoami)/project/i386/dvd/casper/filesystem.squashfs 
```
**[ 2 ]---------------------------------------------------------------------------------**  
Panduan      :   Membuat Folder Kerangka dvd Pertama kali.  
Penjelasan   :  
Catatan      : jika sudah buat lewatin saja  
Buka Terminal dan Ketik Perintah Berikut :  
```bash
cd /home/$(whoami)/project/i386/dvd
sudo mkdir casper .disk isolinux
sudo cp /home/$(whoami)/project/i386/root/boot/vmlinuz-4.13.0-19-generic /home/$(whoami)/project/i386/dvd/casper/vmlinuz
sudo cp /home/$(whoami)/project/i386/root/boot/initrd.img-4.13.0-19-generic /home/$(whoami)/project/i386/dvd/casper/initrd.lz
cd /home/$(whoami)/project/i386/dvd/isolinux/ 
sudo wget -c https://github.com/dindinG41TR3/panduan-debootstraping/raw/master/Indonesia/Modul/isolinux/isolinux.bin
sudo cp /usr/lib/syslinux/modules/bios/Idllinux.c32 /home/$(whoami)/project/i386/dvd/isolinux/
sudo cp /boot/memtest86+.bin dvd/casper/memtest
```

```bash
cd /home/$(whoami)/project/i386/dvd/
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
cd /home/$(whoami)/project/i386/dvd/.disk
sudo echo "base_installable" > base_installable
sudo echo "full_cd/single" > cd_type
sudo echo "Xenta OS 2.0" > info
sudo echo "http://www.xentaos.com/" > release_notes_url
```
```bash
cd /home/$(whoami)/project/i386/dvd/isolinux
cat > isolinux.cfg << "EOF"
DEFAULT live
LABEL live
  menu label ^Start Xenta OS 2.0 LTS Console Edisi
  kernel /casper/vmlinuz
  append boot=casper initrd=/casper/initrd.lz --
DISPLAY isolinux
EOF
```
```bash
cd /home/$(whoami)/project/i386/dvd/isolinux
cat > isolinux << "EOF"
*******************************************************************************
 \XXXXXXXXXXXXXXXXXXXXXXXXXXX  
   \XXXXXXXXXXXXXXXXXXXXXXXXX  WELLCOME TO XENTA OS 2.0 BATIK CONSOLE EDISI
     \XXXXXXXXXXXXXXXXXXXXXXX  
       \XXXXXXXXXXXXXXXXXXXXX  OS          : Xenta OS
        /XXXXXXXXXXXXXXXXXXXX  Arch        : i386
       /XXXXXXXXXXXXXXXXXXXXX  Versi       : 2.0 LTS
      /XXX/\XXXXXXXXXXXXXXXXX  Codename    : Batik
     /XX/  /XXX\XXXXXXXXXXXXX  Edisi       : Console
    /X/   /XXXXXXXXXXXXXXXXXX  
    /    /XXXXXXXXX\XXXXXXXXX  Website      : http://www.xentaos.com/
        /XXXXXX/ \XXXXXXXXXXX  Facebook     : Xenta OS
       /XXXXXX/   /XXXXXXXXXX  Youtube      : Xenta OS Linux
      /XXXXX/    /XXX/XXXXXXX  Twitter      : @xentaoslinux
     /XXX/      /XX/  \XXXXXX  IRC Channel (freenode) #xentaoslinux
    /XX/       /X/     \XXXXX  
   /X/         /         \XXX  
   /                       \X  
                               
*******************************************************************************
EOF
```

**[ 3]---------------------------------------------------------------------------------**  
Panduan      : Membuat List Paket & Info live sistem  
Penjelasan   :  
Catatan      :  
Buka Terminal dan Ketik Perintah Berikut :  
```bash
cd /home/$(whoami)/project/i386/
sudo chroot root dpkg-query -W --showformat='${Package} ${Version}\n' | sudo tee dvd/casper/filesystem.manifest
sudo cp -v dvd/casper/filesystem.manifest dvd/casper/filesystem.manifest-desktop
sudo su
printf $(sudo du -sx --block-size=1 root | cut -f1) > dvd/casper/filesystem.size
exit
```
**[ 4a]---------------------------------------------------------------------------------**  
Panduan      : Membuat Filesistem.squashfs STANDAR COMPRESS  
Penjelasan   :  
Catatan      :  
Buka Terminal dan Ketik Perintah Berikut : 
```bash
cd /home/$(whoami)/project/i386/
sudo mksquashfs root ./dvd/casper/filesystem.squashfs
```

**[ 4b]---------------------------------------------------------------------------------**  
Panduan      : Membuat Filesistem.squashfs HIGH COMPRESS  
Penjelasan   :  
Catatan      :  
Buka Terminal dan Ketik Perintah Berikut :  
```bash
cd /home/$(whoami)/project/i386/
sudo mksquashfs root dvd/casper/filesystem.squashfs -b 1048576 -comp xz -Xdict-size 100%
```

**[ 5 ]---------------------------------------------------------------------------------**  
Panduan      : Membuat md5sum iso  
Penjelasan   :  
Catatan      :  
Buka Terminal dan Ketik Perintah Berikut :  
```bash
cd /home/$(whoami)/project/i386//dvd
find -type f -print0 | sudo xargs -0 md5sum | grep -v isolinux/boot.cat | sudo tee MD5SUMS
```
**[ 6 ]---------------------------------------------------------------------------------**  
Panduan      : Membuat ISO Rilis  
Penjelasan   :  
Catatan      :  
Buka Terminal dan Ketik Perintah Berikut :  
```bash
cd /home/$(whoami)/project/i386/ 
sudo mkisofs -r -V "xentaos-2.0lts-console-i386" -cache-inodes -J -l -b isolinux/isolinux.bin -c isolinux/boot.cat -no-emul-boot -boot-load-size 4 -boot-info-table -o ./xentaos-2.0lts-console-i386.iso dvd
sudo chmod 777 xentaos-2.0lts-console-i386.iso
```

**[ 7 ]---------------------------------------------------------------------------------**  
Panduan      :  Membuat ISOHybrid  
Penjelasan   :  
Catatan      :  
Buka Terminal dan Ketik Perintah Berikut :  
```bash
cd /home/$(whoami)/project/i386/
isohybrid xentaos-2.0lts-console-i386.iso
```
**[ 8a ]---------------------------------------------------------------------------------**  
Panduan      : Membuat MD5sum  
Penjelasan   :  
Catatan      :  
Buka Terminal dan Ketik Perintah Berikut :  
```bash
cd /home/$(whoami)/project/i386/
md5sum xentaos-2.0lts-console-i386.iso > xentaos-2.0lts-console-i386.iso.md5sum
```

**[ 8b ]---------------------------------------------------------------------------------**  
Panduan      : Membuat SHA1sum  
Penjelasan   :  
Catatan      :  
Buka Terminal dan Ketik Perintah Berikut :  
```bash
cd /home/$(whoami)/project/i386/
sha1sum xentaos-2.0lts-console-i386.iso > xentaos-2.0lts-console-i386.iso.sha1sum
```
**[ 8c ]---------------------------------------------------------------------------------**  
Panduan      : Membuat SHA2sum  
Penjelasan   :  
Catatan      :  
Buka Terminal dan Ketik Perintah Berikut :  
```bash
cd /home/$(whoami)/project/i386/
sha2sum xentaos-2.0lts-console-i386.iso > xentaos-2.0lts-console-i386.iso.sha2sum
```
