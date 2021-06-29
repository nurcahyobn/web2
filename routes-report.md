# Membuat Routes dan Report pada Halaman Web

1. Buat sites dengan `http://localhost/kuliah/`

2. Buat database `trigunadharma` dengan structur table berikut:

```sql
-- ----------------------------
-- Table structure for mahasiswa
-- ----------------------------
CREATE TABLE mahasiswa (
  id int(8),
  nama varchar(100),
  nim varchar(100),
  jenis_kelamin varchar(1),
  fakultas varchar(50)
);

-- ----------------------------
-- Records of mahasiswa
-- ----------------------------
INSERT INTO mahasiswa VALUES (1, 'Nurcahyo Budi Nugroho', '2017020000', 'L', 'Komputer');
INSERT INTO mahasiswa VALUES (2, 'Maya Rahmaniah', '1234456667', 'P', 'Ekonomi');
INSERT INTO mahasiswa VALUES (3, 'Diki ALfarabi Hadi', '123345678887', 'L', 'Teknik');
INSERT INTO mahasiswa VALUES (4, 'Suamtono', '123456789', 'L', 'Fisip');
INSERT INTO mahasiswa VALUES (5, 'Jamludin Syah', '12345663536', 'L', 'Teknik');
INSERT INTO mahasiswa VALUES (6, 'Rahmaniah', '212111231133', 'P', 'Ekonomi');
INSERT INTO mahasiswa VALUES (7, 'Qiano Arfabian Putra', '1123555365', 'L', 'Teknik');
INSERT INTO mahasiswa VALUES (8, 'Gibran', '1122432434', 'L', 'Ekonomi');
INSERT INTO mahasiswa VALUES (9, 'Johny', '12363377332', 'L', 'Pertanian');
INSERT INTO mahasiswa VALUES (10, 'Muhammad Riski', '12837373839', 'L', 'Fisip');
```

4. Menghapus index.php pada url. Buat file `.htaccess` pada `kuliah` lalu ketik perintah berikut:

```js
RewriteEngine on
RewriteCond $1 !^(index\.php|resources|robots\.txt)
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)$ index.php/$1 [L,QSA]
```

5. Ubah kode pada /application/config/autoload.php

```php
$autoload['helper'] = array('url');
$autoload['libraries'] = array('database');
```

6. Ubah kode pada /application/config/config.php

```php
$config['base_url'] = 'http://localhost/project-01/';
```

# Membuat Report / Laporan pada Web

#### Langkah 1. Download Library [Dompdf](https://goo.gl/bHyn3A)nya dan Ekstrak filenya di folder `kampus/assets`.

#### Langkah 2. Buat file pdf di folder `libraries` dengan nama file `Mypdf.php` jika sudah selesai struktu Filenya akan seperti ini `libraries/Mypdf`
   
```php 
<?php
defined('BASEPATH') OR exit('No direct script access allowed');

require_once('assets/dompdf/autoload.inc.php');
use Dompdf\Dompdf;

class Mypdf
{
  protected $ci;

  public function __construct()
  {
        $this->ci =& get_instance();
  }

  public function generate($view, $data = array(), $filename = 'Laporan', $paper = 'A4', $orientation='portrait')
  {
    $dompdf = new Dompdf();
    $html = $this->ci->load->view($view, $data, TRUE);
    $dompdf->loadHtml($html);
    $dompdf->setPaper($paper, $orientation);
    // Render the HTML as PDF
    $dompdf->render();
      $dompdf->stream( $filename . ".pdf", array("Attachment" => FALSE));
  }
}

/* End of file Mypdf.php */
/* Location: ./application/libraries/Mypdf.php */
```
  
  
Langkah 3. Buat file `Model` file:`Mahasiswa_model.php`  dan Controllernya file: `Laporan.php`.

```php
<?php
	class Mahasiswa_model extends CI_Model {
		function __construct(){
			parent::__construct();
			$this->load->database();
		}
 
		public function getAllMahasiswa(){
			$query = $this->db->get('mahasiswa');
			return $query->result(); 
		}
	}
?>
```

<hr/>

```php
<?php
defined('BASEPATH') OR exit('No direct script access allowed');

class Laporan extends CI_Controller {

  public function index()
  {
    $this->load->model('mahasiswa_model');

    $this->load->library('mypdf');
    $data['data'] = $this->mahasiswa_model->getAllMahasiswa();
    $this->mypdf->generate('Laporan/dompdf', $data, 'laporan-mahasiswa', 'A4', 'landscape');
  }

}
/* End of file Laporan.php */
/* Location: ./application/controllers/Laporan.php */
```    

  
Langkah 4. View : Selanjutnya anda buat folder `laporan` di folder `view` dan buat file `dompdf.php` didalamnya
    
```php
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <title>Laporan</title>
  <link rel="stylesheet" href="">
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css" integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">
</head>
<body>
  <table style="width: 100%;">
    <tr>
      <td align="center">
        <span style="line-height: 1.6; font-weight: bold;">
          SEKOLAH TINGGI MANAJEMEN INFORMATIKA DAN KOMPUTER
          <br>TRIGUNA DHARMA
        </span>
      </td>
    </tr>
  </table>

  <hr> 
  
  <table class="table table-bordered">
    <tr>
      <th>#</th>
      <th>Nim</th>
      <th>Nama</th>
      <th>Fakultas</th>
    </tr>
    <?php $no = 1; foreach ($data as $row): ?>
      <tr>
        <td><?php echo $no++ ?></td>
        <td><?php echo $row->nim ?></td>
        <td><?php echo $row->nama ?></td>
        <td><?php echo $row['fakultas'] ?></td>
      </tr>
    <?php endforeach ?>
  </table>
</body>
</html>
```
