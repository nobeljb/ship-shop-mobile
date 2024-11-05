# ship_shop


## 1.  Jelaskan apa yang dimaksud dengan stateless widget dan stateful widget, dan jelaskan perbedaan dari keduanya. 
   - Stateless Widget adalah widget yang tidak memiliki perubahan status setelah pertama kali dirender. Sifatnya tetap, sehingga tidak bisa berubah atau memperbarui dirinya sendiri.
   - Stateful Widget adalah widget yang memiliki status atau data yang dapat berubah-ubah. Ketika terjadi perubahan, widget dapat memperbarui tampilan atau UI.
   Perbedaan utama: Stateful Widget dapat mengubah tampilannya secara dinamis berdasarkan perubahan status internal, sedangkan Stateless Widget tidak bisa.
   
## 2. Sebutkan widget apa saja yang kamu gunakan pada proyek ini dan jelaskan fungsinya.
   - MaterialApp: Root dari aplikasi yang memberikan struktur dasar dan tema.
   - Scaffold: Memberikan struktur halaman dengan AppBar dan body.
   - AppBar: Menampilkan judul pada bagian atas aplikasi.
   - GridView.count: Membuat layout grid dengan jumlah kolom yang sudah ditentukan.
   - Column, Row: Menyusun widget secara vertikal (Column) atau horizontal (Row).
   - InfoCard: Kustom widget untuk menampilkan informasi pengguna seperti NPM, nama, dan kelas.
   - ItemCard: Kustom widget untuk tombol-tombol utama aplikasi.
   - SnackBar: Menampilkan pesan singkat di bagian bawah aplikasi ketika sebuah aksi dilakukan.
   - InkWell: Membuat elemen yang dapat ditekan dengan efek visual.

## 3. Apa fungsi dari setState()? Jelaskan variabel apa saja yang dapat terdampak dengan fungsi tersebut.
   Fungsi setState() digunakan untuk memperbarui tampilan atau UI pada Stateful Widget ketika terjadi perubahan status. Dalam aplikasi ini, kami menggunakan Stateless Widget sehingga setState() tidak diperlukan.

## 4.  Jelaskan perbedaan antara const dengan final.
   - const: Digunakan untuk variabel yang bersifat konstan dan nilainya ditentukan saat kompilasi. Harus memiliki nilai tetap pada saat kompilasi.
     - final: Digunakan untuk variabel yang bersifat tetap, tetapi nilai akhir dapat ditentukan saat runtime.

## 5. Implementasi Checklist di Aplikasi

1. Membuat Program Flutter Baru
Membuat proyek Flutter baru bernama **Ship Shop** dan mengatur struktur dasar aplikasi di `main.dart` sebagai berikut:

```dart
import 'package:flutter/material.dart';
import 'package:ship_shop/menu.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Ship Shop',
      theme: ThemeData(
        colorScheme: ColorScheme.fromSwatch(
          primarySwatch: Colors.orange,
        ).copyWith(secondary: Colors.deepOrange[400]),
        useMaterial3: true,
      ),
      home: MyHomePage(),
    );
  }
}
```

Di sini, Mengatur warna utama aplikasi sebagai `Colors.orange` dengan tema **Material3** dan memuat halaman utama `MyHomePage`.

2. Membuat Tombol Utama
Dalam `menu.dart`, Menambahkan tiga tombol utama menggunakan widget `GridView.count`. Setiap tombol diwakili oleh `ItemCard` yang memiliki ikon, teks, dan warna berbeda.

   ```dart
   class MyHomePage extends StatelessWidget {
     final List<ItemHomepage> items = [
       ItemHomepage("Lihat Daftar Produk", Icons.remove_red_eye_outlined, Colors.lightBlue),
       ItemHomepage("Tambah Produk", Icons.add, Colors.green),
       ItemHomepage("Logout", Icons.logout, Colors.red),
     ];

     @override
     Widget build(BuildContext context) {
       return Scaffold(
         appBar: AppBar(
           title: const Text(
             'Ship Shop',
             style: TextStyle(color: Colors.white, fontWeight: FontWeight.bold),
           ),
           backgroundColor: Theme.of(context).colorScheme.primary,
         ),
         body: Padding(
           padding: const EdgeInsets.all(16.0),
           child: Column(
             children: [
               const Padding(
                 padding: EdgeInsets.only(top: 16.0),
                 child: Text(
                   'Welcome to Ship Shop',
                   style: TextStyle(fontWeight: FontWeight.bold, fontSize: 18.0),
                 ),
               ),
               GridView.count(
                 primary: true,
                 padding: const EdgeInsets.all(20),
                 crossAxisSpacing: 10,
                 mainAxisSpacing: 10,
                 crossAxisCount: 3,
                 shrinkWrap: true,
                 children: items.map((ItemHomepage item) {
                   return ItemCard(item);
                 }).toList(),
               ),
             ],
           ),
         ),
       );
     }
   }
   ```

Tombol-tombol tersebut diatur dalam bentuk **grid** dengan ikon dan teks yang menunjukkan fungsi masing-masing tombol.

3. Implementasi Warna untuk Setiap Tombol
Warna tiap tombol ditetapkan dengan menggunakan `ItemHomepage` yang didefinisikan sebagai berikut:

   ```dart
   class ItemHomepage {
     final String name;
     final IconData icon;
     final Color color;

     ItemHomepage(this.name, this.icon, this.color);
   }
   ```

Menggunakan properti `color` untuk menentukan warna tombol pada masing-masing `ItemCard`.

4. Menampilkan Snackbar saat Tombol Ditekan
Setiap tombol menggunakan widget `InkWell` dengan aksi `onTap` untuk menampilkan **Snackbar** saat ditekan. Implementasinya adalah sebagai berikut:

   ```dart
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
               ..showSnackBar(
                   SnackBar(content: Text("Kamu telah menekan tombol ${item.name}!"))
               );
           },
           child: Container(
             padding: const EdgeInsets.all(8),
             child: Center(
               child: Column(
                 mainAxisAlignment: MainAxisAlignment.center,
                 children: [
                   Icon(
                     item.icon,
                     color: Colors.white,
                     size: 30.0,
                   ),
                   const Padding(padding: EdgeInsets.all(3)),
                   Text(
                     item.name,
                     textAlign: TextAlign.center,
                     style: const TextStyle(color: Colors.white),
                   ),
                 ],
               ),
             ),
           ),
         ),
       );
     }
   }
   ```

**Snackbar** akan muncul sesuai dengan tombol yang ditekan, menampilkan pesan yang relevan seperti, "Kamu telah menekan tombol Lihat Daftar Produk".

5. Informasi Tambahan dengan `InfoCard`
Selain tombol utama, aplikasi ini menampilkan informasi pengguna seperti NPM, nama, dan kelas menggunakan widget `InfoCard`. Berikut adalah implementasinya:

   ```dart
   class InfoCard extends StatelessWidget {
     final String title;
     final String content;

     const InfoCard({super.key, required this.title, required this.content});

     @override
     Widget build(BuildContext context) {
       return Card(
         elevation: 2.0,
         child: Container(
           width: MediaQuery.of(context).size.width / 3.5,
           padding: const EdgeInsets.all(16.0),
           child: Column(
             children: [
               Text(
                 title,
                 style: const TextStyle(fontWeight: FontWeight.bold),
               ),
               const SizedBox(height: 8.0),
               Text(content),
             ],
           ),
         ),
       );
     }
   }
   ```



