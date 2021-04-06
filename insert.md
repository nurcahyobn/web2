# Penyimpanan Data ke MySQL pada CodeIgniter

> `Step-1` : ganti folder dengan `latihan` pada aplikasi `CodeIgniter`.

> `Step-2` : Database mysql `dblatihan` dengan nama tabel `mahasiswa`

```sql
CREATE TABLE `mahasiswa` (
    `id` int(11) NOT NULL AUTO_INCREMENT,
    `namamhs` varchar(30) NOT NULL,
    `kelas` varchar(10) NOT NULL,
    `alamat` varchar(100) NOT NULL,
PRIMARY KEY(`id`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1;
```
