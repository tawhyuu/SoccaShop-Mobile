[Tugas 7](../../wiki/Tugas-7-PBP-2025-2026)

# Tugas 8 PBP 2025/2026

## Pertanyaan dan Jawaban

### 1. Jelaskan perbedaan antara `Navigator.push()` dan `Navigator.pushReplacement()` pada Flutter. Dalam kasus apa sebaiknya masing-masing digunakan pada aplikasi Football Shop kamu?

**Perbedaan:**

- **`Navigator.push()`**: Menambahkan route baru ke atas stack navigasi. Route sebelumnya tetap ada di dalam stack, sehingga pengguna dapat kembali ke halaman sebelumnya dengan tombol back. Bagusnya ketika pengguna perlu balik ke halaman sebelumnya, contohnya form product

- **`Navigator.pushReplacement()`**: Menggantikan route yang sedang aktif dengan route baru. Route lama dihapus dari stack, sehingga pengguna tidak dapat kembali ke halaman sebelumnya dengan tombol back. Bagusnya ketika kita tidak ingin pengguna kembali ke halaman sebelumnya

### 2. Bagaimana kamu memanfaatkan hierarchy widget seperti `Scaffold`, `AppBar`, dan `Drawer` untuk membangun struktur halaman yang konsisten di seluruh aplikasi?

Saya memanfaatkan hierarchy widget untuk membangun struktur yang konsisten dengan cara:

1. **`Scaffold`**: Digunakan sebagai struktur dasar pada setiap halaman (menu.dart dan productentry_form.dart). Scaffold menyediakan layout material design standar yang mencakup AppBar, Drawer, dan body.

2. **`AppBar`**:

   - Warna background yang sama menggunakan `Theme.of(context).colorScheme.primary`
   - Teks berwarna putih dan bold
   - Menampilkan judul yang relevan dengan halaman

3. **`Drawer`**: Dibuat sebagai widget terpisah (`LeftDrawer`) yang dapat digunakan ulang di semua halaman. Dengan cara ini:
   - Setiap halaman cukup memanggil `drawer: LeftDrawer()`
   - Drawer memiliki tampilan dan navigasi yang sama di seluruh aplikasi
   - Mudah untuk update drawer di satu tempat saja

### 3. Dalam konteks desain antarmuka, apa kelebihan menggunakan layout widget seperti `Padding`, `SingleChildScrollView`, dan `ListView` saat menampilkan elemen-elemen form? Berikan contoh penggunaannya dari aplikasi kamu.

**Kelebihan masing-masing widget:**

1. **`Padding`**:

   - Memberikan jarak/spacing yang konsisten antar elemen
   - Membuat UI lebih rapi dan mudah dibaca
   - **Contoh:** Membungkus setiap TextFormField

2. **`SingleChildScrollView`**:

   - Memungkinkan konten dapat di-scroll jika melebihi ukuran layar
   - Mencegah overflow error pada layar kecil atau saat keyboard muncul
   - **Contoh:** Membungkus Column yang berisi form

3. **`ListView`**:
   - Efisien untuk menampilkan list item yang banyak (lazy loading)
   - **Contoh:** Digunakan di LeftDrawer untuk menu items

### 4. Bagaimana kamu menyesuaikan warna tema agar aplikasi Football Shop memiliki identitas visual yang konsisten dengan brand toko?

Saya menyesuaikan warna tema dengan cara menggunakan `Theme.of(context).colorScheme.primary` untuk konsistensi di AppBar:

```dart
backgroundColor: Theme.of(context).colorScheme.primary,
foregroundColor: Colors.white,
```

---
