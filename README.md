# UAS_PengolahanCitra
# SEANNETA APFIA AULIA PRAMESTI - 202131099
praktikum terlampir di file UAS.ipynb
untuk data citra ppllatt.jpg
untuk hasil crop citra biner platcitrabiner.png
untuk hasil crop citra edged platcitraedged.png

library yang digunakan :
- imutils
- opencv
- numpy
- matplotlib

teori :

penjelasan
- masukkan library yang dibutuhkan
- masukkan variabel citra
- ubah citra dari BGR ke grayscale
- buat filter grayscale dan cara pengaplikasiannya
- bilateral-filter untuk mengurangi noise pada citra dan tetap mempertahankan detail tepi gambar
- cv2.Canny untuk bantu deteksi tepi gambar
- setelah itu ambil kontur citra untuk crop plat nomor mobilnya
- cv2.RETR_TREE untuk mengambil semua kontur dengan hirarki lengkap
- konturnya pakai library imutils
- mengurutkan kontur secara descending
- pakai looping
- dan terakhir memastikan citra edge dan biner apakah trus atau tidak
