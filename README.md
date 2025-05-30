# advprog-modul11

Nama: Muhammad Naufal Ramadhan <br>
NPM: 2306241700 <br>
Kelas: B
<hr>

1. Compare the application logs before and after you exposed it as a Service. Try to open the app several times while the proxy into the Service is running. What do you see in the logs? Does the number of logs increase each time you open the app?
![log1](/images/log1.png)
![log2](/images/log2.png)

Sebelum aplikasi diekspos sebagai Service, log aplikasi hanya mencatat proses inisialisasi, yaitu "starting HTTP server on port 8080" dan "starting UDP server on port 8080". Tidak ada log yang menunjukkan adanya `traffic` masuk.

Setelah aplikasi diekspos sebagai Service dan diakses beberapa kali melalui proxy, terlihat adanya log tambahan. Setiap kali aplikasi diakses (misalnya dengan membuka browser atau menggunakan `curl`), log mencatat GET request ke root path (/). Hal ini menunjukkan bahwa aplikasi menerima koneksi dari luar pod. Jumlah log GET request ini akan bertambah sesuai dengan frekuensi akses ke aplikasi, mengonfirmasi bahwa Service berhasil meneruskan traffic ke pod.

2. Notice that there are two versions of `kubectl get` invocation during this tutorial section. The first does not have any option, while the latter has `-n` option with value set to `kube-system`. What is the purpose of the `-n` option and why did the output not list the pods/services that you explicitly created?

Perintah `kubectl get` tanpa opsi `-n` (atau `--namespace`) secara default akan menampilkan resource dari namespace `default`. Ini adalah namespace tempat pod dan service yang saya buat secara eksplisit berada, kecuali jika namespace lain ditentukan saat pembuatan.

Opsi `-n kube-system` pada perintah `kubectl get` bertujuan untuk menampilkan resource yang berada dalam namespace `kube-system`. Namespace `kube-system` adalah tempat komponen-komponen inti dan add-on Kubernetes berjalan, seperti kube-apiserver. Kubernetes menggunakan namespace untuk mengisolasi grup resource dalam satu cluster, sehingga resource aplikasi pengguna terpisah dari resource sistem.