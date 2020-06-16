# Pert11 - Insert dan View MySQL CI

![](/CI-CRUD-UI.gif)

> `Step-1` : Menggunakan  `Bootstrap` pada `CodeIgniter`.

* Download [Bootstrap](https://github.com/nurcahyobn/web2/raw/master/bootstrap.zip) letakkan di folder `latih1`

> `Step-2` : Database mysql `test` dengan nama tabel `mahasiswa`:

```sql
    CREATE TABLE `barang` (
        `id` int(11) NOT NULL AUTO_INCREMENT,
        `namabarang` varchar(30) NOT NULL,
        `stok` varchar(10) NOT NULL,
    PRIMARY KEY(`id`)
    ) ENGINE=InnoDB DEFAULT CHARSET=latin1;
```

> `Step-3` : Koneksi CI ke MYSQL. Buka file `database.php` di folder `application/config`.

```php
	'hostname' => 'localhost',
	'username' => 'root',
	'password' => '',
	'database' => 'test',
```

> `Step-4` : Konfigurasi URL Homebase. Edit `config.php` di folder `application/config`.

```
$config['base_url'] = 'http://localhost/latih1/';
```

> `Step-5` : Membuat `MODEL` di CI. 

* Buat file `Barang_model.php` di folder `application/models`.
* Perhatikan bahwa huruf pertama nama model harus dalam huruf CAPITAL.
* Nama model disesuaikan dengan nama `tabel` atau `objek` untuk mudah dipahami.

```php
<?php
	class Barang_model extends CI_Model {
		function __construct(){
			parent::__construct();
			$this->load->database();
		}
 
		public function getAllData(){
			$query = $this->db->get('barang');
			return $query->result(); 
		}
 
		public function insert($barang){
			return $this->db->insert('barang', $barang);
		} 
?>
```

> `Step-6` : Membuat `Controller` di CI

* Buat file `Mahasiswa.php` di folder `application/controllers`.
* Perhatikan penamaan file, sama seperti nama `model` diawali huruf CAPITAL.
* Digunakan untuk mengatur aplikasi pada data mahasiswa.

```php
<?php
defined('BASEPATH') OR exit('No direct script access allowed');
 
class Barang extends CI_Controller {
 
	function __construct(){
		parent::__construct();
		$this->load->helper('url');
		$this->load->model('barang_model');
	}
 
	public function index(){
		$data['barang'] = $this->barang_model->getAllData();
		$this->load->view('barang_list.php', $data);
	}
 
	public function addnew(){
		$this->load->view('addbarang.php');
	}
 
	public function insert(){
		$mahasiswa['namabarang'] = $this->input->post('namabarang');
		$mahasiswa['stok'] = $this->input->post('stok');
 
		$query = $this->barang_model->insert($barang);
 
		if($query){
			header('location:'.base_url().$this->index());
		}
	} 
?>
```

> `Step-8` : Mengatur `ROUTE` di CI. Edit `routes.php` di folder `application/config`.

```
$route['default_controller'] = 'barang';
```

> `Step-9` : Membuat `VIEW` sesuai Controller pada `Step-6`. Buka folder `application/views`.

* Buat file : `barang_list.php`

```php
<!DOCTYPE html>
<html>
<head>
	<link rel="stylesheet" type="text/css" href="<?php echo base_url(); ?>bootstrap/css/bootstrap.min.css">
</head>
<body>
<div class="container">
	<h1 class="page-header text-center">CRUD Data Barang</h1>
    <a href="<?php echo base_url(); ?>index.php/barang/addnew" class="btn btn-primary">
        <span class="glyphicon glyphicon-plus"></span> Add New</a><br><br>
    <table class="table table-bordered table-striped">
        <thead>
            <tr>
                <th>ID</th>
                <th>Nama Barang</th>
                <th>Stok</th>
            </tr>
        </thead>
        <tbody>
            <?php
            foreach($barang as $brg){
                ?>
                <tr>
                    <td><?php echo $brg->id; ?></td>
                    <td><?php echo $brg->namabarang; ?></td>
                    <td><?php echo $brg->stok; ?></td>
                </tr>
                <?php
            }
            ?>
        </tbody>
    </table>
</div>
</body>
</html>
```

* Buat file : `addbarang.php`

```php
<!DOCTYPE html>
<html>
<head>
	<link rel="stylesheet" type="text/css" href="<?php echo base_url(); ?>bootstrap/css/bootstrap.min.css">
</head>
<body>
<div class="container">
	<h1 class="page-header text-center">CRUD Data Barang</h1>
			<h3>Add Form
				<span class="pull-right"><a href="<?php echo base_url(); ?>" class="btn btn-primary"><span class="glyphicon glyphicon-arrow-left"></span> Back</a></span>
			</h3>
			<hr>
			<form method="POST" action="<?php echo base_url(); ?>index.php/barang/insert">
				<div class="form-group">
					<label>Nama Barang:</label>
					<input type="text" class="form-control" name="namabarang">
				</div>
				<div class="form-group">
					<label>Stok:</label>
					<input type="text" class="form-control" name="stok">
				</div>				
				<button type="submit" class="btn btn-primary"><span class="glyphicon glyphicon-floppy-disk"></span> Simpan </button>
			</form>		
</div>
</body>
</html>
```
