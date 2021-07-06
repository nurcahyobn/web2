# UAS Web 2

#### Buat Program untuk DataTables untuk menampilkan semua data berikut

1. Buat sites dengan `http://localhost/uas-nurcahyo/`

2. Buat database `uas-nurcahyo` dengan structur table berikut:

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
