<details>
<summary> <b> Tugas 7: Elemen Dasar Flutter </b> </summary>


### 1. Apa yang Dimaksud dengan Stateless Widget dan Stateful Widget? Jelaskan Perbedaannya.

- **Stateless Widget**: Stateless widget adalah widget yang **tidak memiliki keadaan (state)** yang dapat berubah setelah widget tersebut dibuat. Widget ini digunakan ketika kontennya statis dan tidak akan berubah selama runtime. Contoh widget stateless dalam Flutter adalah `Text`, `Icon`, atau widget yang hanya menampilkan informasi tetap. Di proyek ini, `MyApp` dan `MyHomePage` adalah contoh dari stateless widget karena tidak memiliki state yang berubah.

- **Stateful Widget**: Sebaliknya, stateful widget adalah widget yang memiliki **keadaan (state)** yang dapat diubah selama runtime. Widget ini cocok digunakan ketika ada data yang perlu diperbarui, seperti form input, animasi, atau perubahan UI berdasarkan aksi pengguna. Pada proyek ini, tidak ada contoh stateful widget, tetapi kita bisa menggunakan widget ini jika kita ingin menyimpan dan memperbarui informasi secara dinamis.

### 2. Widget Apa Saja yang Digunakan pada Proyek Ini dan Fungsinya

Berikut adalah beberapa widget utama yang digunakan pada proyek ini beserta fungsinya:

- **MaterialApp**: Widget utama untuk aplikasi Flutter. Ini mencakup pengaturan tema, judul, dan titik masuk utama aplikasi.
- **Scaffold**: Memberikan struktur dasar untuk halaman aplikasi, seperti `AppBar` dan `body`.
- **AppBar**: Menyediakan bar atas pada halaman aplikasi, tempat kita menampilkan judul atau ikon.
- **Text**: Digunakan untuk menampilkan teks pada UI.
- **Padding**: Menambahkan jarak di sekitar widget agar konten lebih rapi dan tidak menempel langsung ke tepi layar.
- **Row** dan **Column**: Digunakan untuk menyusun widget secara horizontal (Row) atau vertikal (Column).
- **GridView.count**: Membuat grid yang menampilkan daftar item dalam jumlah kolom tertentu.
- **Card**: Menyediakan tampilan kotak dengan bayangan di bawahnya. Cocok digunakan untuk menampilkan data yang berbeda dalam kotak terpisah.
- **InkWell**: Menambahkan efek ripple dan deteksi sentuhan pada widget di dalamnya, berguna untuk membuat tombol atau area yang bisa diklik.
- **SnackBar**: Menampilkan pesan pop-up di bagian bawah layar, sering digunakan untuk memberi feedback atas suatu aksi pengguna.

### 3. Apa Fungsi dari `setState()`? Jelaskan Variabel yang Dapat Terdampak oleh Fungsi Tersebut.

`setState()` adalah fungsi yang **memberitahu Flutter untuk merender ulang** widget yang ada di dalam stateful widget saat terjadi perubahan pada data atau variabel yang mempengaruhi tampilan. Fungsi ini hanya tersedia di stateful widget dan digunakan untuk mengupdate UI sesuai perubahan data. Misalnya, jika ada variabel counter di sebuah stateful widget yang bertambah setiap kali pengguna menekan tombol, kita akan memanggil `setState()` setelah mengubah nilai counter agar tampilan UI terupdate.

Pada proyek ini, karena tidak ada stateful widget, `setState()` tidak digunakan.

### 4. Jelaskan Perbedaan Antara `const` dengan `final`.

- **const**: Variabel atau widget yang dideklarasikan dengan `const` **bersifat konstan pada waktu kompilasi** dan tidak dapat diubah lagi setelah itu. Penggunaan `const` membantu mengoptimalkan performa karena objek ini dibuat hanya sekali dan dipakai kembali (immutable). Pada proyek ini, `const` digunakan pada widget statis seperti `Text` dan `Padding`.
  
- **final**: Variabel yang dideklarasikan dengan `final` **hanya bisa diinisialisasi satu kali** dan nilainya tetap konstan setelah itu, tetapi nilainya baru diketahui pada waktu runtime. Ini berbeda dengan `const` yang nilainya sudah diketahui pada waktu kompilasi.

### 5. Implementasi Checklist di Proyek Ini

Implementasi proyek ini mengikuti checklist yang diberikan:

1. Membuat Proyek Flutter Baru
Untuk membuat proyek baru, berikut command yang saya jalankan.
``` bash
flutter create kanade_record_store
```
2. Membuat struktur widget pada aplikasi
- Buat file baru menu.dart di dalam folder lib untuk menyimpan halaman utama aplikasi.
- Pada file main.dart, buat struktur dasar aplikasi seperti berikut:
```main.dart
import 'package:flutter/material.dart';
import 'menu.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'E-Commerce Demo',
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        colorScheme: ColorScheme.fromSwatch(primarySwatch: Colors.cyan),
        useMaterial3: true,
      ),
      home: MyHomePage(),
    );
  }
}
```
3. Menampilkan tiga tombol (Lihat Daftar Produk, Tambah Produk, dan Logout).
- Di dalam file `menu.dart`, buat halaman utama yang menampilkan tiga tombol (Lihat Daftar Produk, Tambah Produk, dan Logout).
- Tambahkan widget `Scaffold` dengan `AppBar` untuk membuat struktur dasar halaman.
```menu.dart
import 'package:flutter/material.dart';

class MyHomePage extends StatelessWidget {
  final String title = 'Kanade Record Store';

  final List<ItemHomepage> items = [
    ItemHomepage("Lihat Daftar Produk", Icons.store, Colors.red.shade100),
    ItemHomepage("Tambah Produk", Icons.add, Colors.red.shade200),
    ItemHomepage("Logout", Icons.logout, Colors.red.shade300),
  ];

  MyHomePage({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(title, style: TextStyle(color: Colors.white)),
        backgroundColor: Theme.of(context).colorScheme.primary,
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Center(
          child: GridView.count(
            crossAxisCount: 3,
            crossAxisSpacing: 10,
            mainAxisSpacing: 10,
            shrinkWrap: true,
            children: items.map((item) => ItemCard(item)).toList(),
          ),
        ),
      ),
    );
  }
}
```
4. Implementasi `ItemHomePage` and `ItemCard` class pembuat widget tombol 
- Buat class `ItemHomepage` untuk menyimpan data dari setiap tombol yang akan ditampilkan (teks, ikon, dan warna).
- Implementasikan `ItemCard`, yang akan menampilkan tombol interaktif dengan ikon, teks, dan warna tertentu. Saat ditekan, ItemCard akan menampilkan `Snackbar`.
```menu.dart
class ItemHomepage {
  final String name;
  final IconData icon;
  final Color color;

  ItemHomepage(this.name, this.icon, this.color);
}

class ItemCard extends StatelessWidget {
  final ItemHomepage item;

  const ItemCard(this.item, {super.key});

  @override
  Widget build(BuildContext context) {
    return Material(
      color: item.color,
      borderRadius: BorderRadius.circular(12),
      child: InkWell(
        onTap: () {
          ScaffoldMessenger.of(context)
            ..hideCurrentSnackBar()
            ..showSnackBar(SnackBar(content: Text("Kamu telah menekan tombol ${item.name}!")));
        },
        child: Container(
          padding: const EdgeInsets.all(8),
          child: Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                Icon(item.icon, color: Colors.white, size: 30.0),
                SizedBox(height: 8.0),
                Text(item.name, textAlign: TextAlign.center, style: TextStyle(color: Colors.white)),
              ],
            ),
          ),
        ),
      ),
    );
  }
}
```
</details>
<details>
<summary> <b> Tugas 8: Flutter Navigation, Layouts, Forms, and Input Elements </b> </summary>

### 1. Apa kegunaan const di Flutter? Jelaskan apa keuntungan ketika menggunakan const pada kode Flutter. Kapan sebaiknya kita menggunakan const, dan kapan sebaiknya tidak digunakan?
const adalah jenis variabel yang immutable (tidak dapat diubah). Keuntungannya, const lebih hemat memori dibandingkan tipe variabel lainnya, seperti var. Waktu yang tepat untuk menggunakan const adalah ketika kita ingin menyimpan nilai yang tidak akan berubah dan sudah ditetapkan saat compile time, misalnya untuk daftar halaman pada drawer. Sebaiknya, const tidak digunakan jika nilai yang disimpan bersifat dinamis, baik yang hanya bisa diatur saat runtime maupun yang bisa berubah-ubah selama runtime.
### 2. Jelaskan dan bandingkan penggunaan Column dan Row pada Flutter. Berikan contoh implementasi dari masing-masing layout widget ini!
Column dan Row adalah widget layout dasar yang digunakan untuk mengatur tata letak widget dalam arah berdasarkan column dan row pada tabel umumnya. column menata letak widget secara horizontal, sementara row menata letak widget secara vertikal.
Contoh penggunaan column:
```
child: Column(
        crossAxisAlignment: CrossAxisAlignment.start,
        children: [
        ...
        ]
)
```
Contoh penggunaan row:
```
Row(
    mainAxisAlignment: MainAxisAlignment.spaceEvenly,
    children: [
      InfoCard(title: 'NPM', content: npm),
      InfoCard(title: 'Name', content: name),
      InfoCard(title: 'Class', content: className),
    ],
  ),
```
### 3.  Sebutkan apa saja elemen input yang kamu gunakan pada halaman form yang kamu buat pada tugas kali ini. Apakah terdapat elemen input Flutter lain yang tidak kamu gunakan pada tugas ini? Jelaskan!
Pengambilan input melalui form yang saya implementasikan hanya menggunakan TextField. TextField digunakan untuk input title, description, dan price dari suatu produk. Alasannya karena saya merasa TextField sudah cukup untuk memenuhi ekspetasi saya terhadap form yang akan dibuat.
### 4. Bagaimana cara kamu mengatur tema (theme) dalam aplikasi Flutter agar aplikasi yang dibuat konsisten? Apakah kamu mengimplementasikan tema pada aplikasi yang kamu buat?
Saya menggunakan ThemeData untuk menjaga agar tema dari aplikasi flutter tetap konsisten. Lebih detail lagi, saya memilih warna cyan sebagai warna utama dalam aplikasi ini. Sehingga pada left_drawer tetap sesuai dengan tema yang diberikan.
### 5. Bagaimana cara kamu menangani navigasi dalam aplikasi dengan banyak halaman pada Flutter?
Flutter bekerja dengan sistem stack. Misalnya, saat pengguna menekan tombol, kita akan menambahkan (push) sebuah Route ke stack Navigator, sehingga halaman tersebut tampil di layar karena berada di posisi teratas. Jika pengguna menekan tombol untuk menuju halaman lain dari halaman tersebut, proses serupa terjadi, yaitu Route baru ditambahkan ke stack. Saat pengguna menekan tombol Back, Navigator akan melakukan pop pada stack (menghapus elemen teratas) dan menampilkan elemen berikutnya. Ini merupakan metode navigasi yang cocok untuk aplikasi mobile yang tidak memerlukan URL seperti di web. Ketika pengguna berada pada elemen terakhir di stack (biasanya halaman utama), keluar dari aplikasi akan menjadi aksi berikutnya.

</details>

<details>
<summary> <b> Tugas 9: Integrasi Layanan Web Django dengan Aplikasi Flutter </b> </summary>

## 1. Jelaskan mengapa kita perlu membuat model untuk melakukan pengambilan ataupun pengiriman data JSON? Apakah akan terjadi error jika kita tidak membuat model terlebih dahulu?
Pembuatan model dalam pengambilan atau pengiriman data JSON dapat memudahkan pengolahan data tersebut. Data yang diterima atau dikirim dapat sesuai dengan tipe data yang seharusnya. Adanya object memudahkan organisasi kode. Apabila tidak membuat model, source code akan menjadi rumit dan rentan terjadi kesalahan tipe data.
## 2. Jelaskan fungsi dari library http yang sudah kamu implementasikan pada tugas ini
Library HTTP yang sudah dibuat itu digunakan untuk request dan response dengan protokol HTTP. Sehingga app flutter dapat mengambil dan mengirim data.
## 3. Jelaskan fungsi dari CookieRequest dan jelaskan mengapa instance CookieRequest perlu untuk dibagikan ke semua komponen di aplikasi Flutter.
CookieRequest adalah mekanisme untuk menyimpan pengguna yang telah login supaya tidak perlu login berulang kali ketika berpindah page. 

## 4. Jelaskan mekanisme pengiriman data mulai dari input hingga dapat ditampilkan pada Flutter.
- pengguna memasukan data melalui form yang tersedia di app.
- flutter mengolah data tersebut menjadi object, kemudian diubah lagi menjadi JSON.
- Backend, dalam hal ini django, mengirimkan json tersebut ke server melalui HTTP request (POST).
- Pengguna mengakses data melalui lihat produk atau sejenisnya, mengirimkan request (GET).
- Django mengembalikan request berupa object json produk yang telah dibuat.

## 5.  Jelaskan mekanisme autentikasi dari login, register, hingga logout. Mulai dari input data akun pada Flutter ke Django hingga selesainya proses autentikasi oleh Django dan tampilnya menu pada Flutter.
Proses Login
1. Pengguna memasukkan email dan kata sandi pada halaman login aplikasi.
2. Ketika tombol Login diklik, data login dikirimkan ke endpoint login Django menggunakan CookieRequest.
3. Django memverifikasi kredensial yang dikirimkan. Jika valid, server mengembalikan cookie autentikasi sebagai tanda berhasil login.
4. Cookie autentikasi disimpan oleh CookieRequest untuk digunakan pada permintaan berikutnya.
5. Tampilkan Menu Utama: Setelah login berhasil, aplikasi menampilkan menu utama sesuai status login pengguna.

Proses Registrasi
1. Input Data: Pengguna mengisi informasi akun seperti nama, email, dan kata sandi pada formulir registrasi.
2. Kirim Permintaan: Ketika tombol Register diklik, data yang diisi dikirimkan ke endpoint registrasi Django menggunakan HTTP request atau CookieRequest.
3. Proses di Backend:
- Django menyimpan data pengguna baru ke dalam database.
- Server memberikan respons sukses atau error.
4. Notifikasi:
- Aplikasi menampilkan pesan sukses atau error berdasarkan respons server.
- Jika berhasil, pengguna diarahkan ke halaman login untuk masuk ke aplikasi.

Proses Logout
1. Permintaan Logout: Ketika tombol Logout diklik, aplikasi mengirimkan permintaan ke endpoint logout Django menggunakan CookieRequest.
2. Hapus Cookie: Django menghapus sesi autentikasi pengguna di server.
3. Perbarui Status Login: Aplikasi memperbarui status pengguna menjadi tidak login.
4. Navigasi ke Halaman Login: Setelah logout berhasil, pengguna diarahkan kembali ke halaman login.

## Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step! (bukan hanya sekadar mengikuti tutorial).
### 1. Backend
- Django digunakan untuk melakukan http request/response untuk mendapatkan ataupun mengirim data.
- Saya membuat app baru di project django untuk web sebelumnya bernama "authentikasi" yang mengatur request untuk login, register, dan logout.
- setelah itu saya melakukan konfigurasi project pada app yang baru dibuat. beserta juga dengan instalasi package.
- pada views.py, saya mengimplementasikan fungsi terkait dengan fungsionalitas authentikasi
- Setelah itu, saya juga menambahkan routing agar metode di view dapat digunakan.
### 2. Frontend
- Awalnya saya membuat laman buat registrasi dan login. yang berisi informasi untuk authentikasi.
```register.dart
import 'dart:convert';
import 'package:flutter/material.dart';
import 'package:kanade_record_store/screens/login.dart';
import 'package:pbp_django_auth/pbp_django_auth.dart';
import 'package:provider/provider.dart';

class RegisterPage extends StatefulWidget {
  const RegisterPage({super.key});

  @override
  State<RegisterPage> createState() => _RegisterPageState();
}

class _RegisterPageState extends State<RegisterPage> {
  final _usernameController = TextEditingController();
  final _passwordController = TextEditingController();
  final _confirmPasswordController = TextEditingController();

  @override
  Widget build(BuildContext context) {
    final request = context.watch<CookieRequest>();
    return Scaffold(
      appBar: AppBar(
        title: const Text('Register'),
        leading: IconButton(
          icon: const Icon(Icons.arrow_back),
          onPressed: () {
            Navigator.pop(context);
          },
        ),
      ),
      body: Center(
        child: SingleChildScrollView(
          padding: const EdgeInsets.all(16.0),
          child: Card(
            elevation: 8,
            shape: RoundedRectangleBorder(
              borderRadius: BorderRadius.circular(12.0),
            ),
            child: Padding(
              padding: const EdgeInsets.all(20.0),
              child: Column(
                mainAxisSize: MainAxisSize.min,
                children: <Widget>[
                  const Text(
                    'Register',
                    style: TextStyle(
                      fontSize: 24.0,
                      fontWeight: FontWeight.bold,
                    ),
                  ),
                  const SizedBox(height: 30.0),
                  TextFormField(
                    controller: _usernameController,
                    decoration: const InputDecoration(
                      labelText: 'Username',
                      hintText: 'Enter your username',
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.all(Radius.circular(12.0)),
                      ),
                      contentPadding:
                          EdgeInsets.symmetric(horizontal: 12.0, vertical: 8.0),
                    ),
                    validator: (value) {
                      if (value == null || value.isEmpty) {
                        return 'Please enter your username';
                      }
                      return null;
                    },
                  ),
                  const SizedBox(height: 12.0),
                  TextFormField(
                    controller: _passwordController,
                    decoration: const InputDecoration(
                      labelText: 'Password',
                      hintText: 'Enter your password',
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.all(Radius.circular(12.0)),
                      ),
                      contentPadding:
                          EdgeInsets.symmetric(horizontal: 12.0, vertical: 8.0),
                    ),
                    obscureText: true,
                    validator: (value) {
                      if (value == null || value.isEmpty) {
                        return 'Please enter your password';
                      }
                      return null;
                    },
                  ),
                  const SizedBox(height: 12.0),
                  TextFormField(
                    controller: _confirmPasswordController,
                    decoration: const InputDecoration(
                      labelText: 'Confirm Password',
                      hintText: 'Confirm your password',
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.all(Radius.circular(12.0)),
                      ),
                      contentPadding:
                          EdgeInsets.symmetric(horizontal: 12.0, vertical: 8.0),
                    ),
                    obscureText: true,
                    validator: (value) {
                      if (value == null || value.isEmpty) {
                        return 'Please confirm your password';
                      }
                      return null;
                    },
                  ),
                  const SizedBox(height: 24.0),
                  ElevatedButton(
                    onPressed: () async {
                      String username = _usernameController.text;
                      String password1 = _passwordController.text;
                      String password2 = _confirmPasswordController.text;

                      // Cek kredensial
                      // TODO: Ganti URL dan jangan lupa tambahkan trailing slash (/) di akhir URL!
                      // Untuk menyambungkan Android emulator dengan Django pada localhost,
                      // gunakan URL http://10.0.2.2/
                      final response = await request.postJson(
                          "http://localhost:8000/auth/register/",
                          jsonEncode({
                            "username": username,
                            "password1": password1,
                            "password2": password2,
                          }));
                      if (context.mounted) {
                        if (response['status'] == 'success') {
                          ScaffoldMessenger.of(context).showSnackBar(
                            const SnackBar(
                              content: Text('Successfully registered!'),
                            ),
                          );
                          Navigator.pushReplacement(
                            context,
                            MaterialPageRoute(
                                builder: (context) => const LoginPage()),
                          );
                        } else {
                          ScaffoldMessenger.of(context).showSnackBar(
                            const SnackBar(
                              content: Text('Failed to register!'),
                            ),
                          );
                        }
                      }
                    },
                    style: ElevatedButton.styleFrom(
                      foregroundColor: Colors.white,
                      minimumSize: Size(double.infinity, 50),
                      backgroundColor: Theme.of(context).colorScheme.primary,
                      padding: const EdgeInsets.symmetric(vertical: 16.0),
                    ),
                    child: const Text('Register'),
                  ),
                ],
              ),
            ),
          ),
        ),
      ),
    );
  }
}
```
kemudian
```login.dart
import 'package:kanade_record_store/screens/menu.dart';
import 'package:flutter/material.dart';
import 'package:pbp_django_auth/pbp_django_auth.dart';
import 'package:provider/provider.dart';
import 'package:kanade_record_store/screens/register.dart';
void main() {
  runApp(const LoginApp());
}

class LoginApp extends StatelessWidget {
  const LoginApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Login',
      theme: ThemeData(
        useMaterial3: true,
        colorScheme: ColorScheme.fromSwatch(
          primarySwatch: Colors.cyan,
        ).copyWith(secondary: Colors.cyan[400]),
      ),
      home: const LoginPage(),
    );
  }
}

class LoginPage extends StatefulWidget {
  const LoginPage({super.key});

  @override
  State<LoginPage> createState() => _LoginPageState();
}

class _LoginPageState extends State<LoginPage> {
  final TextEditingController _usernameController = TextEditingController();
  final TextEditingController _passwordController = TextEditingController();

  @override
  Widget build(BuildContext context) {
    final request = context.watch<CookieRequest>();

    return Scaffold(
      appBar: AppBar(
        title: const Text('Login'),
      ),
      body: Center(
        child: SingleChildScrollView(
          padding: const EdgeInsets.all(16.0),
          child: Card(
            elevation: 8,
            shape: RoundedRectangleBorder(
              borderRadius: BorderRadius.circular(12.0),
            ),
            child: Padding(
              padding: const EdgeInsets.all(20.0),
              child: Column(
                mainAxisSize: MainAxisSize.min,
                children: [
                  const Text(
                    'Login',
                    style: TextStyle(
                      fontSize: 24.0,
                      fontWeight: FontWeight.bold,
                    ),
                  ),
                  const SizedBox(height: 30.0),
                  TextField(
                    controller: _usernameController,
                    decoration: const InputDecoration(
                      labelText: 'Username',
                      hintText: 'Enter your username',
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.all(Radius.circular(12.0)),
                      ),
                      contentPadding:
                          EdgeInsets.symmetric(horizontal: 12.0, vertical: 8.0),
                    ),
                  ),
                  const SizedBox(height: 12.0),
                  TextField(
                    controller: _passwordController,
                    decoration: const InputDecoration(
                      labelText: 'Password',
                      hintText: 'Enter your password',
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.all(Radius.circular(12.0)),
                      ),
                      contentPadding:
                          EdgeInsets.symmetric(horizontal: 12.0, vertical: 8.0),
                    ),
                    obscureText: true,
                  ),
                  const SizedBox(height: 24.0),
                  ElevatedButton(
                    onPressed: () async {
                      String username = _usernameController.text;
                      String password = _passwordController.text;

                      // Cek kredensial
                      // TODO: Ganti URL dan jangan lupa tambahkan trailing slash (/) di akhir URL!
                      // Untuk menyambungkan Android emulator dengan Django pada localhost,
                      // gunakan URL http://10.0.2.2/
                      final response = await request
                          .login("http:/localhost:8000/auth/login/", {
                        'username': username,
                        'password': password,
                      });

                      if (request.loggedIn) {
                        String message = response['message'];
                        String uname = response['username'];
                        if (context.mounted) {
                          Navigator.pushReplacement(
                            context,
                            MaterialPageRoute(
                                builder: (context) => MyHomePage()),
                          );
                          ScaffoldMessenger.of(context)
                            ..hideCurrentSnackBar()
                            ..showSnackBar(
                              SnackBar(
                                  content:
                                      Text("$message Selamat datang, $uname.")),
                            );
                        }
                      } else {
                        if (context.mounted) {
                          showDialog(
                            context: context,
                            builder: (context) => AlertDialog(
                              title: const Text('Login Gagal'),
                              content: Text(response['message']),
                              actions: [
                                TextButton(
                                  child: const Text('OK'),
                                  onPressed: () {
                                    Navigator.pop(context);
                                  },
                                ),
                              ],
                            ),
                          );
                        }
                      }
                    },
                    style: ElevatedButton.styleFrom(
                      foregroundColor: Colors.white,
                      minimumSize: Size(double.infinity, 50),
                      backgroundColor: Theme.of(context).colorScheme.primary,
                      padding: const EdgeInsets.symmetric(vertical: 16.0),
                    ),
                    child: const Text('Login'),
                  ),
                  const SizedBox(height: 36.0),
                  GestureDetector(
                    onTap: () {
                      Navigator.push(
                        context,
                        MaterialPageRoute(
                            builder: (context) => const RegisterPage()),
                      );
                    },
                    child: Text(
                      'Don\'t have an account? Register',
                      style: TextStyle(
                        color: Theme.of(context).colorScheme.primary,
                        fontSize: 16.0,
                      ),
                    ),
                  ),
                ],
              ),
            ),
          ),
        ),
      ),
    );
  }
}
```
- setelah itu saya juga membuat model untuk json saat request maupun request.
- setelah itu saya juga membuat laman untuk menampilkan product yang telah dibuat
</details>