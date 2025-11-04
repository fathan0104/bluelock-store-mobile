# bluelock_store

A new Flutter project.

## Getting Started

This project is a starting point for a Flutter application.

A few resources to get you started if this is your first Flutter project:

- [Lab: Write your first Flutter app](https://docs.flutter.dev/get-started/codelab)
- [Cookbook: Useful Flutter samples](https://docs.flutter.dev/cookbook)

For help getting started with Flutter development, view the
[online documentation](https://docs.flutter.dev/), which offers tutorials,
samples, guidance on mobile development, and a full API reference.

Tugas 7
1. Jelaskan apa itu widget tree pada Flutter dan bagaimana hubungan parent-child (induk-anak) bekerja antar widget.
Widget tree adalah struktur hierarki dari widget-widget di Flutter. Setiap aplikasi Flutter dimulai dari root widget dan berkembang menjadi pohon widget. Hubungan parent-child bekerja dengan cara:
- Parent widget mengandung dan mengatur child widget
- Child widget mewarisi context dari parent
- Data dan state bisa diturunkan dari parent ke child
- Layout dan constraints ditentukan oleh parent dan diteruskan ke child

2. Sebutkan semua widget yang kamu gunakan dalam proyek ini dan jelaskan fungsinya.
Widget yang umum digunakan:
- MaterialApp - Widget root yang menyediakan material design
- Scaffold - Struktur layout dasar material design dengan AppBar dan Body
- AppBar - Bar di bagian atas aplikasi untuk judul
- GridView atau Column/Row - Untuk layout tombol-tombol
- Card atau Container - Untuk membuat kotak tombol
- Icon - Untuk menampilkan ikon
- Text - Untuk menampilkan teks
- InkWell atau ElevatedButton - Untuk membuat tombol yang bisa diklik
- SnackBar - Untuk menampilkan pesan sementara di bawah layar

3. Apa fungsi dari widget MaterialApp? Jelaskan mengapa widget ini sering digunakan sebagai widget root.
MaterialApp adalah widget yang menyediakan:
- Material Design theming dan styling
- Navigation dan routing system
- Localization support
- Berbagai konfigurasi aplikasi (title, theme, home, dll)
Widget ini sering digunakan sebagai root karena menyediakan fondasi untuk seluruh aplikasi dengan Material Design dan mengelola navigation stack.

4. Jelaskan perbedaan antara StatelessWidget dan StatefulWidget. Kapan kamu memilih salah satunya?
- StatelessWidget: Widget yang tidak memiliki state yang berubah. Tampilannya statis dan tidak berubah setelah dibuat. Gunakan ketika UI tidak perlu update berdasarkan perubahan data.
- StatefulWidget: Widget yang memiliki state yang bisa berubah. Bisa melakukan rebuild ketika state berubah menggunakan setState(). Gunakan ketika UI perlu update dinamis berdasarkan interaksi user atau perubahan data.

5. Apa itu BuildContext dan mengapa penting di Flutter? Bagaimana penggunaannya di metode build?
BuildContext adalah handle ke lokasi widget dalam widget tree. Fungsinya:
- Menyediakan akses ke widget ancestor (parent, grandparent, dll)
- Digunakan untuk mengakses Theme, MediaQuery, Navigator, dll
- Penting untuk menampilkan SnackBar, Dialog, dan navigasi
Di metode build, BuildContext diterima sebagai parameter dan digunakan untuk mengakses informasi kontekstual dan melakukan operasi yang memerlukan pengetahuan tentang posisi widget dalam tree.

6. Jelaskan konsep "hot reload" di Flutter dan bagaimana bedanya dengan "hot restart".
- Hot Reload: Menyuntikkan kode yang diupdate ke dalam Dart VM yang sedang berjalan, mempertahankan state aplikasi. Cepat (< 1 detik) dan cocok untuk perubahan UI. State tidak hilang.
- Hot Restart: Merestart seluruh aplikasi dari awal, menghapus semua state. Lebih lambat dari hot reload tapi lebih cepat dari rebuild penuh. Berguna ketika ada perubahan pada state initialization atau perubahan yang memerlukan restart penuh.
