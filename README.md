# tugas-tambahan-nilai-UTS_123140180

Analisis kode tiap modul

MODUL 1
Analisis
1. Baris 11: if __name__ == '__main__':
-> Ini adalah cara Python untuk mengatakan, "Ketika file ini dijalankan langsung (bukan diimpor oleh program lain), mulailah eksekusi dari sini." Ini memastikan bahwa kode untuk menginisialisasi Pyramid dan menyalakan server hanya berjalan saat diminta secara eksplisit dari terminal.

2. Baris 12-14: Configurator (Menghubungkan View ke URL)
Di dalam blok start tersebut, kode menggunakan objek Configurator Pyramid. Tugas objek ini seperti membuat peta jalan untuk aplikasi. Ia melakukan dua hal penting:
a. Ia mendefinisikan sebuah rute, yang pada dasarnya adalah alamat URL (/).
b. Ia kemudian menghubungkan rute tersebut dengan fungsi hello_world.
Pyramid akan tahu: "Jika ada yang meminta alamat URL dasar (/), panggil fungsi hello_world."

3. Baris 6-8: View (Handler Permintaan)
-> Bagian tengah kode adalah fungsi hello_world(request). Fungsi ini disebut sebagai "view" dan merupakan inti dari aplikasi.
Fungsi ini menerima detail permintaan (request) yang masuk dari browser.
Tugasnya adalah memproses permintaan tersebut (meskipun di sini hanya mengembalikan respons statis) dan kemudian mengembalikan objek Response yang berisi konten yang akan dilihat pengguna (yaitu, string "Hello World!").

4. Baris 15-17: Menerbitkan Aplikasi (Menggunakan WSGI Server)
-> Kode menggunakan konfigurasi yang sudah dibuat untuk mempublikasikan aplikasi menggunakan server Waitress.
Waitress mengambil semua konfigurasi Pyramid (yang sudah diubah menjadi standar WSGI—sebuah antarmuka standar Python untuk aplikasi web) dan mulai mendengarkan permintaan di port yang ditentukan (misalnya, http://localhost:6543).
Inilah yang membuat aplikasi dapat diakses oleh browser.

Extra Credit
1. Mengapa menggunakan print('Incoming request') daripada print 'Incoming request'?
-> Ini adalah perbedaan sintaksis antara versi Python.
Python 2: print adalah statement (pernyataan) dan ditulis tanpa tanda kurung: print 'Hello'.
Python 3: print adalah fungsi dan harus ditulis dengan tanda kurung: print('Hello').

2. Apa yang terjadi jika Anda mengembalikan string HTML? Urutan integer?
a. Mengembalikan string HTML: Aplikasi akan gagal (error). View Pyramid harus mengembalikan objek Response, atau objek lain yang dapat dikonversi menjadi Response (seperti objek exception HTTP), bukan string Python biasa.
b. Mengembalikan urutan integer (list atau tuple dari integer): Aplikasi juga akan gagal. Pyramid tidak tahu bagaimana mengonversi urutan angka menjadi respons web yang valid.

3. Apa yang terjadi jika Anda memasukkan statement yang tidak valid (misalnya print xyz) di fungsi view?
a. Saat browser mencoba mengakses halaman (/), Python akan mencapai baris yang tidak valid tersebut.
b. Server Waitress akan menangkap pengecualian (NameError karena xyz tidak terdefinisi).
c. Aplikasi akan mencetak traceback (laporan kesalahan) lengkap ke konsol terminal tempat Anda menjalankan python app.py.
d. Browser kemungkinan besar akan menerima respons "Internal Server Error" (Kode Status 500).

4. GI dalam WSGI adalah "Gateway Interface". Standar web apa yang menjadi modelnya?
-> Standar web yang menjadi model WSGI adalah CGI (Common Gateway Interface).
Penjelasan: Sama seperti CGI menyediakan antarmuka standar bagi web server (seperti Apache) untuk berinteraksi dengan program eksternal, WSGI menyediakan antarmuka standar bagi web server Python (seperti Waitress) untuk berinteraksi dengan web application framework Python (seperti Pyramid).