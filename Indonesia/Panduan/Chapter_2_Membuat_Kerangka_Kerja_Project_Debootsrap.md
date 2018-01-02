**[ 1 ]---------------------------------------------------------------------------------**  
Panduan : Membuat Kerangka Directory Kerja.  
Penjelasan :  
Catatan :  
 * Jalankan Sebagai User Biasa. Jika Berada di posisi root.  
 * Silahkan keluar dan jalankan sebagai user biasa.  
Buka Terminal dan Ketik perintah berikut :
```bash
mkdir -p /home/$(whoami)/Project/{root32,dvd32}
```

**[ 2 ]---------------------------------------------------------------------------------**  
Panduan : Membuat Kerangka Sistem Operasi Awal (Base Sistem).  
Penjelasan :  
Catatan :  
 * Ini Memerlukan Koneksi Internet dan Waktu Cukup lama Tunggu saja sampai Selesai.  
Buka Terminal dan Ketik perintah berikut :  
```bash
sudo debootstrap --arch=i386 --variant=minbase xenial /home/$(whoami)/Project/root32 http://archive.ubuntu.com/ubuntu/
```
