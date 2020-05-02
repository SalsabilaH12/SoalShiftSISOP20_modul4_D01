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
- `void encription1WithLength(char* enc, int length)` Fungsi ini berfungsi untuk mengenkripsi nama file / direktori.
- Terdapat variabel `char key[100] = ` untuk menyimpan character key yang dipakai. Character dengan panjang 87 karakter, dan key yang dipakai adalah 10, Maka, kalau di enkripsi akan bergeser kekanan sebanyak 10 karakter.
- Lalu, terdapat Variabel enc merupakan string yang akan dienkripsi. Variable enc ke-i akan diubah menjadi key ke (j+10) % 87.
- Untuk mengabaikan apabila bertemu tanda / menggunakan `if(enc[i]=='/') continue`. 
- Seperti yg dijelaskan pada soal, apabila mkdir rahasia/encv1_coba, yg di enkripsi hanya string encv1_coba saja, rahasia/ tidak akan di enkripsi. Begitu pula dengan ekstensi dari file. Untuk memenuhi persyaratan tsb menggunakan :
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
- Maka, direktori akan terenkripsi dari karakter start hingga ke length
- Fungsi Dekripsi :
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
- `void decription1WithLength(char* enc, int length)` Fungsi ini untuk mendekrip nama file / direktori. Terdapat perbedaan di pergeseran character saja dengan enkripsi. Jikalau di enkrip akan bergeser ke kanan sebanyak 10 character. Maka, dekripsi akan bergeser ke kanan sebanyak character pada key (87) dikurang key yang dipakai (10), jadi 87-10=77.
- Terdapat Variable enc merupakan string yang akan didekripsi. Variable enc ke-i akan diubah menjadi key ke (j+77) % 87.
- Untuk mengabaikan apabila bertemu tanda / menggunakan `if(enc[i]=='/')` continue
- Seperti yg dijelaskan pada soal, apabila mkdir rahasia/encv1_coba, maka yg di dekrispsi hanya string encv1_coba saja, rahasia/ tidak akan di dekripsi. Begitu juga dengan ekstensi dari file. Untuk memenuhi persyaratan tsb menggunakan :
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
- Maka, direktori akan didekripsi dari character start hingga ke length

## Soal 2. Enkripsi versi 2
**A. Jika sebuah direktori dibuat dengan awalan “encv2_”, maka direktori tersebut akan menjadi direktori terenkripsi menggunakan metode enkripsi v2.**

**B. Jika sebuah direktori di-rename dengan awalan “encv2_”, maka direktori tersebut akan menjadi direktori terenkripsi menggunakan metode enkripsi v2.**
**C. Apabila sebuah direktori terenkripsi di-rename menjadi tidak terenkripsi, maka isi direktori tersebut akan terdekrip.**

**D. Setiap pembuatan direktori terenkripsi baru (mkdir ataupun rename) akan tercatat ke sebuah database/log berupa file.**

**E. Pada enkripsi v2, file-file pada direktori asli akan menjadi bagian-bagian kecil sebesar 1024 bytes dan menjadi normal ketika diakses melalui filesystem rancangan jasir. Sebagai contoh, file File_Contoh.txt berukuran 5 kB pada direktori asli akan menjadi 5 file kecil yakni: File_Contoh.txt.000, File_Contoh.txt.001, File_Contoh.txt.002, File_Contoh.txt.003, dan File_Contoh.txt.004.**

**F. Metode enkripsi pada suatu direktori juga berlaku kedalam direktori lain yang ada didalam direktori tersebut (rekursif).**
- FUngsi Enkripsi :
```
void encription2(char * path){
	FILE * file = fopen(path, "rb");
	int count = 0;
	char topath[1000];
	sprintf(topath, "%s.%03d", path, count);
	void * buffer = malloc(1024);
	while(1){
		size_t readSize = fread(buffer, 1, 1024, file);
		if(readSize == 0)break;
		FILE * op = fopen(topath, "w");
		fwrite(buffer, 1, readSize, op);
		fclose(op);
		count++;
		sprintf(topath, "%s.%03d", path, count);
	}
	free(buffer);
	fclose(file);
	remove(path);
}
```
- `void encription2(char * path)` Fungsi ini untuk mengenkripsi nama file / direktori versi 2. 
- `FILE * file` digunakan untuk menyalin isi file yang akan di enkripsi, dengan command fopen dan fclose.
- `fopen(path, "rb");` untuk Membuka / membuat file. 
- Untuk membuka file sebagai binary file, bukan text file menggunakan "rb".
- Seperti yang terdapat di persayaratan, untuk mengformat nama file digunakan `sprintf(topath, "%s.%03d", path, count)` dengan topath yang akan berisi file yang sama dengan path, tetapi dengan format nama yang berbeda. 
- Untuk menambahkan nama file sesuai ukuran dari file dengan karakter 0 berjumlah 3 setelah titik menggunakan `"%s.%03d"`.
- Terdapat `fopen(topath, "w")` untuk mengcopy isi file ke sub-file topath. 
- Lalu, terdapat size_t fread untuk mengcopy file ke buffer atau disimpan di memory buffer
- Setelah itu, copy isi file, tutup file, dan tambahkan count(sebagai penanda berapa topath/sub-file yang sudah dibuat), serta menggunakan `sprintf(topath, "%s.%03d", path, count)` untuk mengformat nama file lagi dengan count yang sudah bertambah.
- Lanjut, jika sudah terbentuk n sub-file sama seperti ukuran file asli, maka, free buffer, tutup file, dan file aslinya dihapus.
- Fungsi deskripsi :
```
void decription2(char * path){
	FILE * check = fopen(path, "r");
	if(check != NULL)return;
	FILE * file = fopen(path, "w");
	int count = 0;
	char topath[1000];
	sprintf(topath, "%s.%03d", path, count);
	void * buffer = malloc(1024);
	while(1){
		FILE * op = fopen(topath, "rb");
		if(op == NULL)break;
		size_t readSize = fread(buffer, 1, 1024, op);
		fwrite(buffer, 1, readSize, file);
		fclose(op);
		remove(topath);
		count++;
		sprintf(topath, "%s.%03d", path, count);
	}
	free(buffer);
	fclose(file);
}
```
- `void decription2(char * path)` Fungsi ini untuk mendekrip nama file/direktori.
- `fopen(path, "r");` digunakan untuk membuka / membuat file. 
- Untuk membuka file sebagai text file dan menyalin isinya dengan command `fopen(path, "w")` menggunakan `"r"`. 
- Untuk menulis isi file asli (sub-file akan menjadi 1 file asli sesuai file sebelum di enkripsi) menggunakan `"w"`.
- Terdapat `FILE * op = fopen(topath, "rb");` digunakan untuk membuka semua sub-file yang telah di enkripsi. Jika isinya kosong, maka file tersebut tidak ada/not exist.
- size_t fread digunakan untuk mengcopy file ke buffer atau disimpan di memory buffer.
- Kemudian untuk mendekripsi kembali, sub-file hasil enkripsi harus dihapus dengan `remove(topath);`, count bertambah, lalu menggunakan `sprintf(topath, "%s.%03d", path, count)` untuk mengformat nama file kembali dengan count yang sudah bertambah dan menghapus kembali sesuai jumlah sub-file.
- Setelah sudah terbentuk n sub-file sesuai ukuran file asli, free buffer dan tutup file.
- xmp_readdir dan xmp_getattr dan yang lainnya akan memanggil fungsi enkripsi dan dekripsi tersebut. 
- pada xmp_readdir pemanggilan fungsi dekripsi akan menampilkan nama file di folder tujuan yang telah didekripsi. 
- Lalu, pemanggilan fungsi enkripsi pada xmp_getattr agar file dapat menemukan lokasi aslinya dengan nama awalnya.
- Terdapat juga fungsi lainnya yang menyesuaikan, seperti xmp_rename untuk mengganti nama file yang akan di enkripsi atau dekripsi, xmp_unlink untuk menghapus suatu file, xmp_read dan xmp_write untuk membuka / membuat file dan mengcopy isi file dst.Misal xmp_getattr dan xmp_readdir:
- xmp_getattr:
```
static  int  xmp_getattr(const char *path, struct stat *stbuf){
	char * enc1Ptr = strstr(path, encv1);
	if(lastCommand == MKNOD_STATUS || lastCommand == MKDIR_STATUS){

	}else{
		if(enc1Ptr != NULL)
			decription1(enc1Ptr);
	}
	printf("DEBUG getattr %d %s\n", lastCommand, path);
	char * enc2Ptr = strstr(path, encv2);
	int res;
	char fpath[1000];
	sprintf(fpath,"%s%s", dirpath, path);
	// printf("%s\n", fpath);
	res = lstat(fpath, stbuf);
	if (res == -1){
		if(enc2Ptr == NULL){
			return -errno;
		}else{
			sprintf(fpath,"%s%s.000", dirpath, path);
			lstat(fpath, stbuf);
			int count = 0;
			struct stat st;
			int sizeCount = 0;
			while(1){
				if(stat(fpath, &st) < 0){
					break;
				}
				count++;
				sprintf(fpath, "%s%s.%03d", dirpath, path, count);
				sizeCount += st.st_size;
			}
			stbuf->st_size = sizeCount;
		}
	}
	return 0;
}
```
- Fungsi xmp_getattr digunakan agar file dapat menemukan lokasi aslinya dengan nama awalnya.
- Untuk mengambil / mereturn path yang stringnya hanya dimulai dari encv1 menggunakan `strstr(path, encv1);`.
- Untuk mereturn informasi dari suatu file menggunakan `lstat(fpath, stbuf)` dimana informasi tsb merupakan fpath.

- xmp_readdir :
```
static int xmp_readdir(const char *path, void *buf, fuse_fill_dir_t filler, off_t offset, struct fuse_file_info *fi){

	printf("DEBUGGING %s\n", path);
	char * enc1Ptr = strstr(path, encv1);
	if(enc1Ptr != NULL)
		decription1(enc1Ptr);
	char * enc2Ptr = strstr(path, encv2);

	printf("\n\nDEBUG readdir\n\n");

	char fpath[1000];
	if(strcmp(path,"/") == 0){
		path=dirpath;
		sprintf(fpath,"%s",path);
	} else sprintf(fpath, "%s%s", dirpath, path);

	int res = 0;
	DIR *dp;
	struct dirent *de;
	(void) offset;
	(void) fi;
	dp = opendir(fpath);
	if (dp == NULL) return -errno;

	while ((de = readdir(dp)) != NULL) {
		struct stat st;
		memset(&st, 0, sizeof(st));
		st.st_ino = de->d_ino;
		st.st_mode = de->d_type << 12;
		if(enc2Ptr != NULL){
			if(de->d_type == DT_REG ){
				if(strcmp(de->d_name+(strlen(de->d_name)-4), ".000") == 0){
					de->d_name[strlen(de->d_name)-4] = '\0';
					res = (filler(buf, de->d_name, &st, 0));
				}
			}else{
				res = (filler(buf, de->d_name, &st, 0));
			}
		}else{
			if(enc1Ptr != NULL)
				encription1(de->d_name);
			res = (filler(buf, de->d_name, &st, 0));
		}
		if(res!=0) break;
	}
	closedir(dp);

	return 0;
}
```
- Pada fungsi xmp_readdir digunakan untuk menampilkan hasil dekripsi1 dari `char * enc1Ptr = strstr(path, encv1)`.
- Untuk menggabungkan path dari file yang akan di enkripsi jika enc1Ptr tidak kosong dan enc2Ptr berada di dalam menggunakan `fpathspintf(fpath, "%s", path)` dan `sprintf(fpath, "%s%s", dirpath, path);`.
- Kemudian, close(dp) digunakan untuk menutup directory apabila telah selesai menenkripsi atau mendekripsi suatu direktori

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

```
void writeWarning(char * str){
    FILE * logFile = fopen("/home/linuxlite/fs.log", "a");
    time_t rawtime;
    struct tm * timeinfo;
    time ( &rawtime );
    timeinfo = localtime (&rawtime);
    fprintf(logFile, "WARNING::%d%d%d-%d:%d:%d::%s\n", timeinfo->tm_year+1900, timeinfo->tm_mon, timeinfo->tm_mday, timeinfo->tm_hour, timeinfo->tm_min, timeinfo->tm_sec, str);
    fclose(logFile);
}

void writeInfo(char * str){
    FILE * logFile = fopen("/home/linuxlite/fs.log", "a");
    time_t rawtime;
    struct tm * timeinfo;
    time ( &rawtime );
    timeinfo = localtime (&rawtime);
    fprintf(logFile, "INFO::%d%d%d-%d:%d:%d::%s\n", timeinfo->tm_year+1900, timeinfo->tm_mon, timeinfo->tm_mday, timeinfo->tm_hour, timeinfo->tm_min, timeinfo->tm_sec, str);
    fclose(logFile);
}
```
- Fungsi `log_path` berfungsi untuk menyimpan nama path file yang akan digunakan untuk membuat file `fs.log`.
- Untuk `timeinfo->tm_year+1900, timeinfo->tm_mon, timeinfo->tm_mday, timeinfo->tm_hour, timeinfo->tm_min, timeinfo->tm_sec` adalah (tahun, bulan, hari, jam, menit, detik)
- Untuk `localtime(&rawtime)` mengambil argument time_t.
- Untuk `fprintf()` print format logging WARNING / INFO ke logFile.

Tidak lupa untuk Menaruh log `writeINFO` di fungsi `MKDIR`,` MKNOD`,`RENAME`,`TRUNCATE`,`WRITE` dan log `writeWarning` di fungsi `UNLINK`,`RMDIR` dengan mendeklarasikan array str, 
di bagian sprintf melakukan penggabungan dimana fpath yang berformat %s (berisi nama file) digabung dengan `writeInfo` atau `writeWarning` yang akan disimpan di variabel str. 
Fungsi-fungsi tersebut akan tercatat pada file yang bernama fs.log.



