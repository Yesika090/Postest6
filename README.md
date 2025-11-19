Nomor 1

SELECT 
    b.nama_barang,
    (SELECT nama_kategori 
     FROM kategori 
     WHERE kategori.kategori_id = b.kategori_id) AS kategori
FROM barang b
WHERE b.id_barang IN (SELECT id_barang FROM penjualan)
ORDER BY kategori;



nomor 2

SELECT nama_toko
FROM toko
WHERE id_toko IN (
    SELECT id_toko FROM penjualan 
    WHERE id_barang IN (SELECT id_barang FROM barang WHERE kategori_id = 1)
)
AND id_toko IN (
    SELECT id_toko FROM penjualan 
    WHERE id_barang IN (SELECT id_barang FROM barang WHERE kategori_id = 2)
);



nomor 3

SELECT nama_toko
FROM toko
WHERE id_toko IN (
    SELECT p.id_toko
    FROM penjualan p
    WHERE (p.jumlah_terjual * 
          (SELECT harga_barang FROM barang WHERE id_barang = p.id_barang)
          ) <= 1000000
);

