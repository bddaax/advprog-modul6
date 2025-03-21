# Modul 6 Pemrograman Lanjut : Concurrency
oleh **Brenda Po Lok Fahida**

<br>
<br>

## **Milestone 1: Single Threaded Web Server**

Saat mengikuti langkah-langkah bagian Milestone 1 dalam tutorial ini, saya melakukan research tambahan untuk memahami konsep dan implementasinya dengan lebih baik. Berikut ini adalah refleksi saya berdasarkan pemahaman yang saya peroleh.

Program ini menggunakan `TcpListener` untuk mendengarkan permintaan masuk pada alamat `127.0.0.1:7878`. Setiap kali ada koneksi baru, program akan mencetak **"Connection established!"** di terminal sebagai tanda bahwa koneksi berhasil dibuat. Konsep utama yang digunakan adalah pemanfaatan **Transmission Control Protocol (TCP)**, yang memastikan bahwa data dikirim dengan urutan yang benar dan tanpa kehilangan selama proses komunikasi antara klien dan server.

Beberapa fungsi utama yang digunakan dalam program ini antara lain:

- `bind()` digunakan untuk menghubungkan `TcpListener` dengan alamat dan port tertentu agar dapat menerima koneksi.
- `unwrap()` berguna untuk mengekstrak nilai dari `Result` atau `Option`, tetapi berisiko menyebabkan **panic** jika terjadi error.
- `incoming()` menyediakan iterator yang menangani koneksi yang masuk satu per satu sebelum diproses lebih lanjut.

Untuk menangani koneksi yang diterima, dibuat fungsi `handle_connection()`. Fungsi ini membaca permintaan HTTP dari klien menggunakan `BufReader`, yang membantu dalam membaca **stream data** dari `TcpStream` dan memprosesnya baris per baris. Permintaan HTTP yang diterima dikumpulkan dalam variabel `http_request` dan kemudian ditampilkan di konsol.

Meskipun server ini sudah dapat menerima permintaan, ada beberapa keterbatasan yang perlu diperhatikan:

1. **Single-threaded**: Server hanya dapat menangani satu koneksi dalam satu waktu. Jika ada banyak permintaan masuk secara bersamaan, server bisa mengalami **bottleneck** dan memperlambat respons ke klien.
2. **Tidak ada mekanisme error handling yang optimal**: Penggunaan `unwrap()` berisiko menyebabkan program berhenti jika terjadi kesalahan saat menerima koneksi atau membaca data. Dalam proyek yang lebih besar, **error handling** yang lebih baik sangat penting untuk menjaga stabilitas aplikasi.

Langkah selanjutnya dalam pengembangan server ini adalah meningkatkan fungsionalitasnya agar dapat mengirim respons HTML, serta menerapkan mekanisme multi-threading agar dapat menangani lebih dari satu koneksi dalam satu waktu. Saya akan terus mengikuti tutorial ini untuk memahami lebih dalam bagaimana server bekerja dan bagaimana meningkatkan performanya.

<br>

## **Milestone 2: Returning HTML**

Sebagai bagian dari milestone berikutnya, yaitu Milestone 2: Returning HTML, saya mulai memahami bagaimana server dapat memberikan respons dalam bentuk halaman HTML kepada klien. Pada tahap ini, saya mempelajari cara membaca file HTML dari sistem file dan mengirimkannya sebagai respons HTTP.

Dalam implementasinya, server membaca isi file "hello.html" menggunakan fungsi fs::read_to_string(). File ini kemudian dikirim sebagai bagian dari respons HTTP dengan menyertakan header "Content-Length" untuk memberi tahu browser ukuran konten yang dikirim. Saya juga mempelajari bagaimana format HTTP response bekerja dan pentingnya menyusun header dengan benar agar browser dapat memahami dan merender halaman yang diterima.

Melalui milestone ini, saya semakin memahami bagaimana web server bekerja dalam menangani permintaan dan memberikan respons yang sesuai. Saya juga menyadari pentingnya menangani kesalahan dengan lebih baik, misalnya dengan memeriksa apakah file HTML tersedia sebelum mencoba membacanya, untuk menghindari error yang tidak diharapkan.

Berikut ini adalah dokumentasi pengerjaan Milestone 2 berupa screenshot hasil eksekusi perintah `cargo run` pada `http://127.0.0.1:7878`

<img src='img/commit2.png'>

