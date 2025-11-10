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
- Hot Restart: Merestart seluruh aplikasi dari awal, menghapus semua state. Lebih lambat dari hot reload tapi lebih cepat dari rebuild penuh. Berguna ketika ada perubahan pada state initialization atau perubahan yang memerlukan restart penuh.\

Tugas 8
1. Jelaskan perbedaan antara Navigator.push() dan Navigator.pushReplacement() pada Flutter. Dalam kasus apa sebaiknya masing-masing digunakan pada aplikasi Football Shop kamu?

Perbedaan:
Navigator.push():
- Menambahkan route baru ke atas stack navigasi
- Route sebelumnya tetap ada di dalam stack
- User bisa kembali ke halaman sebelumnya dengan tombol back
- Stack: [Home] → [Home, FormPage]

Navigator.pushReplacement():
- Menggantikan route saat ini dengan route baru
- Route sebelumnya dihapus dari stack
- User tidak bisa kembali ke halaman sebelumnya dengan tombol back
- Stack: [Home] → [FormPage] (Home dihapus)

Penggunaan dalam aplikasi:
Navigator.push() digunakan ketika:
- Navigasi dari HomePage ke FormPage saat menekan tombol "Tambah Produk"
- Navigasi dari Drawer ke FormPage saat memilih "Tambah Produk"
- Karena user perlu bisa kembali ke halaman sebelumnya setelah mengisi form

Navigator.pushReplacement() digunakan ketika:
- Navigasi dari Drawer ke HomePage saat memilih "Halaman Utama"
- Karena kita tidak ingin user kembali ke halaman yang sama berkali-kali (menghindari stack yang menumpuk)
- Menggantikan route saat ini dengan HomePage baru

2. Bagaimana kamu memanfaatkan hierarchy widget seperti Scaffold, AppBar, dan Drawer untuk membangun struktur halaman yang konsisten di seluruh aplikasi?

Dalam aplikasi ini, saya memanfaatkan hierarchy widget untuk menciptakan struktur yang konsisten:
a. Scaffold sebagai Base Structure:
- Scaffold digunakan di setiap halaman (HomePage dan FormPage) sebagai struktur dasar
- Menyediakan kerangka Material Design yang konsisten
- Mengatur AppBar di atas, Drawer di samping, dan Body di tengah
b. AppBar untuk Identitas Halaman:
- Setiap halaman memiliki AppBar dengan warna theme yang sama (Theme.of(context).colorScheme.primary)
- Menampilkan judul yang berbeda sesuai konteks halaman ("Football Shop" vs "Form Tambah Produk Baru")
- Teks berwarna putih untuk konsistensi visual
- Icon back button otomatis muncul ketika ada route sebelumnya dalam stack
c. Drawer untuk Navigasi Global:
- LeftDrawer widget yang sama digunakan di semua halaman
- Memberikan akses navigasi yang konsisten dari mana saja dalam aplikasi
- DrawerHeader dengan branding aplikasi yang sama
- ListTile dengan icon dan teks yang jelas untuk setiap menu
d. Konsistensi Theme:
- Menggunakan Theme.of(context) untuk mengambil warna dari theme global
- Memastikan warna primary, text style, dan spacing konsisten di seluruh aplikasi

Contoh implementasi:
dartScaffold(
  appBar: AppBar(
    title: const Text('Judul Halaman'),
    backgroundColor: Theme.of(context).colorScheme.primary,
  ),
  drawer: const LeftDrawer(), // Widget drawer yang sama
  body: // Konten halaman berbeda-beda
)
Dengan hierarchy ini, setiap halaman memiliki struktur yang familiar bagi user, memudahkan navigasi, dan membuat aplikasi terlihat profesional.\

3. Dalam konteks desain antarmuka, apa kelebihan menggunakan layout widget seperti Padding, SingleChildScrollView, dan ListView saat menampilkan elemen-elemen form? Berikan contoh penggunaannya dari aplikasi kamu.

Kelebihan masing-masing layout widget:
a. Padding:
- Kelebihan: Memberikan ruang/jarak di sekitar widget, membuat UI tidak terlalu rapat dan lebih nyaman dibaca
- Penggunaan dalam aplikasi:

dartPadding(
  padding: const EdgeInsets.all(16.0),
  child: Column(
    children: [
      // Form elements
    ],
  ),
)

- Memberikan jarak 16 pixel di semua sisi form dari tepi layar
- Membuat form tidak menempel di pinggir layar

b. SingleChildScrollView:

Kelebihan:
- Membuat konten bisa di-scroll ketika melebihi tinggi layar
- Mencegah overflow error saat keyboard muncul
- Cocok untuk form yang panjang atau device dengan layar kecil

Penggunaan dalam aplikasi:

dartSingleChildScrollView(
  child: Padding(
    padding: const EdgeInsets.all(16.0),
    child: Column(
      children: [
        TextFormField(...), // Name
        TextFormField(...), // Price
        TextFormField(...), // Description
        // dst...
      ],
    ),
  ),
)

- Membungkus semua elemen form di ProductEntryFormPage
- User bisa scroll untuk melihat semua input field
- Ketika keyboard muncul, form bisa di-scroll untuk melihat field yang tertutup

c. ListView:

Kelebihan:
- Efisien untuk menampilkan list data yang panjang (lazy loading)
- Built-in scrolling behavior
- Cocok untuk data dinamis atau list yang berulang

Penggunaan dalam aplikasi:

dartListView(
  children: [
    DrawerHeader(...),
    ListTile(...), // Halaman Utama
    ListTile(...), // Tambah Produk
  ],
)

- Digunakan di LeftDrawer untuk menampilkan menu navigasi
- Otomatis scrollable jika item menu bertambah banyak

Kombinasi yang Efektif:
Dalam form aplikasi, saya menggunakan kombinasi ketiga widget ini:
- SingleChildScrollView untuk scroll capability
- Padding untuk spacing yang nyaman
- Column di dalam untuk menyusun form fields secara vertikal

Hasilnya: Form yang responsif, nyaman digunakan, dan tidak overflow di berbagai ukuran layar.

4. Bagaimana kamu menyesuaikan warna tema agar aplikasi Football Shop memiliki identitas visual yang konsisten dengan brand toko?
Untuk menciptakan identitas visual yang konsisten dengan brand Football Shop, saya menerapkan tema warna sebagai berikut:

a. Primary Color - Hijau (Green):
darttheme: ThemeData(
  colorScheme: ColorScheme.fromSeed(seedColor: Colors.green),
  useMaterial3: true,
),

Warna hijau dipilih karena identik dengan lapangan sepak bola
Digunakan sebagai seed color untuk generate ColorScheme yang harmonis
Material 3 memberikan nuansa modern dan clean

b. Aplikasi Warna di Berbagai Komponen:
AppBar:
dartAppBar(
  backgroundColor: Theme.of(context).colorScheme.primary,
  // Menggunakan primary color dari theme (hijau)
)
- Tombol Action:
dart// Tombol dengan warna berbeda untuk membedakan fungsi
ItemHomepage("All Products", Icons.inventory, Colors.blue),
ItemHomepage("My Products", Icons.person, Colors.green),
ItemHomepage("Create Product", Icons.add, Colors.red),

Biru untuk "lihat semua" (informative)
Hijau untuk "produk saya" (sesuai brand/primary)
Merah untuk "tambah" (action/penting)

- Save Button:
dartElevatedButton(
  style: ElevatedButton.styleFrom(
    backgroundColor: Theme.of(context).colorScheme.primary,
    foregroundColor: Colors.white,
  ),
  // Button hijau dengan text putih
)
- DrawerHeader:
dartDrawerHeader(
  decoration: BoxDecoration(
    color: Theme.of(context).colorScheme.primary,
  ),
  // Header drawer dengan warna primary (hijau)
)

c. Konsistensi Visual:
- Semua elemen utama (AppBar, Button, DrawerHeader) menggunakan warna dari Theme.of(context).colorScheme.primary
- Jika ingin mengubah tema, cukup ubah seedColor di satu tempat (main.dart)
- Text di atas background hijau selalu putih untuk kontras yang baik
- Warna sekunder (biru, merah) hanya untuk accent dan differensiasi fungsi

d. Keuntungan Pendekatan Ini:
- Konsisten: Semua halaman memiliki look and feel yang sama
- Maintainable: Mudah mengubah tema tanpa edit banyak file
- Professional: Penggunaan Material Design 3 memberikan tampilan modern
- Brand Identity: Warna hijau menciptakan asosiasi kuat dengan sepak bola

Dengan pendekatan ini, aplikasi Football Shop memiliki identitas visual yang kuat dan mudah dikenali user.
