
# Belajar PLSQL Sisi 1 - PLSQL #

## Tugas 1 ##

### Membuat tabel mahasiswa ###
```
DROP TABLE MAHASISWA CASCADE CONSTRAINTS;

CREATE TABLE MAHASISWA
(
  IDPEL VARCHAR2(12 BYTE),
  NAMA VARCHAR2(50 BYTE),
  ALAMAT VARCHAR2(50 BYTE),
  KELAS VARCHAR2(20 BYTE),
  TGLJOIN DATE,
  CONSTRAINT idpel_pk PRIMARY KEY (IDPEL)
);
```

![Gambar 1.0](images/create_table.PNG)

### Insert Data Contoh ###
```
INSERT INTO MAHASISWA (
select 'MAM01', 'Mohamad Sholihin', 'BOGOR', '1A', to_date('2022-04-06', 'yyyy-mm-dd') from dual
union
select 'MAM02', 'Faizal Rifqi', 'BOGOR', '1B', to_date('2022-04-07', 'yyyy-mm-dd') from dual
union
select 'MAM03', 'Fauzi Achmad', 'JAKARTA', '1C', to_date('2022-04-14', 'yyyy-mm-dd') from dual
);
```

atau 

```
INSERT all 
into MAHASISWA values ('MAM01', 'Mohamad Sholihin', 'BOGOR', '1A', to_date('2022-04-06', 'yyyy-mm-dd')) 
into MAHASISWA values ('MAM02', 'Faizal Rifqi', 'BOGOR', '1B', to_date('2022-04-07', 'yyyy-mm-dd'))
into MAHASISWA values ('MAM03', 'Fauzi Achmad', 'JAKARTA', '1C', to_date('2022-04-14', 'yyyy-mm-dd'))
select 1 from dual;
```
![Gambar 1.1](images/insert_data.PNG)

### Membuat tabel view dari tabel mahasiswa yang idpel MAM01 dan idpel MAM02 ###
```
create or replace view vw_mahasiswa_teladan
    as 
    select * from mahasiswa where alamat = 'BOGOR' and kelas in ('1A','1B');
```

### Melihat hasil view ###
```
select * from vw_mahasiswa_teladan;
```

![Gambar 1.2](images/image1.PNG)


###  Membuat tabel view dari mahasiswa yang idpel diantara MAM01 juta sampai MAM03 ###
```
create or replace view vw_range_mahasiswa
    as 
    select * from mahasiswa where idpel between 'MAM01' and 'MAM03';
```

### Melihat hasil view ###
```
select * from vw_range_mahasiswa
```

![Gambar 1.3](images/image2.PNG)

### Membuat tabel view dari tabel mahasiswa yang tgljoin dari tanggal 2022-04-06 sampai 2022-04-14 ###
```
create or replace view vw_join_mahasiswa
    as 
    select idpel, nama, kelas, tgljoin from mahasiswa where tgljoin
    between to_date('2022-04-06', 'yyyy-mm-dd') and to_date ('2022-04-07', 'yyyy/mm/dd');
```

### Melihat hasil view ###
```
select * from vw_join_mahasiswa;
```

![Gambar 1.4](images/image3.PNG)

### Membuat function perkalian ###
```
create or replace function func_kali(in_param1 integer, in_param2 integer) return integer
as
    result integer;
begin
    result := in_param1 * in_param2;
    return result;
end;
```

### Melihat hasil fungsi ###
```
select func_kali(5,5) result from dual;
```

![Gambar 1.5](images/image4.PNG)

### Membuat function tanggal hari ini ###
```
create or replace function func_hari_ini return varchar2
as
begin
    return to_char(sysdate, 'DD/MM/YYYY HH24:MI');
end;
```

### Melihat hasil fungsi ###
```
select func_hari_ini result from dual;
```

![Gambar 5.0](images/image5.PNG)

### Membuat function konversi dari dua digit bulan ke nama bulan ###
```
create or replace function func_konversi_bulan(in_param integer) return varchar2
as
result varchar2(100);
begin

    if in_param = 1 then
        result := 'Januari';
    elsif in_param = 2 then
        result := 'Februari';
    elsif in_param = 3 then
        result := 'Maret';
    elsif in_param = 4 then
        result := 'April';
    elsif in_param = 5 then
        result := 'Mei';
    elsif in_param = 6 then
        result := 'Juni';
    elsif in_param = 7 then
        result := 'Juli';
    elsif in_param = 8 then
        result := 'Agustus';
    elsif in_param = 9 then
        result := 'September';
    elsif in_param = 10 then
        result := 'Oktober';
    elsif in_param = 11 then
        result := 'November';
    elsif in_param = 12 then
        result := 'Desember';
    else
        result := 'Number not detected';
    end if;

    return result;

end;
```

### Melihat hasil fungsi ###
```
select func_konversi_bulan(03) result from dual;
```

![Gambar 6.0](images/image6.PNG)