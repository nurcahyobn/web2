# UAS Web 2

#### Buat Program untuk DataTables untuk menampilkan semua data berikut

1. Buat sites dengan `http://localhost/uas-nurcahyo/`

2. Buat database `uas_nurcahyo` dengan structur table berikut:

```sql
-- ----------------------------
-- Table structure for mahasiswa
-- ----------------------------
CREATE TABLE mahasiswa (
  id int(8),
  nama varchar(100),
  nim varchar(100),
  jenis_kelamin varchar(1),
  jurusan varchar(50)
);

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

CREATE TABLE `buku` (
  `id` int(11) NOT NULL,
  `judul_buku` varchar(128) NOT NULL,
  `id_kategori` int(11) NOT NULL,
  `pengarang` varchar(64) NOT NULL,
  `penerbit` varchar(64) NOT NULL,
  `tahun_terbit` year(4) NOT NULL,
  `isbn` varchar(64) NOT NULL,
  `stok` int(11) NOT NULL,
  `dipinjam` int(11) NOT NULL,
  `dibooking` int(11) NOT NULL,
  `image` varchar(256) DEFAULT 'book-default-cover.jpg'
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

INSERT INTO `buku` (`id`, `judul_buku`, `id_kategori`, `pengarang`, `penerbit`, `tahun_terbit`, `isbn`, `stok`, `dipinjam`, `dibooking`, `image`) VALUES
(1, 'Statistika dengan Program Komputer', 1, 'Ahmad Kholiqul Amin', 'Deep Publish', 2014, '9786022809432', 6, 1, 1, 'img1557402455.jpg'),
(2, 'Mudah Belajar Komputer untuk Anak', 1, 'Bambang Agus Setiawan', 'Huta Media', 2014, '9786025118500', 5, 3, 1, 'img1557402397.jpg'),
(5, 'PHP Komplet', 1, 'Jubilee', 'Elex Media Komputindo', 2017, '8346753547', 5, 1, 1, 'img1555522493.jpg'),
(10, 'Detektif Conan Ep 200', 9, 'Okigawa sasuke', 'Cultura', 2016, '874387583987', 5, 0, 0, 'img1557401465.jpg'),
(14, 'Bahasa Indonesia', 2, 'Umri Nur\'aini dan Indriyani', 'Pusat Perbukuan', 2015, '757254724884', 3, 0, 0, 'img1557402703.jpg'),
(15, 'Komunikasi Lintas Budaya', 5, 'Dr. Dedy Kurnia', 'Published', 2015, '878674646488', 5, 0, 0, 'img1557403156.jpg'),
(16, 'Kolaborasi Codeigniter dan Ajax dalam Perancangan CMS', 1, 'Anton Subagia', 'Elex Media komputindo', 2017, '43345356577', 5, 0, 0, 'img1557403502.jpg'),
(17, 'From Hobby to Money', 4, 'Deasylawati', 'Elex Media Komputindo', 2015, '87968686787879', 5, 0, 0, 'img1557403658.jpg'),
(18, 'Buku Saku Pramuka', 8, 'Rudi Himawan', 'Pusat Perbukuan', 2016, '97868687978796', 6, 0, 0, 'img1557404613.jpg'),
(19, 'Rahasia Keajaiban Bumi', 3, 'Nurul Ihsan', 'Luxima', 2014, '565756565768868', 5, 0, 0, 'img1557404689.jpg'),
(20, 'Buku Pintar Puasa Wajib dan Sunnah Sepanjang Masa', 7, 'Ali Hasan', 'Luxima', 2011, '32342342344234', 5, 0, 0, 'img1557404775.jpg'),
(21, 'Aspek Hukum dalam Penelitian', 6, 'Rianto Adi', 'Buku Obor', 2015, '7565646455757', 5, 0, 0, 'img1557404853.jpg');
```

3. Ubah kode pada /application/config/autoload.php

```php
$autoload['helper'] = array('url');
$autoload['libraries'] = array('database');
```

4. Ubah kode pada /application/config/config.php

```php
$config['base_url'] = 'http://localhost/uas-nurcahyo/';
```


5. Ubah kode pada /application/config/database.php

```php
$db['default'] = array(
	'dsn'	=> '',
	'hostname' => 'localhost',
	'username' => 'root',
	'password' => '',
	'database' => 'uas_nurcahyo',
```

##### Tabel Mahasiswa buat kan DataTables (Pert15)

##### Tabel Buku buat kan Report (Pert14)
