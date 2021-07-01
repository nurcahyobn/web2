# Library DataTables di CodeIgniter

Download materi : [database & library](https://file.io/q6aqqghrshTR)

> 1. Buat sites `CodeIgniter` dengan `http://localhost/pos/`

> 2. Buat database `db15` dengan structur table berikut:

##### setelah buat database `db` pilih `Import` pilih file `mahasiswa.sql`

> 3. Ubah kode pada /application/config/autoload.php

```php
$autoload['helper'] = array('url');
$autoload['libraries'] = array('database');
```

> 4. Ubah kode pada /application/config/config.php

```php
$config['base_url'] = 'http://localhost/pos/';
```

> 5. Ubah kode pada /application/config/database.php

```php
   $db['default'] = array(
	'dsn'	=> '',
	'hostname' => 'localhost',
	'username' => 'root',
	'password' => '',
	'database' => 'db15',
```
> 6. Menambahkan library di folder `libraries` dengan nama file `Datatables.php`.

> 7. Buat file `Controller` file: `Mahasiswa.php`.

```php
<?php
defined('BASEPATH') OR exit('No direct script access allowed');

Class Mahasiswa extends CI_Controller{

    function index(){
        $this->load->view('mahasiswa_view)');
    }

    function json(){
        $this->load->library('datatables');
        $this->datatables->select('*');
        $this->datatables->from('mahasiswa');
        return print_r($this->datatables->generate());
    }
}
```

> Run : `http://localhost/pos/index.php/mahasiswa/json`

> 7. Buat file `View` file: `Mahasiswa_view.php`.

```php
<html>
    <head>
        <title>Belajaphp.net - Codeigniter Datatable</title>
        <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css">
        <link href="https://cdn.datatables.net/1.10.13/css/jquery.dataTables.min.css" rel="stylesheet">
    </head>
    <body>
        <div class="container">
            <h3>DATA MAHASISWA</h3>
            <table id="table" class="display" cellspacing="0" width="100%">
                <thead>
                    <tr><th>FOTO</th><th>Nama Mahasiswa</th><th>Email</th><th>Kelas</th></tr>
                </thead>
                <tbody>
                </tbody>
            </table>
        </div>
        <script src="https://code.jquery.com/jquery-1.12.4.js"></script>
        <script src="https://cdn.datatables.net/1.10.13/js/jquery.dataTables.min.js"></script>
        <script src="https://cdn.datatables.net/1.10.13/js/dataTables.bootstrap.min.js"></script>
        <script type="text/javascript">

            var save_method; //for save method string
            var table;

            $(document).ready(function() {
                //datatables
                table = $('#table').DataTable({ 
                    "processing": true, //Feature control the processing indicator.
                    "serverSide": true, //Feature control DataTables' server-side processing mode.
                    "order": [], //Initial no order.
                    // Load data for the table's content from an Ajax source
                    "ajax": {
                        "url": '<?php echo site_url('mahasiswa/json'); ?>',
                        "type": "POST"
                    },
                    //Set column definition initialisation properties.
                    "columns": [
                        {"data": "nim",width:170},
                        {"data": "nama",width:100},
                        {"data": "email",width:100},
                        {"data": "kelas",width:100}
                    ],

                });

            });
        </script>

    </body>
</html>
```
> Run : `http://localhost/pos/index.php/mahasiswa/`
