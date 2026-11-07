# Panduan Tuckfill

Tuckfill adalah ekstensi Chrome untuk teks yang sering kamu ketik di form: email test, password, alamat, template. Simpan sekali, lalu isi field mana pun lewat tombol kecil di dalam field. Semua data tersimpan **terenkripsi di laptop kamu sendiri** dan tidak dikirim ke mana pun.

> Panduan ini juga ada di dalam zip Tuckfill sebagai `PANDUAN.html`. File itu bisa dibuka tanpa internet dan bisa di-print ke PDF.

**Isi:** [1. Pasang](#1-pasang) · [2. Mulai](#2-mulai) · [3. Nyalakan di situs](#3-nyalakan-di-situs) · [4. Isi field](#4-isi-field) · [5. Set](#5-set-isi-beberapa-field-sekaligus) · [6. Touch ID, auto-lock, backup](#6-touch-id-auto-lock-dan-backup) · [7. Lapor masalah](#7-lapor-masalah) · [Batasan dan tanya jawab](#batasan-dan-tanya-jawab)

---

## 1. Pasang

1. Unzip file `tuckfill-<versi>.zip` ke folder yang **tetap**, misalnya `Documents/Tuckfill`. Jangan dihapus atau dipindah, karena Chrome menjalankan Tuckfill dari folder itu.
2. Buka `chrome://extensions` di address bar, lalu nyalakan **Developer mode** di pojok kanan atas.
3. Klik **Load unpacked**, lalu pilih folder tadi (folder yang berisi `manifest.json` dan `PANDUAN.html`).
4. Klik ikon puzzle di toolbar Chrome, lalu pin **Tuckfill** supaya selalu kelihatan.

<img src="images/install.jpg" width="720" alt="Halaman chrome://extensions dengan Developer mode menyala dan kartu Tuckfill">

> **Update ke versi baru:** timpa isi folder yang **sama** dengan isi zip baru, lalu di `chrome://extensions` klik ikon reload di kartu Tuckfill. Data kamu tetap ada.

## 2. Mulai

### Buat passphrase

Klik ikon Tuckfill, lalu buat **passphrase** minimal 10 karakter. Passphrase ini mengunci semua entry kamu.

> [!WARNING]
> **Ingat baik-baik.** Kalau lupa, data tidak bisa dipulihkan, oleh siapa pun.

Kamu cukup memasukkannya sekali per sesi browser. Setelah itu kamu bisa pakai Touch ID (lihat [bagian 6](#6-touch-id-auto-lock-dan-backup)).

<img src="images/setup.jpg" width="300" alt="Layar setup Tuckfill: buat passphrase">

### Simpan entry pertama

Klik **Add** di checklist **Get started**, isi **Name** dan **Value**, lalu klik **Add entry**.

- **Secret**: untuk password atau token. Disamarkan (••••), tidak bisa dicari, dan tidak bisa di-copy.
- **Only on this site**: entry hanya muncul di situs yang sedang dibuka. Matikan supaya muncul di semua situs.
- **Group**: opsional, untuk mengelompokkan, misalnya "Staging ACME".

<img src="images/add-single.jpg" width="300" alt="Form Add entry dengan value qa+{{random}}@acme.test">

**Nilai dinamis.** Tulis kode ini di dalam value, dan Tuckfill menggantinya setiap kali mengisi:

| Tulis | Jadi |
|---|---|
| `{{random}}` | 6 angka acak, misalnya 481920 |
| `{{date}}` | tanggal hari ini, misalnya 2026-11-06 |
| `{{time}}` | jam, misalnya 14:05 |
| `{{uuid}}` | ID unik panjang |

Contoh di gambar: `qa+{{random}}@acme.test` memberi email baru setiap kali daftar.

## 3. Nyalakan di situs

Tuckfill hanya aktif di situs yang kamu pilih sendiri.

1. Buka situs yang mau diisi.
2. Klik ikon Tuckfill, lalu nyalakan switch di bagian atas (**Show the in-field button here**).
3. Chrome akan minta izin untuk **situs itu saja**. Klik **Allow**.

Untuk mematikannya, matikan lagi switch yang sama. Daftar semua situs yang menyala ada di Settings → **Sites**.

<img src="images/get-started.jpg" width="300" alt="Popup Tuckfill dengan switch situs menyala dan checklist Get started">

## 4. Isi field

1. Klik field di situs itu. Tombol biru kecil muncul di dalam field.
2. Klik tombolnya, lalu pilih entry. Bisa juga ketik untuk mencari, lalu tekan <kbd>Enter</kbd>.
3. Nilainya masuk ke field. Tuckfill **tidak pernah** menekan tombol submit, jadi kamu tetap bisa cek dulu. Salah pilih? Klik **Undo**.

| ① Tombol di dalam field | ② Pilih entry | ③ Terisi, dengan angka acak baru |
|---|---|---|
| <img src="images/field-button.jpg" width="260" alt="Field email dengan tombol biru Tuckfill"> | <img src="images/picker.jpg" width="260" alt="Picker Tuckfill terbuka di bawah field email"> | <img src="images/filled-single.jpg" width="260" alt="Field email terisi dengan toast Undo"> |

Shortcut keyboard: klik field, lalu tekan <kbd>Alt</kbd>+<kbd>Shift</kbd>+<kbd>F</kbd> (Mac: <kbd>⌥ Option</kbd>+<kbd>Shift</kbd>+<kbd>F</kbd>). Di picker, pakai <kbd>↑</kbd> <kbd>↓</kbd> dan <kbd>Enter</kbd>, lalu <kbd>Esc</kbd> untuk menutup.

## 5. Set: isi beberapa field sekaligus

Untuk akun test yang terdiri dari beberapa nilai, misalnya Corporate ID + User ID + Password, buat satu **set**:

1. Klik **Add entry**, lalu pilih **Set of fields**.
2. Isi nama tiap field **mirip label di form** ("Email", "User ID", "No. HP", "Kata sandi"), lalu isi nilainya.
3. Tandai password dengan **Secret**.

<img src="images/add-set.jpg" width="300" alt="Form Add entry mode Set of fields dengan Corporate ID, User ID, dan Password">

Klik field **mana saja** di form itu, lalu pilih set-nya. Tiap nilai masuk ke field yang namanya cocok.

| Klik field mana saja, pilih set-nya | Tiga field terisi sekaligus |
|---|---|
| <img src="images/picker-set.jpg" width="340" alt="Picker terbuka di field Corporate ID"> | <img src="images/filled-set.jpg" width="340" alt="Tiga field terisi dengan toast Filled 3 fields"> |

- Field yang tidak ketemu pasangannya **dilewati**, tidak ditebak. Toast akan bilang, misalnya "Filled 2 of 3, 1 not found".
- Password hanya diisi ke kotak password.
- Satu klik **Undo** mengembalikan semua field.
- Dalam satu set, semua `{{random}}` memakai angka yang sama.

## 6. Touch ID, auto-lock, dan backup

Semua ada di **Settings** (ikon slider di kanan atas popup).

<img src="images/settings.jpg" width="300" alt="Settings Tuckfill: Lock, Backup, Sites">

**Touch ID / Windows Hello.** Buka Settings → Lock → **Unlock with Touch ID**, atau terima tawarannya setelah memasukkan passphrase. Simpan passkey ke **iCloud Keychain** atau **Google Password Manager**, bukan "This Chrome profile". Passphrase tetap diminta setiap 2 minggu supaya tidak lupa. Di dalam halaman web, Touch ID hanya jalan di situs https.

**Auto-lock.** Tuckfill terkunci sendiri setelah tidak dipakai (default 15 menit) dan saat Chrome ditutup.

**Backup.**
- **Export** menyimpan file `.tuckfill` terenkripsi, dibuka dengan passphrase yang sama. Lakukan rutin, karena ini satu-satunya cadangan kalau laptop rusak atau passphrase lupa.
- **Import** menggabungkan file `.tuckfill` atau `.csv` tanpa menghapus entry yang sudah ada.
- Di laptop baru, pilih **Restore from a backup** saat setup.
- Ekspor CSV biasa juga ada, tapi file itu **tidak terenkripsi**.

## 7. Lapor masalah

1. Buka Settings, scroll ke **About**, lalu klik **Copy**. Ini menyalin versi Tuckfill, versi Chrome, dan OS, **tanpa** entry atau situs kamu.
2. Kirim lewat chat, atau buka **Issue** di repo ini, dengan format:

| | |
|---|---|
| **Detail** | hasil Copy dari About |
| **Situs** | alamat halaman form-nya |
| **Langkah** | apa yang kamu lakukan |
| **Harapan** | apa yang seharusnya terjadi |
| **Kenyataan** | apa yang terjadi |
| **Screenshot** | form-nya, kalau soal pengisian |

> [!CAUTION]
> Jangan kirim password, isi entry, atau screenshot popup yang menampilkan isi entry.

<img src="images/settings-about.jpg" width="300" alt="Bagian About di Settings dengan tombol Copy">

## Batasan dan tanya jawab

- Maksimal **1.000 entry** (sekitar 3 MB). Satu value maksimal 5.000 karakter, nama entry 60 karakter, 2–12 field per set. File import maksimal 5 MB.
- Belum bisa mengisi dropdown, checkbox, radio, atau field di dalam iframe dari situs lain.
- Nilai yang diisi pasti terlihat oleh situs itu (memang itu tujuannya), jadi isi hanya di situs yang kamu percaya.

**Tombol tidak muncul di field?**
Pastikan switch situs di popup sudah menyala. Tuckfill hanya jalan di halaman http/https biasa, tidak di halaman `chrome://` atau Chrome Web Store.

**Entry saya hilang setelah update?**
Seharusnya tidak, karena Tuckfill punya ID tetap di folder mana pun. Pastikan versi lama sudah di-*remove* (jangan ada dua Tuckfill terpasang), lalu buka popup lagi. Kalau tetap kosong, restore dari backup dan laporkan.

**Lupa passphrase?**
Tidak bisa dipulihkan. Pilih "Forgot passphrase?" untuk reset (semua entry terhapus), lalu restore dari backup kalau punya.

---

<sub>Gambar di panduan ini memakai situs contoh dan data palsu. Screenshot diambil otomatis dari build Tuckfill (`npm run guide:shots` di repo kode).</sub>
