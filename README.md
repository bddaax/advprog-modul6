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
