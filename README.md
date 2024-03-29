### Commit 1 Reflection notes
Method handle_connection membaca *http request* yang dikirimkan *client* lalu mencetaknya. Parameter *stream* dibungkus dalam BufReader agar dapat dibaca dengan efisien. Setelah itu, `buf_reader.lines()` akan membentuk *iterator* untuk setiap baris pada *stream*. Selanjutnya, untuk setiap result akan dipanggil method `unwrap()` pada `.map(|result| result.unwrap())` yang akan mengembalikan String dalam result jika resultnya Ok dan akan panik jika resultnya Err. `.take_while(|line| !line.is_empty())` akan terus mengambil baris dari *iterator* sampai barisnya kosong. Seteah itu, string-string yang didapatkan akan disimpan di dalam vector. Terakhir, string-string tersebut dicetak oleh program.

### Commit 2 Reflection notes
![Commit 2 Screen Capture](assets/images/commit2.png)
Method `handle_connection` yang baru memberikan *response* dari *request* yang diterima. Variabel `status_line`, `contents`, dan `length` adalah bagian-bagian dari *response* yang akan dikirimkan. Variabel `status_line` berisi bagian *status line* dari HTTP response yang mengirimkan status Ok. Variabel `contents` berisi bentuk String dari `hello.html` yang dikirimkan sebagai *body* dari HTTP response. Variabel `length` berisi panjang dari `contents` yang diperlukan dalam header 'Content-Length' HTTP response. Setelah diformat, response dikirimkan ke *client* oleh kode `stream.write_all(response.as_bytes()).unwrap();`

### Commit 3 Reflection notes
![Commit 3 Screen Capture](assets/images/commit3.png)
Sebelumnya, program akan mengembalikan `hello.html` apapun bentuk requestnya. Oleh karena itu, pada program ditambahkan sebuah *conditional* untuk mengatasi request pada halaman yang tidak dikenali. Pada *chapter* 20, terdapat instruksi untuk implementasinya. Awalnya, terdapat banyak repetisi pada blok *conditional* yang diimplementasikan, yaitu blok `if` dan `else` melakukan *read* dan juga *write*. Oleh karena itu, perlu dilakukan *refactoring* agar kode lebih ringkas.

### Commit 4 Reflection notes
Halaman web dengan *request* `http://127.0.0.1:7878/sleep` memerlukan waktu lebih lama untuk memuat halamannya. Hal ini disebabkan oleh potongan kode `thread::sleep(Duration::from_secs(10));`. Potongan kode tersebut menghentikan eksekusi dari *thread* selama 10 detik. Dengan ini, kita dapat mensimulasikan *slow process* pada program. Response lambat dari web seakan-akan menggambarkan web ketika banyak *request* dari user untuk mengakses halaman.

### Commit 5 Reflection notes
*Thread Pool* adalah sekumpulan *thread* yang menunggu dan siap untuk meng-*handle task*. Ketika program mendapatkan *task*, *task* tersebut akan diberikan kepada salah satu *thread* pada *Thread Pool* untuk diproses. *Thread* sisanya tetap tersedia untuk menangani *task* lain saat *thread* pertama masih memproses *task*nya. Setelah menyelesaikan *task, thread* akan siap untuk menangani *task* yang baru. Dengan *thread pool*, program dapat melakukan pekerjaan secara *concurrent*, sehingga dapat meningkatkan *throughput*. Pada tutorial, jumlah *thread* pada *thread pool* dibatasi untuk menghindari terlalu banyak *thread* yang digunakan untuk menjalankan proses.
