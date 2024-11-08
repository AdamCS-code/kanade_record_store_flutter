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
