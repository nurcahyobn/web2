# Pert11 - CRUD Bootstrap

![](/CI-CRUD-UI.gif)

> `Step-1` : Menggunakan  `Bootstrap` pada `CodeIgniter`.

* Download [Bootstrap](https://github.com/nurcahyobn/web2/raw/master/bootstrap.zip) letakkan di folder `latih1`

> `Step-2` : Database mysql `test` dengan nama tabel `mahasiswa`:

```sql
    CREATE TABLE `mahasiswa` (
        `id` int(11) NOT NULL AUTO_INCREMENT,
        `namamhs` varchar(30) NOT NULL,
        `kelas` varchar(10) NOT NULL,
        `alamat` varchar(100) NOT NULL,
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

* Buat file `Mahasiswa_model.php` di folder `application/models`.
* Perhatikan bahwa huruf pertama nama model harus dalam huruf CAPITAL.
* Nama model disesuaikan dengan nama `tabel` atau `objek` untuk mudah dipahami.

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
 
		public function insertMahasiswa($mahasiswa){
			return $this->db->insert('mahasiswa', $mahasiswa);
		}
 
		public function getMahasiswa($id){
			$query = $this->db->get_where('mahasiswa',array('id'=>$id));
			return $query->row_array();
		}
 
		public function updateMahasiswa($mahasiswa, $id){
			$this->db->where('mahasiswa.id', $id);
			return $this->db->update('mahasiswa', $mahasiswa);
		}
 
		public function deleteMahasiswa($id){
			$this->db->where('mahasiswa.id', $id);
			return $this->db->delete('mahasiswa');
		}
 
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
 
class Mahasiswa extends CI_Controller {
 
	function __construct(){
		parent::__construct();
		$this->load->helper('url');
		$this->load->model('mahasiswa_model');
	}
 
	public function index(){
		$data['mahasiswa'] = $this->mahasiswa_model->getAllMahasiswa();
		$this->load->view('mahasiswa_list.php', $data);
	}
 
	public function addnew(){
		$this->load->view('addmahasiswa.php');
	}
 
	public function insert(){
		$mahasiswa['namamhs'] = $this->input->post('namamhs');
		$mahasiswa['kelas'] = $this->input->post('kelas');
		$mahasiswa['alamat'] = $this->input->post('alamat');
 
		$query = $this->mahasiswa_model->insertMahasiswa($mahasiswa);
 
		if($query){
			header('location:'.base_url().$this->index());
		}
 
	}
 
	public function edit($id){
		$data['mahasiswa'] = $this->mahasiswa_model->getMahasiswa($id);
		$this->load->view('editmahasiswa.php', $data);
	}
 
	public function update($id){
		$mahasiswa['namamhs'] = $this->input->post('namamhs');
		$mahasiswa['kelas'] = $this->input->post('kelas');
		$mahasiswa['alamat'] = $this->input->post('alamat');
 
		$query = $this->mahasiswa_model->updateMahasiswa($mahasiswa, $id);
 
		if($query){
			header('location:'.base_url().$this->index());
		}
	}
 
	public function delete($id){
		$query = $this->mahasiswa_model->deleteMahasiswa($id);
 
		if($query){
			header('location:'.base_url().$this->index());
		}
	}
} 
?>
```

> `Step-8` : Mengatur `ROUTE` di CI. Edit `routes.php` di folder `application/config`.

```
$route['default_controller'] = 'mahasiswa';
```

> `Step-9` : Membuat `VIEW` sesuai Controller pada `Step-6`. Buka folder `application/views`.

* Buat file : `mahasiswa_list.php`

```php
<!DOCTYPE html>
<html>
<head>
	<link rel="stylesheet" type="text/css" href="<?php echo base_url(); ?>bootstrap/css/bootstrap.min.css">
</head>
<body>
<div class="container">
	<h1 class="page-header text-center">CRUD Data Mahasiswa</h1>
    <a href="<?php echo base_url(); ?>index.php/mahasiswa/addnew" class="btn btn-primary">
        <span class="glyphicon glyphicon-plus"></span> Add New</a><br><br>
    <table class="table table-bordered table-striped">
        <thead>
            <tr>
                <th>ID</th>
                <th>Nama Mahasiswa</th>
                <th>Kelas</th>
                <th>Alamat</th>
                <th>Action</th>
            </tr>
        </thead>
        <tbody>
            <?php
            foreach($mahasiswa as $mhs){
                ?>
                <tr>
                    <td><?php echo $mhs->id; ?></td>
                    <td><?php echo $mhs->namamhs; ?></td>
                    <td><?php echo $mhs->kelas; ?></td>
                    <td><?php echo $mhs->alamat; ?></td>
                    <td><a href="<?php echo base_url(); ?>index.php/mahasiswa/edit/<?php echo $mhs->id; ?>" class="btn btn-success">
                        <span class="glyphicon glyphicon-edit"></span> Edit</a> || 
                        <a href="<?php echo base_url(); ?>index.php/mahasiswa/delete/<?php echo $mhs->id; ?>" class="btn btn-danger">
                        <span class="glyphicon glyphicon-trash"></span> Delete</a></td>
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

* Buat file : `addmahasiswa.php`

```php
<!DOCTYPE html>
<html>
<head>
	<link rel="stylesheet" type="text/css" href="<?php echo base_url(); ?>bootstrap/css/bootstrap.min.css">
</head>
<body>
<div class="container">
	<h1 class="page-header text-center">CRUD Data Mahasiswa</h1>
			<h3>Add Form
				<span class="pull-right"><a href="<?php echo base_url(); ?>" class="btn btn-primary"><span class="glyphicon glyphicon-arrow-left"></span> Back</a></span>
			</h3>
			<hr>
			<form method="POST" action="<?php echo base_url(); ?>index.php/mahasiswa/insert">
				<div class="form-group">
					<label>Nama Mahasiswa:</label>
					<input type="text" class="form-control" name="namamhs">
				</div>
				<div class="form-group">
					<label>Kelas:</label>
					<input type="text" class="form-control" name="kelas">
				</div>
				<div class="form-group">
					<label>Alamat:</label>
					<input type="text" class="form-control" name="alamat">
				</div>
				<button type="submit" class="btn btn-primary"><span class="glyphicon glyphicon-floppy-disk"></span> Simpan </button>
			</form>		
</div>
</body>
</html>
```

* Buat file : `editmahasiswa.php`, COPY-PASTE dari `addmahasiswa.php`, lalu `edit`:


```php
    <h3>Edit Form
    ...
    <?php extract($mahasiswa); ?>
        <form method="POST" action="<?php echo base_url(); ?>index.php/mahasiswa/update/<?php echo $id; ?>">
        ...
        <input type="text" class="form-control" value="<?php echo $namamhs; ?>" name="namamhs">
        ...
        <input type="text" class="form-control" value="<?php echo $kelas; ?>" name="kelas">
        ...
        <input type="text" class="form-control" value="<?php echo $alamat; ?>" name="alamat">
        ...
        <button type="submit" class="btn btn-primary"><span class="glyphicon glyphicon-floppy-disk"></span> Update </button>
```
