**[ 1 ]---------------------------------------------------------------------------------**  
Panduan : Membuat Kerangka Directory Kerja.  
Penjelasan :  
Catatan :  
 * Jalankan Sebagai User Biasa. Jika Berada di posisi root.  
 * Silahkan keluar dan jalankan sebagai user biasa. 
 
Buka Terminal dan Ketik perintah berikut :
```bash
32-Bit
mkdir -p /home/$(whoami)/project/i386/{root,dvd}

64-Bit
mkdir -p /home/$(whoami)/roject/amd64/{root,dvd}
```

**[ 2 ]---------------------------------------------------------------------------------**  
Panduan : Membuat Kerangka Sistem Operasi Awal (Base Sistem).  
Penjelasan :  
Catatan :  
 * Ini Memerlukan Koneksi Internet dan Waktu Cukup lama Tunggu saja sampai Selesai. 
 
Buka Terminal dan Ketik perintah berikut :  
```bash
32-Bit
sudo debootstrap --arch=i386 --variant=minbase xenial /home/$(whoami)/project/i386/root http://archive.ubuntu.com/ubuntu/

64-Bit
sudo debootstrap --arch=amd64 --variant=minbase xenial /home/$(whoami)/project/amd64/root http://archive.ubuntu.com/ubuntu/
```
