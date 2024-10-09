Berikut adalah materi singkat dan padat tentang berbagai jenis algoritma yang umum digunakan, dengan penjelasan, analogi, contoh kode (dalam JavaScript), kelebihan dan kekurangan, serta contoh penggunaan:

### 1. Pencarian Linear
- **Definisi**: Mencari elemen dalam daftar dengan memeriksa setiap elemen satu per satu.
- **Analogi**: Mencari buku di rak dengan memeriksa satu per satu hingga ditemukan.
- **Contoh Kode**:
  ```javascript
  function linearSearch(arr, target) {
    for (let i = 0; i < arr.length; i++) {
      if (arr[i] === target) return i;
    }
    return -1;
  }
  ```
- **Kelebihan**: Sederhana dan mudah diimplementasikan; tidak memerlukan data yang terurut.
- **Kekurangan**: Tidak efisien untuk daftar besar; waktu pencarian O(n).
- **Contoh Penggunaan**: Mencari elemen dalam daftar yang tidak terurut.
- **Do's and Don'ts**:
  - **Do**: Gunakan untuk daftar kecil atau tidak terurut.
  - **Don't**: Gunakan untuk daftar besar jika performa penting.

### 2. Pencarian Biner
- **Definisi**: Mencari elemen dalam data yang terurut dengan membagi data menjadi dua bagian.
- **Analogi**: Mencari halaman dalam buku dengan membagi buku menjadi bagian-bagian hingga menemukan halaman yang dicari.
- **Contoh Kode**:
  ```javascript
  function binarySearch(arr, target) {
    let left = 0, right = arr.length - 1;
    while (left <= right) {
      const mid = Math.floor((left + right) / 2);
      if (arr[mid] === target) return mid;
      if (arr[mid] < target) left = mid + 1;
      else right = mid - 1;
    }
    return -1;
  }
  ```
- **Kelebihan**: Cepat dengan waktu pencarian O(log n) jika data terurut.
- **Kekurangan**: Data harus terurut; tidak efisien jika data sering berubah.
- **Contoh Penggunaan**: Mencari elemen dalam array terurut.
- **Do's and Don'ts**:
  - **Do**: Gunakan untuk data terurut atau statis.
  - **Don't**: Gunakan untuk data dinamis tanpa pengurutan.

### 3. Bubble Sort
- **Definisi**: Mengurutkan dengan membandingkan dan menukar pasangan elemen yang berdekatan.
- **Analogi**: Menggelembungkan gelembung kecil ke atas dengan cara menukarkan elemen yang lebih besar ke atas.
- **Contoh Kode**:
  ```javascript
  function bubbleSort(arr) {
    let n = arr.length;
    for (let i = 0; i < n; i++) {
      for (let j = 0; j < n - i - 1; j++) {
        if (arr[j] > arr[j + 1]) {
          [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
        }
      }
    }
    return arr;
  }
  ```
- **Kelebihan**: Mudah diimplementasikan; baik untuk data kecil.
- **Kekurangan**: Tidak efisien untuk data besar; waktu pengurutan O(n^2).
- **Contoh Penggunaan**: Mengurutkan data kecil atau sebagai dasar untuk algoritma lainnya.
- **Do's and Don'ts**:
  - **Do**: Gunakan untuk data kecil atau pendidikan.
  - **Don't**: Gunakan untuk data besar; cari algoritma pengurutan lain.

### 4. Merge Sort
- **Definisi**: Mengurutkan dengan membagi data menjadi bagian kecil, mengurutkan, lalu menggabungkannya kembali.
- **Analogi**: Membagi buku menjadi bab-bab kecil, mengurutkan setiap bab, dan menggabungkannya kembali.
- **Contoh Kode**:
  ```javascript
  function mergeSort(arr) {
    if (arr.length <= 1) return arr;
    const mid = Math.floor(arr.length / 2);
    const left = mergeSort(arr.slice(0, mid));
    const right = mergeSort(arr.slice(mid));
    return merge(left, right);
  }
  
  function merge(left, right) {
    let result = [], i = 0, j = 0;
    while (i < left.length && j < right.length) {
      if (left[i] < right[j]) result.push(left[i++]);
      else result.push(right[j++]);
    }
    return result.concat(left.slice(i)).concat(right.slice(j));
  }
  ```
- **Kelebihan**: Stabil dan efisien dengan waktu pengurutan O(n log n).
- **Kekurangan**: Memerlukan ruang tambahan untuk penggabungan.
- **Contoh Penggunaan**: Pengurutan data besar atau kompleks.
- **Do's and Don'ts**:
  - **Do**: Gunakan untuk data besar yang memerlukan stabilitas.
  - **Don't**: Gunakan jika ruang memori terbatas.

### 5. Quick Sort
- **Definisi**: Mengurutkan dengan memilih elemen pivot, mempartisi data, dan mengurutkan sub-bagian secara rekursif.
- **Analogi**: Memilih halaman dalam buku untuk dibagi menjadi bagian yang lebih kecil, lalu mengurutkan bagian tersebut.
- **Contoh Kode**:
  ```javascript
  function quickSort(arr) {
    if (arr.length <= 1) return arr;
    let pivot = arr[Math.floor(arr.length / 2)];
    let left = arr.filter(x => x < pivot);
    let middle = arr.filter(x => x === pivot);
    let right = arr.filter(x => x > pivot);
    return [...quickSort(left), ...middle, ...quickSort(right)];
  }
  ```
- **Kelebihan**: Efisien dengan waktu pengurutan rata-rata O(n log n).
- **Kekurangan**: Kasus terburuk O(n^2) jika pivot dipilih buruk.
- **Contoh Penggunaan**: Pengurutan data besar dan beragam.
- **Do's and Don'ts**:
  - **Do**: Gunakan untuk data besar dengan pivot yang baik.
  - **Don't**: Gunakan jika stabilitas penting atau data hampir terurut.

### 6. Algoritma Dijkstra
- **Definisi**: Mencari jalur terpendek dari satu simpul ke simpul lain dalam graf berbobot.
- **Analogi**: Mencari rute tercepat dalam peta kota.
- **Contoh Kode**:
  ```javascript
  function dijkstra(graph, start) {
    let distances = {};
    let visited = new Set();
    let pq = new PriorityQueue();
    pq.enqueue(start, 0);
    distances[start] = 0;
    
    while (!pq.isEmpty()) {
      let { value: node, priority: dist } = pq.dequeue();
      if (visited.has(node)) continue;
      visited.add(node);
      for (let neighbor in graph[node]) {
        let newDist = dist + graph[node][neighbor];
        if (newDist < (distances[neighbor] || Infinity)) {
          distances[neighbor] = newDist;
          pq.enqueue(neighbor, newDist);
        }
      }
    }
    return distances;
  }
  ```
- **Kelebihan**: Efisien dengan waktu O((V + E) log V), baik untuk graf dengan bobot positif.
- **Kekurangan**: Tidak cocok untuk graf dengan bobot negatif.
- **Contoh Penggunaan**: Menemukan rute tercepat dalam sistem navigasi.
- **Do's and Don'ts**:
  - **Do**: Gunakan untuk graf dengan bobot positif.
  - **Don't**: Gunakan untuk graf dengan bobot negatif; pilih algoritma lain seperti Bellman-Ford.

### 7. Algoritma A*
- **Definisi**: Mencari jalur terpendek dengan menggunakan heuristik untuk memperkirakan biaya dari simpul ke tujuan.
- **Analogi**: Menggunakan peta dengan estimasi waktu perjalanan untuk menemukan rute tercepat.
- **Contoh Kode**:
  ```javascript
  function aStar(start, goal, graph, heuristic) {
    let openSet = new PriorityQueue();
    let cameFrom = {};
    let gScore = {};
    let fScore = {};
    openSet.enqueue(start, 0);
    gScore[start] = 0;
    fScore[start] = heuristic(start);
    
    while (!openSet.isEmpty()) {
      let current = openSet.dequeue().value;
      if (current === goal) return reconstructPath(cameFrom, current);
      
      for (let neighbor in graph[current]) {
        let tentative_gScore = gScore[current] + graph[current][neighbor];
        if (tentative_gScore < (gScore[neighbor] || Infinity)) {
          cameFrom[neighbor] = current;
          gScore[neighbor] = tentative_gScore;
          fScore[neighbor] = gScore[neighbor] + heuristic(neighbor);
          openSet.enqueue(neighbor, fScore[neighbor]);
        }
      }
    }
    return [];
  }
  
  function reconstructPath(cameFrom, current) {
    let path = [current];
    while (cameFrom[current]) {


      current = cameFrom[current];
      path.unshift(current);
    }
    return path;
  }
  ```
- **Kelebihan**: Efisien dengan waktu pencarian terpendek dan heuristik yang baik.
- **Kekurangan**: Kinerja sangat bergantung pada heuristik.
- **Contoh Penggunaan**: Pengaturan rute dalam game atau sistem navigasi.
- **Do's and Don'ts**:
  - **Do**: Gunakan dengan heuristik yang akurat.
  - **Don't**: Gunakan jika heuristik tidak memadai atau tidak tersedia.

### 8. Algoritma Floyd-Warshall
- **Definisi**: Mencari jalur terpendek antara semua pasangan simpul dalam graf berbobot.
- **Analogi**: Mencari jarak terpendek antara semua kota dalam jaringan transportasi.
- **Contoh Kode**:
  ```javascript
  function floydWarshall(graph) {
    let dist = JSON.parse(JSON.stringify(graph));
    let nodes = Object.keys(graph);
    
    for (let k of nodes) {
      for (let i of nodes) {
        for (let j of nodes) {
          if (dist[i][k] + dist[k][j] < dist[i][j]) {
            dist[i][j] = dist[i][k] + dist[k][j];
          }
        }
      }
    }
    return dist;
  }
  ```
- **Kelebihan**: Menyediakan jalur terpendek antara semua pasangan simpul.
- **Kekurangan**: Kompleksitas waktu O(n^3), tidak efisien untuk graf besar.
- **Contoh Penggunaan**: Sistem perencanaan rute yang kompleks.
- **Do's and Don'ts**:
  - **Do**: Gunakan untuk graf dengan bobot positif dan sedikit simpul.
  - **Don't**: Gunakan untuk graf besar dengan banyak simpul.

### 9. Algoritma Fibonacci
- **Definisi**: Menghitung bilangan Fibonacci menggunakan pendekatan rekursif.
- **Analogi**: Menyusun deret Fibonacci seperti merangkai kalimat dengan menambahkan kata-kata yang dihasilkan sebelumnya.
- **Contoh Kode**:
  ```javascript
  function fibonacci(n) {
    if (n <= 1) return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
  }
  ```
- **Kelebihan**: Konsep sederhana dan mudah diimplementasikan.
- **Kekurangan**: Tidak efisien dengan waktu O(2^n) untuk n besar.
- **Contoh Penggunaan**: Studi matematika dan rekursi.
- **Do's and Don'ts**:
  - **Do**: Gunakan untuk pemahaman rekursi atau n kecil.
  - **Don't**: Gunakan untuk n besar; pertimbangkan teknik lain seperti memoization.

### 10. Algoritma Divide and Conquer
- **Definisi**: Memecah masalah menjadi sub-masalah yang lebih kecil, menyelesaikan sub-masalah tersebut, lalu menggabungkannya.
- **Analogi**: Memecah proyek besar menjadi tugas-tugas kecil, menyelesaikannya satu per satu, lalu menggabungkannya.
- **Contoh Kode**:
  ```javascript
  function divideAndConquer(arr) {
    if (arr.length <= 1) return arr;
    let mid = Math.floor(arr.length / 2);
    let left = divideAndConquer(arr.slice(0, mid));
    let right = divideAndConquer(arr.slice(mid));
    return merge(left, right);
  }
  
  function merge(left, right) {
    let result = [], i = 0, j = 0;
    while (i < left.length && j < right.length) {
      if (left[i] < right[j]) result.push(left[i++]);
      else result.push(right[j++]);
    }
    return result.concat(left.slice(i)).concat(right.slice(j));
  }
  ```
- **Kelebihan**: Mengatasi masalah kompleks dengan membaginya menjadi sub-masalah yang lebih mudah.
- **Kekurangan**: Membutuhkan manajemen memori dan overhead penggabungan.
- **Contoh Penggunaan**: Algoritma pengurutan, pencarian, dan masalah kompleks lainnya.
- **Do's and Don'ts**:
  - **Do**: Gunakan untuk masalah yang bisa dibagi menjadi sub-masalah independen.
  - **Don't**: Gunakan jika overhead pemecahan dan penggabungan terlalu tinggi.

### 11. RSA
- **Definisi**: Algoritma kriptografi kunci publik untuk enkripsi dan dekripsi data.
- **Analogi**: Mengunci kotak dengan dua kunci; satu untuk mengunci (enkripsi) dan satu untuk membuka (dekripsi).
- **Contoh Kode**:
  ```javascript
  // RSA Implementation is complex and requires libraries. Here is a simplified example.
  const crypto = require('crypto');

  function rsaEncryptDecrypt() {
    const { publicKey, privateKey } = crypto.generateKeyPairSync('rsa', {
      modulusLength: 2048,
    });

    const message = 'Hello World!';
    const encrypted = crypto.publicEncrypt(publicKey, Buffer.from(message));
    const decrypted = crypto.privateDecrypt(privateKey, encrypted);
    return decrypted.toString();
  }
  ```
- **Kelebihan**: Keamanan tinggi dengan kunci publik dan privat.
- **Kekurangan**: Kinerja lebih lambat dibandingkan dengan metode kriptografi simetris.
- **Contoh Penggunaan**: Pengamanan komunikasi data seperti email dan transaksi online.
- **Do's and Don'ts**:
  - **Do**: Gunakan untuk pengamanan data dengan kebutuhan kunci publik.
  - **Don't**: Gunakan jika kecepatan kriptografi lebih penting.

### 12. AES (Advanced Encryption Standard)
- **Definisi**: Algoritma kriptografi simetris yang digunakan untuk enkripsi data.
- **Analogi**: Kunci yang sama digunakan untuk mengunci dan membuka kotak.
- **Contoh Kode**:
  ```javascript
  const crypto = require('crypto');

  function aesEncryptDecrypt() {
    const algorithm = 'aes-256-cbc';
    const key = crypto.randomBytes(32);
    const iv = crypto.randomBytes(16);
    
    const cipher = crypto.createCipheriv(algorithm, key, iv);
    const encrypted = Buffer.concat([cipher.update('Hello World!'), cipher.final()]);
    
    const decipher = crypto.createDecipheriv(algorithm, key, iv);
    const decrypted = Buffer.concat([decipher.update(encrypted), decipher.final()]);
    
    return decrypted.toString();
  }
  ```
- **Kelebihan**: Cepat dan efisien; sangat aman dengan kunci simetris.
- **Kekurangan**: Kunci harus dijaga kerahasiaannya.
- **Contoh Penggunaan**: Enkripsi data pada sistem penyimpanan dan komunikasi.
- **Do's and Don'ts**:
  - **Do**: Gunakan untuk enkripsi data dengan kunci simetris.
  - **Don't**: Gunakan jika pengelolaan kunci simetris menjadi masalah.

### 13. Algoritma Regresi Linear
- **Definisi**: Memodelkan hubungan antara variabel independen dan dependen.
- **Analogi**: Menarik garis lurus melalui titik-titik data untuk memprediksi nilai.
- **Contoh Kode**:
  ```javascript
  function linearRegression(x, y) {
    const n = x.length;
    const xMean = x.reduce((a, b) => a + b) / n;
    const yMean = y.reduce((a, b) => a + b) / n;

    const numerator = x.reduce((sum, xi, idx) => sum + (xi - xMean) * (y[idx] - yMean), 0);
    const denominator = x.reduce((sum, xi) => sum + Math.pow(xi - xMean, 2), 0);

    const slope = numerator / denominator;
    const intercept = yMean - slope * xMean;

    return { slope, intercept };
  }
  ```
- **Kelebihan**: Mudah dipahami dan diimplementasikan; efektif untuk hubungan linear.
- **Kekurangan**: Hanya untuk hubungan linear; tidak cocok untuk data non-linear.
- **Contoh Penggunaan**: Prediksi harga berdasarkan fitur seperti ukuran atau lokasi.
- **Do's and Don'ts**:
  - **Do**: Gunakan jika data menunjukkan hubungan linear.
  - **Don't**: Gunakan jika hubungan data non-linear.

### 14. Algoritma K-Means
- **Definisi**: Klasterisasi data dengan membagi data menjadi kelompok-kelompok homogen.
- **Analogi**: Mengelompokkan siswa ke dalam kelas berdasarkan kemiripan nilai mereka.
- **Contoh Kode**:
  ```javascript
  function kMeans(data, k) {
    let centroids = data.slice(0, k);
    let clusters = Array(k).fill().map(() => []);

    let changed;
    do {
      clusters = Array(k).fill().map(() => []);
      data.forEach(point => {
        let distances = centroids.map(centroid => Math.sqrt(point.reduce((sum, xi, i) => sum + Math.pow(xi - centroid[i], 2), 0)));
        let minIndex = distances.indexOf(Math.min(...distances));
        clusters[minIndex].push(point);
      });

      changed =

 false;
      clusters.forEach((cluster, index) => {
        let newCentroid = cluster[0].map((_, i) => cluster.reduce((sum, point) => sum + point[i], 0) / cluster.length);
        if (!newCentroid.every((value, i) => value === centroids[index][i])) {
          centroids[index] = newCentroid;
          changed = true;
        }
      });
    } while (changed);

    return { centroids, clusters };
  }
  ```
- **Kelebihan**: Sederhana dan mudah diimplementasikan untuk klasterisasi data.
- **Kekurangan**: Memerlukan pemilihan jumlah klaster k; sensitif terhadap outlier.
- **Contoh Penggunaan**: Pengelompokan pelanggan berdasarkan perilaku pembelian.
- **Do's and Don'ts**:
  - **Do**: Gunakan untuk data yang dapat dikelompokkan menjadi k klaster.
  - **Don't**: Gunakan tanpa menentukan jumlah klaster k dengan benar.

### 15. Algoritma Genetika
- **Definisi**: Mencari solusi optimal dengan prinsip evolusi biologis seperti seleksi, crossover, dan mutasi.
- **Analogi**: Mengembangkan spesies dengan pemilihan dan perkawinan untuk menghasilkan keturunan yang lebih baik.
- **Contoh Kode**:
  ```javascript
  function geneticAlgorithm(population, fitness, mutate, crossover, generations) {
    for (let i = 0; i < generations; i++) {
      let newPopulation = population.map(individual => mutate(crossover(individual)));
      population = newPopulation.sort((a, b) => fitness(b) - fitness(a)).slice(0, population.length);
    }
    return population[0];
  }
  ```
- **Kelebihan**: Baik untuk pencarian solusi dalam ruang pencarian besar.
- **Kekurangan**: Memerlukan banyak iterasi dan pengaturan parameter.
- **Contoh Penggunaan**: Optimisasi masalah kompleks seperti desain atau perencanaan.
- **Do's and Don'ts**:
  - **Do**: Gunakan untuk masalah dengan banyak variabel dan solusi optimal yang tidak diketahui.
  - **Don't**: Gunakan jika solusi bisa ditemukan dengan metode lain yang lebih efisien.

### 16. Algoritma Simulated Annealing
- **Definisi**: Mencari solusi optimal dengan metode probabilistik yang menurunkan suhu secara bertahap untuk mengeksplorasi ruang solusi.
- **Analogi**: Mendinginkan logam panas secara perlahan untuk mencapai struktur yang lebih stabil.
- **Contoh Kode**:
  ```javascript
  function simulatedAnnealing(initialState, costFunction, neighborFunction, initialTemp, coolingRate, iterations) {
    let currentState = initialState;
    let currentCost = costFunction(currentState);
    let temperature = initialTemp;

    for (let i = 0; i < iterations; i++) {
      let nextState = neighborFunction(currentState);
      let nextCost = costFunction(nextState);
      let deltaCost = nextCost - currentCost;

      if (deltaCost < 0 || Math.exp(-deltaCost / temperature) > Math.random()) {
        currentState = nextState;
        currentCost = nextCost;
      }
      temperature *= coolingRate;
    }
    return currentState;
  }
  ```
- **Kelebihan**: Baik untuk masalah optimisasi dengan banyak lokal minima.
- **Kekurangan**: Memerlukan pemilihan parameter yang tepat; hasil dapat bervariasi.
- **Contoh Penggunaan**: Pengoptimalan desain dan rute.
- **Do's and Don'ts**:
  - **Do**: Gunakan untuk masalah optimisasi dengan solusi kompleks dan banyak lokal minima.
  - **Don't**: Gunakan jika parameter sulit disesuaikan atau jika metode lain lebih efisien.