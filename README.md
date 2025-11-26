NO 1

Query Trigger :

DELIMITER $$

CREATE TRIGGER after_topup_insert
AFTER INSERT ON topup_saldo
FOR EACH ROW
BEGIN
    UPDATE pengguna
    SET saldo = saldo + NEW.jumlah_topup
    WHERE id_user = NEW.id_user;
END$$

DELIMITER ;

Query Testing (Insert Top Up) :

INSERT INTO topup_saldo (id_user, jumlah_topup, metode_bayar, waktu_topup)
VALUES (2, 100000, 'Transfer Bank', NOW());

Query Cek Sebelum & Sesudah :

SELECT * FROM pengguna WHERE id_user = 2;


NO 2

Query Trigger :

DELIMITER $$

CREATE TRIGGER before_pengguna_update
BEFORE UPDATE ON pengguna
FOR EACH ROW
BEGIN
    INSERT INTO log_aktivitas (id_user, aktivitas, data_lama, waktu_kejadian)
    VALUES (
        OLD.id_user,
        'Update Data User',
        CONCAT('Nama: ', OLD.nama_user, ', HP: ', OLD.nomor_hp),
        NOW()
    );
END$$

DELIMITER ;

Query Testing (Update Data) :

UPDATE pengguna
SET nomor_hp = '085555555555'
WHERE id_user = 1;

Query Cek Log :

SELECT * FROM log_aktivitas;


NO 3 

Query Trigger :

DELIMITER $$

CREATE TRIGGER before_pengguna_delete
BEFORE DELETE ON pengguna
FOR EACH ROW
BEGIN
    INSERT INTO log_aktivitas (id_user, aktivitas, data_lama, waktu_kejadian)
    VALUES (
        OLD.id_user,
        'Hapus Akun User',
        CONCAT('User ', OLD.nama_user, ' dengan saldo terakhir ', OLD.saldo, ' telah dihapus'),
        NOW()
    );
END$$

Query Testing (Hapus User) :

DELIMITER ;

DELETE FROM pengguna
WHERE id_user = 3;

Query Cek Log :

SELECT * FROM log_aktivitas;


