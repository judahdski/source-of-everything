# Belajar Dasar TypeScript

Dokumen ini dirancang untuk membantu Anda memahami dasar-dasar TypeScript, termasuk konsep fundamental dalam pemrograman seperti variabel, tipe data, perulangan, pernyataan kondisi, dan fungsi.

---

## Apa itu TypeScript?
TypeScript adalah bahasa pemrograman open-source yang merupakan superset dari JavaScript. TypeScript menambahkan fitur seperti tipe statis dan sintaks yang lebih ketat, sehingga mempermudah pengembangan aplikasi besar dan kompleks.

---

## 1. **Variabel**
Variabel adalah cara untuk menyimpan data di dalam program.

### Deklarasi Variabel:
TypeScript menggunakan kata kunci `let`, `const`, dan `var` untuk deklarasi variabel:

```typescript
let nama: string = "Ali"; // Variabel yang dapat berubah
const umur: number = 25;  // Variabel yang tidak dapat diubah
```

### Jenis Tipe Data:
- `string`: untuk teks.
- `number`: untuk angka.
- `boolean`: untuk nilai benar/salah.
- `any`: tipe data fleksibel.
- `array`: daftar data.
- `object`: kumpulan properti dan nilai.
- `undefined`: nilai yang belum didefinisikan.
- `null`: nilai kosong.
- `void`: tipe tanpa nilai, sering digunakan pada fungsi yang tidak mengembalikan apa pun.
- `never`: tipe untuk fungsi yang tidak pernah berhasil atau mengembalikan nilai (misalnya, fungsi dengan error).

Contoh:
```typescript
let nilai: number = 90;
let isLulus: boolean = true;
let hobi: string[] = ["Membaca", "Menulis"];
let data: any = "Teks bebas";
let kosong: void = undefined;
```

---

## 2. **Pernyataan Kondisi (Conditional Statement)**
Pernyataan kondisi digunakan untuk membuat keputusan berdasarkan suatu kondisi.

### Contoh If-Else:
```typescript
let nilai: number = 80;
if (nilai >= 75) {
    console.log("Lulus");
} else {
    console.log("Tidak Lulus");
}
```

### Switch Statement:
```typescript
let hari: string = "Senin";
switch (hari) {
    case "Senin":
        console.log("Hari kerja pertama.");
        break;
    case "Sabtu":
        console.log("Akhir pekan.");
        break;
    default:
        console.log("Hari biasa.");
}
```

---

## 3. **Perulangan (Looping)**
Perulangan digunakan untuk menjalankan blok kode secara berulang.

### For Loop:
```typescript
for (let i = 0; i < 5; i++) {
    console.log(`Iterasi ke-${i}`);
}
```

### While Loop:
```typescript
let i: number = 0;
while (i < 5) {
    console.log(`Iterasi ke-${i}`);
    i++;
}
```

### For-Of Loop:
Digunakan untuk iterasi pada elemen array:
```typescript
let angka: number[] = [1, 2, 3, 4];
for (let num of angka) {
    console.log(num);
}
```

---

## 4. **Fungsi (Function)**
Fungsi adalah blok kode yang dapat digunakan kembali.

### Membuat Fungsi:
```typescript
function tambah(a: number, b: number): number {
    return a + b;
}

let hasil: number = tambah(5, 10);
console.log(hasil); // Output: 15
```

### Fungsi Anonim:
```typescript
let sapa = function(nama: string): string {
    return `Halo, ${nama}!`;
};
console.log(sapa("Dina"));
```

### Arrow Function:
```typescript
const kali = (a: number, b: number): number => a * b;
console.log(kali(3, 4)); // Output: 12
```

### Function Reference:
Fungsi di TypeScript dapat digunakan sebagai referensi untuk callback atau parameter:
```typescript
function prosesData(data: string, callback: (input: string) => void): void {
    console.log("Memproses data...");
    callback(data);
}

prosesData("Halo", (pesan) => console.log(pesan));
```

---

## 5. **Tipe Data Lanjutan**

### Tuple:
Tuple memungkinkan Anda untuk menyimpan beberapa nilai dengan tipe berbeda:
```typescript
let user: [string, number] = ["Ali", 25];
```

### Enum:
Enum digunakan untuk mendefinisikan daftar nilai yang bernama:
```typescript
enum Hari {
    Senin,
    Selasa,
    Rabu,
}
let hariIni: Hari = Hari.Selasa;
console.log(hariIni); // Output: 1
```

---

## 6. **Interface dan Object**
Interface membantu mendefinisikan struktur objek.

### Contoh Interface:
```typescript
interface User {
    nama: string;
    umur: number;
}

let pengguna: User = {
    nama: "Ali",
    umur: 25,
};
```

---

## 7. **Pemrograman Asinkron (Asynchronous Programming)**
TypeScript mendukung pemrograman asinkron menggunakan `Promise`, `async`, dan `await`.

### Promise:
```typescript
let janji: Promise<string> = new Promise((resolve, reject) => {
    let sukses = true;
    if (sukses) {
        resolve("Berhasil!");
    } else {
        reject("Gagal!");
    }
});

janji
    .then((hasil) => console.log(hasil))
    .catch((error) => console.log(error));
```

### Async/Await:
```typescript
async function fetchData(): Promise<string> {
    return "Data diambil";
}

async function main() {
    try {
        let data = await fetchData();
        console.log(data);
    } catch (error) {
        console.log("Terjadi kesalahan", error);
    }
}

main();
```

Dengan fitur ini, Anda dapat menangani operasi asinkron seperti pengambilan data dari API atau membaca file dengan mudah.

---

## 8. **Metode Array**
TypeScript menyediakan berbagai metode bawaan untuk memanipulasi array. Berikut adalah beberapa metode yang sering digunakan:

### `push` dan `pop`
- `push`: Menambahkan elemen ke akhir array.
- `pop`: Menghapus elemen terakhir dari array.

```typescript
let angka: number[] = [1, 2, 3];
angka.push(4); // [1, 2, 3, 4]
angka.pop();   // [1, 2, 3]
```

### `shift` dan `unshift`
- `shift`: Menghapus elemen pertama dari array.
- `unshift`: Menambahkan elemen ke awal array.

```typescript
let buah: string[] = ["apel", "mangga"];
buah.unshift("pisang"); // ["pisang", "apel", "mangga"];
buah.shift();           // ["apel", "mangga"];
```

### `map`
Mengembalikan array baru dengan hasil operasi pada setiap elemen.
```typescript
let angka: number[] = [1, 2, 3];
let hasil: number[] = angka.map((num) => num * 2); // [2, 4, 6]
```

### `filter`
Menyaring elemen berdasarkan kondisi tertentu.
```typescript
let angka: number[] = [1, 2, 3, 4, 5];
let genap: number[] = angka.filter((num) => num % 2 === 0); // [2, 4]
```

### `reduce`
Menghitung nilai tunggal dari array.
```typescript
let angka: number[] = [1, 2, 3, 4];
let total: number = angka.reduce((acc, num) => acc + num, 0); // 10
```

### `find` dan `findIndex`
- `find`: Mengembalikan elemen pertama yang memenuhi kondisi.
- `findIndex`: Mengembalikan indeks elemen pertama yang memenuhi kondisi.

```typescript
let angka: number[] = [1, 2, 3, 4];
let cari: number | undefined = angka.find((num) => num > 2); // 3
let indeks: number = angka.findIndex((num) => num > 2);      // 2
```

### `forEach`
Menjalankan fungsi pada setiap elemen array.
```typescript
let angka: number[] = [1, 2, 3];
angka.forEach((num) => console.log(num));
```

Metode ini mempermudah manipulasi array secara efisien dalam TypeScript.

---

Dengan mempelajari dasar-dasar ini, Anda dapat mulai menulis kode TypeScript yang efektif dan terorganisir. Selamat belajar!

