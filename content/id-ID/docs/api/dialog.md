# dialog

> Tampilkan dialog sistem asli untuk membuka dan menyimpan file, mengingatkan, dll.

Proses: [Utama](../glossary.md#main-process)

Contoh menampilkan dialog untuk memilih beberapa file dan direktori:

```javascript
const {dialog} = require ('electron') console.log (dialog.showOpenDialog ({properties: ['openFile', 'openDirectory', 'multiSelections']}))
```

Dialog dibuka dari thread utama Elektron. Jika Anda ingin menggunakan objek dialog dari proses renderer, ingatlah untuk mengaksesnya dengan menggunakan remote:

```javascript
const {dialog} = membutuhkan ('elektron'). remote console.log (dialog)
```

## Metode

The ` dialog </ 0> modul memiliki metode berikut:</p>

<h3><code>dialog.showOpenDialog ([browserWindow,] options [, callback])`</h3> 

* ` jendela browser </ 0> jendela Browser(opsional)</li>
<li><code>pilihan` Objek 
  * ` judul </ 0>  String (opsional)</li>
<li><code> default jalan</ 0>  String (opsional)</li>
<li><code> buttonLabel </ 0>  String (opsional) - Label khusus untuk tombol konfirmasi, bila dibiarkan kosong, label default akan digunakan.</li>
<li><code> filter </ 0>  <a href="structures/file-filter.md"> FileFilter [] </ 1> (opsional)</li>
<li><code>properti` String [] (opsional) - Berisi fitur mana yang harus digunakan dialog. Nilai berikut didukung: 
    * ` buka file </ 0> - Memungkinkan file dipilih.</li>
<li><code> buka direktorat </ 0> - Biarkan direktori dipilih.</li>
<li><code> multi pilihan</ 0> - Memungkinkan beberapa jalur untuk dipilih.</li>
<li><code>showHiddenFiles` - Tampilkan file tersembunyi dalam dialog.
    * `createDirectory` - Biarkan membuat direktori baru dari dialog. *macOS*
    * `promptToCreate` - Prompt untuk pembuatan jika path file yang dimasukkan dalam dialog tidak ada. Ini tidak benar-benar membuat file di jalan tapi memungkinkan jalur yang tidak ada untuk dikembalikan yang harus dibuat oleh aplikasi. *Windows*
    * `noResolveAliases` - Nonaktifkan jalur alias otomatis (symlink) resolusi. Alias yang dipilih sekarang akan mengembalikan jalur alias alih-alih jalan sasaran mereka *macOS*
    * `treatPackageAsDirectory` - Perlakukan paket, seperti folder `.app` sebagai sebuah direktori, bukan sebuah file. *macOS*
  * `pesan` String (opsional) *macOS* - Pesan untuk menampilkan kotak masukan di atas.
* `callback` Fungsi (opsional) 
  * `filePaths` String[] - Kumpulan jalur file yang dipilih oleh pengguna

Mengembalikan `String[]`, sebuah array path file yang dipilih oleh pengguna, jika callback diberikan, ia akan kembali `undefined`.

Argumen `browserWindow` memungkinkan dialog untuk menempel pada jendela induk, membuatnya menjadi modal.

The `filters` menentukan kumpulan jenis file yang dapat ditampilkan atau dipilih bila Anda ingin membatasi pengguna ke tipe tertentu. Sebagai contoh:

```javascript
{
  filter: [
    {name: 'Images', extensions: ['jpg', 'png', 'gif']},
    {name: 'Movies', extensions: ['mkv', 'avi', 'mp4']},
    {name: 'Custom File Type', ekstensi: ['as']},
    {name: 'All Files', ekstensi: ['*']}
  ]
}
```

Elemen `ekstensi` harus berisi ekstensi tanpa wildcard atau titik (misalnya `'png'` bagus tapi ` '. Png'` dan ` '*.png'` buruk). Untuk menampilkan semua file, gunakan wildcard `'*'` (tidak ada wildcard lain yang didukung).

Jika `callback` dilewati, panggilan API akan menjadi asinkron dan hasilnya akan dilewatkan melalui ` callback (nama file)`

**Catatan:** Pada Windows dan Linux, sebuah dialog terbuka tidak dapat berupa pemilih file dan pemilih direktori, jadi jika Anda menetapkan `properti` ke ` ['openFile', ' openDirectory ']` pada platform ini, pemilih direktori akan ditampilkan.

### `dialog.showSaveDialog ([browserWindow,] options [, callback])`

* ` jendela browser </ 0> jendela Browser(opsional)</li>
<li><code>pilihan` Sasaran 
  * ` judul </ 0>  String (opsional)</li>
<li><code>defaultPath` String (opsional) - Jalur direktori absolut, path file absolut, atau nama file yang akan digunakan secara default.
  * ` buttonLabel </ 0>  String (opsional) - Label khusus untuk tombol konfirmasi, bila dibiarkan kosong, label default akan digunakan.</li>
<li><code> filter </ 0>  <a href="structures/file-filter.md"> FileFilter [] </ 1> (opsional)</li>
<li><code>pesan` String (opsional) *macOS* - Pesan untuk menampilkan teks di atas.
  * `nameFieldLabel` String (opsional) *macOS* - Label khusus untuk teks yang ditampilkan di depan bidang teks nama file.
  * `showsTagField` Boolean (opsional) *macOS* - Tampilkan kotak masukan tag, defaultnya `true`.
* `callback` Fungsi (opsional) 
  * `filename` String

Mengembalikan `String`, path dari file yang dipilih oleh pengguna, jika sebuah callback diberikan maka `tidak terdefinisi`.

Argumen `browserWindow` memungkinkan dialog untuk menempel pada jendela induk, membuatnya menjadi modal.

Filter `` menentukan kumpulan jenis file yang dapat ditampilkan, lihat `dialog.showOpenDialog ` untuk sebuah contoh.

Jika `callback` dilewati, panggilan API akan menjadi asinkron dan hasilnya akan dilewatkan melalui ` callback (namafile) `

### `dialog.showMessageBox ([browserWindow,] options [, callback])`

* ` jendela browser </ 0> jendela Browser(opsional)</li>
<li><code>pilihan` Sasaran 
  * `ketik` String (opsional) - Bisa jadi `"none"`, `"info"`, `"error"`, `"pertanyaan"` atau `"peringatan"`. Pada Windows, `"question"` menampilkan ikon yang sama dengan `"info"`, kecuali jika Anda menyetel ikon menggunakan opsi ` "icon" `. Pada macos, keduanya `"warning"` dan `"error"` menampilkan ikon peringatan yang sama.
  * `tombol` String[] (opsional) - Array teks untuk tombol. Pada Windows, sebuah array kosong akan menghasilkan satu tombol berlabel "OK".
  * `defaultId` Integer (opsional) - Indeks tombol pada susunan tombol yang akan dipilih secara default saat kotak pesan terbuka.
  * `title` String (opsional) - Judul kotak pesan, beberapa platform tidak akan menampilkannya.
  * `pesan` String - Isi kotak pesan.
  * `detail` String (opsional) - Informasi tambahan dari pesan.
  * `kotak centangLabe` String (opsional) - Jika tersedia, kotak pesan akan sertakan kotak centang dengan label yang diberikan. Kotak centangnya bisa jadi diperiksa hanya saat menggunakan `callback`.
  * `checkboxChecked` Boolean (opsional) - Status pemeriksaan awal dari kotak centang. `false` secara default.
  * `ikon` [NativeImage](native-image.md) (opsional)
  * `cancelId` Integer (opsional) - Indeks tombol yang akan digunakan untuk membatalkan dialog, melalui tombol `Esc`. Secara default ini diberikan ke tombol pertama dengan "cancel" atau "no" sebagai label. Jika tidak ada tombol berlabel seperti itu dan pilihan ini tidak diset, `` akan digunakan sebagai nilai balik atau respons balik. Pilihan ini diabaikan pada Windows.
  * `noLink` Boolean (opsional) - Pada Windows Electron akan mencoba untuk mencari tahu dari mana `buttons` adalah tombol yang umum (seperti "Batal" atau "Ya"), dan menampilkan yang lain sebagai link perintah dalam dialog. Hal ini bisa membuat dialog tampil dengan gaya aplikasi Windows modern . Jika Anda tidak menyukai perilaku ini, Anda dapat mengatur `noLink` to `true`.
  * `normalizeAccessKeys` Boolean (opsional) - Menormalisasi tombol akses keyboard. Defaultnya adalah ` false </ 0> . Mengaktifkan asumsi ini <code>&` digunakan pada label tombol untuk penempatan tombol akses pintas keyboard dan label akan dikonversi sehingga bekerja dengan benar pada setiap platform, `&` karakter dihapus di macos, dikonversi ke `_` di Linux, dan tidak tersentuh pada Windows. Misalnya, label tombol `Vie&w` akan dikonversi ke `Vie_w` di Linux dan ` View ` di macos dan dapat dipilih melalui `Alt-W` pada Windows dan Linux.
* `callback` Fungsi (opsional) 
  * `response` Number - Indeks tombol yang diklik
  * `checkboxChecked` Boolean - Status kotak centang jika `checkboxLabel` telah ditetapkan. Jika tidak `false`.

Mengembalikan `Integer`, indeks tombol yang diklik, jika callback diberikan, ia akan kembali terdefinisi.

Menunjukkan kotak pesan, akan memblokir proses sampai kotak pesan ditutup. Ini mengembalikan indeks tombol yang diklik.

Argumen `browserWindow` memungkinkan dialog untuk menempel pada jendela induk, membuatnya menjadi modal.

Jika `callback` dilewati, dialog tidak akan memblokir prosesnya. Panggilan API akan menjadi asinkron dan hasilnya akan dilewatkan melalui `callback (respon)`.

### `dialog.showErrorBox(judul, konten)`

* `title` String - Judul yang akan ditampilkan di kotak kesalahan
* `content` String - Isi teks untuk ditampilkan di kotak kesalahan

Menampilkan dialog modal yang menunjukkan pesan kesalahan.

API ini dapat dipanggil dengan aman sebelum `siap` acara yang digunakan aplikasi `app`, biasanya digunakan untuk melaporkan kesalahan pada tahap awal startup. Jika dipanggil sebelum acara aplikasi `siap` di Linux, pesan akan dipancarkan ke stderr, dan tidak ada dialog GUI yang akan muncul.

### `dialog.showCertificateTrustDialog ([browserWindow,] options, callback)` * macos * * Windows *

* ` jendela browser </ 0> jendela Browser(opsional)</li>
<li><code>pilihan` Sasaran 
  * `sertifikat` [Sertifikat](structures/certificate.md) - Sertifikat untuk dipercaya/diimpor.
  * `pesan` String - Pesan untuk ditampilkan kepada pengguna.
* `callback ` Fungsi

Di macos , ini menampilkan dialog modal yang menampilkan informasi pesan dan sertifikat, dan memberi pengguna pilihan untuk mempercayai / mengimpor sertifikat. Jika Anda memberikan argumen `browserWindow`, dialog akan dilampirkan ke jendela induk, membuatnya menjadi modal.

Pada Windows pilihannya lebih terbatas, karena API Win32 digunakan:

* Argumen `pesan` tidak digunakan, karena OS menyediakan dialog konfirmasinya sendiri.
* Argumen `browserWindow` diabaikan karena tidak mungkin membuat modal dialog konfirmasi ini.

## Lembar

Pada macos, dialog disajikan sebagai lembaran yang dilekatkan pada jendela jika Anda memberikan referensi `BrowserWindow` pada parameter `browserWindow`, atau modalnya jika tidak ada jendela yang disediakan.

Anda dapat memanggil `BrowserWindow.getCurrentWindow (). SetSheetOffset (offset)` untuk mengubah offset dari bingkai jendela tempat lembaran dilekatkan.