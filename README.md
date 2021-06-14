
# PR Sisi 1 - PLSQL #

## Tugas 1 ##
### Membuat tabel view dari dpptes yang kdgerakmasuk 11 dan kdgerakkeluar 23 atau 24 ###
```
create or replace view vw_ms_soal1
    as 
    select * from dpptes where kdgerakmasuk = '11' and kdgerakkeluar in ('23','24');
```

### Melihat hasil fungsi ###
```
select * from vw_ms_soal1
```

![Gambar 1.0](images/tugas1_membuat_view.PNG)


## Tugas 2 ##
###  Membuat tabel view dari dpptes yang rpptl diantara 1 juta sampai 10 juta ###
```
create or replace view vw_ms_soal2
    as 
    select * from dpptes where rpptl between 1000000 and 10000000;
```

### Melihat hasil fungsi ###
```
select * from vw_ms_soal2
```

![Gambar 2.0](images/tugas2_membuat_view_rpptl.PNG)

## Tugas 3 ##
### Membuat tabel view dari tabel dpptes yang tgllunas dari tanggal 2015-04-06 sampai 2015-04-14 ###
```
create or replace view vw_ms_soal3
    as 
    select blth,idpel,nopel,tgllunas from dpptes where tgllunas 
    between to_date('2015-04-06', 'yyyy-mm-dd') and to_date ('2015-04-14', 'yyyy/mm/dd');
```

### Melihat hasil fungsi ###
```
select * from vw_ms_soal3
```

![Gambar 3.0](images/tugas3_membuat_view_by_tgllunas.PNG)

## Tugas 4 ##
### Membuat function perkalian ###
```
create or replace function func_ms_soal4(in_param1 integer, in_param2 integer) return integer
as
    result integer;
begin
    result := in_param1 * in_param2;
    return result;
end;
```

### Melihat hasil fungsi ###
```
select sqltrain.func_ms_soal4(5,5) result from dual;
```

![Gambar 4.0](images/tugas4_membuat_function_perkalian.PNG)

## Tugas 5 ##
### Membuat function tanggal hari ini ###
```
create or replace function func_ms_soal5 return varchar2
as
begin
    return to_char(sysdate, 'DD/MM/YYYY HH24:MI');
end;
```

### Melihat hasil fungsi ###
```
select sqltrain.func_ms_soal5 result from dual;
```

![Gambar 5.0](images/tugas5_membuat_function_tanggal_hari_ini.PNG)

## Tugas 6 ##
### Membuat function konversi dari dua digit bulan ke nama bulan ###
```
create or replace function func_ms_soal6(in_param integer) return varchar2
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
select sqltrain.func_ms_soal6(03) result from dual;
```

![Gambar 6.0](images/tugas6_membuat_function_konversi_dari_dua_digit_bulan_ke_nama_bulan.PNG)


### Catatan: Buatlah Tabel DPPTES Terlebih Dahulu ###
```
DROP TABLE SQLTRAIN.DPPTES CASCADE CONSTRAINTS;

CREATE TABLE SQLTRAIN.DPPTES
(
  BLTH               VARCHAR2(6 BYTE),
  IDPEL              VARCHAR2(12 BYTE),
  NOPEL              VARCHAR2(11 BYTE),
  KDGERAKMASUK       VARCHAR2(2 BYTE)           DEFAULT '11'                  NOT NULL,
  UPLOADTIME         DATE                       NOT NULL,
  UPLOADBY           VARCHAR2(30 BYTE),
  KDGERAKKELUAR      VARCHAR2(2 BYTE),
  TGLBAYAR           VARCHAR2(8 BYTE),
  WKTBAYAR           VARCHAR2(6 BYTE),
  KDPP               VARCHAR2(14 BYTE),
  KDPEMBAYAR         VARCHAR2(30 BYTE),
  KDKOREKSI          VARCHAR2(1 BYTE),
  TGKOREKSI          VARCHAR2(8 BYTE),
  STATUS             VARCHAR2(1 BYTE)           NOT NULL,
  KDPEMBPP           VARCHAR2(2 BYTE)           DEFAULT 'R1',
  KDPEMBAYARSIP3     VARCHAR2(5 BYTE),
  UNITUP             VARCHAR2(5 BYTE)           NOT NULL,
  PEMDA              VARCHAR2(2 BYTE)           DEFAULT '00',
  NAMA               VARCHAR2(30 BYTE)          DEFAULT 'NAMA',
  PNJ                VARCHAR2(2 BYTE),
  NAMAPNJ            VARCHAR2(30 BYTE)          DEFAULT 'ALAMAT',
  NOBANG             VARCHAR2(3 BYTE),
  KETNOBANG          VARCHAR2(3 BYTE),
  RT                 VARCHAR2(3 BYTE),
  RW                 VARCHAR2(2 BYTE),
  NODLMRT            VARCHAR2(3 BYTE),
  KETNODLMRT         VARCHAR2(12 BYTE),
  LINGKUNGAN         VARCHAR2(12 BYTE),
  KODEPOS            VARCHAR2(15 BYTE),
  IDTARIP            VARCHAR2(10 BYTE)          DEFAULT '0000000000',
  TARIP              VARCHAR2(4 BYTE)           NOT NULL,
  KDPEMBTRF          VARCHAR2(1 BYTE),
  ABONMETER          VARCHAR2(1 BYTE)           DEFAULT 'M',
  DAYA               NUMBER(20)                 DEFAULT 0                     NOT NULL,
  KDAYA              VARCHAR2(1 BYTE),
  KOGOL              VARCHAR2(1 BYTE)           DEFAULT '0'                   NOT NULL,
  SUBKOGOL           VARCHAR2(3 BYTE),
  FRT                VARCHAR2(1 BYTE),
  FJN                VARCHAR2(1 BYTE),
  KDPPJ              VARCHAR2(2 BYTE),
  UNITKJ             VARCHAR2(10 BYTE),
  KDINKASO           VARCHAR2(14 BYTE),
  KDKELOMPOK         VARCHAR2(1 BYTE),
  TGLJTTEMPO         VARCHAR2(8 BYTE)           NOT NULL,
  KDDK               VARCHAR2(12 BYTE),
  TGLBACA            VARCHAR2(8 BYTE),
  SLALWBP            VARCHAR2(15 BYTE)          DEFAULT '0'                   NOT NULL,
  SAHLWBP            VARCHAR2(15 BYTE)          DEFAULT '0'                   NOT NULL,
  SLAWBP             VARCHAR2(15 BYTE)          DEFAULT '0'                   NOT NULL,
  SAHWBP             VARCHAR2(15 BYTE)          DEFAULT '0'                   NOT NULL,
  SLAKVARH           VARCHAR2(15 BYTE)          DEFAULT '0'                   NOT NULL,
  SAHKVARH           VARCHAR2(15 BYTE)          DEFAULT '0'                   NOT NULL,
  SKVAMAX            VARCHAR2(15 BYTE)          DEFAULT '0',
  FAKM               VARCHAR2(8 BYTE)           DEFAULT '100',
  FAKMKVARH          VARCHAR2(8 BYTE)           DEFAULT '0',
  FAKMKVAMAX         VARCHAR2(8 BYTE)           DEFAULT '0',
  KWHLWBP            NUMBER(9)                  DEFAULT 0                     NOT NULL,
  KWHWBP             NUMBER(9)                  DEFAULT 0                     NOT NULL,
  BLOK3              NUMBER(9)                  DEFAULT 0                     NOT NULL,
  PEMKWH             NUMBER(9)                  DEFAULT 0                     NOT NULL,
  KWHKVARH           NUMBER(9)                  DEFAULT 0                     NOT NULL,
  KELBKVARH          NUMBER(9)                  DEFAULT 0                     NOT NULL,
  RPLWBP             NUMBER(11)                 DEFAULT 0                     NOT NULL,
  RPWBP              NUMBER(11)                 DEFAULT 0                     NOT NULL,
  RPBLOK3            NUMBER(11)                 DEFAULT 0                     NOT NULL,
  RPKVARH            NUMBER(11)                 DEFAULT 0                     NOT NULL,
  RPBEBAN            NUMBER(11)                 DEFAULT 0                     NOT NULL,
  CTTLB              VARCHAR2(6 BYTE),
  RPTTLB             NUMBER(9)                  DEFAULT 0                     NOT NULL,
  RPPTL              NUMBER(11)                 DEFAULT 0                     NOT NULL,
  RPTB               NUMBER(9)                  DEFAULT 0                     NOT NULL,
  RPPPN              NUMBER(10)                 DEFAULT 0                     NOT NULL,
  RPBPJU             NUMBER(10)                 DEFAULT 0                     NOT NULL,
  RPTRAFO            NUMBER(9)                  DEFAULT 0                     NOT NULL,
  RPSEWATRAFO        NUMBER(9)                  DEFAULT 0                     NOT NULL,
  RPSEWAKAP          NUMBER(9)                  DEFAULT 0                     NOT NULL,
  KDANGSA            VARCHAR2(1 BYTE),
  RPANGSA            NUMBER(9)                  DEFAULT 0                     NOT NULL,
  KDANGSB            VARCHAR2(1 BYTE),
  RPANGSB            NUMBER(9)                  DEFAULT 0                     NOT NULL,
  KDANGSC            VARCHAR2(1 BYTE),
  RPANGSC            NUMBER(9)                  DEFAULT 0                     NOT NULL,
  RPMAT              NUMBER(6)                  DEFAULT 0                     NOT NULL,
  RPPLN              NUMBER(11)                 DEFAULT 0                     NOT NULL,
  RPTAG              NUMBER(11)                 DEFAULT 0                     NOT NULL,
  RPPRODUKSI         NUMBER(11)                 DEFAULT 0                     NOT NULL,
  RPSUBSIDI          NUMBER(15)                 DEFAULT 0                     NOT NULL,
  RPREDUKSI          NUMBER(9)                  DEFAULT 0                     NOT NULL,
  RPINSENTIF         NUMBER(15)                 DEFAULT 0                     NOT NULL,
  RPDISINSENTIF      NUMBER(15)                 DEFAULT 0                     NOT NULL,
  RPBK1              NUMBER(10)                 DEFAULT 0                     NOT NULL,
  RPBK2              NUMBER(10)                 DEFAULT 0                     NOT NULL,
  RPBK3              NUMBER(10)                 DEFAULT 0                     NOT NULL,
  RPTDLLAMA          NUMBER(15)                 DEFAULT 0                     NOT NULL,
  RPTDLBARU          NUMBER(15)                 DEFAULT 0                     NOT NULL,
  RPSELISIH          NUMBER(9)                  DEFAULT 0                     NOT NULL,
  NOREK              VARCHAR2(6 BYTE),
  NOAGENDA           VARCHAR2(50 BYTE),
  FLAGSOPP           VARCHAR2(1 BYTE)           DEFAULT 'Y',
  FLAGANJA           VARCHAR2(1 BYTE)           DEFAULT '0',
  KDKIRIM            VARCHAR2(20 BYTE),
  KDTERIMA           VARCHAR2(20 BYTE),
  TGLKONSLD          DATE,
  KONSLDKE           NUMBER(3)                  DEFAULT 0,
  UPDATEBY           VARCHAR2(30 BYTE),
  UPDATETIME         DATE,
  CETAK              NUMBER(2)                  DEFAULT 0,
  RPINSENTIF_KVA     NUMBER                     DEFAULT 0,
  RPINSENTIF_KWH     NUMBER                     DEFAULT 0,
  RPDISINSENTIF_KVA  NUMBER                     DEFAULT 0,
  RPDISINSENTIF_KWH  NUMBER                     DEFAULT 0,
  RPPPN_R3           NUMBER,
  RPPPN_BPTRAFO      NUMBER,
  RPPPN_SEWATRAFO    NUMBER,
  RPPPN_OPSPARAREL   NUMBER,
  RPPPN_SEWAKAP      NUMBER,
  RPPPN_LAIN         NUMBER,
  RPTAG_MAT          NUMBER,
  RPMAT_LUNAS        NUMBER,
  TGLLUNAS           DATE
)

TABLESPACE PLN
PCTUSED    0
PCTFREE    10
INITRANS   1
MAXTRANS   255
STORAGE    (
            INITIAL          64K
            NEXT             1M
            MINEXTENTS       1
            MAXEXTENTS       UNLIMITED
            PCTINCREASE      0
            BUFFER_POOL      DEFAULT
           )
LOGGING 
NOCOMPRESS 
NOCACHE;
```