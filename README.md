## Pengenalan Codeigniter

Codeigniter merupakan sebuah framework PHP yang menggunakan pola desain (design pattern) MVC (Model View Controller). CodeIgniter dirilis pertama kali pada 28 Februari 2006.

Codeigniter cocok digunakan untuk membuat aplikasi web seperti:

- Portal Berita;
- Sistem Informasi;
- Web Startup;
- Profile Company;
- eComerce;
- Blog;
- dan sebagainya.

### Kelebihan Codeigniter

Ada beberapa kelebihan CodeIgniter (CI) dibandingkan dengan Framework PHP lain, 3

- Performa cepat: Codeigniter merupakan framework yang paling cepat dibanding framework yang lain. 
- Konfigurasi yang minim .
- Dokumentasi yang lengkap: Codeigniter disertai dengan user_guide yang berisi dokumentasi yang lengkap.
- Mudah dipelajari pemula: Bagi pemula, CI sangat mudah dipelajari.

### Memulai Project Codeigniter

Langkah-langkah yang harus dilakukan untuk membuat project CI:

1. Download [Codeigniter Ver 3](https://www.codeigniter.com/download)
2. Copy file CI ke `htdocs` lalu `Ekstrak`
3. Ubah nama folder dengan `latih1`

> Sekarang buka: `http://localhost/latih1/`

![Tampilan Awal](/ci-welcome.png)

## Mengubah isi CodeIgniter

> Buka file 📄 `application/views/welcome_message.php` Lalu ubah teks pada baris 71.

```html
<div id="container">
	<h1>Project CodeIgniter (Nurcahyo-4SIA10)</h1>
```  

# Pertemuan 09 - Bootstrap

* Buka situs [getbootstrap](https://getbootstrap.com) lalu pilih `Documentation`  baca `Get started`.
* Buka file 📄 `application/views/welcome_message.php` Lalu ubah `HTML`.

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<!--bootstrap-->
	<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/css/bootstrap.min.css">
	<script src="https://code.jquery.com/jquery-3.5.1.slim.min.js"></script>
	<script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.0/dist/umd/popper.min.js"></script>
	<script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/js/bootstrap.min.js"></script>
</head>
<body>
```  

* masih di `Documentation` pilih `Components`.
* Tambahkan `body` pada file 📄 `application/views/welcome_message.php`.

```html
<body>
	<div class="container">
		<div class="alert alert-primary" role="alert">
			A simple primary alert—check it out!
		</div>
	</div>
</body>
</html>
```

### Tugas dikumpul besok dengan mencoba tiap2 `component`
