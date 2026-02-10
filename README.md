# Panduan Deployment Aplikasi Klasifikasi Kendaraan

Dokumen ini berisi panduan langkah demi langkah untuk men-deploy aplikasi Streamlit Klasifikasi Kendaraan ke internet agar bisa diakses oleh orang lain.

Kami merekomendasikan **Streamlit Cloud** sebagai cara termudah dan gratis untuk hosting aplikasi Streamlit.

## Persiapan

Pastikan Anda memiliki file-file berikut dalam satu folder proyek:
1. `app.py` (Kode utama aplikasi)
2. `requirements.txt` (Daftar library Python)
3. `model_kendaraan.h5` (File model CNN)
4. `packages.txt` (Opsional, jika membutuhkan dependensi sistem khusus)

## Langkah 1: Upload Kode ke GitHub

Streamlit Cloud mengambil kode langsung dari repositori GitHub.

1. **Buat Akun GitHub**: Jika belum punya, daftar di [github.com](https://github.com).
2. **Buat Repository Baru**:
   - Klik tombol **New** di dashboard GitHub.
   - Beri nama repository (misal: `klasifikasi-kendaraan-cnn`).
   - Pilih **Public**.
   - Klik **Create repository**.
3. **Upload File**:
   - Anda bisa menggunakan Git command line atau upload manual via browser.
   - **Cara Upload Manual**:
     - Di halaman repository baru, klik **uploading an existing file**.
     - Drag & drop file `app.py`, `requirements.txt`, dan `model_kendaraan.h5`.
     - **PENTING**: Pastikan file `model_kendaraan.h5` ikut terupload. Jika file > 25MB, GitHub web upload mungkin menolak. Jika file > 100MB, Anda perlu menggunakan Git LFS (Large File Storage).
     - Klik **Commit changes**.

## Langkah 2: Deploy ke Streamlit Cloud

1. Buka [share.streamlit.io](https://share.streamlit.io/).
2. Login menggunakan akun GitHub Anda.
3. Klik tombol **New app**.
4. Isi konfigurasi berikut:
   - **Repository**: Pilih repository yang baru Anda buat (`klasifikasi-kendaraan-cnn`).
   - **Branch**: Biasanya `main` atau `master`.
   - **Main file path**: `app.py`.
5. Klik **Deploy!**.

## Langkah 3: Tunggu Proses Build

- Streamlit Cloud akan mulai memproses aplikasi Anda.
- Sistem akan otomatis menginstal library yang ada di `requirements.txt`.
- Proses ini memakan waktu 1-3 menit.
- Jika berhasil, aplikasi akan terbuka otomatis.

## Troubleshooting Umum

### 1. Error `ModuleNotFoundError`
Artinya ada library yang kurang di `requirements.txt`. Pastikan isinya sudah benar:
```text
streamlit
tensorflow<2.16
pillow
numpy
```

### 2. Error Memory / Resource Limit
Jika aplikasi crash saat loading model, itu mungkin karena model terlalu besar atau memakan banyak RAM. Streamlit Cloud (versi gratis) memiliki batas resource.

### 3. Masalah Versi TensorFlow
Jika muncul error terkait `batch_shape` atau inkompatibilitas Keras, pastikan `requirements.txt` menggunakan `tensorflow<2.16` (seperti yang sudah kita atur).

## Alternatif: Hugging Face Spaces

Jika Streamlit Cloud bermasalah, Anda bisa mencoba **Hugging Face Spaces**:
1. Buat akun di [huggingface.co](https://huggingface.co/).
2. Buat **New Space**.
3. Pilih SDK: **Streamlit**.
4. Upload file-file Anda ke repository Space tersebut.
