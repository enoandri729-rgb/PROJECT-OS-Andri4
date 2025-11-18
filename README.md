# project_os_Andri4

# ✅ **A. SCRIPT BASH (backup.sh)**

Ini script yang memenuhi seluruh ketentuan project:

✔ Mencari file berdasarkan ekstensi & tanggal
✔ Kompres tar + gzip
✔ Timestamp otomatis
✔ Log aktivitas
✔ Notifikasi sukses/gagal

---

## 🔥 **SCRIPT LENGKAP (copy dan simpan sebagai backup.sh)**

```bash
#!/bin/bash

# ===============================
#   SISTEM BACKUP OTOMATIS
#   LINUX LUBUNTU
# ===============================

# 1. Direktori sumber & tujuan backup
SOURCE_DIR="$HOME/project2/source"
BACKUP_DIR="$HOME/project2/backups"
LOG_FILE="$HOME/project2/backup.log"

# 2. Membuat timestamp
TIMESTAMP=$(date +"%Y-%m-%d_%H-%M-%S")
BACKUP_NAME="backup_$TIMESTAMP.tar.gz"

echo "===== BACKUP DIMULAI pada $TIMESTAMP =====" >> "$LOG_FILE"

# 3. Mencari file berdasarkan ekstensi & tanggal modifikasi
FILES=$(find "$SOURCE_DIR" -type f \( -name "*.txt" -o -name "*.log" -o -name "*.conf" \) -mtime -3)

if [ -z "$FILES" ]; then
    echo "Tidak ada file yang ditemukan untuk backup." >> "$LOG_FILE"
    echo "Backup gagal: tidak ada file sesuai kriteria."
    exit 1
fi

# 4. Kompresi file menggunakan tar + gzip
tar -czf "$BACKUP_DIR/$BACKUP_NAME" $FILES 2>>"$LOG_FILE"

if [ $? -ne 0 ]; then
    echo "Kompresi gagal." >> "$LOG_FILE"
    echo "Backup gagal dilakukan."
    exit 1
fi

# 5. Menyimpan backup di direktori timestamps
echo "Backup tersimpan sebagai: $BACKUP_NAME" >> "$LOG_FILE"

# 6. Log aktivitas selesai
echo "Backup selesai pada $(date)" >> "$LOG_FILE"

# 7. Notifikasi
echo "Backup berhasil dibuat: $BACKUP_NAME"
```

---

# ✅ **B. DOKUMENTASI PENGGUNAAN (Cara Menjalankan di Lubuntu)**

## **1. Buat struktur folder**

Jalankan di Terminal Lubuntu:

```bash
mkdir -p ~/project2/source
mkdir -p ~/project2/backups
touch ~/project2/backup.log
```

---

## **2. Tambahkan file contoh**

```bash
echo "catatan penting" > ~/project2/source/file1.txt
echo "log aplikasi" > ~/project2/source/app.log
echo "konfigurasi system" > ~/project2/source/system.conf
```

---

## **3. Simpan script**

```bash
nano ~/project2/backup.sh
```

Paste scriptnya.

---

## **4. Beri izin eksekusi**

```bash
chmod +x ~/project2/backup.sh
```

---

## **5. Jalankan script**

```bash
./project2/backup.sh
```

---

## **6. Hasil yang muncul**

### ✔ Backup sukses:

```
Backup berhasil dibuat: backup_2025-01-20_20-31-10.tar.gz
```

### ✔ Cek folder backup:

```
ls ~/project2/backups
```

### ✔ Cek log aktivitas:

```
cat ~/project2/backup.log
```

---

# ✅ **C. PANDUAN VIDEO DEMO (3–5 Menit)**

Anda tinggal ikuti *script narasi* ini saat rekam video.

---

## **1. Pembukaan (10–15 detik)**

“Assalamu’alaikum, saya [Nama] dari kelas Sistem Operasi B. Pada video ini saya akan mendemonstrasikan Project 2: Sistem Backup Otomatis menggunakan bash script di Linux Lubuntu.”

---

## **2. Menampilkan struktur folder (30 detik)**

Tampilkan:

```
project2/
 ├── source/
 ├── backups/
 ├── backup.log
 └── backup.sh
```

---

## **3. Menjelaskan fungsi script (60–90 detik)**

Jelaskan 5 komponen:

### 1. **Mencari file dengan find**

Mencari `.txt`, `.log`, `.conf` yang diubah 3 hari terakhir.

### 2. **Kompresi**

Script memakai `tar -czf` untuk membuat file `.tar.gz`.

### 3. **Folder timestamp**

Nama file backup unik berdasarkan tanggal & waktu.

### 4. **Log aktivitas**

Semua aktivitas dicatat di `backup.log`.

### 5. **Notifikasi**

Menampilkan “Backup berhasil” atau “Backup gagal”.

---

## **4. Menjalankan script di terminal (1 menit)**

Jalankan:

```bash
./backup.sh
```

Tunjukkan:

* File `.tar.gz` muncul
* Log terupdate
* Pesan sukses tampil

---

## **5. Penutup (10–15 detik)**

“Demikian demo sistem backup otomatis yang saya buat. Terima kasih.”

---

# ✅ **D. LAPORAN REFLEKSI PEMBELAJARAN**

Silakan copy ke laporan praktikum.

---

## **✔ Refleksi Pembelajaran**

Dalam Project 2 Sistem Backup Otomatis ini saya belajar membuat script bash yang dapat menjalankan proses backup secara otomatis. Saya mempelajari penggunaan perintah `find` untuk mencari file berdasarkan ekstensi dan tanggal modifikasi, kemudian menggabungkannya menggunakan `tar` dan `gzip`.

Saya juga belajar membuat penamaan file dengan timestamp agar backup tidak saling menimpa, serta membuat file log untuk mencatat seluruh aktivitas backup. Hal yang sangat bermanfaat adalah mengetahui cara memberikan notifikasi sederhana ketika backup berhasil atau gagal.

Project ini meningkatkan pemahaman saya tentang automasi di Linux, scripting, serta pentingnya backup untuk keamanan data. Saya merasa tugas ini sangat berguna untuk dunia kerja terutama dalam administrasi server dan DevOps.

---

# 🎉 **Semua Deliverables Sudah Lengkap**
