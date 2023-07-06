# UAS_PengolahanCitra
# SEANNETA APFIA AULIA PRAMESTI - 202131099
praktikum terlampir di file [UAS.ipynb](https://github.com/sensenx/UAS_PengolahanCitra/blob/main/UAS.ipynb) <br>
untuk data citra [ppllatt.jpg](https://github.com/sensenx/UAS_PengolahanCitra/blob/main/ppllatt.jpg) <br>
untuk hasil crop citra biner [platcitrabiner.png](https://github.com/sensenx/UAS_PengolahanCitra/blob/main/platcitrabiner.png) <br>
untuk hasil crop citra grayscale [platcitraedged.png](https://github.com/sensenx/UAS_PengolahanCitra/blob/main/platcitraedged.png) <br>
untuk hasil deskripsi foto melalui kamera hp saya [deskripsi.jpg](https://github.com/sensenx/UAS_PengolahanCitra/blob/main/deskripsi,jpg) <br>

<h3> library yang digunakan : </h3>

* imutils
* opencv
* numpy
* matplotlib

<h3> teori : </h3>

* **Bilateral filter** adalah metode pengolahan citra yang digunakan untuk mengurangi noise atau menghaluskan citra dengan mempertahankan tepi atau detail penting. Filter ini bekerja dengan mempertimbangkan kedua jarak spasial dan perbedaan intensitas piksel. tujuannya untuk mempertahankan tepi atau detail penting dalam citra, karena perbedaan intensitas yang signifikan dianggap sebagai tanda adanya tepi.
* **Contour pada citra kontur** merupakan representasi visual dari bentuk dan struktur dalam citra dan dapat digunakan untuk berbagai tujuan seperti deteksi objek, segmentasi, pengenalan pola, dan analisis bentuk.
* **Mask layer** adalah lapisan tambahan yang digunakan untuk membatasi efek atau operasi tertentu hanya pada area tertentu dalam citra. Biasanya, mask layer memiliki dua nilai piksel yang berbeda: 0 dan 255. Nilai 255 (putih) menandakan area yang dipilih, sementara nilai 0 (hitam) menandakan area yang tidak dipilih. Mask layer ini diterapkan pada citra asli atau lapisan gambar lainnya dalam proses kompositing atau pengeditan citra.
* **Deteksi Tepi** menggunakan Operator Canny, yaitu proses identifikasi dan penyorotan perubahan tajam dalam intensitas piksel di sekitar suatu objek atau struktur dalam citra. Tepi adalah perbatasan atau transisi antara dua wilayah dengan intensitas yang berbeda dalam citra.
* **Citra biner** adalah jenis citra yang hanya memiliki dua nilai piksel yang mungkin, yaitu hitam dan putih. Dalam citra biner, setiap piksel diwakili oleh satu bit informasi, di mana nilai 0 menandakan piksel hitam dan nilai 1 menandakan piksel putih.
* cropped edge untuk memotong data citra yang sudah di deteksi sebelumnya.

<h3> penjelasan : </h3>

* install library yang dibutuhkan, disini saya butuh imutils jadi saya install terlebih dahulu
```python
!pip install imutils
```
* masukkan library yang dibutuhkan
```python
import cv2
from matplotlib import pyplot as plt
import numpy as np
import imutils
```
* masukkan variabel citra ke dalam kode
`cv2.imread`
* ubah citra dari BGR ke grayscale
```python
cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
```
* tampilkan citra dengan warna gray
```python
plt.imshow(gray, cmap='gray')
```
* bilateral-filter untuk mengurangi noise pada citra dan tetap mempertahankan detail tepi gambar
* cv2.Canny untuk bantu deteksi tepi gambar
```python
b_filter = cv2.bilateralFilter(gray, 11, 17, 17)
edged = cv2.Canny(b_filter, 30, 200)
plt.imshow(edged, cmap='gray')
```
* setelah itu ambil kontur citra untuk crop plat nomor mobilnya
* pakai `cv2.findContours` untuk mendapatkan kontur pada citra dengan channel warna tunggal
* pakai `cv2.RETR_TREE` untuk mengambil semua kontur dengan hirarki lengkap
* pakai `cv2.CHAIN_APPROX_SIMPLE` untuk menyimpan data awal dan akhir dari key point
* konturnya pakai library `imutils`
* pakai `imutils.grab_contours` dengan parameter dari titik kunci.
* mengurutkan kontur secara descending lalu memakai `cv2.contourArea`
```python
key_point = cv2.findContours(edged.copy(), cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE)
contours = imutils.grab_contours(key_point)
contours = sorted(contours, key = cv2.contourArea, reverse = True)[:10]
```
* mencari posisi x1, y1 (ukuran panjang) sampai x4, y4 (ukuran lebar) untuk mendapatkan posisi dari plat nomor
```python
location = None
for contour in contours :
    approx = cv2.approxPolyDP(contour, 10, True)
    if len(approx) == 4:
        location = approx
        break
```
* pakai looping untuk memperkirakan posisi kontur plat nomor tersebut
* memunculkan array dari plat nomor menggunakan `location`
* menggambarkan kontur menggunakan mask dan lokasi, isi nilai warna putih (255) ketebalan kontur -1 dan indeks kontur di mulai dari 0
```pyhton
mask = np.zeros(gray.shape, np.uint8)
new_image = cv2.drawContours(mask, [location], 0, 255, -1)
new_image = cv2.bitwise_and(image, image, mask=mask)
```
* lalu kita tampilkan hasil kontur
```python
plt.imshow(new_image, cmap='gray')
```
* kemudian kita potong citra untuk melihat plat nomornya saja
```pyhton
x, y = np.where(mask == 255)
x1, y1 = np.min(x), np.min(y)
x2, y2 = np.max(x), np.max(y)
cropped_image = gray[x1:x2 + 1, y1:y2 +1]
```
> x dan y memiliki nilai mask yaitu 255 <br>
> x1 dan y1 adalah nilai minimum dari x dan y <br>
> x2 dan y2 adalah nilai maksimum dari x dan y <br>
* tampilkan hasil potongan
```python
plt.imshow(cropped_image, cmap='gray')
```
* membuat citra grayscale ke citra biner dan deteksi tepi citra grayscale
```python
cropped_edge = cv2.Canny(cropped_image, 30, 200)
thresh, binary = cv2.threshold(cropped_image, 128, 255, cv2.THRESH_BINARY | cv2.THRESH_OTSU)
```
> untuk merubah ke citra biner pakai nilai ambang 128, di atas 128 putih dan di bawah 128 hitam <br>
* lalu tampilkan hasil citra biner dan citra grayscale
```python
fig, axs = plt.subplots(1, 2, figsize=(15, 5))
axs = axs.ravel()

axs[0].imshow(cropped_edge, cmap='gray')
axs[0].set_title('citraedged')

axs[1].imshow(binary, cmap='gray')
axs[1].set_title('citrabiner')
```
* terakhir, simpan gambar dan memastikan citra grayscale dan biner apakah true atau tidak
```python
cv2.imwrite('./platcitraedged.png', cropped_edge)
cv2.imwrite('./platcitrabiner.png', binary)
```
