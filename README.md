# SoalShiftSISOP20_modul4_D01
## Soal 1. Enkripsi versi 1:
**A. Jika sebuah direktori dibuat dengan awalan “encv1_”, maka direktori tersebut akan menjadi direktori terenkripsi menggunakan metode enkripsi v1.**

**B. Jika sebuah direktori di-rename dengan awalan “encv1_”, maka direktori tersebut akan menjadi direktori terenkripsi menggunakan metode enkripsi v1.**

**C. Apabila sebuah direktori terenkripsi di-rename menjadi tidak terenkripsi, maka isi adirektori tersebut akan terdekrip.**

**D. Setiap pembuatan direktori terenkripsi baru (mkdir ataupun rename) akan tercatat ke sebuah database/log berupa file.**

**E. Semua file yang berada dalam direktori ter enkripsi menggunakan caesar cipher dengan key.**

`9(ku@AW1[Lmvgax6q5Y2Ry?+sF!^HKQiBXCUSe&0M.b%rI'7d)o4~VfZ*{#:}ETt$3J-zpc]lnh8,GwP_ND|jO`

**F. Metode enkripsi pada suatu direktori juga berlaku kedalam direktori lainnya yang ada didalamnya.**
- Fungsi Enkripsi :
```
void encription1WithLength(char* enc, int length) {
	if(strcmp(enc, ".") == 0 || strcmp(enc, "..") == 0)return;
	for(int i = length; i >= 0; i--){
		if(enc[i]=='/')break;
		if(enc[i]=='.'){
			length = i;
			break;
		}
	}
	int start = 0;
	for(int i = 0; i < length; i++){
		if(enc[i] == '/'){
			start = i+1;
			break;
		}
	}
    for ( int i = start; i < length; i++) {
		if(enc[i]=='/')continue;
        for (int j = 0; j < 87; j++) {
            if(enc[i] == key[j]) {
                enc[i] = key[(j+10) % 87];
                break;
            }
        }
    }
}

void encription1(char* enc) {
	encription1WithLength(enc, strlen(enc));
}
```
-	`char key[100] = "9(ku@AW1[Lmvgax6q'5Y2Ry?+sF!^HKQiBXCUSe&0M.b%rI'7d)o4~VfZ*{#:}ETt$3J-zpc]lnh8,GwP_ND|jO"` yaitu untuk menyimpan character key yang dipakai. Character yang memiliki panjang 87 karakter, dan key yang di pakai adalah 10, sehingga kalau di enkrip akan di geser ke kanan sebanyak 10 karakter.
-	Variable enc merupakan string yang akan dienkripsi. Apabila enc ke-i sama dengan key ke-j, maka variable enc ke-i akan diubah menjadi key ke (j+17) % 87.
-	`if(enc[i]=='/')` continue Untuk mengabaikan apabila bertemu tanda / sesuai note pada soal
-	`void encription1WithLength(char* enc, int length)` untuk mengenkripsi nama file / direktori. Misal, apabila mkdir rahasia/encv1_coba, maka yg di enkripsi hanya string encv1_coba saja, rahasia/ tidak akan di enkripsi. Begitu pula dengan ekstensi dari file. Untuk memenuhi persyaratan tsb menggunakan :
```
if(enc[i]=='/')break;
	if(enc[i]=='.'){
		length = i;
		break;
	}
    int start = 0;
	for(int i = 0; i < length; i++){
		if(enc[i] == '/'){
			start = i+1;
			break;
		}
```
- Sehingga enkripsi dimulai dari karakter ke start hingga ke length
- Fungsi Dekripsi versi 1 :
```
void decription1WithLength(char * enc, int length){
	if(strcmp(enc, ".") == 0 || strcmp(enc, "..") == 0)return;
	if(strstr(enc, "/") == NULL)return;
	for(int i = length; i >= 0; i--){
		if(enc[i]=='/')break;
		if(enc[i]=='.'){
			length = i;
			break;
		}
	}
	int start = length;
	for(int i = 0; i < length; i++){
		if(enc[i] == '/'){
			start = i+1;
			break;
		}
	}
    for ( int i = start; i < length; i++) {
		if(enc[i]=='/')continue;
        for (int j = 0; j < 87; j++) {
            if(enc[i] == key[j]) {
                enc[i] = key[(j+77) % 87];
                break;
            }
        }
    }
}
void decription1(char* enc){
	decription1WithLength(enc, strlen(enc));
}
```
- hanya berbeda di pergeseran karakter dengan enkripsi
- `char key[100] = "9(ku@AW1[Lmvgax6q'5Y2Ry?+sF!^HKQiBXCUSe&0M.b%rI'7d)o4~VfZ*{#:}ETt$3J-zpc]lnh8,GwP_ND|jO"` Untuk menyimpan character key yang dipakai. Character ini memiliki panjang 87 karakter, dan key yang di pakai adalah 10, sehingga artinya kalau di enkrip akan di geser ke kanan sebanyak 10 karakter. Jika didekripsi akan bergeser ke kanan sebanyak banyak karakter pada key (87) dikurangi key yang dipakai (10), maka 87-10=77.
- Variable enc merupakan string yang akan didekripsi. Apabila enc ke-i sama dengan key ke-j, maka variable enc ke-i akan dibah menjaid key ke (j+77) % 87.
- `if(enc[i]=='/')` continue Untuk emngabaikan apabila bertemu tanda / sesuai note pada soal
- `void decription1WithLength(char* enc, int length)` untuk mengenkripsi nama file / direktori. Misalkan apabila mkdir rahasia/encv1_coba, maka yg di enkripsi hanya string encv1_coba saja, rahasia/ tidak akan di enkripsi. Begitu juga dengan ekstensi dari file. Untuk memenuhi persyaratan tsb menggunakan :
```
if(enc[i]=='/')break;
	if(enc[i]=='.'){
		length = i;
		break;
	}
    int start = 0;
	for(int i = 0; i < length; i++){
		if(enc[i] == '/'){
			start = i+1;
			break;
		}
```
- Sehingga dekripsi dimulai dari karakter ke start hingga ke length


## Soal 2. Enkripsi versi 2
**A. Jika sebuah direktori dibuat dengan awalan “encv2_”, maka direktori tersebut akan menjadi direktori terenkripsi menggunakan metode enkripsi v2.**

**B. Jika sebuah direktori di-rename dengan awalan “encv2_”, maka direktori tersebut akan menjadi direktori terenkripsi menggunakan metode enkripsi v2.**
**C. Apabila sebuah direktori terenkripsi di-rename menjadi tidak terenkripsi, maka isi direktori tersebut akan terdekrip.**

**D. Setiap pembuatan direktori terenkripsi baru (mkdir ataupun rename) akan tercatat ke sebuah database/log berupa file.**

**E. Pada enkripsi v2, file-file pada direktori asli akan menjadi bagian-bagian kecil sebesar 1024 bytes dan menjadi normal ketika diakses melalui filesystem rancangan jasir. Sebagai contoh, file File_Contoh.txt berukuran 5 kB pada direktori asli akan menjadi 5 file kecil yakni: File_Contoh.txt.000, File_Contoh.txt.001, File_Contoh.txt.002, File_Contoh.txt.003, dan File_Contoh.txt.004.**

**F. Metode enkripsi pada suatu direktori juga berlaku kedalam direktori lain yang ada didalam direktori tersebut (rekursif).**

## Soal 3. Sinkronisasi direktori otomatis:

**A. Kedua directory memiliki parent directory yang sama.**

**B. Kedua directory kosong atau memiliki isi yang sama. Dua directory dapat dikatakan memiliki isi yang sama jika memenuhi:**
  **i. Nama dari setiap berkas di dalamnya sama.**
  
  **ii. Modified time dari setiap berkas di dalamnya tidak berselisih lebih dari 0.1 detik.**
  
**C. Sinkronisasi dilakukan ke seluruh isi dari kedua directory tersebut, tidak hanya di satu child directory saja.**

**D. Sinkronisasi mencakup pembuatan berkas/directory, penghapusan berkas/directory, dan pengubahan berkas/directory.**
## Soal 4. Log system:
**A. Sebuah berkas nantinya akan terbentuk bernama "fs.log" di direktori *home* pengguna (/home/[user]/fs.log) yang berguna menyimpan daftar perintah system call yang telah dijalankan.**

**B. Agar nantinya pencatatan lebih rapi dan terstruktur, log akan dibagi menjadi beberapa level yaitu INFO dan WARNING.**

**C. Untuk log level WARNING, merupakan pencatatan log untuk syscall rmdir dan unlink.**

**D. Sisanya, akan dicatat dengan level INFO.**

**E. Format untuk logging yaitu:**
`[LEVEL]::[yy][mm][dd]-[HH]:[MM]:[SS]::[CMD]::[DESC ...]`





