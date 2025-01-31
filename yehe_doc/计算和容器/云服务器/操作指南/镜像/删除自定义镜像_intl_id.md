## Skenario

Dokumen ini menjelaskan cara menghapus citra kustom.

## Catatan
Sebelum menghapus citra kustom, harap perhatikan item berikut:
 - Setelah citra kustom dihapus, citra tersebut tidak dapat lagi digunakan untuk memulai instans CVM baru, tetapi tidak akan memengaruhi instans yang telah dimulai. Jika Anda ingin menghapus semua instans yang dimulai dari citra ini, lihat [Mengklaim Kembali Instans](https://intl.cloud.tencent.com/document/product/213/4931) atau [Menghentikan Instans](https://intl.cloud.tencent.com/document/product/213/4930).
 - Citra kustom yang telah dibagikan dengan orang lain tidak dapat dihapus. Untuk menghapusnya, Anda harus membatalkan berbagi citra terlebih dahulu. Untuk informasi selengkapnya, lihat [Batalkan Berbagi Citra](https://intl.cloud.tencent.com/document/product/213/7148).
 - Anda hanya dapat menghapus citra kustom, bukan citra umum atau citra bersama.

## Petunjuk

### Hapus citra melalui konsol
1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/).
2. Di bilah kiri, klik **Images** (Citra) dan pilih tab **Custom Image** (Citra Kustom) untuk masuk ke halaman manajemen citra kustom.
3. Pilih metode untuk menghapus citra kustom berdasarkan kebutuhan aktual.
 - Menghapus satu citra: cari citra khusus yang akan dihapus dalam daftar citra dan klik **More** (Lainnya) > **Delete** (Hapus).
 - Menghapus banyak citra: pilih semua citra kustom yang akan dihapus dalam daftar citra, lalu klik **Delete** (Hapus) di bagian atas.
4. Di jendela pop-up, klik **OK** (OKE).
Jika penghapusan gagal, kemungkinan akan ditampilkan alasannya.

### Hapus citra melalui API
Anda dapat menggunakan DeleteImages API untuk menghapus citra. Untuk detailnya, lihat [Menghapus Citra](https://intl.cloud.tencent.com/document/product/213/33275).
