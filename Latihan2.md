# Latihan 2 - PLSQL #

## Tugas 1 - Menampilkan tagihan per unitup berapa pelanggan dan tagihannya berapa (unitup, jmlplg, jmltag) ##

```
select unitup, count(*) jmlplg, sum(rptag) jmltag from dpptes
    group by unitup
```

## Tugas 2 - Menampilkan tagihan per kogol dan penambahan keterangan_kogol (kogol, keterangankogol, jmlplg, jmltag) ##

Note penambahan keterangankogol berdasarkan kogol berikut : 
    0   = UMUM
    1   = ABRI
    2   = pemerintah non ABRI
    3   = PEMDA
    4   = BUMN/BUMD ##

```
select kogol,
    CASE WHEN kogol='0' THEN 'UMUM' 
        WHEN kogol='1' THEN 'ABRI' 
        WHEN kogol='2' THEN 'Pemerintah non ABRI' 
        WHEN kogol='3' THEN 'PEMDA'
        WHEN kogol='4' THEN 'BUMN/BUMD'
        END AS keterangankogol, count(*) jmlplg, sum(rptag) jmltag
from dpptes
group by kogol
```

## Tugas 3 - Menampilkan tagihan per unitup yang rupiah tagihan (rptag) diatas satu juta (unitup, jmlplg, jmltag) ##

```
select unitup, count(*) jmlplg, sum(rptag) jmltag from dpptes where rptag >= 1000000
group by unitup;
```

## Tugas 4 - Menampilkan tagihan per unitup yang jumlah pelanggan diatas 100 (unitup, jmlplg, jmltag) ##

```
select unitup, count(*) jmlplg, sum(rptag) jmltag from dpptes 
group by unitup having count(*) > 100;
```
