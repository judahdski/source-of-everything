Berikut adalah materi singkat untuk setiap algoritma dalam daftar Anda, mencakup definisi, analogi, contoh kode (dalam JavaScript), kelebihan dan kelemahan, contoh penggunaan, serta do's dan don'ts.

### 1. **Selection Sort**
**Definisi:** Algoritma sorting yang memilih elemen terkecil dari unsorted part dan menempatkannya di posisi yang benar.

**Analogi:** Bayangkan Anda memiliki tumpukan kartu yang harus diurutkan. Anda memilih kartu terkecil dari tumpukan yang belum diurutkan dan menempatkannya di posisi yang sesuai.

**Contoh Kode (JavaScript):**
```javascript
function selectionSort(arr) {
    for (let i = 0; i < arr.length - 1; i++) {
        let minIndex = i;
        for (let j = i + 1; j < arr.length; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        [arr[i], arr[minIndex]] = [arr[minIndex], arr[i]];
    }
    return arr;
}
```

**Kelebihan:**
- Mudah diimplementasikan.
- Tidak memerlukan memori tambahan.

**Kelemahan:**
- Kinerja buruk pada array besar (O(n²) waktu).

**Contoh Penggunaan:**
- Untuk dataset kecil dan kasus di mana penggunaan memori tambahan tidak bisa diterima.

**Do's:**
- Gunakan pada dataset kecil.

**Don'ts:**
- Jangan gunakan untuk dataset besar.

### 2. **Merge Sort**
**Definisi:** Algoritma sorting yang menggunakan metode divide-and-conquer untuk mengurutkan array dengan membaginya menjadi sub-array yang lebih kecil, mengurutkannya, dan kemudian menggabungkannya kembali.

**Analogi:** Seperti memecah buku menjadi bab-bab kecil, mengurutkannya, lalu menyatukan bab-bab tersebut untuk mendapatkan buku yang terurut.

**Contoh Kode (JavaScript):**
```javascript
function mergeSort(arr) {
    if (arr.length <= 1) return arr;
    const mid = Math.floor(arr.length / 2);
    const left = mergeSort(arr.slice(0, mid));
    const right = mergeSort(arr.slice(mid));
    return merge(left, right);
}

function merge(left, right) {
    let result = [], leftIndex = 0, rightIndex = 0;
    while (leftIndex < left.length && rightIndex < right.length) {
        if (left[leftIndex] < right[rightIndex]) {
            result.push(left[leftIndex++]);
        } else {
            result.push(right[rightIndex++]);
        }
    }
    return result.concat(left.slice(leftIndex)).concat(right.slice(rightIndex));
}
```

**Kelebihan:**
- Stabil (tidak mengubah urutan elemen dengan nilai sama).
- Kinerja konsisten O(n log n).

**Kelemahan:**
- Memerlukan memori tambahan.

**Contoh Penggunaan:**
- Pengurutan data besar yang memerlukan kestabilan.

**Do's:**
- Gunakan ketika stabilitas pengurutan penting.

**Don'ts:**
- Hindari jika memori terbatas.

### 3. **Quick Sort**
**Definisi:** Algoritma sorting yang memilih elemen pivot, mempartisi array ke dalam elemen yang lebih kecil dan lebih besar dari pivot, dan mengurutkan setiap bagian secara rekursif.

**Analogi:** Seperti membagi tumpukan kartu berdasarkan nilai tertentu dan kemudian mengurutkan setiap bagian secara terpisah.

**Contoh Kode (JavaScript):**
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

**Kelebihan:**
- Kinerja cepat rata-rata O(n log n).
- Memori tambahan minimal.

**Kelemahan:**
- Kinerja terburuk O(n²) dalam kasus tertentu.

**Contoh Penggunaan:**
- Saat memerlukan pengurutan yang cepat dan efisien.

**Do's:**
- Pilih pivot yang baik untuk menghindari kasus terburuk.

**Don'ts:**
- Hindari jika data sudah terurut sebagian besar.

### 4. **Counting Sort**
**Definisi:** Algoritma sorting yang menggunakan frekuensi kemunculan elemen untuk menentukan posisi elemen dalam array terurut.

**Analogi:** Seperti menghitung jumlah setiap jenis barang di toko dan kemudian mengurutkannya berdasarkan jumlah.

**Contoh Kode (JavaScript):**
```javascript
function countingSort(arr) {
    let max = Math.max(...arr);
    let count = Array(max + 1).fill(0);
    let output = [];
    
    for (let num of arr) {
        count[num]++;
    }
    
    for (let i = 0; i < count.length; i++) {
        while (count[i] > 0) {
            output.push(i);
            count[i]--;
        }
    }
    
    return output;
}
```

**Kelebihan:**
- Sangat efisien untuk rentang nilai kecil.

**Kelemahan:**
- Tidak cocok untuk data dengan rentang nilai besar.

**Contoh Penggunaan:**
- Pengurutan data dengan rentang nilai terbatas, seperti pengurutan umur.

**Do's:**
- Gunakan untuk data dengan nilai terbatas dan tidak negatif.

**Don'ts:**
- Hindari jika nilai data sangat bervariasi.

### 5. **Kruskal’s Algorithm**
**Definisi:** Algoritma untuk menemukan Minimum Spanning Tree (MST) dari graf berbobot dengan memilih edge yang memiliki bobot terkecil.

**Analogi:** Seperti menghubungkan kota-kota dengan jalan terpendek tanpa membentuk siklus.

**Contoh Kode (JavaScript):**
```javascript
class DisjointSet {
    constructor(n) {
        this.parent = Array.from({ length: n }, (_, i) => i);
        this.rank = Array(n).fill(0);
    }
    
    find(x) {
        if (this.parent[x] !== x) {
            this.parent[x] = this.find(this.parent[x]);
        }
        return this.parent[x];
    }
    
    union(x, y) {
        const rootX = this.find(x);
        const rootY = this.find(y);
        if (rootX !== rootY) {
            if (this.rank[rootX] > this.rank[rootY]) {
                this.parent[rootY] = rootX;
            } else if (this.rank[rootX] < this.rank[rootY]) {
                this.parent[rootX] = rootY;
            } else {
                this.parent[rootY] = rootX;
                this.rank[rootX]++;
            }
        }
    }
}

function kruskal(vertices, edges) {
    const ds = new DisjointSet(vertices);
    edges.sort((a, b) => a.weight - b.weight);
    let mst = [];
    
    for (let edge of edges) {
        if (ds.find(edge.start) !== ds.find(edge.end)) {
            ds.union(edge.start, edge.end);
            mst.push(edge);
        }
    }
    
    return mst;
}
```

**Kelebihan:**
- Cocok untuk graf dengan banyak edge.
- Memastikan MST.

**Kelemahan:**
- Kinerja tergantung pada pengurutan edge.

**Contoh Penggunaan:**
- Membangun jaringan komunikasi atau listrik.

**Do's:**
- Gunakan untuk graf berbobot dengan banyak edge.

**Don'ts:**
- Hindari jika graf sangat jarang.

### 6. **Dijkstra’s Algorithm**
**Definisi:** Algoritma untuk menemukan jarak terpendek dari sumber ke semua vertex dalam graf berbobot positif.

**Analogi:** Seperti mencari rute tercepat dari rumah ke semua tempat tujuan di peta kota.

**Contoh Kode (JavaScript):**
```javascript
function dijkstra(graph, start) {
    let distances = {};
    let priorityQueue = new PriorityQueue();
    let visited = new Set();
    
    for (let vertex of graph) {
        distances[vertex] = Infinity;
    }
    distances[start] = 0;
    priorityQueue.enqueue(start, 0);
    
    while (!priorityQueue.isEmpty()) {
        let {vertex} = priorityQueue.dequeue();
        if (visited.has(vertex)) continue;
        visited.add(vertex);
        
        for (let neighbor in graph[vertex]) {
            let newDist = distances[vertex] + graph[vertex][neighbor];
            if (newDist < distances[neighbor]) {
                distances[neighbor] = newDist;
                priorityQueue.enqueue(neighbor, newDist);
            }
        }
    }
    
    return distances;
}

class PriorityQueue {
    constructor() {
        this.queue = [];
    }
    
    enqueue(vertex, priority) {
        this.queue.push({vertex, priority});
        this.queue.sort((a, b) => a.priority - b.priority);
    }
    
    dequeue() {
        return this.queue.shift();
    }
    
    isEmpty() {
        return this.queue.length === 0;
    }
}
```

**Kelebihan:**
- Efisien untuk graf dengan bobot positif.
- Menyediakan jarak terpendek dari sumber ke semua vertex.

**Kelemahan:**
- Tidak bekerja dengan baik untuk

 graf dengan bobot negatif.

**Contoh Penggunaan:**
- Navigasi rute, jaringan komputer.

**Do's:**
- Gunakan pada graf berbobot positif.

**Don'ts:**
- Hindari jika graf memiliki bobot negatif.

### 7. **Bellman-Ford Algorithm**
**Definisi:** Algoritma untuk menemukan jarak terpendek dari sumber ke semua vertex dalam graf dengan bobot negatif (asalkan tidak ada siklus negatif).

**Analogi:** Seperti menghitung biaya perjalanan dengan mengunjungi semua jalur yang mungkin dan memilih biaya terendah.

**Contoh Kode (JavaScript):**
```javascript
function bellmanFord(graph, start) {
    let distances = {};
    for (let vertex in graph) {
        distances[vertex] = Infinity;
    }
    distances[start] = 0;
    
    for (let i = 0; i < Object.keys(graph).length - 1; i++) {
        for (let u in graph) {
            for (let v in graph[u]) {
                let newDist = distances[u] + graph[u][v];
                if (newDist < distances[v]) {
                    distances[v] = newDist;
                }
            }
        }
    }
    
    for (let u in graph) {
        for (let v in graph[u]) {
            if (distances[u] + graph[u][v] < distances[v]) {
                throw new Error('Graph contains a negative-weight cycle');
            }
        }
    }
    
    return distances;
}
```

**Kelebihan:**
- Mampu menangani graf dengan bobot negatif.

**Kelemahan:**
- Lebih lambat dari Dijkstra (O(VE)).

**Contoh Penggunaan:**
- Graph dengan bobot negatif, perencanaan rute.

**Do's:**
- Gunakan jika graf memiliki bobot negatif.

**Don'ts:**
- Hindari jika graf tidak memiliki bobot negatif.

### 8. **Floyd-Warshall Algorithm**
**Definisi:** Algoritma untuk menemukan jarak terpendek antara semua pasangan vertex dalam graf berbobot.

**Analogi:** Seperti menghitung jarak terpendek antara semua kota dalam peta.

**Contoh Kode (JavaScript):**
```javascript
function floydWarshall(graph) {
    let dist = {};
    for (let u in graph) {
        dist[u] = {};
        for (let v in graph) {
            dist[u][v] = u === v ? 0 : Infinity;
        }
        for (let v in graph[u]) {
            dist[u][v] = graph[u][v];
        }
    }
    
    for (let k in dist) {
        for (let i in dist) {
            for (let j in dist) {
                if (dist[i][j] > dist[i][k] + dist[k][j]) {
                    dist[i][j] = dist[i][k] + dist[k][j];
                }
            }
        }
    }
    
    return dist;
}
```

**Kelebihan:**
- Menyediakan jarak terpendek untuk semua pasangan vertex.
- Dapat menangani graf dengan bobot negatif.

**Kelemahan:**
- Kompleksitas waktu O(V³), tidak efisien untuk graf besar.

**Contoh Penggunaan:**
- Rute perjalanan antara semua lokasi, jaringan komunikasi.

**Do's:**
- Gunakan ketika jarak antara semua pasangan vertex diperlukan.

**Don'ts:**
- Hindari untuk graf yang sangat besar.

### 9. **Topological Sort Algorithm**
**Definisi:** Algoritma untuk mengurutkan vertex dari DAG (Directed Acyclic Graph) sehingga setiap edge dari u ke v, u muncul sebelum v dalam urutan.

**Analogi:** Seperti menyusun tugas-tugas proyek yang harus diselesaikan dalam urutan tertentu.

**Contoh Kode (JavaScript):**
```javascript
function topologicalSort(graph) {
    let stack = [];
    let visited = new Set();
    
    function visit(vertex) {
        if (visited.has(vertex)) return;
        visited.add(vertex);
        for (let neighbor of graph[vertex]) {
            visit(neighbor);
        }
        stack.push(vertex);
    }
    
    for (let vertex in graph) {
        if (!visited.has(vertex)) {
            visit(vertex);
        }
    }
    
    return stack.reverse();
}
```

**Kelebihan:**
- Berguna untuk memproses tugas yang memiliki ketergantungan.

**Kelemahan:**
- Hanya berlaku untuk DAG (graf tanpa siklus).

**Contoh Penggunaan:**
- Menyusun langkah-langkah dalam proyek, penyusunan jadwal.

**Do's:**
- Gunakan untuk DAG.

**Don'ts:**
- Jangan gunakan pada graf yang memiliki siklus.

### 10. **Flood Fill Algorithm**
**Definisi:** Algoritma untuk mengisi area yang terhubung dalam struktur data 2D, sering digunakan dalam aplikasi grafis.

**Analogi:** Seperti mengecat seluruh area yang terhubung dengan warna yang sama.

**Contoh Kode (JavaScript):**
```javascript
function floodFill(image, sr, sc, newColor) {
    let oldColor = image[sr][sc];
    if (oldColor === newColor) return image;
    
    function fill(r, c) {
        if (r < 0 || c < 0 || r >= image.length || c >= image[0].length || image[r][c] !== oldColor) return;
        image[r][c] = newColor;
        fill(r + 1, c);
        fill(r - 1, c);
        fill(r, c + 1);
        fill(r, c - 1);
    }
    
    fill(sr, sc);
    return image;
}
```

**Kelebihan:**
- Efektif untuk mengisi area terhubung dalam aplikasi grafis.

**Kelemahan:**
- Memerlukan perhatian terhadap batasan area untuk menghindari stack overflow (rekursi).

**Contoh Penggunaan:**
- Pengisian warna dalam aplikasi grafis.

**Do's:**
- Gunakan untuk mengisi area dalam gambar atau grid.

**Don'ts:**
- Hindari untuk area yang sangat besar tanpa kontrol.

### 11. **Lee Algorithm**
**Definisi:** Algoritma pencarian jalur dalam grid yang mirip dengan BFS (Breadth-First Search), digunakan untuk menemukan jalur terpendek di grid.

**Analogi:** Seperti menggunakan peta untuk menemukan jalur terpendek dari satu lokasi ke lokasi lain dalam jaringan kota.

**Contoh Kode (JavaScript):**
```javascript
function leeAlgorithm(grid, start, end) {
    let queue = [start];
    let directions = [[1, 0], [-1, 0], [0, 1], [0, -1]];
    let distance = Array.from({ length: grid.length }, () => Array(grid[0].length).fill(Infinity));
    let [sx, sy] = start;
    distance[sx][sy] = 0;
    
    while (queue.length > 0) {
        let [x, y] = queue.shift();
        for (let [dx, dy] of directions) {
            let nx = x + dx, ny = y + dy;
            if (nx >= 0 && ny >= 0 && nx < grid.length && ny < grid[0].length && grid[nx][ny] === 0 && distance[nx][ny] === Infinity) {
                distance[nx][ny] = distance[x][y] + 1;
                queue.push([nx, ny]);
            }
        }
    }
    
    return distance[end[0]][end[1]] === Infinity ? -1 : distance[end[0]][end[1]];
}
```

**Kelebihan:**
- Menyediakan jalur terpendek dalam grid.

**Kelemahan:**
- Terbatas pada grid atau graf berbobot.

**Contoh Penggunaan:**
- Pencarian jalur dalam permainan labirin.

**Do's:**
- Gunakan untuk grid atau graf berbobot.

**Don'ts:**
- Hindari untuk graf yang tidak berbentuk grid.

### 12. **Kadane’s Algorithm**
**Definisi:** Algoritma untuk menemukan subarray dengan jumlah maksimum dalam array satu dimensi.

**Analogi:** Seperti menemukan segmen dari data yang memiliki nilai total tertinggi.

**Contoh Kode (JavaScript):**
```javascript
function kadane(arr) {
    let maxCurrent = maxGlobal = arr[0];
    
    for (let i = 1; i < arr.length; i++) {
        maxCurrent = Math.max(arr[i], maxCurrent + arr[i]);
        if (maxCurrent > maxGlobal) {
            maxGlobal = maxCurrent;
        }
    }
    
    return maxGlobal;
}
```

**Kelebihan:**
- Sangat efisien dengan kompleksitas O(n).

**Kelemahan:**
- Hanya cocok untuk array satu dimensi.

**Contoh Penggunaan:**
- Menganalisis segmen data terbaik, seperti dalam analisis keuangan.

**Do's:**
- Gunakan untuk menemukan subarray maksimum dalam array satu dimensi.

**Don'ts:**
- Jangan gunakan untuk array multidimensi.

### 13. **Floyd’s Cycle Detection Algorithm**
**Definisi:** Algoritma untuk mendeteksi siklus dalam struktur data seperti linked list.

**Analogi:** Seperti mengidentifikasi apakah ada loop dalam jaringan atau jalur yang kembali ke titik awal.

**Contoh Kode

 (JavaScript):**
```javascript
function hasCycle(head) {
    let slow = head, fast = head;
    
    while (fast !== null && fast.next !== null) {
        slow = slow.next;
        fast = fast.next.next;
        
        if (slow === fast) {
            return true;
        }
    }
    
    return false;
}
```

**Kelebihan:**
- Efisien dengan kompleksitas O(n) dan memori O(1).

**Kelemahan:**
- Tidak berlaku untuk struktur data tanpa referensi berantai (linked list).

**Contoh Penggunaan:**
- Deteksi siklus dalam linked list atau graf.

**Do's:**
- Gunakan untuk deteksi siklus dalam linked list.

**Don'ts:**
- Hindari untuk struktur data non-linked list.

### 14. **KMP Algorithm**
**Definisi:** Algoritma pencarian substring yang efisien menggunakan pre-processing tabel untuk mempercepat pencarian.

**Analogi:** Seperti menggunakan panduan yang menyebutkan di mana harus melanjutkan pencarian jika ada kesalahan pencocokan.

**Contoh Kode (JavaScript):**
```javascript
function kmpSearch(text, pattern) {
    let lps = computeLPSArray(pattern);
    let i = 0, j = 0;
    
    while (i < text.length) {
        if (pattern[j] === text[i]) {
            i++;
            j++;
        }
        if (j === pattern.length) {
            return i - j;
        } else if (i < text.length && pattern[j] !== text[i]) {
            if (j !== 0) {
                j = lps[j - 1];
            } else {
                i++;
            }
        }
    }
    
    return -1;
}

function computeLPSArray(pattern) {
    let lps = Array(pattern.length).fill(0);
    let len = 0;
    let i = 1;
    
    while (i < pattern.length) {
        if (pattern[i] === pattern[len]) {
            len++;
            lps[i] = len;
            i++;
        } else {
            if (len !== 0) {
                len = lps[len - 1];
            } else {
                lps[i] = 0;
                i++;
            }
        }
    }
    
    return lps;
}
```

**Kelebihan:**
- Efisien dengan kompleksitas O(n + m), dimana n dan m adalah panjang teks dan pola.

**Kelemahan:**
- Implementasi lebih kompleks dibandingkan pencarian substring sederhana.

**Contoh Penggunaan:**
- Pencarian pola dalam teks, analisis string.

**Do's:**
- Gunakan untuk pencarian substring dalam teks besar.

**Don'ts:**
- Jangan gunakan untuk teks dengan pola pendek.

### 15. **Quick Select Algorithm**
**Definisi:** Algoritma untuk menemukan elemen ke-k terkecil dalam array tanpa mengurutkan seluruh array.

**Analogi:** Seperti memilih elemen ke-k terkecil dari tumpukan tanpa mengurutkan semua elemen.

**Contoh Kode (JavaScript):**
```javascript
function quickSelect(arr, k) {
    function partition(left, right, pivotIndex) {
        let pivotValue = arr[pivotIndex];
        [arr[pivotIndex], arr[right]] = [arr[right], arr[pivotIndex]];
        let storeIndex = left;
        for (let i = left; i < right; i++) {
            if (arr[i] < pivotValue) {
                [arr[storeIndex], arr[i]] = [arr[i], arr[storeIndex]];
                storeIndex++;
            }
        }
        [arr[right], arr[storeIndex]] = [arr[storeIndex], arr[right]];
        return storeIndex;
    }
    
    function select(left, right, k) {
        if (left === right) return arr[left];
        let pivotIndex = left + Math.floor(Math.random() * (right - left + 1));
        pivotIndex = partition(left, right, pivotIndex);
        if (k === pivotIndex) return arr[k];
        else if (k < pivotIndex) return select(left, pivotIndex - 1, k);
        else return select(pivotIndex + 1, right, k);
    }
    
    return select(0, arr.length - 1, k);
}
```

**Kelebihan:**
- Efisien untuk menemukan elemen ke-k dengan kompleksitas O(n) rata-rata.

**Kelemahan:**
- Kompleksitas terburuk O(n²) dalam kasus terburuk.

**Contoh Penggunaan:**
- Menemukan elemen ke-k terkecil dalam dataset besar.

**Do's:**
- Gunakan untuk menemukan elemen ke-k terkecil dengan cepat.

**Don'ts:**
- Hindari untuk dataset yang sangat besar tanpa pengendalian.

### 16. **Boyer-Moore Majority Vote Algorithm**
**Definisi:** Algoritma untuk menemukan elemen mayoritas (elemen yang muncul lebih dari setengah jumlah elemen) dalam array.

**Analogi:** Seperti mencari kandidat yang mendapat lebih dari setengah suara dalam pemilihan.

**Contoh Kode (JavaScript):**
```javascript
function majorityElement(nums) {
    let count = 0, candidate;
    
    for (let num of nums) {
        if (count === 0) {
            candidate = num;
        }
        count += (num === candidate) ? 1 : -1;
    }
    
    return candidate;
}
```

**Kelebihan:**
- Efisien dengan kompleksitas O(n) dan memori O(1).

**Kelemahan:**
- Tidak selalu ada elemen mayoritas.

**Contoh Penggunaan:**
- Analisis data untuk menemukan elemen yang paling sering muncul.

**Do's:**
- Gunakan untuk mencari elemen mayoritas jika yakin ada elemen yang muncul lebih dari setengahnya.

**Don'ts:**
- Jangan gunakan jika tidak ada jaminan elemen mayoritas.

### 17. **Huffman Coding Compression Algorithm**
**Definisi:** Algoritma kompresi data yang menggunakan frekuensi karakter untuk membuat kode biner yang efisien.

**Analogi:** Seperti membuat kode singkat untuk karakter yang sering muncul dalam teks, sehingga file menjadi lebih kecil.

**Contoh Kode (JavaScript):**
```javascript
class Node {
    constructor(char, freq) {
        this.char = char;
        this.freq = freq;
        this.left = null;
        this.right = null;
    }
}

function buildHuffmanTree(freq) {
    let nodes = Object.entries(freq).map(([char, freq]) => new Node(char, freq));
    let queue = nodes.sort((a, b) => a.freq - b.freq);
    
    while (queue.length > 1) {
        let left = queue.shift();
        let right = queue.shift();
        let newNode = new Node(null, left.freq + right.freq);
        newNode.left = left;
        newNode.right = right;
        queue.push(newNode);
        queue.sort((a, b) => a.freq - b.freq);
    }
    
    return queue[0];
}

function buildHuffmanCodes(node, prefix = '', codes = {}) {
    if (node.char !== null) {
        codes[node.char] = prefix;
    } else {
        buildHuffmanCodes(node.left, prefix + '0', codes);
        buildHuffmanCodes(node.right, prefix + '1', codes);
    }
    return codes;
}

function huffmanCoding(text) {
    let freq = {};
    for (let char of text) {
        freq[char] = (freq[char] || 0) + 1;
    }
    
    let tree = buildHuffmanTree(freq);
    let codes = buildHuffmanCodes(tree);
    return { codes, encoded: text.split('').map(char => codes[char]).join('') };
}
```

**Kelebihan:**
- Kompresi data yang efisien dengan kompleksitas O(n log n) untuk pembuatan pohon Huffman.

**Kelemahan:**
- Tidak efisien untuk data kecil atau jika karakter jarang.

**Contoh Penggunaan:**
- Kompresi teks, penyimpanan data.

**Do's:**
- Gunakan untuk kompresi data teks yang besar.

**Don'ts:**
- Jangan gunakan untuk data yang sudah terkompresi.

### 18. **Euclid’s Algorithm**
**Definisi:** Algoritma untuk menemukan Greatest Common Divisor (GCD) dari dua bilangan.

**Analogi:** Seperti mencari ukuran terbesar dari dua benda yang dapat membagi secara merata tanpa sisa.

**Contoh Kode (JavaScript):**
```javascript
function gcd(a, b) {
    while (b !== 0) {
        [a, b] = [b, a % b];
    }
    return a;
}
```

**Kelebihan:**
- Efisien dengan kompleksitas O(log(min(a, b))).

**Kelemahan:**
- Terbatas untuk mencari GCD dari dua bilangan.

**Contoh Penggunaan:**
- Perhitungan matematika, pemrograman.

**Do's:**
- Gunakan untuk mencari GCD dari dua bilangan.

**Don'ts:**
- Jangan gunakan untuk lebih dari dua bilangan.

### 19. **Union-Find Algorithm**
**Definisi:** Struktur data untuk melacak elemen yang dikelompokkan ke dalam set, dan mendukung operasi union dan find.

**Analogi:** Seperti melacak kelompok orang yang terhub

ung atau tergabung dalam suatu organisasi.

**Contoh Kode (JavaScript):**
```javascript
class UnionFind {
    constructor(size) {
        this.parent = Array.from({ length: size }, (_, i) => i);
        this.rank = Array(size).fill(1);
    }
    
    find(x) {
        if (this.parent[x] !== x) {
            this.parent[x] = this.find(this.parent[x]);
        }
        return this.parent[x];
    }
    
    union(x, y) {
        let rootX = this.find(x);
        let rootY = this.find(y);
        
        if (rootX !== rootY) {
            if (this.rank[rootX] > this.rank[rootY]) {
                this.parent[rootY] = rootX;
            } else if (this.rank[rootX] < this.rank[rootY]) {
                this.parent[rootX] = rootY;
            } else {
                this.parent[rootY] = rootX;
                this.rank[rootX]++;
            }
        }
    }
}
```

**Kelebihan:**
- Efisien dengan hampir O(1) untuk operasi union dan find.

**Kelemahan:**
- Memerlukan memori tambahan untuk struktur data.

**Contoh Penggunaan:**
- Pengelompokan data, algoritma graf seperti Kruskal.

**Do's:**
- Gunakan untuk masalah pengelompokan dan graf.

**Don'ts:**
- Hindari untuk masalah yang tidak melibatkan pengelompokan atau graf.

### 20. **Prim’s Algorithm**
**Definisi:** Algoritma untuk menemukan Minimum Spanning Tree (MST) dari graf berbobot yang terhubung.

**Analogi:** Seperti membangun jembatan untuk menghubungkan pulau-pulau dengan biaya minimum.

**Contoh Kode (JavaScript):**
```javascript
function prim(graph) {
    let nodes = Object.keys(graph);
    let mst = [];
    let visited = new Set();
    let minHeap = [];
    
    const addEdges = (node) => {
        visited.add(node);
        for (let [neighbor, weight] of Object.entries(graph[node])) {
            if (!visited.has(neighbor)) {
                minHeap.push({ weight, from: node, to: neighbor });
            }
        }
    };
    
    addEdges(nodes[0]);
    
    minHeap.sort((a, b) => a.weight - b.weight);
    
    while (minHeap.length > 0) {
        minHeap.sort((a, b) => a.weight - b.weight);
        let edge = minHeap.shift();
        if (!visited.has(edge.to)) {
            mst.push(edge);
            addEdges(edge.to);
        }
    }
    
    return mst;
}
```

**Kelebihan:**
- Efisien untuk menemukan MST dengan kompleksitas O(E log V) menggunakan heap.

**Kelemahan:**
- Memerlukan struktur data heap untuk efisiensi.

**Contoh Penggunaan:**
- Jaringan komputer, desain sistem jaringan.

**Do's:**
- Gunakan untuk menemukan MST dalam graf berbobot.

**Don'ts:**
- Jangan gunakan jika graf tidak berbobot atau tidak terhubung.