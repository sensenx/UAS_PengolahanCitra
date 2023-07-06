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
- Bilateral filter adalah metode pengolahan citra yang digunakan untuk mengurangi noise atau menghaluskan citra dengan mempertahankan tepi atau detail penting. Filter ini bekerja dengan mempertimbangkan kedua jarak spasial dan perbedaan intensitas piksel. tujuannya untuk mempertahankan tepi atau detail penting dalam citra, karena perbedaan intensitas yang signifikan dianggap sebagai tanda adanya tepi.
- Contour pada citra kontur merupakan representasi visual dari bentuk dan struktur dalam citra dan dapat digunakan untuk berbagai tujuan seperti deteksi objek, segmentasi, pengenalan pola, dan analisis bentuk.
- Mask layer adalah lapisan tambahan yang digunakan untuk membatasi efek atau operasi tertentu hanya pada area tertentu dalam citra. Biasanya, mask layer memiliki dua nilai piksel yang berbeda: 0 dan 255. Nilai 255 (putih) menandakan area yang dipilih, sementara nilai 0 (hitam) menandakan area yang tidak dipilih. Mask layer ini diterapkan pada citra asli atau lapisan gambar lainnya dalam proses kompositing atau pengeditan citra.
- Deteksi Tepi menggunakan Operator Canny, yaitu proses identifikasi dan penyorotan perubahan tajam dalam intensitas piksel di sekitar suatu objek atau struktur dalam citra. Tepi adalah perbatasan atau transisi antara dua wilayah dengan intensitas yang berbeda dalam citra.
- Citra biner adalah jenis citra yang hanya memiliki dua nilai piksel yang mungkin, yaitu hitam dan putih. Dalam citra biner, setiap piksel diwakili oleh satu bit informasi, di mana nilai 0 menandakan piksel hitam dan nilai 1 menandakan piksel putih.
- cropped edge untuk memotong data citra yang sudah di deteksi sebelumnya.

penjelasan :
- install library yang dibutuhkan
- masukkan library yang dibutuhkan
- masukkan variabel citra ke dalam kode
![image](https://github.com/sensenx/UAS_PengolahanCitra/assets/120700611/dd3400b2-1561-43df-90ed-e76bfb490877)
- ubah citra dari BGR ke grayscale

- tampilkan 
- buat filter grayscale dan cara pengaplikasiannya
- bilateral-filter untuk mengurangi noise pada citra dan tetap mempertahankan detail tepi gambar
- cv2.Canny untuk bantu deteksi tepi gambar
- setelah itu ambil kontur citra untuk crop plat nomor mobilnya
- cv2.RETR_TREE untuk mengambil semua kontur dengan hirarki lengkap
- konturnya pakai library imutils
- mengurutkan kontur secara descending
- pakai looping
- dan terakhir memastikan citra edge dan biner apakah trus atau tidak
