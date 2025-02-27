# 🌍 cURL - Command Line URL Tool  

`curl` adalah tool command-line untuk mentransfer data menggunakan berbagai protokol, seperti **HTTP, HTTPS, FTP, dan lainnya**.  

---

## 📌 **Instalasi**  
### **Windows**  
1. Download dari [https://curl.se/download.html](https://curl.se/download.html)  
2. Tambahkan `curl.exe` ke **PATH environment variable** (kalau belum otomatis).  

### **Linux & macOS**  
Sudah terinstal secara default. Jika belum, install dengan:  
```sh
# Ubuntu / Debian  
sudo apt install curl  

# macOS  
brew install curl  

# CentOS / RHEL  
sudo yum install curl  


---

## 🔥 **Basic Usage**  

### **1️⃣ GET Request (Ambil Data dari API)**
```sh
curl https://jsonplaceholder.typicode.com/posts/1
```
📌 **Keterangan:** Mengambil data JSON dari API.  

---

### **2️⃣ POST Request (Kirim Data ke API)**
```sh
curl -X POST https://jsonplaceholder.typicode.com/posts \
     -H "Content-Type: application/json" \
     -d '{"title": "Halo", "body": "Ini contoh POST", "userId": 1}'
```
📌 **Keterangan:**  
- `-X POST` → Gunakan metode **POST**.  
- `-H "Content-Type: application/json"` → Header untuk JSON request.  
- `-d` → Kirim data JSON ke API.  

---

### **3️⃣ Download File dari Internet**
```sh
curl -O https://example.com/file.zip
```
📌 **Keterangan:**  
- `-O` → Simpan file dengan nama aslinya.  

Atau ganti nama file saat download:  
```sh
curl -o newname.zip https://example.com/file.zip
```

---

### **4️⃣ Simpan Output ke File**
```sh
curl https://example.com -o output.html
```
📌 **Keterangan:** Simpan HTML halaman ke file `output.html`.  

---

### **5️⃣ Follow Redirects**
```sh
curl -L https://bit.ly/3xyz123
```
📌 **Keterangan:**  
- `-L` → Ikuti redirect otomatis.  

---

### **6️⃣ Request dengan Header Custom (User-Agent)**
```sh
curl -A "MyCustomUserAgent" https://example.com
```
📌 **Keterangan:**  
- `-A` → Set User-Agent kustom.  

---

### **7️⃣ Request dengan Autentikasi (Bearer Token)**
```sh
curl -H "Authorization: Bearer your_token_here" https://api.example.com/data
```
📌 **Keterangan:**  
- `-H` → Tambahkan **Authorization header**.  

---

### **8️⃣ Upload File ke Server**
```sh
curl -X POST -F "file=@document.pdf" https://example.com/upload
```
📌 **Keterangan:**  
- `-F` → Upload file dengan form-data.  

---

## 🚀 **Daftar Flag Penting di `curl`**
| Flag | Keterangan |
|------|-----------|
| `-X` | Tentukan HTTP Method (GET, POST, PUT, DELETE, dll.) |
| `-H` | Tambahkan header ke request |
| `-d` | Kirim data dalam request body |
| `-F` | Kirim form-data (untuk upload file) |
| `-O` | Download file dengan nama aslinya |
| `-o` | Download file dengan nama custom |
| `-L` | Ikuti redirect otomatis |
| `-A` | Set User-Agent custom |
| `-u` | Kirim username & password (`-u user:pass`) |
| `--limit-rate` | Batasi kecepatan download/upload (contoh: `--limit-rate 500k`) |
| `-s` | Silent mode (tidak menampilkan progress) |
| `-v` | Verbose mode (menampilkan debug info) |

---

## 🎯 **Referensi Resmi**
📚 Dokumentasi lengkap `curl`: [https://curl.se/docs/](https://curl.se/docs/)  

**🚀 Happy Curling!**