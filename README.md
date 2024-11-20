# ship_shop

# Tugas 7

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


# Tugas 8

## 1. Apa kegunaan const di Flutter? Jelaskan apa keuntungan ketika menggunakan const pada kode Flutter. Kapan sebaiknya saya menggunakan const, dan kapan sebaiknya tidak digunakan?
const di Flutter digunakan untuk mendeklarasikan objek atau widget yang nilainya tetap dan tidak berubah selama aplikasi berjalan. Keuntungan utama menggunakan const adalah:

- Mengurangi Penggunaan Memori: Objek const hanya akan dibuat sekali dan digunakan kembali ketika dibutuhkan.
- Meningkatkan Performa: Flutter tidak perlu membangun widget const berulang kali, yang dapat mengurangi waktu rendering.
- Konsistensi: Menjamin bahwa objek yang sama digunakan setiap kali, sehingga menghindari pembuatan objek yang sama berulang kali.
Penggunaan const sebaiknya dilakukan pada widget yang tidak berubah nilainya setelah dibuat, seperti widget statis (misalnya, teks atau ikon). Hindari menggunakan const untuk widget yang nilainya dinamis atau bergantung pada input pengguna.

## 2. Jelaskan dan bandingkan penggunaan Column dan Row pada Flutter. Berikan contoh implementasi dari masing-masing layout widget ini!
- Column digunakan untuk menata widget secara vertikal (sumbu Y), sedangkan Row digunakan untuk menata widget secara horizontal (sumbu X).
- Column sering digunakan untuk menata form input, daftar item, atau elemen UI lainnya yang lebih panjang, sementara Row cocok untuk menata elemen yang sejajar secara horizontal, seperti ikon atau tombol.

Contoh Column:
```dart
Column(
  mainAxisAlignment: MainAxisAlignment.center,
  children: <Widget>[
    Text('Item 1'),
    Text('Item 2'),
    Text('Item 3'),
  ],
)
```

Contoh Row:
```dart
Row(
  mainAxisAlignment: MainAxisAlignment.center,
  children: <Widget>[
    Icon(Icons.home),
    Icon(Icons.search),
    Icon(Icons.settings),
  ],
)
```

## 3. Sebutkan apa saja elemen input yang kamu gunakan pada halaman form yang kamu buat pada tugas kali ini. Apakah terdapat elemen input Flutter lain yang tidak kamu gunakan pada tugas ini? Jelaskan!

### Pada tugas ini, elemen input yang digunakan pada form adalah:
- TextField: Digunakan untuk input teks, seperti nama produk dan deskripsi produk.
- ElevatedButton: Digunakan sebagai tombol untuk mengirimkan form (misalnya, tombol untuk menambah produk).

### Elemen input lain yang tidak digunakan dalam aplikasi ini, namun bisa digunakan untuk aplikasi lainnya adalah:
- Checkbox: Digunakan untuk memilih ya/tidak.
- Radio: Digunakan untuk memilih satu pilihan dari beberapa opsi.
- DropdownButton: Digunakan untuk memilih opsi dari daftar.
- /Slider: Untuk memilih nilai dalam rentang tertentu.

## 4. Bagaimana cara kamu mengatur tema (theme) dalam aplikasi Flutter agar aplikasi yang dibuat konsisten? Apakah kamu mengimplementasikan tema pada aplikasi yang kamu buat?
Untuk mengatur tema dalam Flutter, gunakan ThemeData yang didefinisikan dalam properti theme pada MaterialApp. Tema ini mengatur warna, teks, dan banyak elemen visual lainnya secara global di seluruh aplikasi. dalam aplikasi ship-shop sebagai berikut.

```dart
MaterialApp(
      title: 'Ship Shop',
      theme: ThemeData(
        colorScheme: ColorScheme.fromSwatch(
          primarySwatch: Colors.orange,
        ).copyWith(secondary: Colors.deepOrange[400]),
        useMaterial3: true,
      ),
      initialRoute: '/',
      routes: {
        '/': (context) => HomePage(),
        '/add-item': (context) => AddItemPage(),
      },
    )
```

## 5. Bagaimana cara kamu menangani navigasi dalam aplikasi dengan banyak halaman pada Flutter?
Navigasi dalam aplikasi Flutter ditangani menggunakan Navigator. Untuk berpindah dari satu halaman ke halaman lain, saya menggunakan Navigator.push dan untuk kembali ke halaman sebelumnya, saya menggunakan Navigator.pop. Pada aplikasi Ship Shop, navigasi dilakukan ketika pengguna menekan item tertentu di menu atau tombol tertentu di halaman utama.

Contoh Implementasi Navigasi pada aplikasi Ship Shop:
Untuk berpindah ke halaman baru (misalnya halaman "Tambah Produk"):

```dart
Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => AddProductPage()),
);
```

Untuk kembali ke halaman sebelumnya:

```dart
Navigator.pop(context);
```

Selain itu, untuk menggunakan named routes, saya bisa mendaftarkan rute di dalam MaterialApp:

```dart
MaterialApp(
  routes: {
    '/addProduct': (context) => AddProductPage(),
  },
)
```

Kemudian, navigasi dapat dilakukan dengan:

```dart
Navigator.pushNamed(context, '/addProduct');
Dengan cara ini, saya dapat menangani navigasi antar halaman dengan mudah dan memastikan pengalaman pengguna yang baik pada aplikasi dengan banyak halaman.
```

# Tugas 9

## 1. Jelaskan mengapa kita perlu membuat model untuk melakukan pengambilan ataupun pengiriman data JSON? Apakah akan terjadi error jika kita tidak membuat model terlebih dahulu?
Model membantu dalam memetakan data JSON ke objek Python, memudahkan manipulasi data dan memastikan integritas data. Tanpa model, kita harus mengelola data mentah secara manual, yang rentan terhadap kesalahan dan inkonsistensi.

## 2. Jelaskan fungsi dari library http yang sudah kamu implementasikan pada tugas ini
Library http digunakan untuk melakukan permintaan HTTP ke server, seperti GET dan POST, untuk mengambil atau mengirim data. Ini memungkinkan aplikasi Flutter untuk berkomunikasi dengan backend Django.

## 3. Jelaskan fungsi dari CookieRequest dan jelaskan mengapa instance CookieRequest perlu untuk dibagikan ke semua komponen di aplikasi Flutter.
CookieRequest digunakan untuk mengelola sesi pengguna di Flutter, memastikan bahwa permintaan HTTP menyertakan cookie sesi yang valid. Instance CookieRequest perlu dibagikan ke semua komponen untuk menjaga konsistensi sesi dan autentikasi di seluruh aplikasi.

## 4. Jelaskan mekanisme pengiriman data mulai dari input hingga dapat ditampilkan pada Flutter.
Data dikirim dari input pengguna di Flutter ke server Django melalui permintaan HTTP. Django memproses data dan mengembalikan respons dalam format JSON. Flutter kemudian menguraikan JSON dan menampilkan data di UI.

## 5. Jelaskan mekanisme autentikasi dari login, register, hingga logout. Mulai dari input data akun pada Flutter ke Django hingga selesainya proses autentikasi oleh Django dan tampilnya menu pada Flutter.
Pengguna memasukkan data akun di Flutter, yang dikirim ke Django untuk registrasi atau login. Django memverifikasi data dan mengembalikan token sesi. Flutter menyimpan token ini dan menggunakannya untuk permintaan selanjutnya. Logout menghapus token sesi

## 6. Implementasi checklist

### Mengimplementasikan fitur registrasi akun pada proyek tugas Flutter.
Baik, berikut adalah langkah-langkah implementasi yang disesuaikan dengan tutorial dari web yang Anda berikan:

### Implementasi Checklist

1. **Mengintegrasikan sistem autentikasi Django dengan proyek tugas Flutter**:
    - **Langkah 1**: Buat aplikasi Django baru bernama `authentication` dan tambahkan ke `INSTALLED_APPS` di `settings.py`.
    - **Langkah 2**: Gunakan `django-rest-framework` dan `django-rest-auth` untuk mengelola autentikasi.
    - **Langkah 3**: Tambahkan `django-cors-headers` untuk mengizinkan permintaan dari aplikasi Flutter. Contoh konfigurasi di `settings.py`:
    ```python
    INSTALLED_APPS = [
        ...
        'corsheaders',
        ...
    ]

    MIDDLEWARE = [
        ...
        'corsheaders.middleware.CorsMiddleware',
        ...
    ]

    CORS_ALLOW_ALL_ORIGINS = True
    CORS_ALLOW_CREDENTIALS = True
    CSRF_COOKIE_SECURE = True
    SESSION_COOKIE_SECURE = True
    CSRF_COOKIE_SAMESITE = 'None'
    SESSION_COOKIE_SAMESITE = 'None'
    ```
    - **Langkah 4**: menyesuaikan views dan url pada autentication untuk login, registrasi, dan logout
    ```python
    #views.py
    import json
    from django.contrib.auth import authenticate, login as auth_login, logout as auth_logout
    from django.http import JsonResponse
    from django.views.decorators.csrf import csrf_exempt
    from django.contrib.auth.models import User

    @csrf_exempt
    def login(request):
        username = request.POST['username']
        password = request.POST['password']
        user = authenticate(username=username, password=password)
        if user is not None:
            if user.is_active:
                auth_login(request, user)
                # Status login sukses.
                return JsonResponse({
                    "username": user.username,
                    "status": True,
                    "message": "Login sukses!"
                    # Tambahkan data lainnya jika ingin mengirim data ke Flutter.
                }, status=200)
            else:
                return JsonResponse({
                    "status": False,
                    "message": "Login gagal, akun dinonaktifkan."
                }, status=401)

        else:
            return JsonResponse({
                "status": False,
                "message": "Login gagal, periksa kembali email atau kata sandi."
            }, status=401)
        
    @csrf_exempt
    def register(request):
        if request.method == 'POST':
            data = json.loads(request.body)
            username = data['username']
            password1 = data['password1']
            password2 = data['password2']

            # Check if the passwords match
            if password1 != password2:
                return JsonResponse({
                    "status": False,
                    "message": "Passwords do not match."
                }, status=400)
            
            # Check if the username is already taken
            if User.objects.filter(username=username).exists():
                return JsonResponse({
                    "status": False,
                    "message": "Username already exists."
                }, status=400)
            
            # Create the new user
            user = User.objects.create_user(username=username, password=password1)
            user.save()
            
            return JsonResponse({
                "username": user.username,
                "status": 'success',
                "message": "User created successfully!"
            }, status=200)
        
        else:
            return JsonResponse({
                "status": False,
                "message": "Invalid request method."
            }, status=400)
        
    @csrf_exempt
    def logout(request):
        username = request.user.username

        try:
            auth_logout(request)
            return JsonResponse({
                "username": username,
                "status": True,
                "message": "Logout berhasil!"
            }, status=200)
        except:
            return JsonResponse({
            "status": False,
            "message": "Logout gagal."
            }, status=401)

      #urls.py
      from django.urls import path
      from authentication.views import login, register, logout

      app_name = 'authentication'

      urlpatterns = [
          path('login/', login, name='login'),
          path('register/', register, name='register'),
          path('logout/', logout, name='logout'),
      ]
      ```

2. **Mengimplementasikan fitur registrasi akun pada proyek tugas Flutter**:
    - **Langkah 1**: Install package provider dan pbp_django_auth
    - **Langkah 2**: bikin file register.dart yang berisi sebagai berikut
    ```dart
    import 'dart:convert';
    import 'package:flutter/material.dart';
    import 'package:ship_shop/screens/login.dart';
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

                          final response = await request.postJson(
                              "http://127.0.0.1:8000/auth/register/",
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

3. **Membuat halaman login pada proyek tugas Flutter**:
    Membuat login.dart yang berisi sebagai berikut
    ```dart
    import 'package:ship_shop/screens/menu.dart';
    import 'package:flutter/material.dart';
    import 'package:pbp_django_auth/pbp_django_auth.dart';
    import 'package:provider/provider.dart';
    import 'package:ship_shop/screens/register.dart';

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
              primarySwatch: Colors.orange,
            ).copyWith(secondary: Colors.deepOrange[400]),
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

                          final response = await request
                              .login("http://127.0.0.1:8000/auth/login/", {
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


4. **Membuat model kustom sesuai dengan proyek aplikasi Django**:
    Membuat model yang menyesuaikan dengan data JSON pada lib/models/product.dart yang berisi sebagai berikut
    ```dart
    // To parse this JSON data, do
    //
    //     final product = productFromJson(jsonString);

    import 'dart:convert';

    List<Product> productFromJson(String str) => List<Product>.from(json.decode(str).map((x) => Product.fromJson(x)));

    String productToJson(List<Product> data) => json.encode(List<dynamic>.from(data.map((x) => x.toJson())));

    class Product {
        String model;
        String pk;
        Fields fields;

        Product({
            required this.model,
            required this.pk,
            required this.fields,
        });

        factory Product.fromJson(Map<String, dynamic> json) => Product(
            model: json["model"],
            pk: json["pk"],
            fields: Fields.fromJson(json["fields"]),
        );

        Map<String, dynamic> toJson() => {
            "model": model,
            "pk": pk,
            "fields": fields.toJson(),
        };
    }

    class Fields {
        int user;
        String name;
        int price;
        String description;
        int quantity;

        Fields({
            required this.user,
            required this.name,
            required this.price,
            required this.description,
            required this.quantity,
        });

        factory Fields.fromJson(Map<String, dynamic> json) => Fields(
            user: json["user"],
            name: json["name"],
            price: json["price"],
            description: json["description"],
            quantity: json["quantity"],
        );

        Map<String, dynamic> toJson() => {
            "user": user,
            "name": name,
            "price": price,
            "description": description,
            "quantity": quantity,
        };
    }
    ```

5. **Membuat halaman yang berisi daftar semua item yang terdapat pada endpoint JSON di Django yang telah kamu deploy**:
    Membuat list_product.dart yang menampilkan name, price, dan description dari masing-masing product, serta tiap product bisa dipencet untuk pindah ke halaman detail tiap product yang berisikan sebagai berikut, Gunakan `Navigator.push` untuk berpindah ke halaman detail saat item ditekan. Contoh kode sudah disertakan di langkah sebelumnya.
    ```dart
    import 'package:flutter/material.dart';
    import 'package:pbp_django_auth/pbp_django_auth.dart';
    import 'package:provider/provider.dart';
    import 'package:ship_shop/models/product.dart';
    import 'package:ship_shop/widgets/left_drawer.dart';
    import 'package:ship_shop/screens/product_detail.dart'; // Import halaman detail

    class ProductPage extends StatefulWidget {
      const ProductPage({super.key});

      @override
      State<ProductPage> createState() => _ProductPageState();
    }

    class _ProductPageState extends State<ProductPage> {
      Future<List<Product>> fetchProduct(CookieRequest request) async {
        final response = await request.get('http://127.0.0.1:8000/json/');
        var data = response;
        List<Product> listProduct = [];
        for (var d in data) {
          if (d != null) {
            listProduct.add(Product.fromJson(d));
          }
        }
        return listProduct;
      }

      @override
      Widget build(BuildContext context) {
        final request = context.watch<CookieRequest>();
        return Scaffold(
          appBar: AppBar(
            title: const Text('Product List',  
            style: TextStyle(
                color: Colors.white,
                fontWeight: FontWeight.bold,
              ),
            ),
            // Warna latar belakang AppBar diambil dari skema warna tema aplikasi.
            backgroundColor: Theme.of(context).colorScheme.primary,
          ),
          drawer: const LeftDrawer(),
          body: FutureBuilder(
            future: fetchProduct(request),
            builder: (context, AsyncSnapshot snapshot) {
              if (snapshot.data == null) {
                return const Center(child: CircularProgressIndicator());
              } else {
                if (!snapshot.hasData) {
                  return const Column(
                    children: [
                      Text(
                        'Belum ada data product pada ship shop.',
                        style: TextStyle(fontSize: 20, color: Color(0xff59A5D8)),
                      ),
                      SizedBox(height: 8),
                    ],
                  );
                } else {
                  return ListView.builder(
                    itemCount: snapshot.data!.length,
                    itemBuilder: (_, index) => GestureDetector(
                      onTap: () {
                        Navigator.push(
                          context,
                          MaterialPageRoute(
                            builder: (context) => ProductDetailPage(
                              product: snapshot.data![index],
                            ),
                          ),
                        );
                      },
                      child: Container(
                        margin:
                            const EdgeInsets.symmetric(horizontal: 16, vertical: 12),
                        padding: const EdgeInsets.all(20.0),
                        decoration: BoxDecoration(
                          border: Border.all(color: Colors.grey),
                          borderRadius: BorderRadius.circular(8.0),
                        ),
                        child: Column(
                          crossAxisAlignment: CrossAxisAlignment.start,
                          children: [
                            Text(
                              "Kapal ${snapshot.data![index].fields.name}",
                              style: const TextStyle(
                                fontSize: 18.0,
                                fontWeight: FontWeight.bold,
                              ),
                            ),
                            const SizedBox(height: 10),
                            Text("\$${snapshot.data![index].fields.price}"),
                            const SizedBox(height: 10),
                            Text("${snapshot.data![index].fields.description}"),
                          ],
                        ),
                      ),
                    ),
                  );
                }
              }
            },
          ),
        );
      }
    }
    ```

6. **Membuat halaman detail untuk setiap item yang terdapat pada halaman daftar Item**:
    Buat product_detail.dart yang menampilkan semua atribut item. Ada tombol `Back` di halaman detail yang menggunakan `Navigator.pop` untuk kembali ke halaman daftar product sebelumnya.
    ```dart
    import 'package:flutter/material.dart';
    import 'package:ship_shop/models/product.dart';
    import 'package:ship_shop/widgets/left_drawer.dart';

    class ProductDetailPage extends StatelessWidget {
      final Product product;

      const ProductDetailPage({Key? key, required this.product}) : super(key: key);

      @override
      Widget build(BuildContext context) {
        return Scaffold(
          appBar: AppBar(
            title: Text(
              "Detail Kapal",
              style: const TextStyle(
                color: Colors.white,
                fontWeight: FontWeight.bold,
              ),
            ),
            backgroundColor: Theme.of(context).colorScheme.primary,
            actions: [
              IconButton(
                icon: const Icon(Icons.share),
                onPressed: () {
                  // Implement sharing functionality if needed.
                },
              ),
            ],
          ),
          drawer: const LeftDrawer(),
          body: SingleChildScrollView(
            padding: const EdgeInsets.all(16.0),
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.start,
              children: [
                // Product Name
                Text(
                  product.fields.name,
                  style: const TextStyle(
                    fontSize: 28.0,
                    fontWeight: FontWeight.bold,
                    color: Colors.black87,
                  ),
                ),
                const SizedBox(height: 10),

                // Product Price with Styled Text
                Row(
                  children: [
                    const Icon(Icons.attach_money, color: Colors.green),
                    Text(
                      "${product.fields.price.toStringAsFixed(2)}",
                      style: const TextStyle(
                        fontSize: 20.0,
                        fontWeight: FontWeight.w600,
                        color: Colors.green,
                      ),
                    ),
                  ],
                ),
                const SizedBox(height: 16),

                // Product Description
                const Text(
                  "Description",
                  style: TextStyle(
                    fontSize: 18.0,
                    fontWeight: FontWeight.bold,
                    color: Colors.black54,
                  ),
                ),
                const SizedBox(height: 8),
                Text(
                  product.fields.description,
                  style: const TextStyle(
                    fontSize: 16.0,
                    color: Colors.black54,
                    height: 1.5,
                  ),
                ),
                const SizedBox(height: 16),

                // Quantity Information
                Row(
                  children: [
                    const Icon(Icons.inventory, color: Colors.blue),
                    const SizedBox(width: 8),
                    Text(
                      "Quantity: ${product.fields.quantity}",
                      style: const TextStyle(
                        fontSize: 16.0,
                        color: Colors.black87,
                      ),
                    ),
                  ],
                ),
                const SizedBox(height: 24),

                // Action Button
                Center(
                  child: ElevatedButton.icon(
                    onPressed: () {
                      Navigator.pop(context);
                    },
                    icon: const Icon(Icons.arrow_back),
                    label: const Text('Back to Product List'),
                    style: ElevatedButton.styleFrom(
                      padding: const EdgeInsets.symmetric(horizontal: 20, vertical: 12),
                      textStyle: const TextStyle(fontSize: 16),
                    ),
                  ),
                ),
              ],
            ),
          ),
        );
      }
    }
    ```

7. **Melakukan filter pada halaman daftar item dengan hanya menampilkan item yang terasosiasi dengan pengguna yang login**:
    telah dihandle saat fungsi show_json pada app main django yang berada , sebagai berikut.
    ```python
    def show_json(request):
    data = Product.objects.filter(user=request.user)
    return HttpResponse(serializers.serialize("json", data), content_type="application/json")
    ```

8. **Finishing**:
    Memastikan semua terintegrasi baik dari django maupun flutternya