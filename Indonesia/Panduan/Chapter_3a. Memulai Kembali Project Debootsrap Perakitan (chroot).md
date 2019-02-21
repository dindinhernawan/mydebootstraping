**[ 1 ]---------------------------------------------------------------------------------**  
Panduan      :   Memulai kembali proses debootsrap yang sebelumnya  
Penjelasan   : Gunakan Perintah dibawah ini secara berurutan jika ingin memulai kembali proses debootsrap yang sebelumnya  
Catatan      : Gunakan Perintah cd Project jika tidak berada di lokasi Project  

Buka Terminal dan Ketik Perintah Berikut :  
32-Bit  
```bash
cd /home/$(whoami)/Project/
sudo mount --bind /dev/ root32/dev
sudo chroot root32
mount -t proc none /proc && mount -t sysfs none /sys && mount -t devpts none /dev/pts
export HOME=/root && export LC_ALL=C
```
64-Bit  
```bash
cd /home/$(whoami)/Project/
sudo mount --bind /dev/ root64/dev
sudo chroot root32
mount -t proc none /proc && mount -t sysfs none /sys && mount -t devpts none /dev/pts
export HOME=/root && export LC_ALL=C
```