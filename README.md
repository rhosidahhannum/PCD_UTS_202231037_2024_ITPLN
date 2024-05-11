
# TAHAPAN PENYELESAIAN UTS
deteksi warna pada citra
langkah pertama mengimpor library:
import cv2: Ini mengimpor pustaka OpenCV, dengan OpenCV, kita dapat melakukan berbagai operasi pada citra, termasuk pembacaan, penulisan, transformasi, segmentasi, deteksi objek, dan banyak lagi.
import matplotlib.pyplot as plt: Ini mengimpor modul pyplot dari pustaka Matplotlib, yang sering digunakan untuk membuat visualisasi data, seperti plot garis, histogram, dan scatter plot. Dalam konteks ini, kita menggunakan pyplot untuk menampilkan gambar dan histogram citra.
import numpy as np: Ini mengimpor pustaka NumPy, yang merupakan pustaka Python yang kuat untuk komputasi numerik. NumPy menyediakan struktur data seperti array dan matriks, serta berbagai fungsi matematika yang memungkinkan kita untuk melakukan manipulasi data numerik dengan mudah dan efisien.
selanjutnya yaitu membaca data gambar:
img=cv2.imread("uts.jpeg"): fungsi imread dari pustaka OpenCV (cv2). Fungsi imread digunakan untuk membaca citra dari file yang disimpan di sistem file dan memuatnya ke dalam variabel img. Parameter pertama yang diberikan ke fungsi imread adalah nama file citra yang ingin dibaca. Dalam hal ini, citra yang dibaca adalah "uts.jpeg". Setelah citra dibaca, data pikselnya akan disimpan dalam variabel img.
img.shape:memanggil atribut shape dari variabel img, yang memberikan dimensi citra dalam format (tinggi, lebar, jumlah saluran warna).
membaca baris dan kolom:
(baris,kolom)=img.shape[:2] :merupakan teknik pengindeksan slicing pada struktur data array yang digunakan oleh OpenCV untuk menyimpan gambar. Dalam konteks ini, img.shape[:2] mengambil dua elemen pertama dari hasil shape, yang mewakili dimensi tinggi dan lebar citra. Kemudian, nilai ini ditugaskan ke variabel baris dan kolom secara berurutan.
img=cv2.cvtColor(img, cv2.COLOR_BGR2RGB):langkah untuk mengonversi citra yang dibaca menggunakan OpenCV dari ruang warna BGR (Blue-Green-Red), yang merupakan format default untuk citra yang dibaca oleh OpenCV, menjadi ruang warna RGB (Red-Green-Blue), yang lebih umum digunakan dalam pemrosesan citra dan visualisasi.
operasi pixel gabungan:
alpa=1.10
beta=5

citra_gabungan =np.zeros((baris,kolom,3))

for x in range(baris):
    for y in range(kolom):
        gcx=(img[x,y]*alpa)+beta
        citra_gabungan[x,y]=gcx

citra_gabungan = citra_gabungan.astype(np.uint8)
fig, axs=plt.subplots(2,2, figsize=(15,5))
axs[0,0].imshow(img)
axs[0,1].hist(img.ravel(),256,[0,256])
axs[1,0].imshow(citra_gabungan)
axs[1,1].hist(citra_gabungan.ravel(),256,[0,256])
plt.show():kode ini merupakan proses penyesuaian kontras dan kecerahan pada citra menggunakan metode operasi aritmatika. Pertama, citra diinisialisasi sebagai larik nol dengan ukuran yang sama dengan citra asli. Selanjutnya, setiap piksel di citra asli dikalikan dengan faktor kontras (alpha) dan ditambahkan dengan faktor kecerahan (beta) untuk mendapatkan citra yang disesuaikan. Setelah itu, citra hasil disajikan dalam skala 0-255 dengan mengonversi tipe data ke np.uint8. Akhirnya, citra asli dan citra hasil, serta histogram keduanya, ditampilkan dalam subplot matriks 2x2 menggunakan Matplotlib.
Mendeteksi warna pada citra:
plt.subplot(2, 2, 1)
plt.imshow(citra_gabungan)
plt.title('Citra Kontras')

plt.subplot(2, 2, 2)
plt.imshow(citra_gabungan[:, :, 0], cmap="gray")
plt.title('Red')

plt.subplot(2, 2, 3)
plt.imshow(citra_gabungan[:, :, 1], cmap="gray")
plt.title('Green')

plt.subplot(2, 2, 4)
plt.imshow(citra_gabungan[:, :, 2], cmap="gray")
plt.title('Blue')

plt.subplots_adjust(wspace=0.4, hspace=0.4)  # Menambahkan jarak antar subplot

plt.show():kode tersebut menggunakan Matplotlib untuk memvisualisasikan citra hasil penyesuaian kontras dan kecerahan bersama dengan komponen warnanya (merah, hijau, biru) dalam subplot matriks 2x2. Pertama, citra hasil penyesuaian kontras dan kecerahan ditampilkan pada subplot pertama dengan judul "Citra Kontras". Selanjutnya, komponen warna merah, hijau, dan biru dari citra hasil tersebut ditampilkan dalam subplot masing-masing dengan judul "Red", "Green", dan "Blue". Setelah itu, fungsi plt.subplots_adjust digunakan untuk menambahkan jarak antara subplot agar tata letaknya lebih teratur. Dengan demikian, visualisasi ini memberikan pandangan yang komprehensif tentang bagaimana penyesuaian kontras dan kecerahan memengaruhi setiap komponen warna dalam citra.
Menampilkan citra warna dan histogram:
fig, axs = plt.subplots(3, 2, figsize=(15, 15))

# Merah
merah = citra_gabungan[:, :, 0]
hist_merah = cv2.calcHist([merah], [0], None, [256], [0, 256])
axs[0, 0].imshow(merah, cmap='gray')
axs[0, 0].set_title('Red')
axs[0, 1].plot(hist_merah, color='r')
axs[0, 1].set_title('Red histogram')

# Hijau
hijau = citra_gabungan[:, :, 1]
hist_hijau = cv2.calcHist([hijau], [0], None, [256], [0, 256])
axs[1, 0].imshow(hijau, cmap='gray')
axs[1, 0].set_title('Green')
axs[1, 1].plot(hist_hijau, color='g')
axs[1, 1].set_title('Green histogram')

# Biru
biru = citra_gabungan[:, :, 2]
hist_biru = cv2.calcHist([biru], [0], None, [256], [0, 256])
axs[2, 0].imshow(biru, cmap='gray')
axs[2, 0].set_title('Blue')
axs[2, 1].plot(hist_biru, color='b')
axs[2, 1].set_title('Blue histogram')

plt.tight_layout() 
plt.show()
:kode tersebut menggunakan Matplotlib untuk membuat subplot matriks 3x2 dengan ukuran figur 15x15. Subplot-subplot ini digunakan untuk menampilkan citra hasil penyesuaian kontras dan kecerahan bersama dengan histogram untuk setiap komponen warnanya (merah, hijau, biru). Pertama, citra komponen merah ditampilkan pada subplot pertama sebelah kiri dengan judul "Red", sementara histogram untuk komponen merah ditampilkan pada subplot sebelah kanan dengan judul "Red histogram". Hal yang sama berlaku untuk komponen hijau pada baris kedua dan komponen biru pada baris ketiga. Fungsi plt.tight_layout() digunakan untuk mengatur tata letak subplot agar lebih rapi. Dengan demikian, visualisasi ini memberikan pemahaman yang lengkap tentang distribusi intensitas piksel untuk setiap komponen warna dalam citra hasil penyesuaian kontras dan kecerahan.
Hasil analisi  citra:
Empat citra dengan skala warna yang berbeda: merah, hijau, dan biru. Masing-masing citra menampilkan teks "RHOSIDAH" dan "HANNUM" dengan ukuran dan posisi yang sama. Citra juga dilengkapi dengan skala kontras di sisi kiri dan atas.
Berdasarkan skala kontras yang tertera pada citra, dapat diketahui bahwa citra merah memiliki kontras yang paling tinggi, diikuti oleh citra hijau, dan terakhir citra biru. Hal ini dapat dilihat dari perbedaan ketajaman teks dan latar belakang pada masing-masing citra. Pada citra merah, teks "RHOSIDAH" dan "HANNUM" terlihat paling jelas dan mudah dibaca, sedangkan pada citra biru teks tersebut terlihat paling buram dan sulit dibaca.
Secara keseluruhan, kualitas citra merah dapat dikatakan lebih baik dibandingkan dengan citra hijau dan biru. Hal ini disebabkan oleh kontras yang lebih tinggi pada citra merah, sehingga detail teks dan latar belakang lebih jelas terlihat. Citra hijau memiliki kualitas yang cukup baik, namun detail teks dan latar belakang tidak sejelas citra merah. Citra biru memiliki kualitas yang paling rendah, karena detail teks dan latar belakang sangat buram dan sulit dibaca.
Dari analisis tsb dapat disimpulkan bahwa citra merah memiliki kualitas yang paling baik dibandingkan dengan citra hijau dan biru. Hal ini disebabkan oleh kontras yang lebih tinggi pada citra merah, sehingga detail teks dan latar belakang lebih jelas terlihat.
Hasil analisi histogram
analisis red-histogram:
Histogram merah merupakan representasi grafis dari distribusi pixel berwarna merah pada gambar. Histogram ini menunjukkan jumlah pixel yang memiliki nilai merah tertentu, mulai dari 0 (hitam) hingga 255 (putih). Puncak tinggi di sisi kanan histogram. Ini menunjukkan bahwa ada banyak pixel dalam gambar yang memiliki nilai merah tinggi. Artinya, gambar secara keseluruhan berwarna merah. Puncak yang lebih kecil di sisi kiri histogram. Ini menunjukkan bahwa ada juga beberapa pixel dalam gambar yang memiliki nilai merah rendah. Ini berarti gambar tidak sepenuhnya merah, tetapi memiliki beberapa warna lain yang tercampur.  Distribusi pixel yang relatif merata di antara kedua puncak. Ini menunjukkan bahwa ada perpaduan nilai merah yang baik dalam gambar, dan gambar tersebut tidak terlalu terang atau kekurangan cahaya. Secara keseluruhan, histogram merah menunjukkan bahwa gambar tersebut adalah foto objek berwarna merah yang terang dengan baik.
analisis green-histogram:
Puncak datar di tengah histogram.  Hal ini menunjukkan keberadaan jumlah piksel yang signifikan dengan nilai  hijau  yang  hampir sama.  Kemungkinan besar pixel ini berasal dari background  gambar  atau  area  warna  hijau  lainnya  pada  gambar.
Kurangnya puncak yang signifikan pada sisi kiri dan kanan histogram.  Hal ini menunjukkan  tidak  banyak  pixel  berwarna  hijau  tua  (nilai  mendekati  255)  atau  hijau  gelap (nilai mendekati 0) pada gambar.  Dengan kata lain,  warna hijau yang ditampilkan  dalam  gambar  memiliki variasi yang rendah.
Berdasarkan analisis, kita bisa menyimpulkan bahwa warna hijau kemungkinan besar bukanlah warna yang dominan pada gambar.
Analisis blue-histogram:
Analisis histogram biru menunjukkan bahwa warna biru bukan warna dominan pada gambar ini. Hal ini terlihat dari puncak dominan pada sisi kiri histogram yang menunjukkan banyaknya pixel dengan nilai biru rendah, mendekati hitam. Hal ini kemungkinan besar disebabkan oleh teks hitam dan latar belakang gelap pada gambar. Kurangnya puncak signifikan di sisi kanan histogram menunjukkan bahwa hanya sedikit pixel dengan nilai biru tinggi, mendekati putih.

Nilai Ambang Batas Pada Citra
hsv_image = cv2.cvtColor(citra_gabungan, cv2.COLOR_RGB2HSV)

lower_blue = np.array([100, 100, 100])
upper_blue = np.array([140, 255, 255])
lower_green = np.array([20, 100, 100])
upper_green = np.array([250, 255, 255])
lower_red1 = np.array([0, 100, 100])
upper_red1 = np.array([10, 255, 255])
lower_red2 = np.array([160, 100, 100])
upper_red2 = np.array([180, 255, 255])
mask_blue = cv2.inRange(hsv_image, lower_blue, upper_blue)

mask_green = cv2.inRange(hsv_image, lower_green, upper_green)

mask_red1 = cv2.inRange(hsv_image, lower_red1, upper_red1)
mask_red2 = cv2.inRange(hsv_image, lower_red2, upper_red2)
mask_red = cv2.bitwise_or(mask_red1, mask_red2)

gray = cv2.cvtColor(citra_gabungan, cv2.COLOR_RGB2GRAY)
fig, axs = plt.subplots (2, 2, figsize=(10,10))

(thresh, binary1) = cv2.threshold(gray, 0, 0, cv2.THRESH_BINARY)
axs[0,0].imshow(binary1, cmap = 'gray')
axs[0,0].set_title('NONE')

plt.subplot(2, 2, 2)
plt.imshow(mask_blue, cmap='gray')
plt.title('Blue')
plt.xticks(np.arange(0, mask_blue.shape[1]+1, 800))
plt.yticks(np.arange(0, mask_blue.shape[0]+1, 500))
plt.axis('on')

plt.subplot(2, 2, 3)
plt.imshow(np.maximum(mask_red, mask_blue), cmap='gray')
plt.title('Reed-Blue')
plt.xticks(np.arange(0, mask_green.shape[1], 800))
plt.yticks(np.arange(0, mask_green.shape[0], 500))
plt.axis('on')

plt.subplot(2, 2, 4)
plt.imshow(mask_green, cmap='gray')
plt.title('Red-Green-Blue')
plt.xticks(np.arange(0, mask_green.shape[1], 800))
plt.yticks(np.arange(0, mask_green.shape[0], 500))
plt.axis('on')

plt.tight_layout()
plt.show()
penjelasan:kode di atas bertujuan untuk melakukan segmentasi warna pada citra gabungan menggunakan metode HSV (Hue, Saturation, Value). Pertama, citra gabungan dikonversi ke ruang warna HSV menggunakan fungsi cv2.cvtColor. Selanjutnya, ditentukan batas atas dan bawah untuk masing-masing warna yang ingin dideteksi dalam citra, seperti biru, hijau, dan merah. Ini dilakukan dengan mendefinisikan rentang nilai untuk setiap komponen HSV yang merepresentasikan warna tersebut.

Setelah itu, masker dibuat untuk setiap warna dengan menggunakan fungsi cv2.inRange, di mana piksel dalam rentang warna yang ditentukan akan ditandai sebagai putih (255) dan piksel di luar rentang akan ditandai sebagai hitam (0). Untuk warna merah, karena rentangnya melintasi nilai batas 0-180 dalam ruang warna HSV, diperlukan dua rentang dan maskernya digabungkan dengan operator bitwise cv2.bitwise_or.

Selanjutnya, citra gabungan dikonversi menjadi citra grayscale untuk keperluan pemrosesan ambang. Metode ambang digunakan untuk menghasilkan citra biner, di mana piksel yang bernilai di atas ambang akan ditandai sebagai putih dan piksel yang di bawahnya akan ditandai sebagai hitam.

Hasil segmentasi untuk masing-masing warna ditampilkan dalam subplot menggunakan matplotlib. Subplot pertama menunjukkan citra biner tanpa segmentasi (NONE), sedangkan subplot-subplot berikutnya menunjukkan hasil segmentasi warna biru, merah-biru, dan hijau. Hal ini memungkinkan untuk melihat bagaimana setiap warna dipisahkan dan digabungkan dalam citra.

Nilai Hasil Ambang Batas
Nilai ambang batas untuk gambar adalah 300. Ini berarti bahwa setiap piksel dengan nilai skala abu-abu 300 atau lebih tinggi akan dianggap putih, sedangkan setiap piksel dengan nilai skala abu-abu 299 atau lebih rendah akan dianggap hitam.
Nilai ambang batas 300 dipilih karena secara efektif memisahkan teks dari latar belakang. Teks umumnya lebih gelap daripada latar belakang, jadi dengan memilih ambang batas yang cukup tinggi, kita dapat memastikan bahwa teks dipertahankan sambil tetap menghilangkan sebagian besar noise latar belakang.

Teori Pendukung

Deteksi Warna pada Citra

Deteksi warna adalah proses mengidentifikasi objek atau area dengan warna tertentu dalam sebuah citra. Hal ini dapat menjadi langkah awal dalam banyak aplikasi pengolahan citra seperti pemrosesan objek, pelacakan objek, atau pemrosesan gambar medis. Dalam deteksi warna, tujuan utama adalah mengekstrak piksel atau area dengan warna yang sesuai dengan kriteria tertentu.

Langkah-langkah Deteksi Warna pada Citra:
1. Praproses Citra:
Sebelum deteksi warna, seringkali perlu dilakukan praproses pada citra untuk memastikan kualitas dan kecocokan ruang warna.

2. Konversi Ruang Warna:
Citra input umumnya berada dalam format ruang warna seperti RGB (Red, Green, Blue). Namun, untuk deteksi warna, seringkali lebih mudah dan lebih efektif menggunakan ruang warna alternatif seperti HSV (Hue, Saturation, Value) atau LAB (Lightness, Green-Red, Blue-Yellow). Konversi ini memungkinkan kita untuk mengekstrak warna berdasarkan karakteristik warna yang lebih intuitif.
3. Tentukan Rentang Warna:
Setelah konversi ruang warna, tentukan rentang warna yang ingin dideteksi. Rentang warna ini dapat ditentukan dengan menentukan nilai batas bawah dan batas atas untuk setiap saluran warna (misalnya, H, S, V untuk ruang warna HSV). Rentang warna dapat diatur berdasarkan nilai tertentu dari saluran warna untuk mengidentifikasi warna tertentu atau berdasarkan range untuk menangkap variasi warna yang lebih luas.

4. Buat Masking:
Dengan menggunakan rentang warna yang telah ditentukan, buat mask untuk menyoroti piksel dalam citra yang cocok dengan kriteria warna tersebut. Ini dapat dilakukan dengan menggunakan fungsi seperti cv2.inRange() dalam OpenCV untuk membuat mask biner.

5. Operasi Morfologi (Opsional):
Terkadang, operasi morfologi seperti dilasi atau erosi dapat diterapkan pada mask untuk memperbaiki kualitas hasil segmentasi. Operasi ini berguna untuk menghilangkan noise kecil atau menghubungkan bagian-bagian yang terpisah dari objek yang sama.
6. Analisis Hasil:
Setelah mendapatkan mask, gunakan mask tersebut untuk menyoroti objek atau area dalam citra yang memiliki warna yang dicari. Hasilnya dapat digunakan untuk berbagai tujuan seperti pelacakan objek, pengukuran, atau pemrosesan lanjutan.

7. Validasi dan Koreksi:
Terakhir, penting untuk melakukan validasi dan koreksi hasil deteksi warna. Ini mungkin melibatkan pengujian pada berbagai kondisi pencahayaan atau variasi warna untuk memastikan keandalan algoritma deteksi.

Deteksi warna pada citra merupakan teknik penting dalam pengolahan citra komputer yang memungkinkan identifikasi objek atau area dengan warna tertentu. Dengan menggunakan langkah-langkah yang tepat seperti konversi ruang warna, penentuan rentang warna, dan penciptaan mask, kita dapat secara efektif mengekstrak objek berwarna dalam citra untuk digunakan dalam berbagai aplikasi pengolahan citra.

Nilai Ambang Batas Citra

Nilai ambang batas citra adalah konsep penting dalam pengolahan citra yang digunakan untuk mengubah citra menjadi citra biner. Citra biner adalah citra di mana setiap pikselnya hanya memiliki dua nilai, yaitu hitam atau putih. Nilai ambang batas menentukan batas di mana piksel akan diklasifikasikan sebagai hitam atau putih berdasarkan intensitasnya.

 Konsep Dasar Nilai Ambang Batas
Ambang Tunggal: Nilai ambang tunggal adalah nilai yang digunakan untuk membagi citra menjadi dua bagian, yaitu piksel dengan intensitas di bawah nilai ambang akan dianggap sebagai bagian hitam dan yang di atasnya sebagai bagian putih.

Ambang Berganda: Dalam beberapa kasus, ambang batas dapat terdiri dari beberapa nilai. Ini memungkinkan segmentasi citra yang lebih fleksibel di mana beberapa area dengan intensitas yang berbeda dapat dikelompokkan bersama.

Metode Penentuan Nilai Ambang Batas
Metode Ambang Tunggal: Metode yang paling sederhana adalah dengan menentukan nilai ambang secara manual berdasarkan pengamatan visual terhadap histogram citra. Ini memerlukan pengetahuan yang baik tentang data dan kualitas citra.

Metode Otsu: Metode Otsu adalah pendekatan otomatis yang mencoba untuk memilih nilai ambang yang memaksimalkan variabilitas antara dua kelas piksel, yaitu hitam dan putih. Ini berguna ketika distribusi intensitas piksel bimodal atau hampir bimodal.

Metode Adaptif: Metode adaptif memungkinkan penyesuaian nilai ambang berdasarkan wilayah atau blok di dalam citra. Ini berguna dalam citra dengan variasi pencahayaan yang besar.

Aplikasi
Segmentasi Citra: Nilai ambang batas digunakan secara luas dalam segmentasi citra untuk memisahkan objek dari latar belakang.

Pengolahan Gambar Medis: Dalam pengolahan gambar medis, citra sering kali disegmentasi untuk mengidentifikasi struktur anatomis atau kelainan.

Pengenalan Tanda Tangan: Dalam pengenalan tanda tangan atau tulisan tangan, nilai ambang batas digunakan untuk memisahkan tinta dari latar belakang.

Nilai ambang batas citra adalah konsep penting dalam pengolahan citra yang memungkinkan konversi citra ke dalam bentuk biner. Dengan menggunakan nilai ambang yang tepat, kita dapat memisahkan objek dari latar belakang dengan efektif, yang merupakan langkah penting dalam banyak aplikasi pengolahan citra modern. Metode penentuan nilai ambang yang tepat sangat bergantung pada karakteristik citra dan kebutuhan aplikasi.









