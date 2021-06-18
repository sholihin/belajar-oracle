LATIHAN 3 - PLSQL

1. Bikin procedure validasi untuk mengecek angka atau bukan, dengan parameter input valuenya, output ada dua out_return (integer), 
	out_message (varchar2), jika valid return 1 dan jika gagal return 0 dengan keterangan ada di out_message.
	
```
CREATE OR REPLACE PROCEDURE PROC_MS_SOAL1 (IN_PARAM      IN     VARCHAR2,
                                           OUT_RETURN       OUT INTEGER,
                                           OUT_MESSAGE      OUT VARCHAR2)
AS
BEGIN
    IF REGEXP_LIKE (IN_PARAM, '^[0-9]*$')
    THEN
        OUT_RETURN := 1;
        OUT_MESSAGE := 'Data inputan adalah number';
    ELSE
        OUT_RETURN := 0;
        OUT_MESSAGE := 'Data inputan bukan number!';
    END IF;
END;
```

## Cara untuk melihat hasil fungsi ##

```
DECLARE
    IN_PARAM VARCHAR2(100);
    OUT_RETURN INTEGER(1);
    OUT_MESSAGE VARCHAR2(100);
BEGIN
    IN_PARAM := 'satu';
    OUT_RETURN := NULL;
    OUT_MESSAGE := NULL;
    SQLTRAIN.PROC_MS_SOAL1(IN_PARAM, OUT_RETURN, OUT_MESSAGE);
    dbms_output.put_line(OUT_RETURN || ' - ' || OUT_MESSAGE);
    COMMIT;
END;
```

2. Bikin function validasi untuk mengecek data yang diinput harus huruf alfabet (besar/kecil), return integer dan ada output keterangan jika gagal

```
CREATE OR REPLACE FUNCTION FUNC_MS_SOAL2(IN_PARAM IN VARCHAR2, OUT_RETURN OUT INTEGER, OUT_MESSAGE OUT VARCHAR2) RETURN INTEGER 
AS
BEGIN
	IF REGEXP_LIKE(IN_PARAM, '^[A-Z]*$') THEN
		OUT_MESSAGE := 'Data inputan adalah alfabet besar';
		OUT_RETURN := 1;
	ELSIF REGEXP_LIKE(IN_PARAM, '^[a-z]*$') THEN
		OUT_MESSAGE := 'Data inputan adalah alfabet kecil';
		OUT_RETURN := 1;
	ELSE
		OUT_MESSAGE := 'Data inputan bukan alfabet!';
		OUT_RETURN := 0;
	END IF;
	
	RETURN OUT_RETURN;
END;
```

## Cara untuk melihat hasil fungsi ##

```
DECLARE
    RETVAL INT;
    IN_PARAM VARCHAR2(100);
    OUT_RETURN NUMBER;
    OUT_MESSAGE VARCHAR2(100);
BEGIN
    IN_PARAM := 'a';
    OUT_MESSAGE := NULL;
    RETVAL := SQLTRAIN.FUNC_MS_SOAL2(IN_PARAM, OUT_RETURN, OUT_MESSAGE);
    dbms_output.put_line(RETVAL || ' - ' || OUT_MESSAGE);
    COMMIT;
END;
```

3. Bikin function reverse misal jika input 1abc akan return cba1

### CARA 1 ###
```
CREATE OR REPLACE FUNCTION FUNC_MS_SOAL3 (IN_PARAM IN VARCHAR2)
    RETURN VARCHAR2
AS
    STR   VARCHAR2 (100);
BEGIN
    FOR i IN REVERSE 1 .. LENGTH (IN_PARAM)
    LOOP
        STR := STR || SUBSTR (IN_PARAM, i, 1);
    END LOOP;

    RETURN STR;
END;
```

## Cara melihat function yang di buat - Cara 1 ##

```
DECLARE
    IN_PARAM VARCHAR2(100);
    RETVAL VARCHAR2(100);
BEGIN
    IN_PARAM := 'satu';
    RETVAL := SQLTRAIN.FUNC_MS_SOAL3(IN_PARAM);
    dbms_output.put_line(RETVAL);
    COMMIT;
END;
```

### CARA 2 ###

```
CREATE OR REPLACE FUNCTION FUNC_MS_SOAL3 (IN_PARAM IN VARCHAR2) RETURN VARCHAR2
AS
RESULT VARCHAR2(100);
BEGIN
SELECT REVERSE(TO_CHAR(IN_PARAM)) INTO RESULT FROM DUAL;
RETURN RESULT;
END;
```

## Cara melihat function yang di buat - Cara 2 ##

```
SELECT SQLTRAIN.FUNC_MS_SOAL3('SHOLIHIN') FUNC_REVERSE FROM DUAL;
```

4. Bikin view untuk menampilan data yang sudah cetakpk (bill52.trans_101 mohon, bill52.trans_109=cetakpk) tapi belum bayar (bill52.trans_106=bayar) 
yang yg tgl_106/tgllunas transaksi bulan ini (noagenda, tglmohon (tglcatat trans_101), tglbayar(tgl_106), tglpk)


```
CREATE OR REPLACE VIEW VW_MS_SOAL4
AS
    SELECT A.NOAGENDA,
           A.TGLCATAT     TGLMOHON,
           B.TGLBAYAR,
           C.TGLPK
      FROM BILL52.TRANS_101 A, BILL52.TRANS_106 B, BILL52.TRANS_109 C
     WHERE     B.TGL_106 BETWEEN TO_DATE ('6/1/2021', 'mm/dd/yyyy')
                             AND TO_DATE ('6/30/2021', 'mm/dd/yyyy')
           AND NOT (C.TGLPK IS NULL)
           AND B.TGLBAYAR IS NULL
           AND A.NOAGENDA = B.NOAGENDA
           AND C.NOAGENDA = B.NOAGENDA;
```

Cara melihat hasil view:

```
SELECT * FROM SQLTRAIN.VW_MS_SOAL4;
```

5. Bikin view untuk menampilkan data (bill52.trans_101 mohon, bill52.trans_106 bayar, bill52.trans_109 table cetakpk) 
per unitup yang sudah bayar brp pelanggan dan sudah cetak brp pelanggan untuk transaksi a.tglagenda bulan ini

```
CREATE VIEW VW_MS_SOAL5
AS
      SELECT A.UNITUP,
             COUNT (B.TGLBAYAR)     JUMLAH_SUDAH_BAYAR,
             COUNT (A.IDPEL)        JUMLAH_PELANGGAN,
             COUNT (C.TGLPK)        JUMLAH_CETAK_PK
        FROM BILL52.TRANS_101 A, BILL52.TRANS_106 B, BILL52.TRANS_109 C
       WHERE     A.TGLAGENDA BETWEEN TO_DATE ('6/1/2021', 'mm/dd/yyyy')
                                 AND TO_DATE ('6/30/2021', 'mm/dd/yyyy')
             AND B.NOAGENDA = A.NOAGENDA
             AND C.NOAGENDA = A.NOAGENDA
    GROUP BY A.UNITUP;
```

### Cara melihat hasil view ###

```
SELECT * FROM SQLTRAIN.VW_MS_SOAL5;
```