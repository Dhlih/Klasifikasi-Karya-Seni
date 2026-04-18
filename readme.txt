# Deteksi Karya Seni: Manusia vs AI (Human Art vs AI Art Classification)

## Deskripsi Proyek
Proyek ini adalah model penglihatan komputer (Computer Vision) yang dibangun menggunakan TensorFlow dan Keras. Tujuannya adalah untuk mengklasifikasikan apakah sebuah gambar merupakan karya seni buatan manusia (Human Art) atau hasil generasi kecerdasan buatan (AI Art). 

Model ini dirancang untuk mendeteksi detail halus pada gambar dengan menggunakan resolusi tinggi dan arsitektur *Deep Learning* yang sudah terbukti andal.

## Arsitektur Model
Model ini menggunakan arsitektur dasar **ResNet50** dengan teknik *Transfer Learning*.
* **Base Model:** ResNet50 (Pre-trained pada dataset ImageNet, bobot dibekukan pada tahap awal).
* **Input Shape:** 416 x 416 x 3 (Resolusi tinggi untuk menangkap detail pola/tekstur gambar).
* **Custom Top Layers:** * Convolutional 2D (512 filter, ukuran 3x3, aktivasi ReLU)
  * Batch Normalization
  * MaxPooling 2D (ukuran 2x2)
  * Global Average Pooling 2D
  * Fully Connected / Dense Layer (512 neuron, aktivasi ReLU)
  * Dropout (0.3) untuk mencegah *overfitting*
  * Output Layer (1 neuron, aktivasi Sigmoid) untuk klasifikasi biner.
* **Kompilasi:** Optimizer Adam (Learning Rate = 0.0001), Loss function Binary Crossentropy, dengan metrik Akurasi.

## Dataset dan Augmentasi
Data gambar latih (Train Data) diproses menggunakan `ImageDataGenerator` dengan *batch size* 16. Teknik augmentasi dirancang khusus agar model belajar secara generalisasi tanpa merusak esensi lukisan:
* **Rotation Range (10):** Rotasi ringan sebesar 10 derajat.
* **Zoom Range (0.1):** Perbesaran gambar sebesar 10%.
* **Horizontal Flip (True):** Membalik gambar secara horizontal.
* **Width/Height Shift (0.15):** Pergeseran gambar secara horizontal dan vertikal sebesar 15%.
* **Brightness Range (0.8 - 1.2):** Menyimulasikan variasi pencahayaan.
* **Shear Range (0.1):** Menyimulasikan sudut pandang miring pada gambar.
* **Preprocessing:** Menggunakan fungsi bawaan `preprocess_input` dari ResNet50. (Data validasi dan tes hanya menggunakan *preprocessing* ini tanpa augmentasi tambahan).