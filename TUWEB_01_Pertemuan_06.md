# MATERI TUWEB 1 - PERTEMUAN 6
# PRAKTIKUM IONIC FRAMEWORK DENGAN VUE.JS

> **Catatan penyusunan:** file final ini merupakan adaptasi dari **TUWEB_2.md** sesuai pemetaan pada README repository. Isi utama dipertahankan, lalu diperkaya dengan contoh live-coding, pertanyaan diskusi, expected output, dan penjelasan konsep yang selaras dengan materi UT MSIM4401, khususnya instalasi Ionic, Ionic berbasis Vue, struktur proyek, integrasi Ionic-Vue, layout/theme, komponen antarmuka, router, dan event handler.

---

## 📋 INFORMASI MATA KULIAH

**Mata Kuliah**: Pemrograman Berbasis Perangkat Bergerak (MSIM4401)
**Pertemuan**: 6 (TUWEB 1)
**Pokok Bahasan**: Praktikum Integrasi Ionic dengan Vue, Teknik Layout, Theme, dan Komponen Ionic
**Pendekatan**: Learning by Doing

---

## 🎯 TUJUAN PEMBELAJARAN

Setelah menyelesaikan praktikum ini, mahasiswa diharapkan mampu:

1. Memahami konsep Ionic Framework dan integrasinya dengan Vue.js
2. Melakukan instalasi dan konfigurasi lingkungan pengembangan Ionic
3. Membuat aplikasi mobile pertama menggunakan Ionic dan Vue
4. Mengimplementasikan teknik layout menggunakan Ionic Grid System
5. Menyesuaikan tema dan styling aplikasi mobile
6. Menggunakan berbagai komponen UI Ionic untuk membangun antarmuka aplikasi
7. Memahami struktur direktori dan file dalam project Ionic

---

## 📚 PRASYARAT

Sebelum memulai praktikum ini, pastikan Anda telah:

- ✅ Memiliki pemahaman dasar HTML, CSS, dan JavaScript
- ✅ Memahami konsep dasar Vue.js (data binding, components, directives)
- ✅ Memahami pemrograman TypeScript dasar
- ✅ Memiliki komputer dengan spesifikasi minimal:
  - RAM 4GB (disarankan 8GB)
  - Storage kosong minimal 10GB
  - Sistem Operasi: Windows 10/11, macOS, atau Linux

---

## 🛠️ PERSIAPAN LINGKUNGAN PENGEMBANGAN

### Langkah 1: Instalasi Node.js dan npm

Node.js adalah runtime JavaScript yang diperlukan untuk menjalankan Ionic Framework.

#### Untuk Windows:

1. **Download Node.js**
   - Buka browser, kunjungi: https://nodejs.org/
   - Download versi LTS (Long Term Support) - versi yang paling stabil
   - Pada saat materi ini dibuat, versi LTS adalah v20.x.x

2. **Instalasi Node.js**
   - Jalankan file installer yang sudah didownload (contoh: `node-v20.11.0-x64.msi`)
   - Klik "Next" pada welcome screen
   - Setujui License Agreement dengan mencentang "I accept..."
   - Pilih lokasi instalasi (biarkan default: `C:\Program Files\nodejs\`)
   - Pada bagian "Custom Setup", biarkan semua fitur tercentang
   - Centang opsi "Automatically install the necessary tools..." jika ada
   - Klik "Install"
   - Tunggu proses instalasi selesai
   - Klik "Finish"

3. **Verifikasi Instalasi**
   - Buka Command Prompt (tekan `Win + R`, ketik `cmd`, Enter)
   - Ketik perintah berikut untuk mengecek versi Node.js:
   ```bash
   node --version
   ```
   - Akan muncul versi Node.js, contoh: `v20.11.0`

   - Ketik perintah berikut untuk mengecek versi npm:
   ```bash
   npm --version
   ```
   - Akan muncul versi npm, contoh: `10.2.4`

#### Untuk macOS:

1. **Menggunakan Homebrew (cara termudah)**
   - Buka Terminal
   - Install Homebrew jika belum punya:
   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```
   - Install Node.js:
   ```bash
   brew install node
   ```

2. **Atau download installer**
   - Kunjungi https://nodejs.org/
   - Download versi macOS installer
   - Jalankan file .pkg dan ikuti instruksi

3. **Verifikasi sama seperti Windows**

#### Untuk Linux (Ubuntu/Debian):

```bash
# Update package index
sudo apt update

# Install Node.js dan npm
sudo apt install nodejs npm

# Verifikasi instalasi
node --version
npm --version
```

---

### Langkah 2: Instalasi TypeScript dan ts-node

Sebelum masuk ke Ionic, kita perlu memahami **TypeScript** karena project Ionic berbasis Vue banyak menggunakan file `.ts` dan `<script setup lang="ts">`. Materi UT memulai TypeScript dengan kompilator `tsc` dan `ts-node`, kemudian membahas variabel, tipe data, struktur kendali, fungsi, interface, OOP, generics, hingga asynchronous programming.

> **Urutan belajar pada Tuweb 01 ini:** Node.js/npm → TypeScript Dasar → TypeScript Lanjutan → Pembahasan Tugas 1 → baru masuk ke Ionic + Vue.

Install TypeScript secara global:

~~~bash
npm install -g typescript
~~~

Periksa hasil instalasi:

~~~bash
tsc --version
~~~

Install `ts-node` agar kode TypeScript dapat dijalankan langsung untuk eksperimen:

~~~bash
npm install -g ts-node
ts-node --version
~~~

### Cara 1 — Menjalankan TypeScript melalui REPL

~~~bash
ts-node
~~~

Kemudian:

~~~ts
console.log("Halo dari TypeScript");
~~~

Keluar dari REPL dengan `Ctrl+C` dua kali.

### Cara 2 — Menjalankan dari file .ts

Buat file `app.ts`:

~~~ts
let message: string = "Hello, TypeScript!";
console.log(message);
~~~

Kompilasi:

~~~bash
tsc app.ts
~~~

Akan terbentuk:

~~~text
app.ts
app.js
~~~

Jalankan JavaScript hasil kompilasi:

~~~bash
node app.js
~~~

Atau untuk praktikum sederhana langsung:

~~~bash
ts-node app.ts
~~~

### Opsional — Membuat project TypeScript kecil

~~~bash
mkdir belajar-typescript
cd belajar-typescript
npm init -y
tsc --init
~~~

Struktur awal:

~~~text
belajar-typescript/
├── package.json
└── tsconfig.json
~~~

Untuk contoh pada tutorial ini kita dapat menggunakan konfigurasi sederhana:

~~~json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "commonjs",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true
  }
}
~~~

> **Catatan tutor:** materi UT menggunakan versi TypeScript/Node yang lebih lama pada contoh. Konsepnya tetap sama, tetapi untuk praktikum sekarang kita dapat menggunakan versi LTS/versi TypeScript yang tersedia pada komputer mahasiswa.

---

# 📘 BAGIAN I — DASAR-DASAR TYPESCRIPT

## 1. Mengapa TypeScript?

TypeScript dapat dipahami sebagai JavaScript yang ditambah sistem tipe. Pada saat development, TypeScript membantu mendeteksi banyak kesalahan sebelum program dijalankan.

Contoh JavaScript:

~~~js
let nilai = 100;
nilai = "seratus";
~~~

JavaScript mengizinkan perubahan tipe tersebut.

TypeScript:

~~~ts
let nilai: number = 100;
// nilai = "seratus"; // error
~~~

Ini penting dalam aplikasi mobile karena struktur data user, respons API, data form, lokasi, kamera, dan state aplikasi dapat dibuat lebih eksplisit.

---

## 2. Variabel: var, let, dan const

### var

~~~ts
var angka = 10;
console.log(angka);

var angka = 20;
console.log(angka);
~~~

`var` dapat dideklarasikan ulang dan mempunyai **function scope**.

### let

~~~ts
let umur: number = 20;
console.log(umur);

umur = 21;
console.log(umur);

// let umur = 22; // error: deklarasi ulang pada scope yang sama
~~~

`let` mempunyai **block scope**.

### const

~~~ts
const kampus: string = "Universitas Terbuka";
console.log(kampus);

// kampus = "UT"; // error
~~~

Gunakan `const` jika reference tidak akan diganti, dan `let` jika nilai perlu berubah. Untuk kode modern, hindari `var` kecuali memang sedang menjelaskan perbedaan scope.

---

## 3. Tipe Data Dasar

### Boolean

~~~ts
let aktif: boolean = true;
let lulus: boolean = false;
~~~

### Number

~~~ts
let umur: number = 21;
let ipk: number = 3.75;
let biner: number = 0b1010;
let heksa: number = 0xff;
~~~

### String

~~~ts
let nama: string = "Taufik";
let prodi: string = "Sistem Informasi";

console.log(nama + " - " + prodi);
~~~

### Array

~~~ts
let nilai: number[] = [80, 90, 75, 88];
let matkul: string[] = [
  "Pemrograman Perangkat Bergerak",
  "Basis Data",
  "Sistem Terdistribusi"
];

console.log(nilai[0]);
console.log(matkul.length);
~~~

Bentuk generic:

~~~ts
let daftarNim: Array<string> = [
  "230411013",
  "230411014"
];
~~~

### Tuple

Tuple digunakan saat posisi elemen mempunyai arti dan tipe tertentu.

~~~ts
let mahasiswa: [string, string, number];

mahasiswa = [
  "230411013",
  "Budi",
  3.75
];

console.log(mahasiswa[0]);
console.log(mahasiswa[1]);
console.log(mahasiswa[2]);
~~~

### Enum

~~~ts
enum StatusMahasiswa {
  Aktif,
  Cuti,
  Lulus,
  NonAktif
}

let status: StatusMahasiswa = StatusMahasiswa.Aktif;
console.log(status);
~~~

### Union Type

Satu variabel dapat menerima lebih dari satu tipe.

~~~ts
let kode: string | number;

kode = "MSIM4401";
console.log(kode);

kode = 4401;
console.log(kode);
~~~

### any

~~~ts
let dataBebas: any;

dataBebas = 10;
dataBebas = "sepuluh";
dataBebas = true;
~~~

`any` fleksibel tetapi kehilangan banyak manfaat pemeriksaan tipe.

### unknown

~~~ts
let dataTidakDiketahui: unknown = "Universitas Terbuka";

if (typeof dataTidakDiketahui === "string") {
  console.log(dataTidakDiketahui.toUpperCase());
}
~~~

`unknown` lebih aman daripada `any` karena nilai harus diperiksa sebelum digunakan sebagai tipe tertentu.

### null dan undefined

~~~ts
let belumAda: null = null;
let belumDiisi: undefined = undefined;

console.log(belumAda);
console.log(belumDiisi);
~~~

---

## 4. Type Inference

TypeScript tidak selalu membutuhkan penulisan tipe secara eksplisit.

~~~ts
let jumlah = 10;
// TypeScript menginferensikan jumlah sebagai number

let fakultas = "Sains dan Teknologi";
// diinferensikan sebagai string
~~~

Namun pada parameter fungsi, object kompleks, data API, dan model aplikasi, penulisan tipe eksplisit sering membuat kode lebih mudah dipahami.

---

## 5. Operator

### Operator aritmatika

~~~ts
let a = 10;
let b = 3;

console.log(a + b); // 13
console.log(a - b); // 7
console.log(a * b); // 30
console.log(a / b); // 3.333...
console.log(a % b); // 1
console.log(a ** b); // 1000
~~~

Operator modulo `%` sangat penting untuk soal bilangan prima.

### Operator perbandingan

~~~ts
console.log(10 > 5);
console.log(10 >= 10);
console.log(10 < 20);
console.log(10 === 10);
console.log(10 !== 5);
~~~

### Operator logika

~~~ts
let sudahLogin = true;
let akunAktif = true;

console.log(sudahLogin && akunAktif);
console.log(sudahLogin || akunAktif);
console.log(!sudahLogin);
~~~

---

## 6. Konversi String dan Number

NIM sebaiknya diperlakukan sebagai **string**, bukan number.

~~~ts
const nim: string = "230411013";
~~~

Mengambil karakter:

~~~ts
console.log(nim.charAt(0));
console.log(nim.charAt(nim.length - 1));
~~~

Mengambil beberapa karakter:

~~~ts
const duaDigitTerakhir = nim.slice(-2);
console.log(duaDigitTerakhir); // "13"
~~~

Mengubah string ke number:

~~~ts
const angka = Number(duaDigitTerakhir);
console.log(angka); // 13
~~~

### Mengapa NIM lebih aman sebagai string?

Karena NIM adalah **identifier**, bukan nilai yang akan dihitung secara keseluruhan. Dengan string kita mudah menggunakan `slice()`, `charAt()`, dan mempertahankan kemungkinan digit nol di depan.

---

# 🔀 STRUKTUR KENDALI

## 7. Percabangan if, else if, else

~~~ts
let nilaiAkhir: number = 82;

if (nilaiAkhir >= 85) {
  console.log("Grade A");
} else if (nilaiAkhir >= 70) {
  console.log("Grade B");
} else if (nilaiAkhir >= 60) {
  console.log("Grade C");
} else {
  console.log("Perlu perbaikan");
}
~~~

### Contoh dengan NIM

~~~ts
const nim = "230411013";
const digitTerakhir = Number(nim.charAt(nim.length - 1));

if (digitTerakhir % 2 === 0) {
  console.log("Digit terakhir genap");
} else {
  console.log("Digit terakhir ganjil");
}
~~~

---

## 8. switch

~~~ts
let hari: number = 3;
let namaHari: string;

switch (hari) {
  case 1:
    namaHari = "Senin";
    break;
  case 2:
    namaHari = "Selasa";
    break;
  case 3:
    namaHari = "Rabu";
    break;
  case 4:
    namaHari = "Kamis";
    break;
  case 5:
    namaHari = "Jumat";
    break;
  default:
    namaHari = "Tidak valid";
}

console.log(namaHari);
~~~

### Kapan if dan switch digunakan?

- `if`: cocok untuk rentang dan ekspresi logika.
- `switch`: cocok untuk banyak kondisi berdasarkan nilai diskrit yang sama.

---

# 🔁 PERULANGAN

## 9. for

~~~ts
for (let i = 1; i <= 5; i++) {
  console.log("Perulangan ke-" + i);
}
~~~

Struktur:

~~~text
for (inisialisasi; kondisi; perubahan) {
    perintah
}
~~~

Contoh:

~~~ts
for (let i = 1; i <= 3; i++) {
  console.log(i);
}
~~~

Output:

~~~text
1
2
3
~~~

---

## 10. Nested Loop

Nested loop berarti loop di dalam loop. Konsep ini **sangat penting untuk Tugas 1 Soal 1**.

~~~ts
for (let baris = 1; baris <= 3; baris++) {
  let output = "";

  for (let kolom = 1; kolom <= baris; kolom++) {
    output += kolom + " ";
  }

  console.log(output.trim());
}
~~~

Output:

~~~text
1
1 2
1 2 3
~~~

Perhatikan:
- loop luar menentukan jumlah **baris**,
- loop dalam menentukan berapa angka yang dicetak pada setiap baris.

---

## 11. for...of

Digunakan untuk mengambil **nilai** dari iterable.

~~~ts
const daftarNilai = [80, 90, 75];

for (const nilai of daftarNilai) {
  console.log(nilai);
}
~~~

---

## 12. for...in

Digunakan untuk mengambil **index/key**.

~~~ts
const daftarNilai = [80, 90, 75];

for (const index in daftarNilai) {
  console.log(index, daftarNilai[index]);
}
~~~

> Untuk array, pada banyak kasus `for...of` lebih mudah dibaca jika kita membutuhkan nilainya.

---

## 13. while

~~~ts
let angka = 1;

while (angka <= 5) {
  console.log(angka);
  angka++;
}
~~~

`while` cocok ketika jumlah perulangan belum tentu diketahui sejak awal.

---

## 14. do...while

~~~ts
let angka = 1;

do {
  console.log(angka);
  angka++;
} while (angka <= 5);
~~~

Perbedaan penting: isi `do` dijalankan **minimal satu kali** sebelum kondisi diperiksa.

---

## 15. break dan continue

### break

~~~ts
for (let i = 1; i <= 10; i++) {
  if (i === 6) {
    break;
  }

  console.log(i);
}
~~~

Output berhenti pada 5.

### continue

~~~ts
for (let i = 1; i <= 10; i++) {
  if (i % 2 === 0) {
    continue;
  }

  console.log(i);
}
~~~

Hanya angka ganjil yang ditampilkan.

---

# 🧩 PEMROGRAMAN MODULAR — FUNGSI

## 16. Function Definition

~~~ts
function tambah(x: number, y: number): number {
  return x + y;
}

console.log(tambah(10, 5));
~~~

Anatomi:

~~~text
function namaFungsi(parameter: tipe): tipeKembalian {
    ...
}
~~~

---

## 17. Function Expression

~~~ts
const kali = function (
  x: number,
  y: number
): number {
  return x * y;
};

console.log(kali(4, 5));
~~~

---

## 18. Arrow Function

~~~ts
const kurang = (
  a: number,
  b: number
): number => a - b;

console.log(kurang(10, 3));
~~~

---

## 19. void

Fungsi yang tidak mengembalikan nilai:

~~~ts
function tampilkanPesan(pesan: string): void {
  console.log(pesan);
}

tampilkanPesan("Selamat belajar TypeScript");
~~~

---

## 20. Parameter Optional dan Default

### Optional

~~~ts
function salam(
  nama: string,
  gelar?: string
): string {
  if (gelar) {
    return "Halo " + gelar + " " + nama;
  }

  return "Halo " + nama;
}

console.log(salam("Budi"));
console.log(salam("Budi", "Dr."));
~~~

### Default

~~~ts
function pangkat(
  angka: number,
  eksponen: number = 2
): number {
  return angka ** eksponen;
}

console.log(pangkat(5));
console.log(pangkat(5, 3));
~~~

---

## 21. Scope let dan var

~~~ts
function demoScope() {
  if (true) {
    let hanyaDiBlok = 10;
    var diFungsi = 20;

    console.log(hanyaDiBlok);
  }

  // console.log(hanyaDiBlok); // error
  console.log(diFungsi); // bisa
}

demoScope();
~~~

Ini memperlihatkan:
- `let` → block scope,
- `var` → function scope.

---

# 🧱 TYPESCRIPT LANJUTAN — DATA MODEL DAN OOP

## 22. Interface

Interface dapat dipakai sebagai kontrak struktur data.

~~~ts
interface Mahasiswa {
  nim: string;
  nama: string;
  prodi: string;
  ipk?: number;
}

const mhs: Mahasiswa = {
  nim: "230411013",
  nama: "Budi Santoso",
  prodi: "Sistem Informasi"
};

console.log(mhs.nama);
~~~

`ipk?` berarti properti tersebut optional.

---

## 23. readonly

~~~ts
interface AkunMahasiswa {
  readonly nim: string;
  nama: string;
}

const akun: AkunMahasiswa = {
  nim: "230411013",
  nama: "Budi"
};

// akun.nim = "999"; // error
~~~

---

## 24. Class dan Object

~~~ts
class MahasiswaUT {
  constructor(
    public nim: string,
    public nama: string,
    private nilai: number
  ) {}

  getNilai(): number {
    return this.nilai;
  }

  setNilai(nilaiBaru: number): void {
    this.nilai = nilaiBaru;
  }

  statusLulus(): boolean {
    return this.nilai >= 60;
  }
}

const mhs = new MahasiswaUT(
  "230411013",
  "Budi Santoso",
  85
);

console.log(mhs.nama);
console.log(mhs.getNilai());
console.log(mhs.statusLulus());
~~~

### Istilah penting
- **class**: cetakan object.
- **object/instance**: hasil dari class.
- **constructor**: dipanggil saat object dibuat.
- **public**: dapat diakses dari luar class.
- **private**: hanya dari dalam class.
- **protected**: class dan turunannya.
- **method**: fungsi yang menjadi bagian class.

---

## 25. Inheritance

~~~ts
class Person {
  constructor(
    public nama: string
  ) {}
}

class MahasiswaAktif extends Person {
  constructor(
    nama: string,
    public nim: string
  ) {
    super(nama);
  }

  info(): string {
    return this.nim + " - " + this.nama;
  }
}

const mhs = new MahasiswaAktif(
  "Budi",
  "230411013"
);

console.log(mhs.info());
~~~

---

## 26. Generics

Tanpa generics:

~~~ts
function identitasNumber(value: number): number {
  return value;
}

function identitasString(value: string): string {
  return value;
}
~~~

Dengan generics:

~~~ts
function identitas<T>(value: T): T {
  return value;
}

console.log(identitas<number>(100));
console.log(identitas<string>("UT"));
console.log(identitas<boolean>(true));
~~~

Generics membuat fungsi tetap **type-safe** tetapi dapat digunakan untuk banyak tipe.

---

# ⚡ TYPESCRIPT LANJUTAN — ASYNCHRONOUS PROGRAMMING

## 27. Mengapa Asynchronous?

Operasi berikut tidak selalu selesai seketika:
- mengakses REST API,
- membaca file,
- query database,
- mengambil lokasi,
- menggunakan kamera/native plugin.

Dua masalah yang harus diantisipasi:
1. **latency** — operasi membutuhkan waktu;
2. **failure** — operasi dapat gagal.

---

## 28. Promise

~~~ts
function cekAngka(
  angka: number
): Promise<string> {
  return new Promise((resolve, reject) => {
    if (angka >= 60) {
      resolve("Lulus");
    } else {
      reject("Belum lulus");
    }
  });
}

cekAngka(80)
  .then((hasil) => {
    console.log(hasil);
  })
  .catch((error) => {
    console.log("ERROR:", error);
  });
~~~

Status konseptual Promise:
- pending,
- fulfilled,
- rejected.

---

## 29. Promise Chaining

~~~ts
Promise.resolve(10)
  .then((angka) => {
    console.log(angka);
    return angka * 2;
  })
  .then((angka) => {
    console.log(angka);
    return angka + 5;
  })
  .then((angka) => {
    console.log(angka);
  });
~~~

Output:

~~~text
10
20
25
~~~

Hasil dari satu `.then()` menjadi input bagi chain berikutnya.

---

## 30. async/await

Versi async/await biasanya lebih mudah dibaca:

~~~ts
function tunggu(
  ms: number
): Promise<void> {
  return new Promise((resolve) => {
    setTimeout(resolve, ms);
  });
}

async function demoAsync(): Promise<void> {
  console.log("Mulai");

  await tunggu(1000);

  console.log("Selesai setelah sekitar 1 detik");
}

demoAsync();
~~~

---

## 31. try...catch...finally

~~~ts
async function ambilData(): Promise<void> {
  try {
    console.log("Mulai proses");

    await tunggu(500);

    console.log("Proses berhasil");
  } catch (error) {
    console.error("Terjadi error:", error);
  } finally {
    console.log("Bagian finally selalu dijalankan");
  }
}

ambilData();
~~~

Pola ini nanti digunakan saat mengakses API, Camera, Geolocation, dan penyimpanan.

---

## 32. Contoh REST API dengan fetch

> Bagian ini adalah pengayaan untuk menjembatani TypeScript menuju materi Ionic.

~~~ts
interface User {
  id: number;
  name: string;
  email: string;
}

async function getUsers(): Promise<User[]> {
  const response = await fetch(
    "https://jsonplaceholder.typicode.com/users"
  );

  if (!response.ok) {
    throw new Error(
      "HTTP error: " + response.status
    );
  }

  return await response.json() as User[];
}

async function main(): Promise<void> {
  try {
    const users = await getUsers();

    for (const user of users) {
      console.log(
        user.id,
        user.name,
        user.email
      );
    }
  } catch (error) {
    console.error(error);
  }
}

main();
~~~

### Hubungan dengan Ionic

Nanti di Ionic:
- fungsi `getUsers()` dapat dipindahkan ke service;
- hasilnya disimpan ke reactive state;
- `v-for` menampilkan daftar user;
- loading/error dapat ditampilkan dengan komponen Ionic.

---

# 🧪 LATIHAN CEPAT SEBELUM TUGAS 1

## Latihan A — Genap atau Ganjil

~~~ts
const angka = 17;

if (angka % 2 === 0) {
  console.log("Genap");
} else {
  console.log("Ganjil");
}
~~~

## Latihan B — Menjumlah 1 sampai N

~~~ts
const n = 5;
let total = 0;

for (let i = 1; i <= n; i++) {
  total += i;
}

console.log(total); // 15
~~~

## Latihan C — Membuat Array Hasil Perkalian

~~~ts
const hasil: number[] = [];

for (let i = 1; i <= 10; i++) {
  hasil.push(i * 3);
}

console.log(hasil);
~~~

## Latihan D — Fungsi Faktor

~~~ts
function faktorDari(
  bilangan: number
): number[] {
  const faktor: number[] = [];

  for (
    let i = 1;
    i <= bilangan;
    i++
  ) {
    if (bilangan % i === 0) {
      faktor.push(i);
    }
  }

  return faktor;
}

console.log(faktorDari(12));
~~~

Output:

~~~text
[1, 2, 3, 4, 6, 12]
~~~

Latihan faktor ini menjadi jembatan ke soal bilangan prima.

---

# 📝 PEMBAHASAN TUGAS 1 — TYPESCRIPT

Bagian ini tidak hanya memberikan jawaban, tetapi juga menunjukkan **cara berpikir algoritmik** yang diharapkan ketika mengerjakan tugas.

## Persiapan

Buat folder:

~~~bash
mkdir tugas1-typescript
cd tugas1-typescript
~~~

Buat file:
- `soal1.ts`
- `soal2.ts`
- `soal3.ts`

Untuk mencoba:

~~~bash
ts-node soal1.ts
ts-node soal2.ts
ts-node soal3.ts
~~~

Gunakan NIM contoh:

~~~ts
const nim: string = "230411013";
~~~

> **Penting:** ganti dengan NIM masing-masing mahasiswa.

---

# ✅ SOAL 1 — POLA SEGITIGA DARI NIM

## Deskripsi

Ambil digit terakhir NIM sebagai tinggi segitiga.

Contoh:

~~~text
NIM = 230411013
digit terakhir = 3
tinggi = 3
~~~

Output:

~~~text
1
1 2
1 2 3
~~~

Jika tinggi = 5:

~~~text
1
1 2
1 2 3
1 2 3 4
1 2 3 4 5
~~~

## Analisis Algoritma

Kita membutuhkan dua perulangan:

~~~text
loop baris dari 1 sampai tinggi
    output = kosong

    loop angka dari 1 sampai baris
        tambahkan angka ke output

    cetak output
~~~

Mengapa nested loop?

Karena:
- baris ke-1 mencetak 1 angka,
- baris ke-2 mencetak 2 angka,
- baris ke-3 mencetak 3 angka,
- dan seterusnya.

Dengan kata lain, batas loop dalam selalu mengikuti nomor baris.

## Implementasi TypeScript

~~~ts
const nim: string = "230411013";

const digitTerakhir: string =
  nim.charAt(nim.length - 1);

const tinggi: number =
  Number(digitTerakhir);

console.log("NIM:", nim);
console.log("Tinggi segitiga:", tinggi);
console.log();

for (
  let baris = 1;
  baris <= tinggi;
  baris++
) {
  let output: string = "";

  for (
    let angka = 1;
    angka <= baris;
    angka++
  ) {
    output += angka;

    if (angka < baris) {
      output += " ";
    }
  }

  console.log(output);
}
~~~

## Dry Run untuk tinggi = 3

### Baris 1

~~~text
baris = 1
angka berjalan: 1
output = "1"
~~~

### Baris 2

~~~text
baris = 2
angka berjalan: 1, 2
output = "1 2"
~~~

### Baris 3

~~~text
baris = 3
angka berjalan: 1, 2, 3
output = "1 2 3"
~~~

## Versi Fungsi

~~~ts
function buatSegitiga(
  tinggi: number
): void {
  for (
    let baris = 1;
    baris <= tinggi;
    baris++
  ) {
    const angkaBaris: number[] = [];

    for (
      let angka = 1;
      angka <= baris;
      angka++
    ) {
      angkaBaris.push(angka);
    }

    console.log(
      angkaBaris.join(" ")
    );
  }
}

const nim = "230411013";
const tinggi = Number(
  nim.charAt(nim.length - 1)
);

buatSegitiga(tinggi);
~~~

### Mengapa versi fungsi lebih baik?

Karena logika pembuatan segitiga tidak bergantung pada sumber tinggi. Kita dapat menjalankan:

~~~ts
buatSegitiga(3);
buatSegitiga(5);
buatSegitiga(7);
~~~

## Kesalahan umum Soal 1

1. Menggunakan hanya satu loop.
2. Loop dalam selalu sampai `tinggi`, sehingga semua baris sama panjang.
3. Dimulai dari 0 sehingga output menjadi `0 1 2`.
4. Mengubah seluruh NIM menjadi number tanpa kebutuhan.
5. Menulis output secara hard-coded.

---

# ✅ SOAL 2 — DERET ARITMATIKA DENGAN NIM

## Deskripsi

Aturan:
1. dua digit terakhir → angka awal;
2. digit ke-3 dari belakang + 1 → beda/step;
3. tampilkan 10 angka pertama.

Contoh:

~~~text
NIM = 230411013
dua digit terakhir = 13
digit ke-3 dari belakang = 0
step = 0 + 1 = 1
~~~

Output:

~~~text
13, 14, 15, 16, 17, 18, 19, 20, 21, 22
~~~

## Memahami Posisi Digit

NIM:

~~~text
2 3 0 4 1 1 0 1 3
                ^ ^ dua digit terakhir = 13
              ^
              digit ke-3 dari belakang = 0
~~~

Dengan string:

~~~ts
const nim = "230411013";

console.log(nim.slice(-2)); // "13"

console.log(
  nim.charAt(nim.length - 3)
); // "0"
~~~

## Rumus Deret Aritmatika

Secara konseptual:

~~~text
suku ke-n =
start + (n - 1) × step
~~~

Namun pada program, kita bisa menggunakan loop.

## Implementasi TypeScript

~~~ts
const nim: string = "230411013";

const start: number =
  Number(nim.slice(-2));

const digitKetigaDariBelakang: number =
  Number(
    nim.charAt(nim.length - 3)
  );

const step: number =
  digitKetigaDariBelakang + 1;

const deret: number[] = [];

for (
  let i = 0;
  i < 10;
  i++
) {
  const nilai =
    start + (i * step);

  deret.push(nilai);
}

console.log("NIM:", nim);
console.log("Start:", start);
console.log("Step:", step);
console.log(
  "Deret:",
  deret.join(", ")
);
~~~

Output untuk contoh:

~~~text
NIM: 230411013
Start: 13
Step: 1
Deret: 13, 14, 15, 16, 17, 18, 19, 20, 21, 22
~~~

## Dry Run

~~~text
i = 0 → 13 + (0 × 1) = 13
i = 1 → 13 + (1 × 1) = 14
i = 2 → 13 + (2 × 1) = 15
...
i = 9 → 13 + (9 × 1) = 22
~~~

## Versi dengan variabel current

~~~ts
const nim = "230411013";

const start =
  Number(nim.slice(-2));

const step =
  Number(
    nim.charAt(nim.length - 3)
  ) + 1;

let current = start;
const hasil: number[] = [];

for (let i = 0; i < 10; i++) {
  hasil.push(current);
  current += step;
}

console.log(hasil.join(", "));
~~~

Kedua pendekatan benar:
- formula langsung,
- update nilai `current`.

## Versi Fungsi

~~~ts
function buatDeretAritmatika(
  start: number,
  step: number,
  jumlah: number
): number[] {
  const hasil: number[] = [];

  for (
    let i = 0;
    i < jumlah;
    i++
  ) {
    hasil.push(
      start + i * step
    );
  }

  return hasil;
}
~~~

Pemakaian:

~~~ts
const nim = "230411013";

const start =
  Number(nim.slice(-2));

const step =
  Number(
    nim.charAt(nim.length - 3)
  ) + 1;

const hasil =
  buatDeretAritmatika(
    start,
    step,
    10
  );

console.log(
  hasil.join(", ")
);
~~~

## Kesalahan umum Soal 2

1. Mengambil tiga digit terakhir sebagai start.
2. Lupa menambahkan `+1` pada digit ke-3 dari belakang.
3. Mencetak 11 angka karena kondisi loop `i <= 10`.
4. Menganggap step selalu 1.
5. Mengubah NIM ke number lalu kesulitan mengambil posisi digit.

---

# ✅ SOAL 3 — BILANGAN PRIMA DARI NIM

## Deskripsi

Aturan:
1. ambil dua digit terakhir NIM;
2. tambahkan 10;
3. jadikan hasil sebagai batas pencarian bilangan prima;
4. tampilkan seluruh bilangan prima dari 1 sampai batas tersebut.

Contoh:

~~~text
NIM = 230411013
2 digit terakhir = 13
batas = 13 + 10 = 23
~~~

Output:

~~~text
2, 3, 5, 7, 11, 13, 17, 19, 23
~~~

## Apa Itu Bilangan Prima?

Bilangan prima adalah bilangan bulat lebih besar dari 1 yang hanya mempunyai dua pembagi positif:
- 1;
- dirinya sendiri.

Contoh:
- 2 → prima;
- 3 → prima;
- 4 → bukan prima karena habis dibagi 2;
- 5 → prima;
- 9 → bukan prima karena habis dibagi 3.

---

## Algoritma Dasar

Untuk setiap angka dari 2 sampai batas:
1. asumsikan angka tersebut prima;
2. coba cari pembagi;
3. jika ada pembagi selain 1 dan dirinya, berarti bukan prima;
4. jika tidak ada, masukkan ke hasil.

---

## Fungsi isPrime — Versi Mudah Dipahami

~~~ts
function isPrime(
  angka: number
): boolean {
  if (angka < 2) {
    return false;
  }

  for (
    let pembagi = 2;
    pembagi < angka;
    pembagi++
  ) {
    if (
      angka % pembagi === 0
    ) {
      return false;
    }
  }

  return true;
}
~~~

Contoh:

~~~ts
console.log(isPrime(2)); // true
console.log(isPrime(4)); // false
console.log(isPrime(17)); // true
~~~

---

## Fungsi isPrime — Versi Lebih Efisien

Kita tidak perlu memeriksa pembagi sampai `angka - 1`. Cukup sampai akar kuadratnya.

~~~ts
function isPrime(
  angka: number
): boolean {
  if (angka < 2) {
    return false;
  }

  for (
    let pembagi = 2;
    pembagi * pembagi <= angka;
    pembagi++
  ) {
    if (
      angka % pembagi === 0
    ) {
      return false;
    }
  }

  return true;
}
~~~

Mengapa kondisi:

~~~ts
pembagi * pembagi <= angka
~~~

Jika sebuah bilangan komposit mempunyai faktor lebih besar dari akar kuadratnya, ia pasti mempunyai pasangan faktor yang lebih kecil atau sama dengan akar kuadratnya. Karena itu tidak perlu memeriksa semua angka sampai `angka - 1`.

---

## Implementasi Lengkap Soal 3

~~~ts
const nim: string = "230411013";

const duaDigitTerakhir: number =
  Number(nim.slice(-2));

const batas: number =
  duaDigitTerakhir + 10;

function isPrime(
  angka: number
): boolean {
  if (angka < 2) {
    return false;
  }

  for (
    let pembagi = 2;
    pembagi * pembagi <= angka;
    pembagi++
  ) {
    if (
      angka % pembagi === 0
    ) {
      return false;
    }
  }

  return true;
}

const bilanganPrima: number[] = [];

for (
  let angka = 2;
  angka <= batas;
  angka++
) {
  if (isPrime(angka)) {
    bilanganPrima.push(angka);
  }
}

console.log("NIM:", nim);
console.log(
  "2 digit terakhir:",
  duaDigitTerakhir
);
console.log("Batas:", batas);
console.log(
  "Bilangan prima:",
  bilanganPrima.join(", ")
);
~~~

Output:

~~~text
NIM: 230411013
2 digit terakhir: 13
Batas: 23
Bilangan prima: 2, 3, 5, 7, 11, 13, 17, 19, 23
~~~

---

## Dry Run Singkat

Untuk angka 9:

~~~text
9 % 2 != 0
9 % 3 == 0
→ bukan prima
~~~

Untuk angka 11:

~~~text
11 % 2 != 0
11 % 3 != 0
3 × 3 <= 11
pembagi berikutnya 4
4 × 4 > 11
→ prima
~~~

---

## Kesalahan umum Soal 3

1. Menganggap angka 1 sebagai prima.
2. Memulai pencarian dari 1.
3. Menggunakan kondisi modulo yang salah.
4. Tidak menghentikan pemeriksaan ketika menemukan pembagi.
5. Batas akhir tidak ikut diperiksa karena menggunakan `angka < batas`, padahal harus `angka <= batas`.
6. Lupa menambahkan 10 pada dua digit terakhir NIM.

---

# 🧠 SATU PROGRAM UNTUK MENYELESAIKAN TIGA SOAL

Setelah mahasiswa memahami masing-masing soal, ketiganya dapat dirapikan menjadi fungsi terpisah.

~~~ts
function digitTerakhir(
  nim: string
): number {
  return Number(
    nim.charAt(nim.length - 1)
  );
}

function duaDigitTerakhir(
  nim: string
): number {
  return Number(
    nim.slice(-2)
  );
}

function digitKetigaDariBelakang(
  nim: string
): number {
  return Number(
    nim.charAt(nim.length - 3)
  );
}

function buatSegitiga(
  tinggi: number
): string[] {
  const hasil: string[] = [];

  for (
    let baris = 1;
    baris <= tinggi;
    baris++
  ) {
    const angka: number[] = [];

    for (
      let kolom = 1;
      kolom <= baris;
      kolom++
    ) {
      angka.push(kolom);
    }

    hasil.push(
      angka.join(" ")
    );
  }

  return hasil;
}

function buatDeretAritmatika(
  start: number,
  step: number,
  jumlah: number
): number[] {
  const hasil: number[] = [];

  for (
    let i = 0;
    i < jumlah;
    i++
  ) {
    hasil.push(
      start + i * step
    );
  }

  return hasil;
}

function isPrime(
  angka: number
): boolean {
  if (angka < 2) {
    return false;
  }

  for (
    let pembagi = 2;
    pembagi * pembagi <= angka;
    pembagi++
  ) {
    if (
      angka % pembagi === 0
    ) {
      return false;
    }
  }

  return true;
}

function daftarPrima(
  batas: number
): number[] {
  const hasil: number[] = [];

  for (
    let angka = 2;
    angka <= batas;
    angka++
  ) {
    if (isPrime(angka)) {
      hasil.push(angka);
    }
  }

  return hasil;
}

const nim = "230411013";

// Soal 1
const tinggi =
  digitTerakhir(nim);

console.log("SOAL 1");
for (
  const baris of
  buatSegitiga(tinggi)
) {
  console.log(baris);
}

// Soal 2
const start =
  duaDigitTerakhir(nim);

const step =
  digitKetigaDariBelakang(nim)
  + 1;

console.log("\nSOAL 2");
console.log(
  buatDeretAritmatika(
    start,
    step,
    10
  ).join(", ")
);

// Soal 3
const batas =
  duaDigitTerakhir(nim)
  + 10;

console.log("\nSOAL 3");
console.log(
  daftarPrima(batas)
    .join(", ")
);
~~~

### Keuntungan versi modular

- logika ekstraksi NIM tidak diulang;
- setiap fungsi mempunyai satu tanggung jawab;
- mudah diuji;
- mudah digunakan kembali;
- lebih dekat dengan gaya pengembangan aplikasi sebenarnya.

---

# 🔍 VALIDASI NIM

Untuk menghindari error jika input tidak sesuai:

~~~ts
function validasiNim(
  nim: string
): void {
  if (nim.length < 3) {
    throw new Error(
      "NIM minimal harus 3 digit."
    );
  }

  if (!/^[0-9]+$/.test(nim)) {
    throw new Error(
      "NIM hanya boleh berisi angka."
    );
  }
}
~~~

Pemakaian:

~~~ts
const nim = "230411013";

try {
  validasiNim(nim);

  console.log(
    "NIM valid:",
    nim
  );
} catch (error) {
  console.error(error);
}
~~~

> Validasi ini merupakan **pengayaan** agar mahasiswa melihat bahwa program yang baik tidak hanya menghasilkan output saat input benar, tetapi juga mempertimbangkan input yang salah.

---

# 🧪 TEST CASE TUGAS 1

Mahasiswa sebaiknya tidak hanya mencoba satu NIM.

Contoh simulasi:

| NIM Uji | Tinggi Soal 1 | Start Soal 2 | Digit ke-3 + 1 | Batas Prima |
|---|---:|---:|---:|---:|
| 230411013 | 3 | 13 | 1 | 23 |
| 230411025 | 5 | 25 | 1 | 35 |
| 230411147 | 7 | 47 | 2 | 57 |

### Pertanyaan untuk mahasiswa

1. Jika digit terakhir NIM = 0, berapa baris yang dihasilkan oleh algoritma persis sesuai aturan?
2. Jika digit ke-3 dari belakang = 9, berapa nilai step?
3. Mengapa angka 1 tidak masuk daftar bilangan prima?
4. Mengapa `nim` lebih baik disimpan sebagai string?
5. Apa perbedaan `slice(-2)` dan `charAt(nim.length - 1)`?

---

# 🎤 PERTANYAAN DISKUSI TUGAS 1 + JAWABAN

### 1. Mengapa Soal 1 membutuhkan nested loop?

Karena terdapat dua dimensi pengulangan: baris dan isi setiap baris. Banyaknya elemen pada baris ke-`n` juga bergantung pada nilai `n`.

### 2. Mengapa Soal 2 dimulai dari i = 0?

Karena rumus yang digunakan:

~~~text
nilai = start + i × step
~~~

Untuk suku pertama, `i = 0`, sehingga nilai tetap sama dengan `start`.

### 3. Mengapa Soal 3 memakai modulo (%)?

Karena kita perlu mengetahui apakah suatu angka habis dibagi angka lain. Jika:

~~~text
angka % pembagi = 0
~~~

maka pembagi tersebut adalah faktor dari angka.

### 4. Mengapa function isPrime mengembalikan boolean?

Karena pertanyaannya hanya memiliki dua jawaban: bilangan tersebut prima (`true`) atau bukan prima (`false`).

### 5. Mengapa hasil deret dan bilangan prima disimpan dalam array?

Agar mudah diproses lagi, diuji, di-filter, atau diformat menggunakan `join(", ")`.

---

# 🧑‍🏫 SKENARIO LIVE CODING TYPESCRIPT SEBELUM IONIC

| Durasi | Materi |
|---|---|
| 0–15 menit | Instalasi TypeScript, tsc, ts-node |
| 15–30 menit | Hello World, compile TS → JS |
| 30–50 menit | var, let, const, tipe data |
| 50–65 menit | array, tuple, enum, union, any, unknown |
| 65–80 menit | operator + parsing NIM |
| 80–100 menit | if/else dan switch |
| 100–125 menit | for, nested loop, for...of, for...in |
| 125–140 menit | while, do...while, break, continue |
| 140–165 menit | function, arrow function, scope |
| 165–185 menit | interface, class, generics |
| 185–210 menit | Promise, chaining, async/await |
| 210–240 menit | Tugas 1 Soal 1 |
| 240–270 menit | Tugas 1 Soal 2 |
| 270–310 menit | Tugas 1 Soal 3 |
| 310–330 menit | Refactoring menjadi fungsi modular |
| 330–345 menit | Validasi + test case |
| 345–360 menit | Review sebelum masuk Ionic |

---

# ✅ CHECKLIST TYPESCRIPT SEBELUM MASUK IONIC

Mahasiswa diharapkan sudah mampu:

- [ ] Menginstall TypeScript dan ts-node.
- [ ] Menjelaskan proses TypeScript → JavaScript.
- [ ] Menggunakan var, let, const.
- [ ] Menggunakan tipe number, string, boolean.
- [ ] Menggunakan array dan tuple.
- [ ] Menjelaskan enum dan union.
- [ ] Membedakan any dan unknown.
- [ ] Menggunakan operator aritmatika, perbandingan, dan logika.
- [ ] Mengambil digit dari NIM menggunakan string.
- [ ] Membuat if/else dan switch.
- [ ] Membuat for, nested for, while, dan do...while.
- [ ] Menggunakan break dan continue.
- [ ] Membuat function dan arrow function.
- [ ] Memahami scope let dan var.
- [ ] Membuat interface.
- [ ] Memahami class dan object.
- [ ] Memahami generic sederhana.
- [ ] Menjelaskan Promise.
- [ ] Menggunakan async/await dan try/catch.
- [ ] Menyelesaikan ketiga soal Tugas 1 tanpa hard-code output.
- [ ] Menjelaskan algoritma, bukan hanya menunjukkan hasil.

---

# ➡️ TRANSISI DARI TYPESCRIPT KE IONIC

Setelah memahami bagian di atas, konsep yang sama akan muncul kembali di Ionic:

| TypeScript | Penggunaan pada Ionic/Vue |
|---|---|
| interface | tipe data API / form / model |
| array | daftar item yang ditampilkan dengan v-for |
| function | event handler |
| class/service | akses API atau native service |
| Promise | HTTP, Camera, Geolocation |
| async/await | menunggu operasi asynchronous |
| try/catch | menangani error API/native |
| if | conditional logic |
| loop | pengolahan data |
| string parsing | validasi dan transformasi input |

Dengan demikian, Ionic bukan materi yang terpisah dari TypeScript. Ionic menggunakan kembali konsep-konsep yang telah dipelajari, tetapi ditempatkan pada konteks aplikasi perangkat bergerak.

---


### Langkah 3: Instalasi Ionic CLI

Ionic CLI (Command Line Interface) adalah tool untuk membuat dan mengelola project Ionic.

1. **Buka Command Prompt / Terminal**

2. **Install Ionic CLI secara global**
   ```bash
   npm install -g @ionic/cli
   ```

   **Penjelasan:**
   - `npm install`: perintah untuk menginstal package
   - `-g`: flag untuk instalasi global (bisa diakses dari mana saja)
   - `@ionic/cli`: nama package Ionic CLI

3. **Tunggu proses instalasi** (sekitar 2-5 menit tergantung koneksi internet)

4. **Verifikasi Instalasi Ionic**
   ```bash
   ionic --version
   ```
   - Akan muncul versi Ionic, contoh: `7.1.1`

---

### Langkah 4: Instalasi Visual Studio Code (Editor Code)

Visual Studio Code adalah text editor yang sangat populer untuk development web dan mobile.

1. **Download VS Code**
   - Kunjungi: https://code.visualstudio.com/
   - Klik tombol "Download for Windows/Mac/Linux" (sesuai OS Anda)

2. **Instalasi VS Code**
   - Jalankan installer
   - Ikuti wizard instalasi
   - **Penting**: Pada bagian "Select Additional Tasks", centang:
     - ✅ Add "Open with Code" action to Windows Explorer file context menu
     - ✅ Add "Open with Code" action to Windows Explorer directory context menu
     - ✅ Add to PATH

3. **Instalasi Extension yang Direkomendasikan**

   Setelah VS Code terbuka:
   - Klik icon Extensions di sidebar kiri (atau tekan `Ctrl+Shift+X`)
   - Install extension berikut:
     - **Volar** - untuk Vue.js support
     - **Ionic** - untuk Ionic framework support
     - **ESLint** - untuk code quality
     - **Prettier** - untuk code formatting

---

## 🚀 PRAKTIKUM 1: MEMBUAT PROJECT IONIC PERTAMA

### Pengantar

Pada praktikum pertama ini, kita akan membuat aplikasi Ionic sederhana dari awal. Anda akan mempelajari struktur project Ionic dan cara menjalankan aplikasi di browser.

---

### Langkah 1: Membuat Project Baru

1. **Buat folder untuk menyimpan project**

   Buka Command Prompt / Terminal, buat folder untuk project Anda:
   ```bash
   cd Desktop
   mkdir ionic-projects
   cd ionic-projects
   ```

2. **Buat project Ionic baru**
   ```bash
   ionic start aplikasi-pertama blank --type=vue
   ```

   **Penjelasan perintah:**
   - `ionic start`: perintah untuk membuat project baru
   - `aplikasi-pertama`: nama project (bebas, sesuaikan dengan keinginan)
   - `blank`: template yang digunakan (template kosong/minimal)
   - `--type=vue`: menggunakan Vue.js sebagai framework

3. **Proses instalasi**

   Anda akan ditanya beberapa pertanyaan:

   ```
   ? Install the free Ionic Appflow SDK and connect your app? (Y/n)
   ```
   Ketik `n` lalu Enter (kita tidak memerlukan Appflow untuk pembelajaran ini)

4. **Tunggu proses pembuatan project** (sekitar 3-5 menit)

   Ionic CLI akan:
   - Membuat folder project
   - Mendownload semua dependencies yang diperlukan
   - Mengkonfigurasi project

   Jika sudah selesai, akan muncul pesan:
   ```
   ✔ Preparing directory ./aplikasi-pertama
   ✔ Downloading and extracting blank starter
   ✔ Installing dependencies with npm - done!

   Your Ionic app is ready! Follow these next steps:

   - Go to your new project: cd ./aplikasi-pertama
   - Run ionic serve within the app directory to see your app in the browser
   ```

---

### Langkah 2: Menjalankan Aplikasi

1. **Masuk ke folder project**
   ```bash
   cd aplikasi-pertama
   ```

2. **Jalankan development server**
   ```bash
   ionic serve
   ```

   **Penjelasan:**
   - Perintah ini akan menjalankan web server lokal
   - Aplikasi akan otomatis dibuka di browser
   - Server akan berjalan di: `http://localhost:8100`

3. **Melihat aplikasi di browser**

   Browser akan otomatis terbuka dan menampilkan aplikasi Anda. Anda akan melihat:
   - Halaman kosong dengan header "Blank"
   - Latar belakang putih
   - Di DevTools (F12), Anda bisa melihat tampilan mobile

4. **Hot Reload**

   Keunggulan `ionic serve`:
   - Setiap kali Anda menyimpan perubahan kode, browser akan otomatis refresh
   - Tidak perlu manual refresh browser
   - Sangat membantu dalam development

5. **Menghentikan server**

   Untuk menghentikan server, tekan `Ctrl + C` di Command Prompt/Terminal

---

### Langkah 3: Membuka Project di VS Code

1. **Buka VS Code**

2. **Open Folder**
   - File → Open Folder (atau tekan `Ctrl+K Ctrl+O`)
   - Pilih folder `aplikasi-pertama`
   - Klik "Select Folder"

3. **Struktur Folder Project**

   Anda akan melihat struktur folder seperti ini:

   ```
   aplikasi-pertama/
   ├── node_modules/          # Dependencies (jangan diubah)
   ├── public/                # Asset publik (gambar, icon, dll)
   ├── src/                   # Source code utama
   │   ├── components/        # Komponen Vue reusable
   │   ├── router/            # Konfigurasi routing
   │   ├── views/             # Halaman-halaman aplikasi
   │   ├── theme/             # File CSS untuk tema
   │   ├── App.vue            # Komponen root
   │   └── main.ts            # Entry point aplikasi
   ├── .gitignore             # File yang diabaikan Git
   ├── index.html             # HTML utama
   ├── ionic.config.json      # Konfigurasi Ionic
   ├── package.json           # Dependencies dan scripts
   ├── tsconfig.json          # Konfigurasi TypeScript
   └── vite.config.ts         # Konfigurasi Vite (build tool)
   ```

---

### Langkah 4: Memahami File-File Penting

#### 1. **src/App.vue**

File ini adalah komponen root aplikasi. Buka file ini di VS Code:

```vue
<template>
  <ion-app>
    <ion-router-outlet />
  </ion-app>
</template>

<script setup lang="ts">
import { IonApp, IonRouterOutlet } from '@ionic/vue';
</script>
```

**Penjelasan:**
- `<ion-app>`: Komponen wrapper utama Ionic
- `<ion-router-outlet>`: Tempat untuk menampilkan halaman sesuai routing
- `import { IonApp, IonRouterOutlet }`: Mengimport komponen Ionic yang diperlukan

#### 2. **src/views/HomePage.vue**

File ini adalah halaman utama aplikasi:

```vue
<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Blank</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Blank</ion-title>
        </ion-toolbar>
      </ion-header>

      <div id="container">
        <strong>Ready to create an app?</strong>
        <p>Start with Ionic <a target="_blank" rel="noopener noreferrer" href="https://ionicframework.com/docs/components">UI Components</a></p>
      </div>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar } from '@ionic/vue';
</script>

<style scoped>
#container {
  text-align: center;
  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
}

#container strong {
  font-size: 20px;
  line-height: 26px;
}

#container p {
  font-size: 16px;
  line-height: 22px;
  color: #8c8c8c;
  margin: 0;
}

#container a {
  text-decoration: none;
}
</style>
```

**Penjelasan Komponen Ionic:**
- `<ion-page>`: Wrapper untuk setiap halaman
- `<ion-header>`: Header aplikasi (bagian atas)
- `<ion-toolbar>`: Toolbar dalam header
- `<ion-title>`: Judul halaman
- `<ion-content>`: Konten utama halaman

---

### Langkah 5: Modifikasi Aplikasi Pertama

Sekarang kita akan memodifikasi aplikasi agar lebih personal!

1. **Edit file `src/views/HomePage.vue`**

2. **Ubah judul halaman**

   Cari baris:
   ```vue
   <ion-title>Blank</ion-title>
   ```

   Ubah menjadi:
   ```vue
   <ion-title>Aplikasi Pertama Saya</ion-title>
   ```

3. **Ubah konten halaman**

   Cari section:
   ```vue
   <div id="container">
     <strong>Ready to create an app?</strong>
     <p>Start with Ionic <a target="_blank" rel="noopener noreferrer" href="https://ionicframework.com/docs/components">UI Components</a></p>
   </div>
   ```

   Ubah menjadi:
   ```vue
   <div id="container">
     <strong>Selamat Datang di Aplikasi Mobile Saya!</strong>
     <p>Nama: [Isi dengan nama Anda]</p>
     <p>NIM: [Isi dengan NIM Anda]</p>
     <p>Program Studi: Sistem Informasi</p>
     <p>Universitas Terbuka</p>
   </div>
   ```

4. **Simpan file** (Ctrl+S)

5. **Lihat perubahan di browser**

   Jika `ionic serve` masih berjalan, browser akan otomatis refresh dan menampilkan perubahan Anda!

---

## 🎨 PRAKTIKUM 2: TEKNIK LAYOUT DENGAN IONIC GRID

### Pengantar

Ionic Grid adalah sistem layout yang responsif dan fleksibel, mirip dengan Bootstrap Grid. Grid system memudahkan kita untuk membuat layout yang rapi dan terstruktur.

### Konsep Dasar Ionic Grid

Ionic Grid terdiri dari 3 komponen utama:
1. **`<ion-grid>`**: Container utama
2. **`<ion-row>`**: Baris dalam grid
3. **`<ion-col>`**: Kolom dalam baris

Setiap row bisa dibagi menjadi maksimal 12 kolom.

---

### Langkah 1: Membuat Halaman Baru untuk Grid

1. **Buat file baru** di folder `src/views` dengan nama `GridPage.vue`

2. **Isi file dengan kode berikut:**

```vue
<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Layout dengan Grid</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content class="ion-padding">
      <h2>Contoh Grid System</h2>

      <!-- Grid 1: Baris dengan 3 kolom sama besar -->
      <h3>1. Tiga Kolom Sama Besar</h3>
      <ion-grid>
        <ion-row>
          <ion-col>
            <div class="box">Kolom 1</div>
          </ion-col>
          <ion-col>
            <div class="box">Kolom 2</div>
          </ion-col>
          <ion-col>
            <div class="box">Kolom 3</div>
          </ion-col>
        </ion-row>
      </ion-grid>

      <!-- Grid 2: Kolom dengan ukuran berbeda -->
      <h3>2. Kolom dengan Ukuran Berbeda</h3>
      <ion-grid>
        <ion-row>
          <ion-col size="3">
            <div class="box">25%</div>
          </ion-col>
          <ion-col size="6">
            <div class="box">50%</div>
          </ion-col>
          <ion-col size="3">
            <div class="box">25%</div>
          </ion-col>
        </ion-row>
      </ion-grid>

      <!-- Grid 3: Responsive Grid -->
      <h3>3. Responsive Grid</h3>
      <ion-grid>
        <ion-row>
          <ion-col size="12" size-md="6" size-lg="4">
            <div class="box">Responsif 1</div>
          </ion-col>
          <ion-col size="12" size-md="6" size-lg="4">
            <div class="box">Responsif 2</div>
          </ion-col>
          <ion-col size="12" size-md="6" size-lg="4">
            <div class="box">Responsif 3</div>
          </ion-col>
        </ion-row>
      </ion-grid>

      <!-- Grid 4: Alignment -->
      <h3>4. Alignment (Perataan)</h3>
      <ion-grid>
        <ion-row class="ion-align-items-center" style="height: 150px; background: #f0f0f0;">
          <ion-col>
            <div class="box">Vertikal Center</div>
          </ion-col>
          <ion-col>
            <div class="box">Vertikal Center</div>
          </ion-col>
        </ion-row>
      </ion-grid>

      <h3>5. Offset (Geser Kolom)</h3>
      <ion-grid>
        <ion-row>
          <ion-col size="3" offset="3">
            <div class="box">Offset 3</div>
          </ion-col>
          <ion-col size="3">
            <div class="box">Normal</div>
          </ion-col>
        </ion-row>
      </ion-grid>

    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
  IonGrid,
  IonRow,
  IonCol
} from '@ionic/vue';
</script>

<style scoped>
.box {
  background-color: #3880ff;
  color: white;
  padding: 15px;
  text-align: center;
  border-radius: 5px;
  margin: 5px 0;
  font-weight: bold;
}

h2 {
  color: #3880ff;
  margin-top: 20px;
}

h3 {
  color: #666;
  margin-top: 30px;
  margin-bottom: 10px;
  font-size: 16px;
}
</style>
```

**Penjelasan Kode:**

1. **Grid 1 - Tiga Kolom Sama Besar:**
   - Tanpa atribut `size`, kolom akan otomatis sama besar
   - Setiap kolom mendapat 4 dari 12 bagian (33.33%)

2. **Grid 2 - Ukuran Custom:**
   - `size="3"` = 3/12 = 25%
   - `size="6"` = 6/12 = 50%
   - Total harus 12 untuk satu baris penuh

3. **Grid 3 - Responsive:**
   - `size="12"` = full width di mobile (layar kecil)
   - `size-md="6"` = 50% di tablet (medium screen)
   - `size-lg="4"` = 33.33% di desktop (large screen)

4. **Grid 4 - Alignment:**
   - `ion-align-items-center` = vertikal center
   - Ada juga: `ion-justify-content-center` (horizontal center)

5. **Grid 5 - Offset:**
   - `offset="3"` = geser 3 kolom dari kiri
   - Berguna untuk membuat spacing

---

### Langkah 2: Menambahkan Route

Agar halaman GridPage bisa diakses, kita perlu menambahkan routing.

1. **Buka file `src/router/index.ts`**

2. **Import GridPage:**

   Tambahkan di bagian atas:
   ```typescript
   import GridPage from '../views/GridPage.vue'
   ```

3. **Tambahkan route:**

   Dalam array `routes`, tambahkan:
   ```typescript
   {
     path: '/grid',
     component: GridPage
   }
   ```

4. **Kode lengkap `src/router/index.ts`:**

```typescript
import { createRouter, createWebHistory } from '@ionic/vue-router';
import { RouteRecordRaw } from 'vue-router';
import HomePage from '../views/HomePage.vue';
import GridPage from '../views/GridPage.vue';

const routes: Array<RouteRecordRaw> = [
  {
    path: '/',
    redirect: '/home'
  },
  {
    path: '/home',
    name: 'Home',
    component: HomePage
  },
  {
    path: '/grid',
    name: 'Grid',
    component: GridPage
  }
]

const router = createRouter({
  history: createWebHistory(import.meta.env.BASE_URL),
  routes
})

export default router
```

5. **Simpan file**

6. **Akses halaman Grid di browser:**

   Buka: `http://localhost:8100/grid`

---

### Langkah 3: Menambahkan Navigasi

Agar lebih mudah berpindah halaman, kita tambahkan tombol navigasi.

1. **Edit `src/views/HomePage.vue`**

2. **Tambahkan button untuk navigasi ke GridPage:**

```vue
<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Aplikasi Pertama Saya</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true" class="ion-padding">
      <div id="container">
        <strong>Selamat Datang di Aplikasi Mobile Saya!</strong>
        <p>Nama: [Isi dengan nama Anda]</p>
        <p>NIM: [Isi dengan NIM Anda]</p>
        <p>Program Studi: Sistem Informasi</p>
        <p>Universitas Terbuka</p>

        <!-- Tombol Navigasi -->
        <ion-button expand="block" router-link="/grid" style="margin-top: 30px;">
          Lihat Contoh Grid Layout
        </ion-button>
      </div>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import {
  IonContent,
  IonHeader,
  IonPage,
  IonTitle,
  IonToolbar,
  IonButton
} from '@ionic/vue';
</script>

<style scoped>
#container {
  text-align: center;
  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
  padding: 0 20px;
}

#container strong {
  font-size: 20px;
  line-height: 26px;
}

#container p {
  font-size: 16px;
  line-height: 22px;
  color: #8c8c8c;
  margin: 5px 0;
}
</style>
```

3. **Tambahkan tombol kembali di GridPage:**

Edit `src/views/GridPage.vue`, tambahkan tombol di bagian bawah content:

```vue
<!-- Tambahkan sebelum closing tag </ion-content> -->
<ion-button expand="block" router-link="/home" color="medium">
  Kembali ke Home
</ion-button>
```

4. **Simpan dan test navigasi di browser!**

---

## 🎨 PRAKTIKUM 3: THEME DAN STYLING

### Pengantar

Ionic menyediakan sistem theming yang powerful berbasis CSS Variables. Kita bisa dengan mudah mengubah warna, font, dan style aplikasi.

---

### Langkah 1: Memahami File Theme

1. **Buka file `src/theme/variables.css`**

   File ini berisi CSS variables yang mengontrol warna dan style aplikasi.

2. **Struktur CSS Variables:**

```css
:root {
  /** primary **/
  --ion-color-primary: #3880ff;
  --ion-color-primary-rgb: 56, 128, 255;
  --ion-color-primary-contrast: #ffffff;
  --ion-color-primary-contrast-rgb: 255, 255, 255;
  --ion-color-primary-shade: #3171e0;
  --ion-color-primary-tint: #4c8dff;

  /** secondary **/
  --ion-color-secondary: #3dc2ff;
  /* ... dst */
}
```

**Penjelasan:**
- `--ion-color-primary`: Warna utama aplikasi
- `--ion-color-primary-contrast`: Warna teks di atas primary
- `--ion-color-primary-shade`: Warna lebih gelap (untuk hover/active)
- `--ion-color-primary-tint`: Warna lebih terang

---

### Langkah 2: Mengubah Warna Tema

Mari kita ubah warna tema aplikasi menjadi hijau!

1. **Edit `src/theme/variables.css`**

2. **Ubah warna primary:**

```css
:root {
  /** primary - diubah ke hijau **/
  --ion-color-primary: #28a745;
  --ion-color-primary-rgb: 40, 167, 69;
  --ion-color-primary-contrast: #ffffff;
  --ion-color-primary-contrast-rgb: 255, 255, 255;
  --ion-color-primary-shade: #24923d;
  --ion-color-primary-tint: #3fb058;

  /* Biarkan warna lain tetap default */
}
```

3. **Simpan dan lihat perubahannya!**

   Toolbar dan button akan berubah menjadi hijau.

---

### Langkah 3: Membuat Custom Color

Kita bisa membuat warna custom sendiri!

1. **Tambahkan di `src/theme/variables.css`:**

```css
:root {
  /* ... warna default ... */

  /** custom color - untan **/
  --ion-color-untan: #FFD700;
  --ion-color-untan-rgb: 255, 215, 0;
  --ion-color-untan-contrast: #000000;
  --ion-color-untan-contrast-rgb: 0, 0, 0;
  --ion-color-untan-shade: #e0bc00;
  --ion-color-untan-tint: #ffd966;
}

.ion-color-untan {
  --ion-color-base: var(--ion-color-untan);
  --ion-color-base-rgb: var(--ion-color-untan-rgb);
  --ion-color-contrast: var(--ion-color-untan-contrast);
  --ion-color-contrast-rgb: var(--ion-color-untan-contrast-rgb);
  --ion-color-shade: var(--ion-color-untan-shade);
  --ion-color-tint: var(--ion-color-untan-tint);
}
```

2. **Gunakan warna custom:**

Buat halaman baru `src/views/ThemePage.vue`:

```vue
<template>
  <ion-page>
    <ion-header>
      <ion-toolbar color="untan">
        <ion-title>Custom Theme</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content class="ion-padding">
      <h2>Contoh Penggunaan Warna</h2>

      <ion-button expand="block" color="primary">
        Primary Color (Hijau)
      </ion-button>

      <ion-button expand="block" color="secondary">
        Secondary Color
      </ion-button>

      <ion-button expand="block" color="untan">
        Custom Color (Untan Gold)
      </ion-button>

      <ion-button expand="block" color="success">
        Success Color
      </ion-button>

      <ion-button expand="block" color="warning">
        Warning Color
      </ion-button>

      <ion-button expand="block" color="danger">
        Danger Color
      </ion-button>

      <ion-button expand="block" color="dark">
        Dark Color
      </ion-button>

      <ion-button expand="block" color="light">
        Light Color
      </ion-button>

      <h3 style="margin-top: 30px;">Cards dengan Warna</h3>

      <ion-card color="primary">
        <ion-card-header>
          <ion-card-title>Primary Card</ion-card-title>
        </ion-card-header>
        <ion-card-content>
          Ini adalah card dengan warna primary.
        </ion-card-content>
      </ion-card>

      <ion-card color="untan">
        <ion-card-header>
          <ion-card-title>Untan Card</ion-card-title>
        </ion-card-header>
        <ion-card-content>
          Ini adalah card dengan warna custom Untan.
        </ion-card-content>
      </ion-card>

      <ion-button expand="block" router-link="/home" color="medium">
        Kembali ke Home
      </ion-button>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
  IonButton,
  IonCard,
  IonCardHeader,
  IonCardTitle,
  IonCardContent
} from '@ionic/vue';
</script>

<style scoped>
h2 {
  color: #333;
  margin-bottom: 20px;
}

h3 {
  color: #666;
}

ion-button {
  margin: 10px 0;
}

ion-card {
  margin: 15px 0;
}
</style>
```

3. **Tambahkan route di `src/router/index.ts`:**

```typescript
import ThemePage from '../views/ThemePage.vue';

// Dalam routes array:
{
  path: '/theme',
  name: 'Theme',
  component: ThemePage
}
```

4. **Tambahkan link dari HomePage:**

Tambahkan button di `HomePage.vue`:

```vue
<ion-button expand="block" router-link="/theme" color="secondary" style="margin-top: 10px;">
  Lihat Contoh Theme
</ion-button>
```

---

### Langkah 4: Dark Mode

Ionic mendukung dark mode secara native!

1. **Dark mode sudah ada di `src/theme/variables.css`**

   Cari bagian:
   ```css
   @media (prefers-color-scheme: dark) {
     /* Dark mode variables */
   }
   ```

2. **Mengaktifkan dark mode:**

   Dark mode akan otomatis aktif jika sistem operasi dalam mode gelap.

3. **Toggle dark mode manual:**

   Buat file baru `src/views/SettingsPage.vue`:

```vue
<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Pengaturan</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content class="ion-padding">
      <ion-list>
        <ion-item>
          <ion-label>Dark Mode</ion-label>
          <ion-toggle
            :checked="isDarkMode"
            @ionChange="toggleDarkMode"
          ></ion-toggle>
        </ion-item>
      </ion-list>

      <ion-button expand="block" router-link="/home" color="medium" style="margin-top: 30px;">
        Kembali ke Home
      </ion-button>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
  IonList,
  IonItem,
  IonLabel,
  IonToggle,
  IonButton
} from '@ionic/vue';

const isDarkMode = ref(false);

const toggleDarkMode = (event: CustomEvent) => {
  isDarkMode.value = event.detail.checked;
  document.body.classList.toggle('dark', isDarkMode.value);
};
</script>
```

4. **Tambahkan route dan link seperti sebelumnya**

---

## 🧩 PRAKTIKUM 4: KOMPONEN UI IONIC

### Pengantar

Ionic menyediakan puluhan komponen UI siap pakai yang mengikuti design pattern iOS dan Android. Mari kita coba beberapa komponen penting!

---

### Langkah 1: Membuat Halaman Komponen

Buat file `src/views/ComponentsPage.vue`:

```vue
<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-back-button default-href="/home"></ion-back-button>
        </ion-buttons>
        <ion-title>Komponen Ionic</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content>
      <!-- List -->
      <ion-list>
        <ion-list-header>
          <ion-label>Daftar Item</ion-label>
        </ion-list-header>

        <ion-item>
          <ion-icon :icon="personOutline" slot="start"></ion-icon>
          <ion-label>Profil Saya</ion-label>
        </ion-item>

        <ion-item>
          <ion-icon :icon="settingsOutline" slot="start"></ion-icon>
          <ion-label>Pengaturan</ion-label>
          <ion-badge slot="end" color="danger">3</ion-badge>
        </ion-item>

        <ion-item>
          <ion-icon :icon="notificationsOutline" slot="start"></ion-icon>
          <ion-label>Notifikasi</ion-label>
          <ion-toggle slot="end"></ion-toggle>
        </ion-item>
      </ion-list>

      <!-- Cards -->
      <div class="ion-padding">
        <h2>Cards</h2>

        <ion-card>
          <img src="https://picsum.photos/400/200" alt="Gambar" />
          <ion-card-header>
            <ion-card-subtitle>Subtitle Card</ion-card-subtitle>
            <ion-card-title>Judul Card</ion-card-title>
          </ion-card-header>
          <ion-card-content>
            Ini adalah contoh card dengan gambar. Card sangat berguna untuk menampilkan informasi dalam bentuk kotak yang rapi.
          </ion-card-content>
        </ion-card>

        <!-- Buttons -->
        <h2>Buttons</h2>

        <ion-button expand="full">Full Button</ion-button>
        <ion-button expand="block">Block Button</ion-button>

        <div style="display: flex; gap: 10px;">
          <ion-button expand="full" fill="solid">Solid</ion-button>
          <ion-button expand="full" fill="outline">Outline</ion-button>
          <ion-button expand="full" fill="clear">Clear</ion-button>
        </div>

        <div style="display: flex; gap: 10px; margin-top: 10px;">
          <ion-button size="small">Small</ion-button>
          <ion-button size="default">Default</ion-button>
          <ion-button size="large">Large</ion-button>
        </div>

        <!-- Icons -->
        <h2>Icons</h2>
        <div style="display: flex; gap: 20px; font-size: 32px;">
          <ion-icon :icon="heartOutline" color="danger"></ion-icon>
          <ion-icon :icon="starOutline" color="warning"></ion-icon>
          <ion-icon :icon="thumbsUpOutline" color="primary"></ion-icon>
          <ion-icon :icon="shareOutline" color="secondary"></ion-icon>
        </div>

        <!-- Chips -->
        <h2>Chips</h2>
        <div>
          <ion-chip color="primary">
            <ion-label>Primary Chip</ion-label>
          </ion-chip>

          <ion-chip color="secondary">
            <ion-icon :icon="personOutline"></ion-icon>
            <ion-label>User</ion-label>
          </ion-chip>

          <ion-chip color="success">
            <ion-icon :icon="checkmarkOutline"></ion-icon>
            <ion-label>Success</ion-label>
            <ion-icon :icon="closeCircleOutline"></ion-icon>
          </ion-chip>
        </div>

        <!-- Input -->
        <h2>Form Input</h2>

        <ion-item>
          <ion-label position="floating">Nama</ion-label>
          <ion-input type="text" placeholder="Masukkan nama"></ion-input>
        </ion-item>

        <ion-item>
          <ion-label position="floating">Email</ion-label>
          <ion-input type="email" placeholder="email@example.com"></ion-input>
        </ion-item>

        <ion-item>
          <ion-label position="floating">Password</ion-label>
          <ion-input type="password"></ion-input>
        </ion-item>

        <ion-item>
          <ion-label>Tanggal Lahir</ion-label>
          <ion-datetime></ion-datetime>
        </ion-item>

        <ion-item>
          <ion-label>Program Studi</ion-label>
          <ion-select placeholder="Pilih Prodi">
            <ion-select-option value="si">Sistem Informasi</ion-select-option>
            <ion-select-option value="ti">Teknik Informatika</ion-select-option>
            <ion-select-option value="mi">Manajemen Informatika</ion-select-option>
          </ion-select>
        </ion-item>

        <!-- Alerts & Toasts -->
        <h2>Alerts & Toasts</h2>

        <ion-button expand="block" @click="presentAlert">
          Tampilkan Alert
        </ion-button>

        <ion-button expand="block" @click="presentToast">
          Tampilkan Toast
        </ion-button>

        <ion-button expand="block" @click="presentActionSheet">
          Tampilkan Action Sheet
        </ion-button>

        <!-- Loading -->
        <ion-button expand="block" @click="presentLoading">
          Tampilkan Loading
        </ion-button>

        <ion-button expand="block" router-link="/home" color="medium" style="margin-top: 30px;">
          Kembali ke Home
        </ion-button>
      </div>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
  IonButtons,
  IonBackButton,
  IonList,
  IonListHeader,
  IonItem,
  IonLabel,
  IonIcon,
  IonBadge,
  IonToggle,
  IonCard,
  IonCardHeader,
  IonCardSubtitle,
  IonCardTitle,
  IonCardContent,
  IonButton,
  IonChip,
  IonInput,
  IonDatetime,
  IonSelect,
  IonSelectOption,
  alertController,
  toastController,
  actionSheetController,
  loadingController
} from '@ionic/vue';

import {
  personOutline,
  settingsOutline,
  notificationsOutline,
  heartOutline,
  starOutline,
  thumbsUpOutline,
  shareOutline,
  checkmarkOutline,
  closeCircleOutline
} from 'ionicons/icons';

// Alert
const presentAlert = async () => {
  const alert = await alertController.create({
    header: 'Perhatian',
    subHeader: 'Ini adalah subtitle',
    message: 'Ini adalah contoh alert dialog di Ionic.',
    buttons: ['OK']
  });

  await alert.present();
};

// Toast
const presentToast = async () => {
  const toast = await toastController.create({
    message: 'Ini adalah toast message!',
    duration: 2000,
    position: 'bottom',
    color: 'success'
  });

  await toast.present();
};

// Action Sheet
const presentActionSheet = async () => {
  const actionSheet = await actionSheetController.create({
    header: 'Pilih Aksi',
    buttons: [
      {
        text: 'Delete',
        role: 'destructive',
        data: {
          action: 'delete',
        },
      },
      {
        text: 'Share',
        data: {
          action: 'share',
        },
      },
      {
        text: 'Cancel',
        role: 'cancel',
        data: {
          action: 'cancel',
        },
      },
    ],
  });

  await actionSheet.present();
};

// Loading
const presentLoading = async () => {
  const loading = await loadingController.create({
    message: 'Loading...',
    duration: 2000,
  });

  await loading.present();
};
</script>

<style scoped>
h2 {
  color: #333;
  margin-top: 30px;
  margin-bottom: 15px;
  font-size: 18px;
}

ion-card {
  margin: 15px 0;
}
</style>
```

**Penjelasan Komponen:**

1. **IonList & IonItem**: Untuk menampilkan daftar
2. **IonIcon**: Icon dari Ionicons
3. **IonBadge**: Label kecil (notifikasi)
4. **IonToggle**: Switch on/off
5. **IonCard**: Kotak informasi
6. **IonButton**: Tombol dengan berbagai style
7. **IonChip**: Label/tag
8. **IonInput**: Input teks
9. **IonSelect**: Dropdown
10. **IonDatetime**: Pemilih tanggal/waktu
11. **Alert, Toast, ActionSheet, Loading**: Dialog interaktif

---

### Langkah 2: Menambahkan Route

```typescript
// src/router/index.ts
import ComponentsPage from '../views/ComponentsPage.vue';

// Dalam routes:
{
  path: '/components',
  name: 'Components',
  component: ComponentsPage
}
```

---

### Langkah 3: Link dari HomePage

Tambahkan di HomePage:

```vue
<ion-button expand="block" router-link="/components" color="tertiary" style="margin-top: 10px;">
  Lihat Komponen UI
</ion-button>
```

---

## 📱 PRAKTIKUM 5: MEMBUAT APLIKASI SEDERHANA

### Studi Kasus: Aplikasi Daftar Tugas (To-Do List)

Sekarang kita akan membuat aplikasi sederhana yang menggabungkan semua yang sudah dipelajari!

---

### Langkah 1: Membuat Halaman To-Do

Buat file `src/views/TodoPage.vue`:

```vue
<template>
  <ion-page>
    <ion-header>
      <ion-toolbar color="primary">
        <ion-buttons slot="start">
          <ion-back-button default-href="/home"></ion-back-button>
        </ion-buttons>
        <ion-title>Daftar Tugas Saya</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content>
      <!-- Form Input Tugas -->
      <div class="ion-padding">
        <ion-item>
          <ion-label position="floating">Tugas Baru</ion-label>
          <ion-input
            v-model="newTodo"
            placeholder="Apa yang perlu dilakukan?"
            @keyup.enter="addTodo"
          ></ion-input>
        </ion-item>

        <ion-button expand="block" @click="addTodo" style="margin-top: 10px;">
          <ion-icon :icon="addOutline" slot="start"></ion-icon>
          Tambah Tugas
        </ion-button>
      </div>

      <!-- Statistik -->
      <div class="ion-padding">
        <ion-grid>
          <ion-row>
            <ion-col>
              <ion-card color="primary">
                <ion-card-content class="stat-card">
                  <div class="stat-number">{{ totalTodos }}</div>
                  <div class="stat-label">Total</div>
                </ion-card-content>
              </ion-card>
            </ion-col>
            <ion-col>
              <ion-card color="success">
                <ion-card-content class="stat-card">
                  <div class="stat-number">{{ completedTodos }}</div>
                  <div class="stat-label">Selesai</div>
                </ion-card-content>
              </ion-card>
            </ion-col>
            <ion-col>
              <ion-card color="warning">
                <ion-card-content class="stat-card">
                  <div class="stat-number">{{ pendingTodos }}</div>
                  <div class="stat-label">Pending</div>
                </ion-card-content>
              </ion-card>
            </ion-col>
          </ion-row>
        </ion-grid>
      </div>

      <!-- Daftar Tugas -->
      <ion-list v-if="todos.length > 0">
        <ion-list-header>
          <ion-label>Daftar Tugas</ion-label>
        </ion-list-header>

        <ion-item-sliding v-for="(todo, index) in todos" :key="index">
          <ion-item>
            <ion-checkbox
              slot="start"
              :checked="todo.completed"
              @ionChange="toggleTodo(index)"
            ></ion-checkbox>
            <ion-label :class="{ 'completed': todo.completed }">
              {{ todo.text }}
            </ion-label>
            <ion-badge :color="todo.completed ? 'success' : 'warning'" slot="end">
              {{ todo.completed ? 'Selesai' : 'Pending' }}
            </ion-badge>
          </ion-item>

          <ion-item-options side="end">
            <ion-item-option color="danger" @click="deleteTodo(index)">
              <ion-icon :icon="trashOutline"></ion-icon>
              Hapus
            </ion-item-option>
          </ion-item-options>
        </ion-item-sliding>
      </ion-list>

      <!-- Empty State -->
      <div v-else class="empty-state">
        <ion-icon :icon="checkmarkDoneOutline" style="font-size: 80px; color: #ccc;"></ion-icon>
        <h2>Belum Ada Tugas</h2>
        <p>Tambahkan tugas pertama Anda!</p>
      </div>

    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue';
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
  IonButtons,
  IonBackButton,
  IonItem,
  IonLabel,
  IonInput,
  IonButton,
  IonIcon,
  IonGrid,
  IonRow,
  IonCol,
  IonCard,
  IonCardContent,
  IonList,
  IonListHeader,
  IonItemSliding,
  IonItemOptions,
  IonItemOption,
  IonCheckbox,
  IonBadge,
  toastController
} from '@ionic/vue';

import {
  addOutline,
  trashOutline,
  checkmarkDoneOutline
} from 'ionicons/icons';

// State
interface Todo {
  text: string;
  completed: boolean;
}

const newTodo = ref('');
const todos = ref<Todo[]>([
  { text: 'Belajar Ionic Framework', completed: false },
  { text: 'Membuat aplikasi mobile', completed: false },
  { text: 'Mengerjakan tugas kuliah', completed: false }
]);

// Computed
const totalTodos = computed(() => todos.value.length);
const completedTodos = computed(() => todos.value.filter(t => t.completed).length);
const pendingTodos = computed(() => todos.value.filter(t => !t.completed).length);

// Methods
const addTodo = async () => {
  if (newTodo.value.trim() === '') {
    const toast = await toastController.create({
      message: 'Tugas tidak boleh kosong!',
      duration: 2000,
      position: 'bottom',
      color: 'danger'
    });
    await toast.present();
    return;
  }

  todos.value.push({
    text: newTodo.value,
    completed: false
  });

  newTodo.value = '';

  const toast = await toastController.create({
    message: 'Tugas berhasil ditambahkan!',
    duration: 1500,
    position: 'bottom',
    color: 'success'
  });
  await toast.present();
};

const toggleTodo = (index: number) => {
  todos.value[index].completed = !todos.value[index].completed;
};

const deleteTodo = async (index: number) => {
  todos.value.splice(index, 1);

  const toast = await toastController.create({
    message: 'Tugas berhasil dihapus!',
    duration: 1500,
    position: 'bottom',
    color: 'warning'
  });
  await toast.present();
};
</script>

<style scoped>
.stat-card {
  text-align: center;
  padding: 10px;
}

.stat-number {
  font-size: 32px;
  font-weight: bold;
  margin-bottom: 5px;
}

.stat-label {
  font-size: 12px;
  text-transform: uppercase;
}

.completed {
  text-decoration: line-through;
  opacity: 0.6;
}

.empty-state {
  text-align: center;
  padding: 60px 20px;
}

.empty-state h2 {
  color: #999;
  margin-top: 20px;
}

.empty-state p {
  color: #ccc;
}
</style>
```

---

### Langkah 2: Tambahkan Route dan Link

```typescript
// router/index.ts
import TodoPage from '../views/TodoPage.vue';

{
  path: '/todo',
  name: 'Todo',
  component: TodoPage
}
```

Tambahkan button di HomePage:

```vue
<ion-button expand="block" router-link="/todo" color="success" style="margin-top: 10px;">
  Aplikasi To-Do List
</ion-button>
```

---

### Langkah 3: Test Aplikasi

1. Buka aplikasi di browser
2. Klik "Aplikasi To-Do List"
3. Coba fitur:
   - Tambah tugas baru
   - Centang tugas yang selesai
   - Geser ke kiri untuk hapus
   - Lihat statistik berubah

**Selamat! Anda sudah membuat aplikasi To-Do List yang fungsional!**

---

## 📝 LATIHAN MANDIRI

Untuk memperdalam pemahaman, kerjakan latihan berikut:

### Latihan 1: Modifikasi Aplikasi To-Do

1. Tambahkan fitur **prioritas** (Tinggi, Sedang, Rendah) untuk setiap tugas
2. Tambahkan **tanggal deadline** untuk tugas
3. Tambahkan **filter** untuk menampilkan:
   - Semua tugas
   - Tugas selesai
   - Tugas pending
4. Implementasikan **local storage** agar data tidak hilang saat reload

**Petunjuk:**
```typescript
// Untuk local storage
import { Storage } from '@ionic/storage';

// Simpan data
localStorage.setItem('todos', JSON.stringify(todos.value));

// Load data
const saved = localStorage.getItem('todos');
if (saved) {
  todos.value = JSON.parse(saved);
}
```

---

### Latihan 2: Buat Halaman Profil

Buat halaman profil dengan:
1. Avatar/foto profil
2. Informasi diri (Nama, NIM, Prodi, Email)
3. Form untuk edit profil
4. Menggunakan minimal 5 komponen Ionic yang berbeda

---

### Latihan 3: Eksplorasi Komponen

Coba komponen Ionic lainnya yang belum dibahas:
1. **IonFab** - Floating Action Button
2. **IonSegment** - Segmented Control
3. **IonRefresher** - Pull to Refresh
4. **IonInfiniteScroll** - Infinite Scrolling
5. **IonModal** - Modal Dialog

Dokumentasi: https://ionicframework.com/docs/components

---

## 🎯 RANGKUMAN

Pada praktikum ini, Anda telah mempelajari:

### 1. **Instalasi & Setup**
- ✅ Instalasi Node.js dan npm
- ✅ Instalasi Ionic CLI
- ✅ Instalasi VS Code dan extensions
- ✅ Membuat project Ionic dengan Vue

### 2. **Struktur Project**
- ✅ Memahami folder `src/`, `views/`, `router/`, `theme/`
- ✅ Memahami file `App.vue`, `main.ts`, `index.html`
- ✅ Cara kerja routing di Ionic

### 3. **Layout & Grid**
- ✅ Menggunakan `<ion-grid>`, `<ion-row>`, `<ion-col>`
- ✅ Responsive grid dengan size breakpoints
- ✅ Alignment dan offset

### 4. **Theme & Styling**
- ✅ CSS Variables untuk theming
- ✅ Mengubah warna utama aplikasi
- ✅ Membuat custom color
- ✅ Dark mode

### 5. **Komponen UI**
- ✅ List, Item, Card
- ✅ Button, Icon, Badge, Chip
- ✅ Input, Select, Datetime
- ✅ Alert, Toast, ActionSheet, Loading
- ✅ Checkbox, Toggle

### 6. **Praktik Aplikasi**
- ✅ Membuat aplikasi To-Do List
- ✅ State management dengan Vue ref & computed
- ✅ Event handling
- ✅ Conditional rendering

---

## 📚 REFERENSI

1. **Ionic Framework Documentation**
   - https://ionicframework.com/docs

2. **Vue.js Documentation**
   - https://vuejs.org/guide/

3. **Ionicons**
   - https://ionic.io/ionicons

4. **TypeScript Handbook**
   - https://www.typescriptlang.org/docs/handbook/intro.html

5. **Ionic Forum**
   - https://forum.ionicframework.com/

---

## ❓ TROUBLESHOOTING

### Masalah Umum:

**1. Error: ionic: command not found**
- Solusi: Install ulang Ionic CLI dengan `npm install -g @ionic/cli`

**2. Error: npm tidak ditemukan**
- Solusi: Install Node.js atau tambahkan ke PATH

**3. Port 8100 sudah digunakan**
- Solusi: Gunakan port lain dengan `ionic serve --port=8101`

**4. Import error untuk komponen**
- Solusi: Pastikan komponen sudah diimport dari `@ionic/vue`

**5. Style tidak muncul**
- Solusi: Periksa apakah tag `<style scoped>` sudah benar

---

## 🎓 EVALUASI DIRI

Jawab pertanyaan berikut untuk mengecek pemahaman Anda:

1. Apa perbedaan antara `ionic start` dengan template `blank`, `tabs`, dan `sidemenu`?
2. Bagaimana cara membuat grid dengan 3 kolom di mobile dan 6 kolom di desktop?
3. Komponen apa yang digunakan untuk membuat list yang bisa di-slide?
4. Bagaimana cara menambahkan icon di button?
5. Apa fungsi dari `router-link` di komponen button?
6. Bagaimana cara membuat custom color theme?
7. Apa perbedaan `IonContent` dengan `IonPage`?
8. Komponen apa yang digunakan untuk menampilkan notifikasi singkat?

---

## 📧 PENUTUP

Selamat! Anda telah menyelesaikan Praktikum 1 - Ionic Framework dengan Vue.js.

Pada pertemuan berikutnya, kita akan belajar:
- **Tuweb 1 (Pertemuan 10)**: Ionic pada Platform Android
- Build aplikasi menjadi APK
- Menggunakan Native API & Plugins
- Akses data dari REST API
- Deploy ke perangkat Android

**Terus berlatih dan jangan ragu untuk bereksperimen!**

---

**Disusun oleh:**
Anton Prafanto, S.Kom, M.T.
Dosen Program Studi Informatika
Universitas Mulawarman
Tutor Universitas Terbuka

**Mata Kuliah:** Pemrograman Berbasis Perangkat Bergerak (MSIM4401)
**Tahun:** 2025


---

# 🧑‍🏫 PENGAYAAN UNTUK SESI TUTORIAL PANJANG

Bagian ini disediakan khusus agar materi dapat digunakan untuk **live coding 3–4 jam**. Contoh dibuat bertahap: mulai dari konsep yang sangat kecil, lalu berkembang menjadi mini-aplikasi. Tutor dapat menjalankan contoh satu per satu dan meminta mahasiswa menebak hasil sebelum program dieksekusi.

## A. Peta Keterkaitan dengan Materi UT

| Fokus di Tuweb | Keterkaitan materi UT | Hal yang perlu ditekankan saat menjelaskan |
|---|---|---|
| Instalasi Ionic CLI | Aktivitas 6 | Perbedaan Node.js, npm, Ionic CLI, dan project Ionic |
| Ionic berbasis Vue | Aktivitas 7 | Hubungan Ionic sebagai UI framework dengan Vue sebagai framework reaktif |
| Struktur proyek | Aktivitas 8 | Peran App.vue, main.ts, router, views, components, theme |
| Starter Ionic | Aktivitas 9 | blank, tabs, sidemenu, list dan kapan masing-masing digunakan |
| Layout dan theme | Aktivitas 10 | single-page layout, responsive grid, CSS variables |
| Komponen UI | Aktivitas 11 | IonButton, IonList, IonItem, IonCard, Alert, event handler |

> **Poin narasi tutor:** jangan hanya menjelaskan “cara mengetik kode”. Jelaskan aliran program: browser menjalankan aplikasi → main.ts membuat aplikasi Vue → App.vue menjadi root component → router menentukan view → komponen Ionic merender UI.

---

## B. Demo 1 — Membandingkan Starter Ionic

Jalankan empat perintah berikut dan minta mahasiswa memperhatikan isi folder **src**.

~~~bash
ionic start demo-blank blank --type=vue
ionic start demo-tabs tabs --type=vue
ionic start demo-menu sidemenu --type=vue
ionic start demo-list list --type=vue
~~~

### Pertanyaan diskusi
1. Mengapa starter blank paling sederhana?
2. Mengapa tabs membutuhkan nested route?
3. Mengapa sidemenu biasanya membutuhkan IonSplitPane?
4. Starter mana yang cocok untuk aplikasi katalog?
5. Starter mana yang cocok untuk aplikasi dashboard mahasiswa?

### Jawaban inti
- **blank** cocok ketika arsitektur navigasi ingin ditentukan sendiri.
- **tabs** cocok untuk 3–5 area utama yang sering berpindah.
- **sidemenu** cocok jika menu relatif banyak.
- **list** cocok untuk aplikasi yang halaman pertamanya langsung berupa daftar data.

---

## C. Demo 2 — Halaman Ionic Minimum

Buat project:

~~~bash
ionic start demo-halaman blank --type=vue
cd demo-halaman
ionic serve
~~~

Ubah **src/views/HomePage.vue** menjadi:

~~~vue
<template>
  <ion-page>
    <ion-header>
      <ion-toolbar color="primary">
        <ion-title>Demo Pertemuan 6</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content class="ion-padding">
      <h2>Halo Ionic + Vue</h2>
      <p>Nilai counter: {{ counter }}</p>
      <ion-button @click="counter++">Tambah</ion-button>
      <ion-button color="medium" @click="counter = 0">Reset</ion-button>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
  IonButton
} from '@ionic/vue';

const counter = ref(0);
</script>
~~~

### Yang dapat dijelaskan cukup panjang
- **ref(0)** membuat reactive state.
- Pada template, Vue otomatis membaca nilai ref.
- **@click** adalah event binding.
- Komponen Ionic tetap mengikuti model komponen Vue.
- Warna **primary** dan **medium** berasal dari sistem theme Ionic.
- IonPage, IonHeader, IonToolbar, dan IonContent membentuk struktur halaman yang konsisten.

### Eksperimen
Ubah tombol tambah menjadi:

~~~vue
<ion-button @click="counter += 5">Tambah 5</ion-button>
~~~

Lalu tanyakan: *apakah kita perlu mengubah DOM secara manual?* Tidak. Vue akan melakukan re-render bagian yang berubah.

---

## D. Demo 3 — v-model, v-if, dan v-for dalam Satu Contoh

~~~vue
<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Daftar Mata Kuliah</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content class="ion-padding">
      <ion-item>
        <ion-input
          v-model="keyword"
          label="Cari"
          placeholder="Ketik nama mata kuliah">
        </ion-input>
      </ion-item>

      <ion-list v-if="filteredCourses.length > 0">
        <ion-item v-for="course in filteredCourses" :key="course.id">
          {{ course.name }}
        </ion-item>
      </ion-list>

      <ion-text color="medium" v-else>
        <p>Tidak ada data yang cocok.</p>
      </ion-text>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue';
import {
  IonPage, IonHeader, IonToolbar, IonTitle,
  IonContent, IonItem, IonInput, IonList, IonText
} from '@ionic/vue';

interface Course {
  id: number;
  name: string;
}

const keyword = ref('');

const courses = ref<Course[]>([
  { id: 1, name: 'Pemrograman Perangkat Bergerak' },
  { id: 2, name: 'Algoritma dan Pemrograman' },
  { id: 3, name: 'Sistem Terdistribusi' },
  { id: 4, name: 'Basis Data' }
]);

const filteredCourses = computed(() => {
  const q = keyword.value.toLowerCase();
  return courses.value.filter(item =>
    item.name.toLowerCase().includes(q)
  );
});
</script>
~~~

### Konsep untuk diterangkan
- **v-model** = two-way binding.
- **v-if / v-else** = conditional rendering.
- **v-for** = rendering list.
- **:key** membantu Vue melakukan update DOM secara efisien.
- **computed** cocok untuk data turunan; bukan tempat melakukan side effect.

---

## E. Demo 4 — Router: Home dan About

Buat **src/views/AboutPage.vue**:

~~~vue
<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-back-button default-href="/home"></ion-back-button>
        </ion-buttons>
        <ion-title>Tentang</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content class="ion-padding">
      Aplikasi demonstrasi MSIM4401.
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import {
  IonPage, IonHeader, IonToolbar, IonButtons,
  IonBackButton, IonTitle, IonContent
} from '@ionic/vue';
</script>
~~~

Tambahkan route:

~~~ts
{
  path: '/about',
  component: () => import('@/views/AboutPage.vue')
}
~~~

Tambahkan tombol dari Home:

~~~vue
<ion-button router-link="/about">Buka About</ion-button>
~~~

### Penjelasan
Router memisahkan **URL**, **komponen yang ditampilkan**, dan **cara berpindah halaman**. Ini menjadi fondasi untuk praktikum berikutnya saat route mempunyai parameter seperti **/user/:id**.

---

## F. Demo 5 — Responsive Grid

~~~vue
<ion-grid>
  <ion-row>
    <ion-col
      v-for="item in 8"
      :key="item"
      size="12"
      size-sm="6"
      size-md="4"
      size-lg="3">

      <ion-card>
        <ion-card-header>
          <ion-card-title>Card {{ item }}</ion-card-title>
        </ion-card-header>
        <ion-card-content>
          Responsive menggunakan breakpoint Ionic.
        </ion-card-content>
      </ion-card>
    </ion-col>
  </ion-row>
</ion-grid>
~~~

### Cara membaca size
- **size=12** → 1 kolom per baris di layar sempit.
- **size-sm=6** → 2 kolom.
- **size-md=4** → 3 kolom.
- **size-lg=3** → 4 kolom.

### Eksperimen kelas
Buka Chrome DevTools → Toggle Device Toolbar → ubah lebar layar dan amati perubahan jumlah card per baris.

---

## G. Demo 6 — Theme dengan CSS Variables

Di **src/theme/variables.css**:

~~~css
:root {
  --ion-color-primary: #1d4ed8;
  --ion-color-primary-rgb: 29, 78, 216;
  --ion-color-primary-contrast: #ffffff;

  --ion-background-color: #f8fafc;
  --ion-text-color: #0f172a;
}
~~~

Buat custom class:

~~~css
.hero-card {
  border-radius: 20px;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.08);
}
~~~

Gunakan:

~~~vue
<ion-card class="hero-card">
  <ion-card-header>
    <ion-card-title>Selamat Datang</ion-card-title>
  </ion-card-header>
</ion-card>
~~~

### Diskusi
Mengapa theme sebaiknya menggunakan variable global, bukan menulis warna berbeda-beda di setiap komponen? Karena konsistensi dan maintenance.

---

## H. Demo 7 — Props dan Emits: Komponen Reusable

Buat **src/components/ScoreCard.vue**:

~~~vue
<template>
  <ion-card>
    <ion-card-header>
      <ion-card-title>{{ title }}</ion-card-title>
    </ion-card-header>

    <ion-card-content>
      <h1>{{ score }}</h1>
      <ion-button size="small" @click="emit('increase')">
        Tambah
      </ion-button>
    </ion-card-content>
  </ion-card>
</template>

<script setup lang="ts">
import {
  IonCard, IonCardHeader, IonCardTitle,
  IonCardContent, IonButton
} from '@ionic/vue';

defineProps<{
  title: string;
  score: number;
}>();

const emit = defineEmits<{
  (event: 'increase'): void;
}>();
</script>
~~~

Gunakan pada page:

~~~vue
<ScoreCard
  title="Nilai Praktikum"
  :score="score"
  @increase="score++"
/>
~~~

### Konsep
- **props**: data parent → child.
- **emit**: event child → parent.
- Pola ini menghindari komponen besar yang menangani semuanya sendiri.

---

## I. Demo 8 — Event Handler + Alert Controller

~~~ts
import { alertController } from '@ionic/vue';

async function confirmDelete() {
  const alert = await alertController.create({
    header: 'Konfirmasi',
    message: 'Hapus data ini?',
    buttons: [
      { text: 'Batal', role: 'cancel' },
      {
        text: 'Hapus',
        role: 'destructive',
        handler: () => {
          console.log('Data dihapus');
        }
      }
    ]
  });

  await alert.present();
}
~~~

Tombol:

~~~vue
<ion-button color="danger" @click="confirmDelete">
  Hapus
</ion-button>
~~~

### Poin penting
Event di aplikasi mobile sering memicu komponen overlay: alert, modal, action sheet, toast. Karena proses presentasi overlay asynchronous, fungsi dibuat **async**.

---

## J. Demo 9 — Service untuk REST API

Pola service membantu memisahkan logika akses data dari tampilan.

**src/services/UserService.ts**

~~~ts
import axios from 'axios';

export interface User {
  id: number;
  name: string;
  email: string;
}

const api = axios.create({
  baseURL: 'https://jsonplaceholder.typicode.com',
  timeout: 5000
});

export async function getUsers(): Promise<User[]> {
  const response = await api.get<User[]>('/users');
  return response.data;
}
~~~

Page:

~~~ts
import { onMounted, ref } from 'vue';
import { getUsers, type User } from '@/services/UserService';

const users = ref<User[]>([]);
const loading = ref(false);
const errorMessage = ref('');

async function loadUsers() {
  loading.value = true;
  errorMessage.value = '';

  try {
    users.value = await getUsers();
  } catch (error) {
    errorMessage.value = 'Data tidak berhasil diambil.';
  } finally {
    loading.value = false;
  }
}

onMounted(loadUsers);
~~~

### Tiga state yang wajib dijelaskan
1. **Loading** — request sedang berjalan.
2. **Success** — data berhasil diterima.
3. **Error** — request gagal.

Ini lebih realistis dibanding hanya menampilkan data jika request sukses.

---

## K. Demo 10 — Mini To-Do Sederhana Tanpa Backend

~~~vue
<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Mini To-Do</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content class="ion-padding">
      <ion-item>
        <ion-input v-model="newTask" label="Tugas"></ion-input>
      </ion-item>

      <ion-button expand="block" @click="addTask">
        Tambah
      </ion-button>

      <ion-list>
        <ion-item v-for="task in tasks" :key="task.id">
          <ion-checkbox
            slot="start"
            v-model="task.done">
          </ion-checkbox>

          <ion-label :class="{ selesai: task.done }">
            {{ task.title }}
          </ion-label>

          <ion-button
            slot="end"
            fill="clear"
            color="danger"
            @click="removeTask(task.id)">
            Hapus
          </ion-button>
        </ion-item>
      </ion-list>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import {
  IonPage, IonHeader, IonToolbar, IonTitle, IonContent,
  IonItem, IonInput, IonButton, IonList, IonCheckbox, IonLabel
} from '@ionic/vue';

interface Task {
  id: number;
  title: string;
  done: boolean;
}

const newTask = ref('');
const tasks = ref<Task[]>([]);
let nextId = 1;

function addTask() {
  const title = newTask.value.trim();
  if (!title) return;

  tasks.value.push({
    id: nextId++,
    title,
    done: false
  });

  newTask.value = '';
}

function removeTask(id: number) {
  tasks.value = tasks.value.filter(task => task.id !== id);
}
</script>

<style scoped>
.selesai {
  text-decoration: line-through;
  opacity: 0.6;
}
</style>
~~~

### Pengembangan bertahap untuk memperpanjang praktikum
- Tambahkan filter Semua / Aktif / Selesai.
- Tambahkan priority.
- Tambahkan deadline.
- Tambahkan IonBadge.
- Tambahkan konfirmasi sebelum delete.
- Pisahkan item menjadi komponen TaskItem.vue.

---

# 🧠 PERTANYAAN DISKUSI + JAWABAN YANG DIHARAPKAN

1. **Apa beda Ionic dan Vue?**  
   Ionic menyediakan komponen UI dan runtime mobile; Vue mengelola state, reactivity, component lifecycle, dan rendering.

2. **Apa beda component dan view?**  
   Secara teknis keduanya komponen Vue. Dalam struktur project, view biasanya mewakili satu halaman/rute, sedangkan component bersifat reusable.

3. **Mengapa menggunakan router?**  
   Agar navigasi mempunyai struktur URL yang jelas dan setiap pola URL dapat dipetakan ke komponen tertentu.

4. **Mengapa data list membutuhkan key?**  
   Agar Vue dapat mengidentifikasi item secara stabil saat melakukan update DOM.

5. **Mengapa service layer berguna?**  
   Supaya logika HTTP tidak bercampur dengan UI dan dapat digunakan kembali.

6. **Apa keuntungan Ionic Grid?**  
   Memudahkan responsive layout dengan sistem baris, kolom, dan breakpoint.

---

# ⏱️ SKENARIO PENJELASAN 180 MENIT

| Durasi | Aktivitas |
|---|---|
| 0–20 menit | Konsep Ionic, Vue, TypeScript, Capacitor, struktur ekosistem |
| 20–40 menit | Instalasi/verifikasi CLI dan membandingkan starter |
| 40–65 menit | Struktur main.ts, App.vue, router, views, components |
| 65–90 menit | Live coding state, event, v-model, v-if, v-for |
| 90–115 menit | Router dan navigasi |
| 115–140 menit | Grid, theme, responsive UI |
| 140–165 menit | Reusable component + alert/event |
| 165–180 menit | REST service, tanya jawab, challenge |

---

# ✅ CHECKLIST AKHIR PERTEMUAN 6

Mahasiswa seharusnya sudah mampu menjelaskan dan mendemonstrasikan:

- [ ] ionic start dan ionic serve
- [ ] Perbedaan starter blank/tabs/sidemenu/list
- [ ] Peran main.ts, App.vue, router, views, components, theme
- [ ] Reactive state dengan ref
- [ ] Event handler
- [ ] v-model, v-if, v-for
- [ ] Navigasi menggunakan router
- [ ] Responsive grid
- [ ] CSS variables untuk theme
- [ ] Props dan emits
- [ ] Mengambil data REST API melalui service
- [ ] Membuat mini aplikasi yang dapat dijalankan

