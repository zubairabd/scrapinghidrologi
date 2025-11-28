# 🌧️ TRMM Rainfall Scraper 2019
Script Python untuk melakukan **web scraping data curah hujan TRMM** (Tahun 2019) dari hidrologi.net untuk seluruh grid **TRMM-0001 s/d TRMM-2456**.  
Script sudah dilengkapi **checkpoint otomatis**, handling error, dan output CSV yang rapi.

---

## 🏷️ Status & Tools
![Python](https://img.shields.io/badge/Python-3.8+-blue?style=for-the-badge&logo=python&logoColor=white)
![BeautifulSoup](https://img.shields.io/badge/BeautifulSoup-4-green?style=for-the-badge)
![Requests](https://img.shields.io/badge/Requests-HTTP-yellow?style=for-the-badge)
![Pandas](https://img.shields.io/badge/Pandas-Dataframe-purple?style=for-the-badge&logo=pandas)
![Google Colab](https://img.shields.io/badge/Colab-Notebook-orange?style=for-the-badge&logo=googlecolab)

---

## 📁 Notebook:
👉 **[scraping.ipynb](./scraping.ipynb)**

---

## 🚀 Fitur Utama (Ringkas)
| Fitur | Deskripsi |
|-------|-----------|
| **Scraping otomatis 2456 grid** | Mengambil TRMM-0001 hingga TRMM-2456 (tahun 2019) |
| **Parsing HTML** | Menggunakan BeautifulSoup untuk membaca tabel curah hujan |
| **Anti-Blocked (User-Agent)** | Permintaan HTTP dipalsukan sebagai Chrome browser |
| **Checkpoint tiap 100 grid** | Aman jika runtime Colab terputus |
| **Progress monitoring** | Log setiap 50 grid untuk memantau proses |
| **Output CSV rapi** | Format TRMM-XXXX + 13 kolom curah hujan |
| **SSL Warning disabled** | Membersihkan output console |

---

## 🧭 Flowchart Alur Scraping

```
          ┌────────────────────┐
          │ Mulai Scraping     │
          └─────────┬──────────┘
                    │
        ┌───────────▼───────────┐
        │ Loop Grid 1–2456      │
        └───────────┬───────────┘
                    │
        ┌───────────▼───────────┐
        │ Request halaman TRMM  │
        │ dengan headers browser│
        └───────────┬───────────┘
                    │
        ┌───────────▼───────────┐
        │ Parsing tabel HTML    │
        │ Cari baris '2019'     │
        └───────────┬───────────┘
                    │
        ┌───────────▼───────────┐
        │ Apakah data ditemukan?│
        └───────┬─────┬────────┘
                │     │Tidak
              Ya│     └───────────────► Lewati grid
                │
        ┌───────▼────────┐
        │ Simpan ke list │
        └───────┬────────┘
                │
     ┌──────────▼──────────┐
     │ Checkpoint tiap 100  │
     │ → Simpan CSV sementara│
     └──────────┬───────────┘
                │
     ┌──────────▼──────────┐
     │ Grid berikutnya      │
     └──────────┬───────────┘
                │
     ┌──────────▼──────────┐
     │ Setelah selesai →    │
     │ Simpan CSV final     │
     └──────────┬───────────┘
                │
       ┌────────▼─────────┐
       │ Unduh CSV         │
       └───────────────────┘
```

---

## 🧰 Library yang Digunakan

### 🔹 `requests`
Mengirim permintaan HTTP ke URL TRMM.

### 🔹 `BeautifulSoup`
Memproses HTML dan mengekstrak tabel curah hujan.

### 🔹 `pandas`
Mengubah hasil scraping menjadi DataFrame dan CSV.

### 🔹 `urllib3`
Menonaktifkan SSL warning untuk kebersihan output Colab.

### 🔹 `time`
Mengukur progress dan runtime.

### 🔹 `google.colab.files`
Untuk mendownload file langsung dari Colab.

---

## 📦 Output
File CSV:
```
curah_hujan_2019_complete.csv
```

Kolom:
```
Grid, Jan, Feb, Mar, Apr, Mei, Jun, Jul, Agu, Sep, Okt, Nov, Des, Tahunan
```

---

## ▶️ Cara Menjalankan (Google Colab)
1. Upload file `scraping.ipynb`
2. Klik **Runtime → Run All**
3. Tunggu proses scraping (±5–15 menit)
4. File CSV otomatis muncul di bagian unduhan Colab

---

## 📊 Cuplikan Kode
```python
resp = requests.get(url, headers=headers, verify=False, timeout=10)
soup = BeautifulSoup(resp.text, "html.parser")

if cells and cells[0] == "2019":
    hasil = {"Grid": f"TRMM-{grid:04d}"}
    for i in range(len(bulan)):
        hasil[bulan[i]] = nilai_hujan[i]
```

---

## 👤 Author
**Zubair Abdurrohman**  
Data Scraping | Data Engineering | Python Enthusiast

