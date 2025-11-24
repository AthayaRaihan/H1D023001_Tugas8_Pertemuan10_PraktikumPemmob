# Tugas  9 - Pertemuan 11
Athaya Raihan Anafi <br>
H1D023001 <br>
Shift A <br>

# Toko Kita 
Aplikasi Flutter untuk manajemen produk dengan fitur CRUD (Create, Read, Update, Delete).

## Deskripsi
Aplikasi ini adalah sistem manajemen produk sederhana yang memungkinkan pengguna untuk:
- Login dan Register
- Melihat daftar produk
- Menambah produk baru
- Mengubah data produk
- Menghapus produk

## Proses Register
 a. Screenshoot form dan isi form <br>
 <img width="291" height="658" alt="Screenshot 2025-11-24 222354" src="https://github.com/user-attachments/assets/35d92716-43f4-4623-b3a4-81aa5ae3b409" /><br>
 ini adalah tampilan form register
   - Input form (Gagal register) <br>
     <img width="291" height="658" alt="Screenshot 2025-11-24 222506" src="https://github.com/user-attachments/assets/57e5e3bd-7708-4558-b2dd-8697e5519e99" /><br>
     akan muncul alert jika salah satu form salah untuk pengisiannya
  - Input form (Berhasil register)<br>
    <img width="291" height="658" alt="Screenshot 2025-11-24 222634" src="https://github.com/user-attachments/assets/4a38ecb5-96d6-469f-9671-b44997c4c5dc" /> <br>
    Jika berhasil akan mengeluarkan dialog success register dan klik ok, akan diarahkan ke halaman login
     
## Proses Login
 a. Screenshoot form dan isi form <br>
 <img width="291" height="658" alt="Screenshot 2025-11-24 221505" src="https://github.com/user-attachments/assets/a0a614cb-1135-4d74-9daf-0b949e4d2dc6" /><br>
 ini adalah tampilan form login.
   - Input form (Gagal Login)<br>
     <img width="291" height="658" alt="Screenshot 2025-11-24 221808" src="https://github.com/user-attachments/assets/896c45bd-47f4-4794-b0af-bf0624f9060f" /><br>
     Jika saat input email dan password tidak sesuai dengan yang di daftarkan maka akan muncul dialog gagal login.
   - Input Form (Berhasil Login)<br>
     Jika Login berhaasil akan langsung diarahkan ke halaman list produk (produk_page)

## Proses Create Produk
```
simpan() {
    setState(() {
      _isLoading = true;
    });
    Produk createProduk = Produk(id: null);
    createProduk.kodeProduk = _kodeProdukTextboxController.text;
    createProduk.namaProduk = _namaProdukTextboxController.text;
    createProduk.hargaProduk = int.parse(_hargaProdukTextboxController.text);
    ProdukBloc.addProduk(produk: createProduk).then(
      (value) {
        Navigator.of(context).push(
          MaterialPageRoute(
            builder: (BuildContext context) => const ProdukPage(),
          ),
        );
      },
      onError: (error) {
        showDialog(
          context: context,
          builder: (BuildContext context) => const WarningDialog(
            description: "Simpan gagal, silahkan coba lagi",
          ),
        );
      },
    );
    setState(() {
      _isLoading = false;
    });
  }
```
Untuk fungsi create ada pada function simpan diatas jadi ketika button simpan diklik akan membuat sebuah produk baru yang akan masuk ke dalam database
- Screenshoot<br>
  <img width="291" height="658" alt="Screenshot 2025-11-24 222921" src="https://github.com/user-attachments/assets/217e29bc-22f4-4d01-a666-e1ea4839adcf" />
  <img width="291" height="658" alt="Screenshot 2025-11-24 223213" src="https://github.com/user-attachments/assets/c32deb96-57bc-4c9a-8f68-a217fd1065f1" />

## Proses Edit
```
ubah() {
    setState(() {
      _isLoading = true;
    });
    Produk updateProduk = Produk(id: widget.produk!.id!);
    updateProduk.kodeProduk = _kodeProdukTextboxController.text;
    updateProduk.namaProduk = _namaProdukTextboxController.text;
    updateProduk.hargaProduk = int.parse(_hargaProdukTextboxController.text);
    ProdukBloc.updateProduk(produk: updateProduk).then(
      (value) {
        Navigator.of(context).push(
          MaterialPageRoute(
            builder: (BuildContext context) => const ProdukPage(),
          ),
        );
      },
      onError: (error) {
        showDialog(
          context: context,
          builder: (BuildContext context) => const WarningDialog(
            description: "Permintaan ubah data gagal, silahkan coba lagi",
          ),
        );
      },
    );
    setState(() {
      _isLoading = false;
    });
  }
```
Untuk fungsi edit data ada pada function ubah diatas, jadi ketika dihalaman list produk salah satu produk diklik akan menampilkan form dengan isi yang sama dengan produk yang kita pilih dan bisa mengedit data misal nama atau harganya dan klik ubah, itu akan mengubah data suatu produk yang nantiknya di list produknya juga ikut keubah
- Screenshoot<br>
  <img width="291" height="658" alt="Screenshot 2025-11-24 224722" src="https://github.com/user-attachments/assets/93679342-ae8b-4833-ad7b-536393fc42bd" /><br>
  ketika salah satu produk diklik akan memunculkan halaman detail produk yang ada fitur untuk edit dan delete
  <img width="291" height="658" alt="Screenshot 2025-11-24 223618" src="https://github.com/user-attachments/assets/f164ce68-2fec-4ce4-a410-a788aaa47cf5" />
  <img width="291" height="658" alt="Screenshot 2025-11-24 223708" src="https://github.com/user-attachments/assets/a234be0f-b817-41bb-91cc-dda9bd6cff8e" />

## Proses Delete
```
void confirmHapus() {
    AlertDialog alertDialog = AlertDialog(
      content: const Text("Yakin ingin menghapus data ini?"),
      actions: [
        //tombol hapus
        OutlinedButton(
          child: const Text("Ya"),
          onPressed: () {
            ProdukBloc.deleteProduk(id: int.parse(widget.produk!.id!)).then(
              (value) => {
                Navigator.of(context).push(
                  MaterialPageRoute(builder: (context) => const ProdukPage()),
                ),
              },
              onError: (error) {
                showDialog(
                  context: context,
                  builder: (BuildContext context) => const WarningDialog(
                    description: "Hapus gagal, silahkan coba lagi",
                  ),
                );
              },
            );
          },
        ),
        //tombol batal
        OutlinedButton(
          child: const Text("Batal"),
          onPressed: () => Navigator.pop(context),
        ),
      ],
    );
    showDialog(builder: (context) => alertDialog, context: context);
  }
```
Ketika klik delete akan ada confirm ketika klik ya akan mengarah ke halaman list produk dengan produk yang dihapus itu akan hilang
- Screenshoot <br>
  <img width="291" height="658" alt="Screenshot 2025-11-24 223921" src="https://github.com/user-attachments/assets/e108d599-2999-469c-8182-f7506d62c832" />
  <img width="291" height="658" alt="Screenshot 2025-11-24 224049" src="https://github.com/user-attachments/assets/676e098d-c086-433d-b2bb-92186b80ff51" />

## Proses Logout
Ketika logout diklik maka akan keluar dari halaman list produk dan kembalik ke halaman login <br>
<img width="291" height="658" alt="Screenshot 2025-11-24 224141" src="https://github.com/user-attachments/assets/89eb2980-cdcb-47ed-80a2-4dcf51aee318" />

# Sekian Terima Kasih

  
  

  
  





