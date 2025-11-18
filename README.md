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

TUGAS 8

1. Jelaskan mengapa kita perlu membuat model Dart saat mengambil/mengirim data JSON? Apa konsekuensinya jika langsung memetakan Map<String, dynamic>?
Jawab: Kita perlu membuat model Dart (seperti class Product yang kita buat via QuickType) untuk menjamin Type Safety (keamanan tipe data) dan struktur data yang jelas.
Mengapa perlu? Dengan model, kita mengubah data JSON yang "liar" menjadi Objek Dart yang terstruktur. Compiler akan tahu persis bahwa product.fields.price itu isinya angka (int), dan product.fields.name itu teks (String). Ini memudahkan kita saat coding karena fitur autocomplete di IDE akan jalan.
Konsekuensi jika pakai Map<String, dynamic> langsung:
- Rawan Error (Human Error): Kita harus mengetik key secara manual, misal data['prce'] (typo kurang 'i'). Error ini tidak akan ketahuan saat koding (compile-time), tapi baru meledak saat aplikasi dijalankan (runtime error).
- Susah di-Maintain: Kita harus hafal struktur JSON-nya. Kalau datanya kompleks, kodingan jadi berantakan dan susah dibaca.
- Tidak Type-Safe: Kita bisa tidak sengaja memasukkan String ke variabel Integer tanpa peringatan dari compiler.

2. Apa fungsi package http dan CookieRequest? Jelaskan peran http vs CookieRequest.
Jawab:
- Package http: Adalah pustaka dasar di Flutter untuk melakukan permintaan HTTP (seperti GET, POST, PUT, DELETE) ke server/API. Ini ibarat "kendaraan" standar untuk ngobrol sama internet.
- CookieRequest (dari pbp_django_auth): Adalah wrapper (pembungkus) di atas package http yang didesain khusus untuk menangani sesi (session) dan cookies.
- Perbedaannya: Package http sifatnya stateless, artinya dia tidak menyimpan informasi sesi antar request. Setiap request dianggap baru. Sedangkan CookieRequest menyimpan cookies (seperti sessionid dari Django) secara otomatis. Ini krusial untuk autentikasi Django, karena tanpa menyimpan cookie, Django akan menganggap pengguna "belum login" di request berikutnya.

3. Jelaskan mengapa instance CookieRequest perlu dibagikan ke semua komponen di aplikasi Flutter.
Jawab: Instance CookieRequest harus dibagikan (biasanya menggunakan Provider di main.dart) karena ia menyimpan state login (session cookie/token) pengguna.
Jika kita membuat instance CookieRequest baru (new CookieRequest()) di setiap halaman (misal di Login Page bikin baru, di Product Page bikin baru lagi), maka cookie yang sudah didapat saat login akan hilang. Akibatnya, saat pindah halaman, aplikasi akan "lupa" bahwa user sudah login, dan user harus login ulang terus-menerus. Dengan membagikan satu instance yang sama (Singleton pattern via Provider), status login tetap terjaga di seluruh aplikasi.

4. Jelaskan konfigurasi konektivitas agar Flutter dapat berkomunikasi dengan Django.
Jawab: Ada beberapa konfigurasi penting agar HP/Emulator bisa ngobrol sama Laptop (Server Django):
- ALLOWED_HOSTS di Django: Kita harus menambahkan IP host, seperti 10.0.2.2, localhost, atau 127.0.0.1 agar Django mau menerima request dari alamat tersebut.
- 10.0.2.2: Ini adalah alamat IP khusus yang digunakan oleh Emulator Android untuk mengakses localhost komputer kita. Kalau kita pakai localhost di emulator, emulator akan menganggap itu dirinya sendiri, bukan komputer kita.
- django-cors-headers (CORS): Browser dan perangkat mobile memiliki fitur keamanan yang memblokir request ke domain yang berbeda (Cross-Origin). Kita perlu mengaktifkan CORS di Django agar server mengizinkan aplikasi Flutter mengambil data.
- AndroidManifest.xml: Kita perlu menambahkan izin <uses-permission android:name="android.permission.INTERNET" /> agar aplikasi Android boleh menggunakan internet.
Apa yang terjadi jika salah? Aplikasi akan mengalami Connection Refused, Network Error, atau 403 Forbidden. Data tidak akan muncul di Flutter.

5. Jelaskan mekanisme pengiriman data mulai dari input hingga dapat ditampilkan pada Flutter.
Jawab:
- Input: Pengguna memasukkan data (misal: nama produk, harga) di Form Flutter.
- Request POST: Saat tombol simpan ditekan, Flutter menggunakan CookieRequest mengirim data tersebut ke endpoint Django (misal: /create-flutter/) via metode POST. Data dikirim dalam format JSON.
- Proses Backend: Django menerima request, memvalidasi data, membuat objek model baru, dan menyimpannya ke database (product.save()). Django mengembalikan respon JSON "Success".
- Request GET: Flutter menerima respon sukses, lalu (biasanya) melakukan navigasi balik ke halaman List atau me-refresh halaman. Flutter melakukan request GET ke endpoint JSON Django (misal: /json/).
- Parsing & Display: Django mengirim daftar produk dalam format JSON. Flutter menerima JSON tersebut, mengubahnya menjadi List of Objects menggunakan Model Dart (Product.fromJson), lalu menampilkannya ke layar menggunakan widget seperti ListView atau GridView.

6. Jelaskan mekanisme autentikasi dari login, register, hingga logout.
Jawab:
- Register:
Flutter mengirim username & password via POST ke endpoint register Django.
Django membuat User baru menggunakan User.objects.create_user().
- Login:
Flutter mengirim username & password via POST ke endpoint login Django menggunakan request.login().
Django memverifikasi kredensial dengan authenticate().
Jika valid, Django membuat session dan mengirimkan cookie sessionid ke Flutter.
CookieRequest di Flutter menyimpan cookie tersebut. Status loggedIn menjadi true.
- Logout:
Flutter memanggil endpoint logout Django (bisa GET/POST).
Django memanggil auth_logout() yang menghapus session di server.
Flutter menerima respon sukses, lalu menghapus/mereset cookie yang tersimpan di CookieRequest lokal dan mengembalikan user ke halaman login.

7. Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step!
Jawab: (Ini rangkuman dari yang lu kerjain tadi)
- Persiapan Backend (Django): Menambahkan django-cors-headers, menambahkan 10.0.2.2 ke ALLOWED_HOSTS, dan membuat view login/logout/register yang mengembalikan JSON.
- Persiapan Frontend (Flutter): Menginstall package provider dan pbp_django_auth.
- Setup Provider: Memodifikasi main.dart untuk membungkus aplikasi dengan Provider yang menyediakan instance CookieRequest.
- Membuat Model: Mengambil contoh JSON dari Django, lalu membuat model Dart (class Product) menggunakan QuickType.
- Halaman Login: Membuat screen Login yang menggunakan request.login() untuk mengirim data akun ke Django.
- Halaman Daftar Item: Mengambil data JSON dari Django menggunakan request.get(), melakukan parsing ke model Product, dan menampilkannya dengan FutureBuilder dan ListView.
- Integrasi: Menambahkan menu di Drawer untuk navigasi antar halaman.
