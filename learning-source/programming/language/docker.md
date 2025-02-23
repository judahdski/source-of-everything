## Docker command list

### **1. Informasi Container**

-   `docker ps` → Menampilkan container yang sedang berjalan
-   `docker ps -a` → Menampilkan semua container (termasuk yang sudah berhenti)
-   `docker stats` → Menampilkan statistik penggunaan resource container yang sedang berjalan
-   `docker inspect <container_id>` → Menampilkan detail lengkap tentang container
-   `docker logs <container_id>` → Menampilkan log output dari container
-   `docker top <container_id>` → Menampilkan proses yang berjalan di dalam container
-   `docker diff <container_id>` → Menampilkan perubahan yang terjadi pada container

### **2. Mengelola Container**

-   `docker run <image>` → Menjalankan container dari image
-   `docker run -d <image>` → Menjalankan container di background (detached mode)
-   `docker run --name <name> <image>` → Menjalankan container dengan nama tertentu
-   `docker run -p 8080:80 <image>` → Menjalankan container dengan port mapping
-   `docker run -v /local/path:/container/path <image>` → Menjalankan container dengan volume mapping
-   `docker start <container_id>` → Menyalakan container yang sudah ada
-   `docker stop <container_id>` → Menghentikan container
-   `docker restart <container_id>` → Me-restart container
-   `docker rm <container_id>` → Menghapus container
-   `docker exec -it <container_id> bash` → Masuk ke shell dalam container

### **3. Mengelola Image**

-   `docker images` → Menampilkan daftar image yang tersedia
-   `docker pull <image>` → Mengunduh image dari Docker Hub
-   `docker build -t <image_name> .` → Build image dari Dockerfile di direktori saat ini
-   `docker tag <image_id> <new_name>` → Memberikan tag baru pada image
-   `docker push <image>` → Meng-upload image ke Docker Hub
-   `docker rmi <image_id>` → Menghapus image

### **4. Mengelola Volume dan Network**

-   `docker volume ls` → Menampilkan daftar volume
-   `docker volume rm <volume_name>` → Menghapus volume
-   `docker network ls` → Menampilkan daftar network Docker
-   `docker network create <network_name>` → Membuat network baru
-   `docker network connect <network_name> <container_id>` → Menghubungkan container ke network

### **5. Docker Compose**

-   `docker-compose up` → Menjalankan semua container dalam `docker-compose.yml`
-   `docker-compose up -d` → Menjalankan container di background
-   `docker-compose down` → Menghentikan dan menghapus container dari `docker-compose.yml`
-   `docker-compose ps` → Menampilkan status container yang dikelola oleh Compose
