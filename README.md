# Pet Image Classification: Transfer Learning vs Baseline

## 📌 Deskripsi Proyek
Repositori ini berisi eksperimen *Deep Learning* untuk memecahkan masalah klasifikasi citra multi-kelas menggunakan subset dari dataset **Oxford-IIIT Pet** (10 kelas hewan peliharaan: 5 ras anjing dan 5 ras kucing). 

Fokus utama dari studi ini adalah menganalisis disparitas performa, stabilitas pelatihan, dan representasi fitur visual antara model yang dilatih dari awal (*from scratch*) dibandingkan dengan model yang memanfaatkan paradigma *Transfer Learning* (menggunakan *pretrained weights* ImageNet).

## 🧪 Skenario Eksperimen
Proyek ini membandingkan 5 skenario arsitektur dan strategi pelatihan menggunakan framework **PyTorch**:
1. **B1 - Baseline from Scratch:** Melatih arsitektur ResNet-18 dari inisialisasi bobot acak.
2. **B2 - Feature Extraction:** Menggunakan ResNet-18 dengan membekukan (*freeze*) seluruh lapisan ekstraksi fitur, hanya melatih *classifier head*.
3. **B3 - Progressive Fine-Tuning:** Membuka pembekuan pada blok residual terakhir (`layer4`) ResNet-18 dengan implementasi *differential learning rate*.
4. **B4 - Uji Kontrol Tanpa Augmentasi:** Identik dengan B3, namun dilatih tanpa augmentasi citra untuk menganalisis dan mendemonstrasikan kerentanan model terhadap *overfitting*.
5. **B5 - Arsitektur Pembanding (EfficientNet-B0):** Menggunakan model yang jauh lebih ringan untuk membandingkan rasio efisiensi jumlah parameter terhadap performa metrik akhir.

## 📊 Hasil Utama & Analisis
* **Performa Metrik:** Pendekatan *Transfer Learning* (B2, B3, B4) dan *EfficientNet-B0* (B5) secara konsisten mencapai *Macro F1-Score* di atas **0.91**, mengalahkan *Baseline* (B1) yang gagal konvergen dengan baik akibat kelangkaan data terbatas (F1-Score ~0.43).
* **Failure Analysis:** Repositori ini menyertakan skrip ekstraksi otomatis untuk membedah sampel citra yang mengalami misklasifikasi (*edge-cases*) akibat ambiguitas antar ras, oklusi, dan bias pencahayaan.
* **Visualisasi Grad-CAM:** Membuktikan secara empiris bahwa *Progressive Fine-Tuning* berhasil menggeser peta atensi model (*feature maps*) dari sekadar menangkap siluet badan generik menjadi fokus pada fitur morfologis wajah tingkat tinggi yang sangat diskriminatif.

## 🛠️ Teknologi yang Digunakan
* **Model & Framework:** PyTorch, Torchvision (ResNet-18, EfficientNet-B0)
* **Data Processing:** NumPy, Python
* **Visualisasi & Analisis:** Matplotlib, PyTorch Grad-CAM
* **Environment:** Jupyter Notebook / Google Colab

## 📁 Struktur Repositori
* `notebook_eksperimen.ipynb` : *Source code* utama berisi *pipeline preprocessing*, konfigurasi model, pelatihan (dengan *Early Stopping*), visualisasi grafik komparatif, analisis kegagalan, dan Grad-CAM. *(Catatan: sesuaikan nama file ini jika berbeda)*
* `log_hasil_mentah.json` : Catatan riwayat mentah untuk metrik pelatihan (*train/val loss & accuracy*) per *epoch* sebagai bukti integritas eksekusi.
* `README.md` : Dokumentasi repositori.
