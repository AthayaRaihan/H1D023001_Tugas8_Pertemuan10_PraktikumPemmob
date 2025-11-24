# Toko Kita 

Aplikasi Flutter untuk manajemen produk dengan fitur CRUD (Create, Read, Update, Delete).

## Deskripsi

Aplikasi ini adalah sistem manajemen produk sederhana yang memungkinkan pengguna untuk:

- Melihat daftar produk
- Menambah produk baru
- Mengubah data produk
- Menghapus produk

## Struktur Aplikasi

### Model (`lib/model/`)

- **`produk.dart`**: Model data produk dengan properti id, kodeProduk, namaProduk, dan hargaProduk. Dilengkapi dengan factory method `fromJson()` untuk parsing data dari API.
  ```
    class Produk {
    String? id;
    String? kodeProduk;
    String? namaProduk;
    var hargaProduk;
    Produk({this.id, this.kodeProduk, this.namaProduk, this.hargaProduk});
    factory Produk.fromJson(Map<String, dynamic> obj) {
      return Produk(
        id: obj['id'],
        kodeProduk: obj['kode_produk'],
        namaProduk: obj['nama_produk'],
        hargaProduk: obj['harga'],
      );
    }
  }

### UI (`lib/ui/`)

#### **`produk_page.dart`**: Halaman utama yang menampilkan daftar produk dalam bentuk ListView. Setiap item produk dapat diklik untuk melihat detail.
- **Penjelasan Code**
  ```
  onTap: () async {
  Navigator.push(
    context,
    MaterialPageRoute(builder: (context) => ProdukForm()),
  );
  }
  ```
  Saat ikon + ditekan, aplikasi berpindah ke halaman form untuk menambah produk baru.
  ```
  Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => ProdukDetail(produk: produk)),
  );
  ```
  Aplikasi akan membuka halaman detail produk (ProdukDetail).

#### **`produk_detail.dart`**: Halaman detail produk yang menampilkan informasi lengkap produk (kode, nama, harga) dengan tombol Edit dan Delete.
- **Penjelasan Code**
  ```
  Text("Kode : ${widget.produk!.kodeProduk}")
  ```
  Pada bagian body, halaman menampilkan: Kode Produk, Nama Produk, Harga Produk
  ```
  Navigator.push(context,
  MaterialPageRoute(
    builder: (context) => ProdukForm(produk: widget.produk!)
  ),
  );
  ```
  Tombol Edit Mengarah ke halaman ProdukForm sambil membawa data produk untuk diedit.
  Tombol Delete Memanggil fungsi confirmHapus() untuk menampilkan dialog konfirmasi sebelum menghapus data.

#### **`produk_form.dart`**: Form untuk menambah atau mengubah data produk. Form ini memiliki validasi input untuk memastikan semua field terisi.
- **Penjelasan Code**
  ```
  Produk? produk;
  ```
  Jika produk ada → berarti sedang mengubah data
  Jika produk null → berarti sedang menambahkan data baru
  ```
  final _kodeProdukTextboxController = TextEditingController();
  final _namaProdukTextboxController = TextEditingController();
  final _hargaProdukTextboxController = TextEditingController();
  ```
  Controller ini digunakan untuk mengisi dan mengambil teks dari textbox.
  ```
    OutlinedButton(
    child: Text(tombolSubmit),
    onPressed: () {
      var validate = _formKey.currentState!.validate();
    },
  );
  ```
  Saat ditekan, hanya mengecek validasi form
  Belum ada proses simpan/update ke database (blok sininya belum dibuat)

#### Bloc (`lib/bloc/`)

- **`produk_bloc.dart`**: Business Logic Component untuk mengelola operasi data produk. Saat ini berisi method `deleteProduk()` yang siap untuk integrasi REST API di pertemuan selanjutnya.
  ```
    class ProdukBloc {
    static Future<bool> deleteProduk({required int id}) async {
      // Untuk sementara return true karena belum menggunakan REST API
      // Nanti akan diimplementasikan dengan API call yang sebenarnya
      await Future.delayed(const Duration(seconds: 1));
      return true;
    }
  }

#### Widget (`lib/widget/`)

- **`warning_dialog.dart`**: Widget dialog custom untuk menampilkan peringatan atau notifikasi kepada pengguna.
  ```
  import 'package:flutter/material.dart';

  class WarningDialog extends StatelessWidget {
    final String? description;
    final VoidCallback? okClick;
  
    const WarningDialog({Key? key, this.description, this.okClick})
      : super(key: key);
  
    @override
    Widget build(BuildContext context) {
      return AlertDialog(
        title: const Text("Warning"),
        content: Text(description!),
        actions: [
          OutlinedButton(
            child: const Text("OK"),
            onPressed: () {
              Navigator.pop(context);
              if (okClick != null) okClick!();
            },
          ),
        ],
      );
    }
  }

## Screenshot
<img width="495" height="968" alt="Screenshot 2025-11-23 141007" src="https://github.com/user-attachments/assets/b181e2ae-f6f3-44f2-b3fd-bf7d1086ccb5" />  
<img width="495" height="968" alt="Screenshot 2025-11-23 141047" src="https://github.com/user-attachments/assets/6a807349-2d18-4add-863d-0224f51cd2a5" /> 
<img width="495" height="968" alt="Screenshot 2025-11-23 141415" src="https://github.com/user-attachments/assets/928f818b-98c2-4e32-a961-f5c8cac637a1" />
<img width="495" height="968" alt="Screenshot 2025-11-23 141453" src="https://github.com/user-attachments/assets/f56af9fe-ee82-4c2d-9149-4b1a9b1d9343" /> 
<img width="495" height="968" alt="Screenshot 2025-11-23 141601" src="https://github.com/user-attachments/assets/d68b5265-0f9b-49a0-8df1-32be8c35d1f7" /> 
<img width="495" height="968" alt="Screenshot 2025-11-23 141621" src="https://github.com/user-attachments/assets/dca3747d-8c28-4a68-891d-1904c8506bc6" />




