# PROJECT-OS-Andri4

Baik! Berikut saya buatkan **struktur lengkap Project 2: Sistem Backup Otomatis**, termasuk:

✅ Script bash lengkap
✅ Penjelasan cara kerjanya
✅ Format dokumentasi penggunaan
✅ Ide untuk video demo
✅ Contoh laporan refleksi

Semua sudah siap kamu gunakan untuk tugas kampus 👍

---

# 🎯 **1. Script Bash Backup Otomatis (backup.sh)**

Script ini sudah memenuhi seluruh komponen wajib.

> **CATATAN:** *Tidak saya jalankan, hanya simulasi & penjelasan. Kamu bisa copy-paste ke file `.sh`.*

---

# 📌 **backup.sh (lengkap & siap pakai)**

```bash
#!/bin/bash

# ================================
# SCRIPT BACKUP OTOMATIS
# ================================

# Direktori sumber yang ingin dibackup
SOURCE_DIR="/home/user/data_penting"

# Direktori tujuan backup
BACKUP_DIR="/home/user/backup"

# Buat folder tujuan jika belum ada
mkdir -p "$BACKUP_DIR"

# Tanggal dan waktu untuk nama file
TIMESTAMP=$(date +"%Y-%m-%d_%H-%M-%S")

# File log
LOG_FILE="/home/user/backup/backup.log"

echo "===== Backup dimulai: $TIMESTAMP =====" >> "$LOG_FILE"

# ================================
# 1. Cari file berdasarkan kriteria
# (pdf & docx yang diubah 7 hari terakhir)
# ================================

echo "[INFO] Mencari file yang akan dibackup..." >> "$LOG_FILE"

FILES=$(find "$SOURCE_DIR" -type f \( -name "*.pdf" -o -name "*.docx" \) -mtime -7)

if [ -z "$FILES" ]; then
    echo "[WARNING] Tidak ada file yang memenuhi kriteria." >> "$LOG_FILE"
    echo "Backup GAGAL (tidak ada file memenuhi syarat)"
    exit 1
fi

# Simpan file ke list sementara
TMP_LIST="/tmp/backup_list_$TIMESTAMP.txt"
echo "$FILES" > "$TMP_LIST"

# ================================
# 2. Kompresi file
# ================================

BACKUP_FILE="$BACKUP_DIR/backup_$TIMESTAMP.tar.gz"

echo "[INFO] Mengkompres file..." >> "$LOG_FILE"
tar -czf "$BACKUP_FILE" -T "$TMP_LIST"

if [ $? -ne 0 ]; then
    echo "[ERROR] Kompresi gagal." >> "$LOG_FILE"
    echo "Backup GAGAL saat kompresi!"
    exit 1
fi

# ================================
# 3. Pindahkan file backup
# (Sudah otomatis karena tar.gz dibuat di BACKUP_DIR)
# ================================

echo "[INFO] File backup disimpan di: $BACKUP_FILE" >> "$LOG_FILE"

# ================================
# 4. Menulis log
# ================================

echo "[SUCCESS] Backup berhasil diselesaikan." >> "$LOG_FILE"
echo "===== Backup selesai: $TIMESTAMP =====" >> "$LOG_FILE"

# ================================
# 5. Notifikasi sederhana
# ================================

echo "Backup BERHASIL! File tersimpan: $BACKUP_FILE"
```

---

# 📘 **Penjelasan Singkat Cara Kerja Script**

| Bagian                  | Fungsi                                |
| ----------------------- | ------------------------------------- |
| `find`                  | mencari file pdf/docx 7 hari terakhir |
| `tar -czf`              | mengkompres menjadi .tar.gz           |
| `mkdir -p`              | membuat direktori backup otomatis     |
| `date`                  | menambahkan timestamp                 |
| `echo >> backup.log`    | menulis log                           |
| `if [ $? -ne 0 ]; then` | mendeteksi error                      |

---

# 📝 **2. Dokumentasi Penggunaan (Siap Copy-Paste ke Tugas)**

## **Cara Menjalankan Script Backup Otomatis**

### **1. Simpan script sebagai:**

```
backup.sh
```

### **2. Beri izin eksekusi:**

```
chmod +x backup.sh
```

### **3. Jalankan script:**

```
./backup.sh
```

### **4. Hasil Backup**

File backup akan disimpan di:

```
/home/user/backup/backup_YYYY-MM-DD_HH-MM-SS.tar.gz
```

### **5. Log aktivitas**

Cek file log:

```
cat /home/user/backup/backup.log
```

---

# 🎥 **3. Skenario Video Demo (3–5 Menit)**

Berisi:

### ✔️ **Pembukaan (10–20 detik)**

* Nama & kelas
* Deskripsi project

### ✔️ **Isi Video**

1. Menunjukkan struktur folder sebelum backup
2. Menjalankan script:

   ```
   ./backup.sh
   ```
3. Menunjukkan:

   * file backup .tar.gz terbentuk
   * isi log file
4. Membuka file dalam arsip untuk menunjukkan berhasil

### ✔️ **Penutup**

* Ringkas cara kerja script
* Apa yang dipelajari

---

# 📄 **4. Contoh Laporan Refleksi Pembelajaran (Singkat & Siap Pakai)**

### **Refleksi Pembelajaran**

Pada project ini, saya mempelajari bagaimana mengotomatisasi proses backup menggunakan Bash scripting. Saya memahami penggunaan perintah Linux seperti `find`, `tar`, `gzip`, `mkdir`, dan `echo` untuk log aktivitas.

Saya juga belajar bagaimana mendeteksi error dengan `if [ $? -ne 0 ]`, serta membuat timestamp otomatis untuk manajemen versi file backup. Tantangan yang saya hadapi adalah memahami opsi tar dan membuat log yang rapi, namun akhirnya dapat terselesaikan setelah mencoba beberapa pendekatan.

Project ini meningkatkan kemampuan saya dalam scripting dan memahami pentingnya backup otomatis untuk menjaga keamanan data.

---
