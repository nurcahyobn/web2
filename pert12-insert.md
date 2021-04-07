# Insert dan View MySQL CI
![](/latih1.jpg)

> `Step-1` : Buat folder `latih1` untuk aplikasi `CodeIgniter`.

> `Step-2` : Download [Bootstrap](https://github.com/nurcahyobn/web2/raw/master/bootstrap.zip), extract pindahkan ke folder `latih1`

> `Step-3` : Database mysql `test` dengan nama tabel `barang` berikut ini:

```sql
CREATE TABLE `barang` (
`id` int(11) NOT NULL AUTO_INCREMENT,
`namabarang` varchar(30) NOT NULL,
`stok` varchar(10) NOT NULL,
PRIMARY KEY(`id`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

INSERT INTO `barang` (`id`, `namabarang`, `stok`) VALUES
(1, 'Buku Tulis', '4'),
(2, 'Jam Tangan ', '5');
```

> `Step-4` : Di folder `application/config`, edit file `database.php`

```php
	'hostname' => 'localhost',
	'username' => 'root',
	'password' => '',
	'database' => 'test',
```

> `Step-5` : Membuat `MODEL` di folder `application/models`, dengan file `Barang_model.php`

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
	}
```

> `Step-6` : Membuat `CONTROLLER` di folder `application/controllers`, dengan file `Barang.php`

```php
<?php
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
			$barang['namabarang'] = $this->input->post('namabarang');
			$barang['stok'] = $this->input->post('stok');
	
			$query = $this->barang_model->insert($barang);
	
			if($query){
				header('location:../barang');
			}
		} 
	}
```

> `Step-7` : Membuat `VIEW` sesuai Controller pada `Step-6`. Buka folder `application/views`.

1. Buat file : `barang_list.php`

```php
<!DOCTYPE html>
<html>
<head>
	<link rel="stylesheet" type="text/css" href="../bootstrap/css/bootstrap.min.css">
</head>
<body>
<div class="container">
	<h1 class="page-header text-center">Data Barang</h1>
    <a href="barang/addnew" class="btn btn-primary">
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

2. Buat file : `addbarang.php`

```php
<!DOCTYPE html>
<html>
<head>
	<link rel="stylesheet" type="text/css" href="../../bootstrap/css/bootstrap.min.css">
</head>
<body>
<div class="container">
	<h1 class="page-header text-center">Input Data Barang</h1>
			<h3>Add Form
				<span class="pull-right"><a href="../barang" class="btn btn-primary"><span class="glyphicon glyphicon-arrow-left"></span> Back</a></span>
			</h3>
			<hr>
			<form method="POST" action="../barang/insert">
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

> `Step-8` : Buka Browser lalu jalankan `http://localhost/latih1/index.php/barang`.
