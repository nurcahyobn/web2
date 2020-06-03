# Aplikasi CI : Mengatur Bootstrap untuk Data Mahasiswa

> `Step-1` : Menggunakan  `Bootstrap` pada `CodeIgniter`
> Download [Bootstrap] (https://github.com/nurcahyobn/web2/raw/master/bootstrap.zip) letakkan di folder `latih1`

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
	'mahasiswaname' => 'root',
	'kelas' => '',
	'database' => 'test',
```

> `Step-4` : Konfigurasi URL Homebase. Edit `config.php` di folder `application/config`.

```
$config['base_url'] = 'http://localhost/latih1/';
```

> `Step-5` : Membuat `MODEL` di CI. 

* Buat file `Mahasiswas_model.php` di folder `application/models`.
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
		$data['mahasiswa'] = $this->mahasiswa_model->getmahasiswa($id);
		$this->load->view('editform', $data);
	}
 
	public function update($id){
		$mahasiswa['namamhs'] = $this->input->post('namamhs');
		$mahasiswa['kelas'] = $this->input->post('kelas');
		$mahasiswa['alamat'] = $this->input->post('alamat');
 
		$query = $this->mahasiswa_model->updatemahasiswa($mahasiswa, $id);
 
		if($query){
			header('location:'.base_url().$this->index());
		}
	}
 
	public function delete($id){
		$query = $this->mahasiswa_model->deletemahasiswa($id);
 
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
