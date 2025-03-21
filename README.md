# advprog-modul6

### Commit 1 Reflection Notes
Function `handle_connection` memproses koneksi TCP yang datang, membaca HTTP request per line, dan mem-printnya.

Keyword `mut` menyatakan bahwa stream tersebut mutable. Artinya, function dapat mengubah stream.

`buf_reader` melakukan banyak read tetapi tidak sering sehingga mengurangi system call, dibanding menggunakan `read` yang menggunakan system call tiap kali dipanggil.

Lalu, function akan membaca HTTP request per line dan memprintnya menggunakan format pretty print untuk debugging yaitu `{:#?}`.

---

### Commit 2 Reflection Notes
![Commit 2 screen capture](image.png)
Berbeda dengan sebelumnya, handle_connection kali ini tidak mem-print request, tapi mengirimkan response ke client dalam bentuk html.

Function akan membaca file `hello.html` dan membacanya ke dalam String. Lalu, function akan membuat HTTP response dan mengirimkannya ke client. Hasil dari response tersebut dapat dilihat pada gambar di atas.

---

### Commit 3 Reflection Notes
Sebelumnya, semua HTTP request akan mengirimkan response dari `hello.html`. Sekarang, function akan memeriksa apakah requestnya "GET / HTTP/1.1" (valid) atau tidak. Jika request tidak valid, maka function akan mengirimkan response dari `404.html` yaitu sebuah pesan error.

---

### Commit 4 Reflection Notes
Alasan mengapa `127.0.0.1` lama dimuat setelah membuka `127.0.0.1/sleep` adalah karena server masih meng-handle request `127.0.0.1/sleep` sehingga `127.0.0.1` harus menunggu terlebih dahulu. Hal ini terjadi karena function meng-handle koneksi secara sekuensial (satu per satu), sehingga server akan terasa lebih lama jika ada banyak pengguna yang mengaksesnya sekaligus.

---

### Commit 5 Reflection Notes
Sekarang, `handle_connection` menggunakan ThreadPool agar dapat meng-handle banyak request secara bersamaan agar lebih efisien dan cepat. Sebelumnya, setiap request `pool.execute` membuat thread baru menggunakan `thread::spawn` yang tidak efisien karena membuat dan menghapus thread terus-menerus. Dengan ThreadPool, semua thread dibuat sekali dan digunakan berulang-ulang. Dengan setup sekarang, kita bisa meng-handle sebanyak 4 request secara bersamaan yang ditentukan oleh `ThreadPool::new(4)`.

---

### Commit Bonus Reflection Notes
#### Hal yang di-improve:
* Lebih readable karena lebih konsisten dengan idiom di Rust
* Lebih fleksibel untuk modifikasi atau di extend di masa depan