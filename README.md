Nomor 1

SELECT 
    s.nama_studio AS "Nama Studio",
    SUM(p.penjualan_tiket) AS "Total Penjualan Tiket"
FROM studio s
JOIN film f ON s.id_studio = f.id_studio
JOIN penayangan p ON f.id_film = p.id_film
GROUP BY s.nama_studio
ORDER BY SUM(p.penjualan_tiket) DESC;


nomor 2

SELECT 
    genre AS "Genre",
    AVG(durasi) AS "Rata-rata Durasi"
FROM film
GROUP BY genre
ORDER BY AVG(durasi) ASC;


nomor 3

SELECT 
    tahun_rilis AS "Tahun Rilis",
    COUNT(*) AS "Jumlah Film"
FROM film
GROUP BY tahun_rilis
ORDER BY tahun_rilis DESC;




nomor 4

SELECT 
    s.nama_studio AS "Nama Studio",
    AVG(f.rating) AS "Rata-rata Rating"
FROM studio s
JOIN film f ON s.id_studio = f.id_studio
GROUP BY s.nama_studio
HAVING AVG(f.rating) > 8
ORDER BY AVG(f.rating) DESC;
