# Tugas 7 PBP 2025/2026

## Pertanyaan dan Jawaban

### 1. Jelaskan apa itu widget tree pada Flutter dan bagaimana hubungan parent-child (induk-anak) bekerja antar widget.

Widget tree adalah struktur hierarki berbentuk pohon yang menggambarkan bagaimana widget-widget di Flutter disusun dan saling berhubungan. Setiap widget dapat memiliki widget induk (parent) dan widget anak (child).

**Cara kerja hubungan parent-child:**

- Widget parent "membungkus" atau "mengandung" widget child-nya
- Widget parent bertanggung jawab untuk menentukan posisi, ukuran, dan tampilan widget child
- Widget child mewarisi konteks dan properti tertentu dari parent-nya
- Komunikasi data mengalir dari parent ke child melalui constructor dan properties
- Saat parent di-rebuild, child-nya juga akan di-rebuild

### 2. Sebutkan semua widget yang kamu gunakan dalam proyek ini dan jelaskan fungsinya.

**Widget yang digunakan:**

1. **MaterialApp**: Widget root yang menyediakan konfigurasi dasar aplikasi Material Design, termasuk tema, title, dan halaman home.
2. **Scaffold**: Menyediakan struktur layout dasar Material Design dengan AppBar, Body, Drawer, BottomNavigationBar, dan komponen visual lainnya.
3. **AppBar**: Menampilkan bar di bagian atas aplikasi yang berisi judul dan dapat menampung action buttons.
4. **Text**: Menampilkan teks di layar dengan berbagai styling seperti font weight, size, dan color.
5. **Padding**: Memberikan jarak (padding) di sekitar widget child-nya untuk mengatur spacing.
6. **Column**: Menyusun widget children secara vertikal (dari atas ke bawah).
7. **Row**: Menyusun widget children secara horizontal (dari kiri ke kanan).
8. **InfoCard (Custom Widget)**: Widget custom yang menampilkan informasi dalam bentuk kartu (NPM, Nama, Kelas).
9. **Card**: Widget Material Design yang menampilkan informasi dalam kotak dengan elevation (bayangan).
10. **Container**: Widget serbaguna untuk styling, padding, margin, width, height, dan dekorasi.
11. **SizedBox**: Memberikan jarak dengan ukuran tetap atau membuat box dengan ukuran tertentu.
12. **Center**: Menempatkan child widget di tengah-tengah area yang tersedia.
13. **GridView.count**: Menampilkan children dalam bentuk grid dengan jumlah kolom yang ditentukan.
14. **ItemCard (Custom Widget)**: Widget custom yang menampilkan tombol dalam bentuk kartu dengan ikon dan teks.
15. **Material**: Memberikan efek visual Material Design seperti warna latar belakang dan border radius.
16. **Icon**: Menampilkan ikon dari material icons library.
17. **SnackBar**: Menampilkan pesan singkat di bagian bawah layar.

### 3. Apa fungsi dari widget `MaterialApp`? Jelaskan mengapa widget ini sering digunakan sebagai widget root.

MaterialApp itu kayak "bos besar" di aplikasi Flutter yang ngatur segalanya dari paling atas. Dia yang nentuin tema aplikasi (warna-warna, font, dll), ngatur navigasi antar halaman, dan bikin semua widget Material Design bisa jalan dengan baik.
Kenapa sering jadi widget root? Karena dia itu fondasi dari aplikasi Material Design. Harus ada di paling atas dan jadi pedoman untuk yang lain-lain. Tanpa MaterialApp, widget-widget kayak Scaffold, AppBar, Card, dan temen-temennya bakal error karena mereka butuh "konteks" Material Design yang cuma bisa disediain sama MaterialApp.
Plus, MaterialApp juga bikin hidup kita lebih gampang karena udah include Navigator (buat pindah halaman), Theme (buat styling konsisten), dan banyak fitur lain yang siap pakai. Jadi ya dijadiin root widget aja biar efisien dan ga ribet.

### 4. Jelaskan perbedaan antara `StatelessWidget` dan `StatefulWidget`. Kapan kamu memilih salah satunya?

StatelessWidget itu widget yang immutable atau tidak bisa berubah setelah dibuat. Sekali widget di-render, tampilannya ya gitu aja sampai widget parent-nya rebuild atau widget-nya dihapus dari tree. Widget ini lebih ringan dan efisien karena ga perlu tracking state apapun.Sementara StatefulWidget punya internal state yang bisa berubah-ubah selama aplikasi berjalan. Widget ini terdiri dari dua class: class widget-nya sendiri dan class State. Kita bisa trigger rebuild dengan memanggil setState(), dan Flutter bakal render ulang tampilan sesuai state terbaru. Ini lebih berat dari StatelessWidget karena harus maintain state dan lifecycle-nya lebih kompleks.Kapan pakai yang mana?Pakai StatelessWidget kalau widget cuma perlu render data yang udah final dan ga ada perubahan internal. Contohnya ya widget dalam proyek ini - tombol yang cuma nampilin SnackBar tanpa perlu simpen atau ubah data apapun.Pakai StatefulWidget kalau ada data yang perlu ditrack dan bisa berubah berdasarkan user interaction atau event tertentu. Misalnya form input di mana user bisa ngetik dan kita perlu validasi, atau counter yang angkanya bertambah tiap tombol dipencet, atau checkbox yang bisa di-toggle. Intinya kalau butuh setState() untuk update tampilan, berarti butuh StatefulWidget.

### 5. Apa itu `BuildContext` dan mengapa penting di Flutter? Bagaimana penggunaannya di metode `build`?

BuildContext adalah handle atau reference ke lokasi widget dalam widget tree. Setiap widget punya BuildContext sendiri yang dikasih sama Flutter framework. Ini basically representasi posisi widget dalam hierarki tree.
BuildContext penting karena dia jadi jembatan buat widget untuk akses informasi dari widget-widget di atasnya (ancestor) dalam tree. Tanpa context, widget ga bisa tau apa-apa tentang environment-nya - ga bisa akses theme, ga bisa tau ukuran layar, ga bisa navigasi, dan sebagainya.

Di method build, kita dikasih parameter context yang bisa kita pakai untuk berbagai keperluan. Dalam proyek ini, context dipakai di beberapa tempat: untuk akses warna theme di AppBar (Theme.of(context).colorScheme.primary), untuk bikin InfoCard responsive dengan MediaQuery.of(context).size.width, dan untuk nampilin SnackBar pas tombol diklik dengan ScaffoldMessenger.of(context). Jadi context ini essential banget untuk komunikasi antar widget dalam tree.

### 6. Jelaskan konsep "hot reload" di Flutter dan bagaimana bedanya dengan "hot restart".

Hot Reload adalah fitur Flutter yang inject perubahan source code langsung ke Dart VM yang sedang running tanpa kehilangan state aplikasi. Prosesnya sangat cepat. Saat kita save file atau tekan 'r' di terminal, Flutter compile kode yang berubah, kirim ke running app, dan rebuild widget tree-nya. Yang penting, semua state dan data tetap tersimpan.

Hot Restart itu dia restart aplikasi dari awal, menjalankan ulang method main(), dan menghapus semua state yang ada. Prosesnya lebih lambat. Widget tree dibuat ulang dari nol dan semua initialization code dijalankan lagi.
Bedanya:

Hot Reload (r): cepat, state dipertahankan, ga jalanin ulang main()
Hot Restart (R): lebih lambat, state dihapus, jalanin ulang main()

Hot restart diperlukan kalau ada perubahan fundamental seperti ubah method main(), ubah global variables, tambahin dependencies baru di pubspec.yaml, atau ubah enum values. Kalau hot reload ga kasih hasil yang diharapkan atau ada error aneh, biasanya hot restart bisa solve masalahnya.
