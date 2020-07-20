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
- Dokumentasi yang lengkap: Codeigniter disertai dengan mahasiswa_guide yang berisi dokumentasi yang lengkap.
- Mudah dipelajari pemula: Bagi pemula, CI sangat mudah dipelajari.

### Memulai Project Codeigniter

Langkah-langkah yang harus dilakukan untuk membuat project CI:

1. Download [Codeigniter] Ver-3 (https://www.codeigniter.com/download)
2. Copy file CI ke `htdocs` lalu `Ekstrak`
3. Ubah nama folder dengan `project-01`

> Sekarang buka: `http://localhost/project-01/`

![Tampilan Awal](/ci-welcome.png)

> `Step-1` : Membuat `MODEL` di CI. 

* Buat file `Buku_model.php` di folder `application/models`.
* Perhatikan bahwa huruf pertama nama model harus dalam huruf CAPITAL.
* Nama model disesuaikan dengan nama `tabel` atau `objek` untuk mudah dipahami.

```php
<?php
	class Buku_model extends CI_Model {
 
		public function getBuku() {
			return array(
				array(
					'judul' => 'Belajar FrameWork CI',
					'pengarang' => 'Budi Raharjo',
					'penerbit' => 'Informatika'
				),
				array(
					'judul' => 'Belajar Photoshop',
					'pengarang' => 'Abdul Kadir',
					'penerbit' => 'Andi Offset'
				)
			); 
		}

	}
?>
```


> `Step-2` : Membuat `Controller` di CI

* Buat file `Buku.php` di folder `application/controllers`.
* Perhatikan penamaan file, sama seperti nama `model` diawali huruf CAPITAL.

```php
<?php
defined('BASEPATH') OR exit('No direct script access allowed');
 
class Buku extends CI_Controller {
 
	function __construct(){
		parent::__construct();
		$this->load->model('buku_model');
	}
 
	public function index(){
		$data['data_buku'] = $this->mahasiswa_model->getBook();
		$this->load->view('buku_view.php', $data);
	}
 
} 
?>
```

> `Step-3` : Membuat `VIEW` sesuai Controller.

* Buat file `buku_view.php` di folder `application/views`.
* Perhatikan penamaan file dibuat dalam huruf kecil.

```php
<!DOCTYPE html>
<html>
<body>
    <table border="1">
        <thead>
            <tr>
                <th>No</th>
                <th>Judul</th>
                <th>Pengarang</th>
                <th>Penerbit</th>
            </tr>
        </thead>
        <tbody>
			<?php
				$no = 1;
				// lanjutkan
			?>
        </tbody>
    </table>
</div>
</body>
</html>
```
