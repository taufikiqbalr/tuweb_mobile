# MATERI TUWEB 2 - PERTEMUAN 10
# IONIC PADA PLATFORM ANDROID & APLIKASI TERINTEGRASI

> **Catatan penyusunan:** file final ini merupakan adaptasi dari **TUWEB_3.md** sesuai pemetaan pada README repository. Isi utama dipertahankan dan diperkaya dengan contoh siap-jalankan yang menghubungkan konsep UT tentang RESTful API, akses data, native API/plugins, Camera, Geolocation, proses build APK, serta debugging Android.

---

## 📋 INFORMASI MATA KULIAH

**Mata Kuliah**: Pemrograman Berbasis Perangkat Bergerak (MSIM4401)
**Pertemuan**: 10 (TUWEB 2)
**Pokok Bahasan**: Ionic pada Platform Android, Native API, Plugins, dan Aplikasi Terintegrasi
**Pendekatan**: Learning by Doing

---

## 🎯 TUJUAN PEMBELAJARAN

Setelah menyelesaikan praktikum ini, mahasiswa diharapkan mampu:

1. Memahami cara kerja Ionic pada platform Android
2. Melakukan instalasi dan konfigurasi Android development environment
3. Mengintegrasikan Native API dan Plugins ke dalam aplikasi Ionic
4. Mengakses data dari REST API eksternal
5. Membuild aplikasi Ionic menjadi file APK
6. Menjalankan aplikasi di perangkat Android nyata atau emulator
7. Memahami proses debugging aplikasi mobile
8. Membuat aplikasi terintegrasi dengan fitur native

---

## 📚 PRASYARAT

Sebelum memulai praktikum ini, pastikan Anda telah:

- ✅ Menyelesaikan Tuweb 1 (Pertemuan 6)
- ✅ Memahami dasar Ionic Framework dan Vue.js
- ✅ Memiliki komputer dengan spesifikasi:
  - RAM minimal 8GB (disarankan 16GB untuk emulator Android)
  - Storage kosong minimal 20GB
  - Sistem Operasi: Windows 10/11, macOS, atau Linux
- ✅ Koneksi internet yang stabil untuk download Android SDK

---

## 🚀 QUICK REFERENCE

> [!IMPORTANT]
> **Mengalami masalah saat mengikuti praktikum?** Kami menyediakan solusi!

### 📁 Working Code Sample (Ready to Use)

Kami telah menyediakan project lengkap yang **siap dijalankan** untuk membantu Anda:

```
📂 Lokasi: code-samples/tuweb02-weather-app/
```

**Cara menggunakan:**
```bash
cd code-samples/tuweb02-weather-app
npm install
npm run dev
```

### 📖 Dokumentasi Troubleshooting

- **Troubleshooting Section**: Lihat bagian "TROUBLESHOOTING COMMON ERRORS" di bawah (baris 1912+)
- **Dokumentasi Fix Lengkap**: `PERBAIKAN_TUWEB02.md` - Solusi untuk semua error umum

### ⚡ Langkah-Langkah Penting

1. **WAJIB**: Ikuti "Langkah 0: Setup Configuration Files" sebelum mulai coding
2. **WAJIB**: Setup `vite.config.ts` dengan alias `@/`
3. **WAJIB**: Install `@capacitor/android` sebelum `npx cap add android`

---

## 🛠️ PERSIAPAN LINGKUNGAN ANDROID

### Langkah 1: Instalasi Java Development Kit (JDK)

Android memerlukan JDK untuk proses build.

#### Untuk Windows:

1. **Download JDK**
   - Kunjungi: https://www.oracle.com/java/technologies/downloads/
   - Download **Java SE Development Kit 17** (versi LTS)
   - Pilih installer untuk Windows (contoh: `jdk-17_windows-x64_bin.exe`)

2. **Instalasi JDK**
   - Jalankan installer
   - Klik "Next"
   - Pilih lokasi instalasi (default: `C:\Program Files\Java\jdk-17\`)
   - Tunggu proses instalasi selesai
   - Klik "Close"

3. **Setting Environment Variable**

   **Langkah-langkah:**
   - Klik kanan "This PC" → Properties
   - Klik "Advanced system settings"
   - Klik tombol "Environment Variables"

   **Menambahkan JAVA_HOME:**
   - Di bagian "System variables", klik "New"
   - Variable name: `JAVA_HOME`
   - Variable value: `C:\Program Files\Java\jdk-17` (sesuaikan dengan lokasi instalasi)
   - Klik "OK"

   **Menambahkan ke PATH:**
   - Di "System variables", cari variable `Path`, klik "Edit"
   - Klik "New"
   - Tambahkan: `%JAVA_HOME%\bin`
   - Klik "OK" pada semua dialog

4. **Verifikasi Instalasi**
   ```bash
   java -version
   ```
   Output: `java version "17.0.x"`

   ```bash
   javac -version
   ```
   Output: `javac 17.0.x`

#### Untuk macOS:

```bash
# Menggunakan Homebrew
brew install openjdk@17

# Tambahkan ke PATH di ~/.zshrc atau ~/.bash_profile
echo 'export PATH="/usr/local/opt/openjdk@17/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc

# Verifikasi
java -version
```

#### Untuk Linux (Ubuntu/Debian):

```bash
sudo apt update
sudo apt install openjdk-17-jdk

# Verifikasi
java -version
javac -version
```

---

### Langkah 2: Instalasi Android Studio

Android Studio menyediakan Android SDK yang diperlukan untuk build aplikasi.

1. **Download Android Studio**
   - Kunjungi: https://developer.android.com/studio
   - Download versi terbaru untuk OS Anda
   - File berukuran sekitar 1-2 GB

2. **Instalasi Android Studio**

   **Windows:**
   - Jalankan file installer (contoh: `android-studio-2023.x.x.xx-windows.exe`)
   - Klik "Next" pada welcome screen
   - Pilih komponen yang akan diinstall (biarkan semua tercentang)
   - Pilih lokasi instalasi (default atau custom)
   - Klik "Install"
   - Tunggu proses instalasi (bisa 10-30 menit)
   - Centang "Start Android Studio"
   - Klik "Finish"

3. **Setup Wizard Android Studio**

   Setelah Android Studio terbuka:

   **a. Import Settings**
   - Pilih "Do not import settings" (jika install pertama kali)
   - Klik "OK"

   **b. Data Sharing**
   - Pilih "Don't send" atau "Send" (sesuai preferensi)
   - Klik "Next"

   **c. Install Type**
   - Pilih **"Standard"** (recommended untuk pemula)
   - Klik "Next"

   **d. Select UI Theme**
   - Pilih "Light" atau "Darcula" (sesuai selera)
   - Klik "Next"

   **e. Verify Settings**
   - Akan menampilkan komponen yang akan didownload:
     - Android SDK
     - Android SDK Platform
     - Android Virtual Device
   - Total download sekitar 3-5 GB
   - Klik "Next"

   **f. License Agreement**
   - Baca setiap license
   - Pilih "Accept" untuk semua
   - Klik "Finish"

   **g. Downloading Components**
   - Proses download dan instalasi akan berjalan
   - Bisa memakan waktu 30 menit - 2 jam (tergantung internet)
   - Tunggu hingga selesai

   **h. Finish**
   - Klik "Finish"
   - Android Studio siap digunakan!

4. **Instalasi SDK Tools Tambahan**

   Setelah setup selesai:
   - Klik "More Actions" → "SDK Manager"

   **SDK Platforms:**
   - Centang "Show Package Details" di pojok kanan bawah
   - Expand "Android 13.0 (Tiramisu)" atau versi terbaru
   - Centang:
     - ✅ Android SDK Platform 33
     - ✅ Google APIs Intel x86 Atom System Image
   - Klik "Apply" → "OK"

   **SDK Tools:**
   - Klik tab "SDK Tools"
   - Centang:
     - ✅ Android SDK Build-Tools
     - ✅ Android SDK Command-line Tools
     - ✅ Android Emulator
     - ✅ Android SDK Platform-Tools
     - ✅ Google Play services
   - Klik "Apply" → "OK"
   - Tunggu proses instalasi

5. **Cek Lokasi Android SDK**

   Di SDK Manager, lihat "Android SDK Location":
   - Windows: biasanya `C:\Users\[Username]\AppData\Local\Android\Sdk`
   - macOS: `/Users/[Username]/Library/Android/sdk`
   - Linux: `/home/[Username]/Android/Sdk`

   **Catat path ini, akan digunakan nanti!**

---

### Langkah 3: Setting Environment Variable untuk Android

#### Windows:

1. **Buka Environment Variables** (seperti langkah JDK)

2. **Tambahkan ANDROID_HOME**
   - Variable name: `ANDROID_HOME`
   - Variable value: `C:\Users\[Username]\AppData\Local\Android\Sdk`
   - Ganti `[Username]` dengan username Windows Anda
   - Klik "OK"

3. **Update PATH**
   - Edit variable `Path`
   - Tambahkan:
     - `%ANDROID_HOME%\platform-tools`
     - `%ANDROID_HOME%\emulator`
     - `%ANDROID_HOME%\tools`
     - `%ANDROID_HOME%\tools\bin`

4. **Restart Command Prompt**

5. **Verifikasi**
   ```bash
   adb --version
   ```
   Seharusnya muncul versi adb (Android Debug Bridge)

#### macOS/Linux:

Tambahkan di `~/.zshrc` atau `~/.bash_profile`:

```bash
export ANDROID_HOME=$HOME/Library/Android/sdk  # macOS
# atau
export ANDROID_HOME=$HOME/Android/Sdk  # Linux

export PATH=$PATH:$ANDROID_HOME/platform-tools
export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/tools
export PATH=$PATH:$ANDROID_HOME/tools/bin
```

Reload:
```bash
source ~/.zshrc  # atau source ~/.bash_profile
```

Verifikasi:
```bash
adb --version
```

---

### Langkah 4: Instalasi Gradle (Opsional, biasanya sudah include)

Gradle adalah build tool untuk Android.

**Cek apakah sudah terinstall:**
```bash
gradle --version
```

Jika belum, install:

**Windows:**
- Download dari: https://gradle.org/releases/
- Extract ke folder (contoh: `C:\Gradle`)
- Tambahkan `C:\Gradle\bin` ke PATH

**macOS:**
```bash
brew install gradle
```

**Linux:**
```bash
sudo apt install gradle
```

---

## 📱 MEMBUAT EMULATOR ANDROID

Emulator diperlukan untuk testing aplikasi tanpa perangkat fisik.

### Langkah 1: Membuat AVD (Android Virtual Device)

1. **Buka Android Studio**

2. **Akses AVD Manager**
   - Klik "More Actions" → "Virtual Device Manager"
   - Atau dari menu: Tools → Device Manager

3. **Create Virtual Device**
   - Klik tombol "Create Device"

4. **Pilih Hardware**
   - Category: Phone
   - Pilih device: **Pixel 5** (recommended)
   - Klik "Next"

5. **Pilih System Image**
   - Tab "Recommended"
   - Pilih: **Tiramisu (API 33)** atau versi terbaru
   - Jika ada tombol "Download", klik untuk download image (sekitar 1-2 GB)
   - Tunggu download selesai
   - Klik "Next"

6. **Verify Configuration**
   - AVD Name: biarkan default atau ganti (contoh: `Pixel_5_API_33`)
   - Startup orientation: Portrait
   - **Advanced Settings:**
     - RAM: 2048 MB atau lebih (jika RAM komputer cukup)
     - Internal Storage: 2048 MB
     - SD card: 512 MB
   - Klik "Finish"

7. **Jalankan Emulator (Test)**
   - Di AVD Manager, klik tombol ▶️ (Play) pada device yang baru dibuat
   - Tunggu emulator booting (pertama kali bisa 3-5 menit)
   - Jika berhasil, akan muncul layar Android

**Tips:**
- Jangan tutup emulator setelah dibuka, biarkan berjalan selama development
- Gunakan "Cold Boot" untuk booting penuh, "Quick Boot" untuk lebih cepat

---

## 🚀 PRAKTIKUM 1: BUILD APLIKASI IONIC KE ANDROID

> [!WARNING]
> **PERHATIAN - Baca Ini Sebelum Mulai!**
>
> Praktikum ini memiliki beberapa **langkah konfigurasi CRITICAL** yang WAJIB dilakukan. Jika dilewati, aplikasi **tidak akan jalan** dan akan muncul error seperti:
> - `Cannot find module '@/services/weatherService'`
> - `Failed to resolve import`
> - `Could not find the android platform`
>
> **✅ SOLUSI**: Pastikan Anda mengikuti **"Langkah 0: Setup Configuration Files"** dengan teliti!

> [!TIP]
> **Working Code Sample Tersedia!**
>
> Jika mengalami masalah, kami menyediakan **project lengkap yang siap dijalankan**:
>
> 📁 **Lokasi**: `code-samples/tuweb02-weather-app/`
>
> **Cara menggunakan**:
> ```bash
> cd code-samples/tuweb02-weather-app
> npm install
> npm run dev
> ```
>
> 📖 **Dokumentasi Lengkap**: `PERBAIKAN_TUWEB02.md`

---

### Persiapan

Kita akan menggunakan project dari Tuweb 1. Jika belum punya, buat project baru:

```bash
ionic start myApp tabs --type=vue
cd myApp
```

---

> [!CAUTION]
> **🔴 LANGKAH 0 ADALAH CRITICAL - JANGAN DILEWATI!**
>
> Langkah berikut adalah **WAJIB** dan **HARUS** dilakukan sebelum coding. Jika Anda skip langkah ini, **aplikasi tidak akan jalan** dan akan muncul error import module.
>
> Langkah 0 ini mengatasi masalah utama yang sering dialami mahasiswa:
> - ❌ Error: `Cannot find module '@/services/weatherService'`
> - ❌ Error: `Failed to resolve import`
> - ❌ TypeScript errors tentang path
>
> **Pastikan Anda membaca dan mengikuti SEMUA instruksi di Langkah 0!**

### Langkah 0: Setup Configuration Files

**PENTING**: Sebelum melanjutkan, Anda perlu setup beberapa file konfigurasi untuk menghindari error.

#### 1. Buat/Update `vite.config.ts`

File ini diperlukan agar import path `@/` berfungsi.

Buat atau edit file `vite.config.ts` di root project:

```typescript
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import { fileURLToPath, URL } from 'node:url'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [vue()],
  resolve: {
    alias: {
      '@': fileURLToPath(new URL('./src', import.meta.url))
    }
  }
})
```

**Penjelasan**:
- `alias: { '@': ... }` - Membuat shortcut `@/` untuk folder `src/`
- Tanpa ini, import `from '@/services/...'` akan error

#### 2. Update `tsconfig.json`

Tambahkan path mapping di `tsconfig.json`:

```json
{
  "compilerOptions": {
    // ... konfigurasi lain ...
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  }
}
```

**Penjelasan**:
- Memberi tahu TypeScript tentang alias `@/`
- Diperlukan agar tidak ada error TypeScript

#### 3. Buat `capacitor.config.ts`

Buat file `capacitor.config.ts` di root project:

```typescript
import { CapacitorConfig } from '@capacitor/cli';

const config: CapacitorConfig = {
  appId: 'id.ac.ut.myapp',
  appName: 'My App',
  webDir: 'dist',
  server: {
    androidScheme: 'https'
  }
};

export default config;
```

**Penjelasan**:
- `appId` - Unique identifier untuk app (ganti sesuai kebutuhan)
- `webDir` - Folder hasil build (biasanya `dist`)

**⚠️ CATATAN**: Jika Anda skip langkah ini, akan muncul error import module!

---

### Langkah 1: Menambahkan Platform Android

1. **Tambahkan Capacitor ke project**

   Capacitor adalah tool untuk membuild aplikasi web menjadi native mobile app.

   ```bash
   ionic integrations enable capacitor
   ```

   Atau jika sudah ada, skip langkah ini.

2. **Build project untuk production**

   ```bash
   ionic build
   ```

   **Penjelasan:**
   - Perintah ini akan mengkompilasi kode Vue/TypeScript menjadi HTML/CSS/JS
   - Hasil build ada di folder `dist/`
   - File-file ini yang akan di-package menjadi APK

   **Output:**
   ```
   ✔ Building...
   ✔ Copying web assets from dist to android/app/src/main/assets/public in 123 ms
   ```

3. **Install package Android Capacitor**

   **⚠️ PENTING - Langkah ini HARUS dilakukan terlebih dahulu!**

   Sebelum menambahkan platform Android, install package yang diperlukan:

   ```bash
   npm install @capacitor/android
   ```

   **Penjelasan:**
   - Package `@capacitor/android` diperlukan untuk menambahkan platform Android
   - Jika dilewati, akan muncul error: `Could not find the android platform`
   
   **Troubleshooting:**
   
   Jika Anda mendapat error seperti ini:
   ```
   [error] Could not find the android platform.
           You must install it in your project first, e.g. w/ npm install @capacitor/android
   ```
   
   Artinya Anda lupa menjalankan `npm install @capacitor/android` terlebih dahulu.

4. **Tambahkan platform Android**

   Setelah package terinstall, tambahkan platform Android:

   ```bash
   npx cap add android
   ```

   **Penjelasan:**
   - `npx cap`: menjalankan Capacitor CLI
   - `add android`: menambahkan platform Android ke project
   - Akan membuat folder `android/` di project

   **Output:**
   ```
   ✔ Adding native android project in android in 45.32ms
   ✔ add in 45.45ms
   ✔ Copying web assets from dist to android/app/src/main/assets/public in 123.45ms
   ✔ Creating capacitor.config.json in 2.34ms
   ✔ copy android in 125.79ms
   ✔ Updating Android plugins in 4.56ms
   ✔ update android in 234.56ms
   ```

5. **Sync project dengan platform**

   Setiap kali ada perubahan di kode web, jalankan:
   ```bash
   npx cap sync
   ```

   **Penjelasan:**
   - Menyalin file web (dist/) ke folder android
   - Mengupdate plugin Capacitor
   - Memastikan kode web dan native sinkron

---

### Langkah 2: Membuka Project di Android Studio

1. **Buka project Android**

   ```bash
   npx cap open android
   ```

   Atau manual:
   - Buka Android Studio
   - File → Open
   - Pilih folder `android/` di dalam project Ionic Anda

2. **Gradle Sync**

   Android Studio akan otomatis melakukan Gradle Sync:
   - Mendownload dependencies
   - Mengkonfigurasi project
   - Proses ini bisa 2-10 menit (pertama kali)

   Jika ada error, klik "Try Again" atau "Sync Project with Gradle Files"

   **⚠️ Troubleshooting: AGP Version Incompatibility**

   Jika Anda mendapat error seperti ini:
   ```
   The project is using an incompatible version (AGP 8.7.2) of the Android Gradle plugin. 
   Latest supported version is AGP 8.5.1
   ```

   **Solusi:**

   1. Buka file `android/build.gradle` (bukan `android/app/build.gradle`)
   
   2. Cari baris yang berisi `com.android.tools.build:gradle`, contoh:
      ```gradle
      classpath 'com.android.tools.build:gradle:8.7.2'
      ```
   
   3. Ubah versi menjadi `8.5.1` atau versi yang kompatibel:
      ```gradle
      classpath 'com.android.tools.build:gradle:8.5.1'
      ```
   
   4. Klik "Sync Now" atau File → Sync Project with Gradle Files
   
   5. Tunggu proses sync selesai

   **Penjelasan:**
   - AGP (Android Gradle Plugin) adalah tool untuk build aplikasi Android
   - Setiap versi Android Studio hanya support AGP versi tertentu
   - Capacitor kadang generate project dengan AGP versi terbaru yang belum support di Android Studio Anda
   - Solusinya menurunkan versi AGP ke versi yang kompatibel

3. **Struktur Project Android**

   Di panel kiri, Anda akan melihat:
   ```
   android/
   ├── app/
   │   ├── src/
   │   │   └── main/
   │   │       ├── assets/
   │   │       │   └── public/  # File web Ionic
   │   │       ├── java/
   │   │       ├── res/          # Resources (icon, splash screen)
   │   │       └── AndroidManifest.xml
   │   └── build.gradle
   ├── build.gradle
   └── gradle/
   ```

---

### Langkah 3: Menjalankan di Emulator

1. **Pastikan emulator sudah berjalan**
   - Buka AVD Manager
   - Jalankan emulator yang sudah dibuat
   - Tunggu hingga home screen Android muncul

2. **Pilih device target**
   - Di toolbar Android Studio, akan ada dropdown device
   - Pilih emulator yang sedang berjalan (contoh: `Pixel 5 API 33`)

3. **Run aplikasi**
   - Klik tombol ▶️ (Run) di toolbar
   - Atau: Run → Run 'app'
   - Atau: `Shift + F10`

4. **Proses Build**
   - Gradle akan build project
   - Progress ada di panel "Build" di bawah
   - Proses pertama kali bisa 3-10 menit

   **⚠️ Troubleshooting: Java Version Mismatch**

   Jika Anda mendapat error seperti ini:
   ```
   error: invalid source release: 21
   ```

   **Penyebab:**
   - Project Android memerlukan Java 21, tapi JDK Anda versi 17 (atau sebaliknya)
   - Ini umum terjadi karena Capacitor generate project dengan Java version terbaru

   **Solusi (Recommended - Ubah ke Java 17):**

   1. Buka file `android/app/build.gradle`
   
   2. Cari bagian `compileOptions` dan `kotlinOptions`:
      ```gradle
      android {
          ...
          compileOptions {
              sourceCompatibility JavaVersion.VERSION_21
              targetCompatibility JavaVersion.VERSION_21
          }
          kotlinOptions {
              jvmTarget = '21'
          }
      }
      ```
   
   3. Ubah semua versi Java menjadi `17`:
      ```gradle
      android {
          ...
          compileOptions {
              sourceCompatibility JavaVersion.VERSION_17
              targetCompatibility JavaVersion.VERSION_17
          }
          kotlinOptions {
              jvmTarget = '17'
          }
      }
      ```
   
   4. Klik "Sync Now" atau File → Sync Project with Gradle Files
   
   5. Coba Run aplikasi lagi

   **Solusi Alternatif (Install JDK 21):**
   
   Jika ingin menggunakan Java 21:
   - Download JDK 21 dari https://www.oracle.com/java/technologies/downloads/
   - Install dan update `JAVA_HOME` environment variable
   - Restart Android Studio

   **Penjelasan:**
   - JDK 17 sudah cukup untuk development Android modern
   - Mengubah konfigurasi project lebih cepat daripada install JDK baru
   - Error ini terjadi karena mismatch antara JDK sistem dan requirement project

5. **Aplikasi terbuka di emulator**
   - Jika berhasil, aplikasi akan otomatis install dan buka di emulator
   - Anda akan melihat aplikasi Ionic berjalan seperti aplikasi Android asli!

**Selamat! Aplikasi Ionic Anda sudah berjalan di Android!**

---

### Langkah 4: Build APK untuk Distribusi

Untuk membuat file APK yang bisa diinstall di perangkat manapun:

1. **Build → Build Bundle(s) / APK(s) → Build APK(s)**

2. **Tunggu proses build**
   - Progress di panel "Build"
   - Jika sukses, akan muncul notifikasi: "APK(s) generated successfully"

3. **Locate APK**
   - Klik "locate" pada notifikasi
   - Atau manual: `android/app/build/outputs/apk/debug/app-debug.apk`

4. **Install APK**
   - Copy file APK ke perangkat Android
   - Buka file APK di perangkat
   - Klik "Install"
   - (Mungkin perlu enable "Install from Unknown Sources")

**Catatan:**
- APK debug hanya untuk testing
- Untuk production, gunakan signed release APK

---

## 🔌 PRAKTIKUM 2: NATIVE API & PLUGINS

### Pengantar

Capacitor Plugins memungkinkan aplikasi Ionic mengakses fitur native perangkat seperti kamera, geolocation, storage, dll.

---

### Langkah 1: Menggunakan Plugin Geolocation

Mari kita buat fitur untuk mendapatkan lokasi pengguna.

1. **Install Plugin**

   ```bash
   npm install @capacitor/geolocation
   npx cap sync
   ```

2. **Buat halaman Location**

   Buat file `src/views/LocationPage.vue`:

```vue
<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-back-button default-href="/home"></ion-back-button>
        </ion-buttons>
        <ion-title>Geolocation</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content class="ion-padding">
      <h2>Lokasi Saya</h2>

      <ion-card v-if="location">
        <ion-card-header>
          <ion-card-title>Koordinat</ion-card-title>
        </ion-card-header>
        <ion-card-content>
          <p><strong>Latitude:</strong> {{ location.latitude }}</p>
          <p><strong>Longitude:</strong> {{ location.longitude }}</p>
          <p><strong>Akurasi:</strong> {{ location.accuracy }} meter</p>
          <p><strong>Waktu:</strong> {{ locationTime }}</p>
        </ion-card-content>
      </ion-card>

      <ion-button expand="block" @click="getCurrentLocation" :disabled="loading">
        <ion-icon :icon="locateOutline" slot="start"></ion-icon>
        {{ loading ? 'Mengambil Lokasi...' : 'Dapatkan Lokasi' }}
      </ion-button>

      <ion-card v-if="error" color="danger">
        <ion-card-content>
          <strong>Error:</strong> {{ error }}
        </ion-card-content>
      </ion-card>

      <!-- Google Maps (iframe) -->
      <ion-card v-if="location">
        <ion-card-header>
          <ion-card-title>Peta</ion-card-title>
        </ion-card-header>
        <ion-card-content>
          <iframe
            :src="`https://maps.google.com/maps?q=${location.latitude},${location.longitude}&z=15&output=embed`"
            width="100%"
            height="300"
            style="border:0;"
            loading="lazy"
          ></iframe>
        </ion-card-content>
      </ion-card>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { Geolocation } from '@capacitor/geolocation';
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
  IonButtons,
  IonBackButton,
  IonCard,
  IonCardHeader,
  IonCardTitle,
  IonCardContent,
  IonButton,
  IonIcon
} from '@ionic/vue';
import { locateOutline } from 'ionicons/icons';

interface LocationData {
  latitude: number;
  longitude: number;
  accuracy: number;
}

const location = ref<LocationData | null>(null);
const locationTime = ref('');
const loading = ref(false);
const error = ref('');

const getCurrentLocation = async () => {
  loading.value = true;
  error.value = '';

  try {
    // Request permission
    const permission = await Geolocation.requestPermissions();

    if (permission.location === 'granted') {
      // Get current position
      const coordinates = await Geolocation.getCurrentPosition({
        enableHighAccuracy: true,
        timeout: 10000
      });

      location.value = {
        latitude: coordinates.coords.latitude,
        longitude: coordinates.coords.longitude,
        accuracy: coordinates.coords.accuracy
      };

      locationTime.value = new Date().toLocaleString('id-ID');
    } else {
      error.value = 'Izin lokasi ditolak. Harap aktifkan di pengaturan.';
    }
  } catch (err: any) {
    error.value = `Gagal mendapatkan lokasi: ${err.message}`;
    console.error('Error getting location:', err);
  } finally {
    loading.value = false;
  }
};
</script>

<style scoped>
h2 {
  margin-bottom: 20px;
}

ion-card p {
  margin: 8px 0;
}

iframe {
  border-radius: 8px;
}
</style>
```

3. **Tambahkan route**

```typescript
// router/index.ts
import LocationPage from '../views/LocationPage.vue';

{
  path: '/location',
  name: 'Location',
  component: LocationPage
}
```

4. **Tambahkan permission di AndroidManifest.xml**

   File: `android/app/src/main/AndroidManifest.xml`

   Tambahkan sebelum tag `<application>`:

```xml
<!-- Geolocation Permissions -->
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
```

5. **Sync dan Run**

```bash
npx cap sync
npx cap open android
```

6. **Test di emulator**
   - Di emulator, buka menu Extended Controls (ikon "...")
   - Pilih "Location"
   - Set lokasi manual atau gunakan GPX file
   - Klik tombol "Dapatkan Lokasi" di app

---

### Langkah 2: Menggunakan Plugin Camera

Mari buat fitur ambil foto.

1. **Install Plugin**

```bash
npm install @capacitor/camera
npx cap sync
```

2. **Buat halaman Camera**

   File: `src/views/CameraPage.vue`

```vue
<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-back-button default-href="/home"></ion-back-button>
        </ion-buttons>
        <ion-title>Camera</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content class="ion-padding">
      <h2>Ambil Foto</h2>

      <ion-card v-if="photo">
        <img :src="photo" alt="Foto" />
        <ion-card-content>
          <p>Foto berhasil diambil!</p>
        </ion-card-content>
      </ion-card>

      <div v-else class="placeholder">
        <ion-icon :icon="cameraOutline" style="font-size: 80px; color: #ccc;"></ion-icon>
        <p>Belum ada foto</p>
      </div>

      <ion-button expand="block" @click="takePicture">
        <ion-icon :icon="cameraOutline" slot="start"></ion-icon>
        Ambil Foto
      </ion-button>

      <ion-button expand="block" fill="outline" @click="selectFromGallery">
        <ion-icon :icon="imagesOutline" slot="start"></ion-icon>
        Pilih dari Galeri
      </ion-button>

      <ion-button
        v-if="photo"
        expand="block"
        color="danger"
        fill="clear"
        @click="deletePhoto"
      >
        Hapus Foto
      </ion-button>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { Camera, CameraResultType, CameraSource } from '@capacitor/camera';
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
  IonButtons,
  IonBackButton,
  IonCard,
  IonCardContent,
  IonButton,
  IonIcon
} from '@ionic/vue';
import { cameraOutline, imagesOutline } from 'ionicons/icons';

const photo = ref<string | null>(null);

const takePicture = async () => {
  try {
    const image = await Camera.getPhoto({
      quality: 90,
      allowEditing: false,
      resultType: CameraResultType.DataUrl,
      source: CameraSource.Camera
    });

    photo.value = image.dataUrl || null;
  } catch (error) {
    console.error('Error taking photo:', error);
  }
};

const selectFromGallery = async () => {
  try {
    const image = await Camera.getPhoto({
      quality: 90,
      allowEditing: false,
      resultType: CameraResultType.DataUrl,
      source: CameraSource.Photos
    });

    photo.value = image.dataUrl || null;
  } catch (error) {
    console.error('Error selecting photo:', error);
  }
};

const deletePhoto = () => {
  photo.value = null;
};
</script>

<style scoped>
.placeholder {
  text-align: center;
  padding: 60px 20px;
  background: #f5f5f5;
  border-radius: 8px;
  margin-bottom: 20px;
}

.placeholder p {
  color: #999;
  margin-top: 10px;
}

ion-card img {
  width: 100%;
  height: auto;
}

h2 {
  margin-bottom: 20px;
}
</style>
```

3. **Tambahkan permission di AndroidManifest.xml**

```xml
<!-- Camera Permissions -->
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
```

4. **Tambahkan route dan test!**

---

### Langkah 3: Storage (Menyimpan Data Lokal)

1. **Install Plugin**

```bash
npm install @capacitor/preferences
npx cap sync
```

2. **Contoh penggunaan:**

```typescript
import { Preferences } from '@capacitor/preferences';

// Simpan data
await Preferences.set({
  key: 'name',
  value: 'Anton Prafanto'
});

// Ambil data
const { value } = await Preferences.get({ key: 'name' });
console.log('Name:', value);

// Hapus data
await Preferences.remove({ key: 'name' });

// Hapus semua
await Preferences.clear();
```

3. **Implementasi di aplikasi To-Do**

   Edit `TodoPage.vue` dari Tuweb 1, tambahkan storage:

```typescript
import { Preferences } from '@capacitor/preferences';
import { onMounted } from 'vue';

// Load data saat component mounted
onMounted(async () => {
  const { value } = await Preferences.get({ key: 'todos' });
  if (value) {
    todos.value = JSON.parse(value);
  }
});

// Simpan setiap kali ada perubahan
const saveTodos = async () => {
  await Preferences.set({
    key: 'todos',
    value: JSON.stringify(todos.value)
  });
};

// Update method addTodo, toggleTodo, deleteTodo untuk memanggil saveTodos()
```

---

## 🌐 PRAKTIKUM 3: AKSES DATA DARI REST API

### Studi Kasus: Aplikasi Info Cuaca

Mari buat aplikasi yang mengambil data cuaca dari API.

---

### Langkah 1: Instalasi HTTP Client

```bash
npm install axios
```

---

### Langkah 2: Membuat Service API

> [!WARNING]
> **Prerequisite Check - Wajib Dilakukan Dulu!**
>
> Sebelum melanjutkan, pastikan Anda sudah menyelesaikan **Langkah 0** dari Praktikum 1:
>
> - ✅ File `vite.config.ts` sudah ada dengan alias `@/`
> - ✅ File `tsconfig.json` sudah ada dengan path mapping
> - ✅ File `capacitor.config.ts` sudah dibuat
>
> **Jika belum**, kembali ke **Praktikum 1 → Langkah 0** dan selesaikan setup tersebut terlebih dahulu!
>
> **Kenapa penting?** Code di bawah ini menggunakan import `@/services/weatherService` yang **tidak akan bekerja** tanpa konfigurasi alias.

> [!TIP]
> **Mengalami error module not found?**
>
> Gunakan working code sample sebagai reference:
> ```bash
> cd code-samples/tuweb02-weather-app
> code .
> ```
> Bandingkan file konfigurasi Anda dengan working sample.

#### 1. Buat folder services

```bash
mkdir src/services
```

#### 2. Buat file weatherService.ts

Buat file baru: `src/services/weatherService.ts`

```typescript
import axios from 'axios';

const API_BASE_URL = 'https://api.open-meteo.com/v1';

export interface WeatherData {
  time: string[];
  temperature_2m: number[];
}

export interface WeatherResponse {
  latitude: number;
  longitude: number;
  hourly: WeatherData;
}

export const weatherService = {
  /**
   * Mendapatkan data cuaca berdasarkan koordinat
   */
  async getWeather(latitude: number, longitude: number): Promise<WeatherResponse> {
    try {
      const response = await axios.get(`${API_BASE_URL}/forecast`, {
        params: {
          latitude,
          longitude,
          hourly: 'temperature_2m,relative_humidity_2m,precipitation,weather_code',
          timezone: 'Asia/Jakarta'
        }
      });

      return response.data;
    } catch (error) {
      console.error('Error fetching weather:', error);
      throw error;
    }
  },

  /**
   * Mendapatkan cuaca kota tertentu (preset)
   */
  async getWeatherByCity(city: string): Promise<WeatherResponse> {
    const cities: { [key: string]: { lat: number; lon: number } } = {
      'jakarta': { lat: -6.2, lon: 106.8 },
      'samarinda': { lat: -0.5, lon: 117.15 },
      'balikpapan': { lat: -1.24, lon: 116.89 },
      'surabaya': { lat: -7.25, lon: 112.75 },
      'bandung': { lat: -6.9, lon: 107.6 },
    };

    const coords = cities[city.toLowerCase()];
    if (!coords) {
      throw new Error('Kota tidak ditemukan');
    }

    return this.getWeather(coords.lat, coords.lon);
  }
};
```

---

### Langkah 3: Membuat Halaman Weather

File: `src/views/WeatherPage.vue`

```vue
<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-back-button default-href="/home"></ion-back-button>
        </ion-buttons>
        <ion-title>Info Cuaca</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content>
      <!-- City Selector -->
      <div class="ion-padding">
        <ion-item>
          <ion-label>Pilih Kota</ion-label>
          <ion-select v-model="selectedCity" @ionChange="loadWeather">
            <ion-select-option value="jakarta">Jakarta</ion-select-option>
            <ion-select-option value="samarinda">Samarinda</ion-select-option>
            <ion-select-option value="balikpapan">Balikpapan</ion-select-option>
            <ion-select-option value="surabaya">Surabaya</ion-select-option>
            <ion-select-option value="bandung">Bandung</ion-select-option>
          </ion-select>
        </ion-item>
      </div>

      <!-- Loading -->
      <div v-if="loading" class="ion-padding ion-text-center">
        <ion-spinner></ion-spinner>
        <p>Memuat data cuaca...</p>
      </div>

      <!-- Error -->
      <ion-card v-if="error" color="danger">
        <ion-card-content>
          <strong>Error:</strong> {{ error }}
        </ion-card-content>
      </ion-card>

      <!-- Weather Data -->
      <div v-if="weatherData && !loading">
        <!-- Current Weather -->
        <ion-card>
          <ion-card-header>
            <ion-card-subtitle>Cuaca Saat Ini</ion-card-subtitle>
            <ion-card-title style="text-transform: capitalize;">
              {{ selectedCity }}
            </ion-card-title>
          </ion-card-header>
          <ion-card-content>
            <div class="current-temp">
              <ion-icon :icon="sunnyOutline" style="font-size: 48px; color: #FFA500;"></ion-icon>
              <h1>{{ currentTemp }}°C</h1>
            </div>
            <p><strong>Koordinat:</strong> {{ weatherData.latitude }}°, {{ weatherData.longitude }}°</p>
          </ion-card-content>
        </ion-card>

        <!-- Hourly Forecast -->
        <div class="ion-padding">
          <h3>Prakiraan Per Jam</h3>
          <ion-card v-for="(item, index) in hourlyForecast" :key="index">
            <ion-card-content>
              <ion-grid>
                <ion-row class="ion-align-items-center">
                  <ion-col size="6">
                    <strong>{{ formatTime(item.time) }}</strong>
                  </ion-col>
                  <ion-col size="6" class="ion-text-right">
                    <span style="font-size: 20px; font-weight: bold;">
                      {{ item.temp }}°C
                    </span>
                  </ion-col>
                </ion-row>
              </ion-grid>
            </ion-card-content>
          </ion-card>
        </div>
      </div>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue';
import { weatherService, WeatherResponse } from '@/services/weatherService';
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
  IonSelect,
  IonSelectOption,
  IonCard,
  IonCardHeader,
  IonCardSubtitle,
  IonCardTitle,
  IonCardContent,
  IonSpinner,
  IonIcon,
  IonGrid,
  IonRow,
  IonCol
} from '@ionic/vue';
import { sunnyOutline } from 'ionicons/icons';

const selectedCity = ref('samarinda');
const weatherData = ref<WeatherResponse | null>(null);
const loading = ref(false);
const error = ref('');

const currentTemp = computed(() => {
  if (!weatherData.value) return 0;
  return weatherData.value.hourly.temperature_2m[0].toFixed(1);
});

const hourlyForecast = computed(() => {
  if (!weatherData.value) return [];

  // Ambil 12 jam pertama
  return weatherData.value.hourly.time.slice(0, 12).map((time, index) => ({
    time,
    temp: weatherData.value!.hourly.temperature_2m[index].toFixed(1)
  }));
});

const formatTime = (timeStr: string) => {
  const date = new Date(timeStr);
  return date.toLocaleString('id-ID', {
    day: 'numeric',
    month: 'short',
    hour: '2-digit',
    minute: '2-digit'
  });
};

const loadWeather = async () => {
  loading.value = true;
  error.value = '';

  try {
    weatherData.value = await weatherService.getWeatherByCity(selectedCity.value);
  } catch (err: any) {
    error.value = err.message || 'Gagal memuat data cuaca';
    console.error('Error loading weather:', err);
  } finally {
    loading.value = false;
  }
};

// Load initial data
loadWeather();
</script>

<style scoped>
.current-temp {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 20px;
  margin: 20px 0;
}

.current-temp h1 {
  font-size: 48px;
  margin: 0;
  font-weight: bold;
}

h3 {
  margin-bottom: 15px;
  color: #333;
}

ion-card {
  margin: 10px 0;
}
</style>
```

---

### Langkah 4: Tambahkan Route dan Test

1. **Tambahkan route**

2. **Build dan run di Android**

```bash
ionic build
npx cap sync
npx cap open android
```

3. **Test aplikasi:**
   - Pilih kota
   - Lihat data cuaca muncul
   - Data diambil dari API real-time!

---

## 🎨 PRAKTIKUM 4: APLIKASI TERINTEGRASI LENGKAP

### Studi Kasus: Aplikasi "My Daily"

Kita akan membuat aplikasi yang menggabungkan semua fitur:
- To-Do List dengan Storage
- Weather Info dengan API
- Location dengan GPS
- Profile dengan Camera

---

### Struktur Aplikasi

```
MyDaily App
├── Home (Dashboard)
├── To-Do List
├── Weather
├── Location
└── Profile
```

---

### Langkah 1: Buat Halaman Home dengan Tabs

File: `src/views/HomePage.vue` (update)

```vue
<template>
  <ion-page>
    <ion-tabs>
      <ion-router-outlet></ion-router-outlet>

      <ion-tab-bar slot="bottom">
        <ion-tab-button tab="dashboard" href="/tabs/dashboard">
          <ion-icon :icon="homeOutline"></ion-icon>
          <ion-label>Home</ion-label>
        </ion-tab-button>

        <ion-tab-button tab="todo" href="/tabs/todo">
          <ion-icon :icon="checkboxOutline"></ion-icon>
          <ion-label>Tugas</ion-label>
          <ion-badge v-if="pendingTodos > 0">{{ pendingTodos }}</ion-badge>
        </ion-tab-button>

        <ion-tab-button tab="weather" href="/tabs/weather">
          <ion-icon :icon="cloudOutline"></ion-icon>
          <ion-label>Cuaca</ion-label>
        </ion-tab-button>

        <ion-tab-button tab="profile" href="/tabs/profile">
          <ion-icon :icon="personOutline"></ion-icon>
          <ion-label>Profil</ion-label>
        </ion-tab-button>
      </ion-tab-bar>
    </ion-tabs>
  </ion-page>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import {
  IonPage,
  IonTabs,
  IonTabBar,
  IonTabButton,
  IonIcon,
  IonLabel,
  IonBadge,
  IonRouterOutlet
} from '@ionic/vue';
import {
  homeOutline,
  checkboxOutline,
  cloudOutline,
  personOutline
} from 'ionicons/icons';

const pendingTodos = ref(3); // Bisa diganti dengan data real
</script>
```

---

### Langkah 2: Dashboard

File: `src/views/DashboardPage.vue`

```vue
<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>My Daily App</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content class="ion-padding">
      <!-- Greeting -->
      <ion-card>
        <ion-card-content>
          <h2>Halo, {{ userName }}! 👋</h2>
          <p>{{ greeting }}</p>
        </ion-card-content>
      </ion-card>

      <!-- Quick Stats -->
      <ion-grid>
        <ion-row>
          <ion-col size="6">
            <ion-card color="primary" button @click="router.push('/tabs/todo')">
              <ion-card-content class="stat-card">
                <ion-icon :icon="checkboxOutline" style="font-size: 32px;"></ion-icon>
                <h3>{{ todoStats.total }}</h3>
                <p>Tugas</p>
              </ion-card-content>
            </ion-card>
          </ion-col>
          <ion-col size="6">
            <ion-card color="success" button>
              <ion-card-content class="stat-card">
                <ion-icon :icon="checkmarkDoneOutline" style="font-size: 32px;"></ion-icon>
                <h3>{{ todoStats.completed }}</h3>
                <p>Selesai</p>
              </ion-card-content>
            </ion-card>
          </ion-col>
        </ion-row>
      </ion-grid>

      <!-- Current Weather -->
      <h3>Cuaca Hari Ini</h3>
      <ion-card button @click="router.push('/tabs/weather')">
        <ion-card-content>
          <ion-grid>
            <ion-row class="ion-align-items-center">
              <ion-col size="3">
                <ion-icon :icon="sunnyOutline" style="font-size: 48px; color: #FFA500;"></ion-icon>
              </ion-col>
              <ion-col>
                <h2>{{ currentWeather.temp }}°C</h2>
                <p>{{ currentWeather.city }}</p>
              </ion-col>
            </ion-row>
          </ion-grid>
        </ion-card-content>
      </ion-card>

      <!-- Quick Actions -->
      <h3>Aksi Cepat</h3>
      <ion-list>
        <ion-item button @click="router.push('/location')">
          <ion-icon :icon="locateOutline" slot="start"></ion-icon>
          <ion-label>Lihat Lokasi Saya</ion-label>
        </ion-item>

        <ion-item button @click="router.push('/camera')">
          <ion-icon :icon="cameraOutline" slot="start"></ion-icon>
          <ion-label>Ambil Foto</ion-label>
        </ion-item>
      </ion-list>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { ref, computed, onMounted } from 'vue';
import { useRouter } from 'vue-router';
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
  IonCard,
  IonCardContent,
  IonGrid,
  IonRow,
  IonCol,
  IonIcon,
  IonList,
  IonItem,
  IonLabel
} from '@ionic/vue';
import {
  checkboxOutline,
  checkmarkDoneOutline,
  sunnyOutline,
  locateOutline,
  cameraOutline
} from 'ionicons/icons';

const router = useRouter();

const userName = ref('Anton');
const todoStats = ref({
  total: 8,
  completed: 3
});

const currentWeather = ref({
  temp: 28,
  city: 'Samarinda'
});

const greeting = computed(() => {
  const hour = new Date().getHours();
  if (hour < 12) return 'Selamat pagi! Semangat hari ini!';
  if (hour < 18) return 'Selamat siang! Tetap produktif!';
  return 'Selamat malam! Istirahat yang cukup ya!';
});

onMounted(() => {
  // Load data dari storage/API
});
</script>

<style scoped>
h2 {
  margin: 0;
  font-size: 24px;
}

h3 {
  margin: 20px 0 10px 0;
  color: #666;
}

.stat-card {
  text-align: center;
  padding: 15px;
}

.stat-card h3 {
  font-size: 32px;
  margin: 10px 0 5px 0;
  color: white;
}

.stat-card p {
  margin: 0;
  color: white;
  opacity: 0.9;
}
</style>
```

---

### Langkah 3: Update Router

File: `src/router/index.ts`

```typescript
import { createRouter, createWebHistory } from '@ionic/vue-router';
import { RouteRecordRaw } from 'vue-router';
import TabsPage from '../views/TabsPage.vue';

const routes: Array<RouteRecordRaw> = [
  {
    path: '/',
    redirect: '/tabs/dashboard'
  },
  {
    path: '/tabs/',
    component: TabsPage,
    children: [
      {
        path: '',
        redirect: '/tabs/dashboard'
      },
      {
        path: 'dashboard',
        component: () => import('@/views/DashboardPage.vue')
      },
      {
        path: 'todo',
        component: () => import('@/views/TodoPage.vue')
      },
      {
        path: 'weather',
        component: () => import('@/views/WeatherPage.vue')
      },
      {
        path: 'profile',
        component: () => import('@/views/ProfilePage.vue')
      }
    ]
  },
  // Routes lainnya (location, camera, dll)
  {
    path: '/location',
    component: () => import('@/views/LocationPage.vue')
  },
  {
    path: '/camera',
    component: () => import('@/views/CameraPage.vue')
  }
]

const router = createRouter({
  history: createWebHistory(import.meta.env.BASE_URL),
  routes
})

export default router
```

---

## 🐛 DEBUGGING & TESTING

### Chrome DevTools untuk Android

1. **Enable USB Debugging di perangkat Android:**
   - Settings → About Phone
   - Tap "Build Number" 7x untuk enable Developer Options
   - Settings → Developer Options
   - Enable "USB Debugging"

2. **Connect perangkat ke komputer**

3. **Buka Chrome di komputer:**
   - URL: `chrome://inspect`
   - Perangkat Android akan muncul
   - Klik "inspect" pada aplikasi Anda

4. **Gunakan DevTools seperti biasa:**
   - Console untuk log
   - Network untuk monitoring API calls
   - Elements untuk inspect UI

---

### Logcat (Android Studio)

1. **Buka Android Studio**

2. **Window → Logcat** (atau panel di bawah)

3. **Filter log:**
   - Pilih device/emulator
   - Pilih app package
   - Filter by severity: Verbose, Debug, Info, Warn, Error

4. **Tambahkan log di kode:**

```typescript
console.log('Debug info:', data);
console.error('Error occurred:', error);
```

Log akan muncul di Logcat.

---

## 📦 BUILD RELEASE APK

Untuk distribusi ke pengguna.

### Langkah 1: Generate Signing Key

```bash
keytool -genkey -v -keystore my-release-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000
```

Isi informasi:
- Password keystore
- Nama, organisasi, dll.

**Simpan file `my-release-key.keystore` dengan aman!**

---

### Langkah 2: Konfigurasi Gradle

File: `android/app/build.gradle`

Tambahkan di bagian `android`:

```gradle
signingConfigs {
    release {
        storeFile file('my-release-key.keystore')
        storePassword 'password-anda'
        keyAlias 'my-key-alias'
        keyPassword 'password-anda'
    }
}

buildTypes {
    release {
        signingConfig signingConfigs.release
        minifyEnabled false
        proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
    }
}
```

---

### Langkah 3: Build Release

Di Android Studio:
1. **Build → Generate Signed Bundle / APK**
2. Pilih **APK**
3. **Next**
4. Pilih keystore file
5. Masukkan password
6. **Next**
7. Pilih **release**
8. **Finish**

APK release ada di: `android/app/release/app-release.apk`

---

## 📝 LATIHAN MANDIRI

### Latihan 1: Notifikasi Lokal

Install plugin:
```bash
npm install @capacitor/local-notifications
```

Implementasikan:
1. Notifikasi pengingat tugas
2. Notifikasi cuaca buruk
3. Notifikasi harian

### Latihan 2: Share

Implementasikan fitur share:
```bash
npm install @capacitor/share
```

Buat fitur:
- Share lokasi
- Share foto
- Share to-do list

### Latihan 3: Network Status

Deteksi koneksi internet:
```bash
npm install @capacitor/network
```

Tampilkan banner jika offline.

---

## ⚠️ TROUBLESHOOTING COMMON ERRORS

### Error 1: "Cannot find module '@/services/weatherService'"

**Penyebab**: Alias `@/` tidak dikonfigurasi di `vite.config.ts`

**Solusi**:

1. Pastikan file `vite.config.ts` ada dan berisi:
   ```typescript
   import { defineConfig } from 'vite'
   import vue from '@vitejs/plugin-vue'
   import { fileURLToPath, URL } from 'node:url'

   export default defineConfig({
     plugins: [vue()],
     resolve: {
       alias: {
         '@': fileURLToPath(new URL('./src', import.meta.url))
       }
     }
   })
   ```

2. Restart dev server:
   ```bash
   # Ctrl+C untuk stop
   npm run dev
   ```

3. Jika masih error, hapus cache:
   ```bash
   rm -rf node_modules/.vite
   npm run dev
   ```

---

### Error 2: "Module not found: Error: Can't resolve ..."

**Penyebab**: File tidak ada atau path salah

**Solusi**:

1. Cek nama file dan folder exact (case-sensitive)
2. Cek struktur folder:
   ```
   src/
   ├── services/
   │   └── weatherService.ts  ✅
   ├── views/
   │   └── WeatherPage.vue    ✅
   └── router/
       └── index.ts           ✅
   ```

3. Gunakan relative path jika alias tidak bekerja:
   ```typescript
   // Gunakan ini
   import { weatherService } from '../services/weatherService';
   ```

---

### Error 3: "No such file or directory: dist"

**Penyebab**: Belum run `npm run build` atau `ionic build`

**Solusi**:
```bash
# Ionic project
ionic build

# Atau Vite project
npm run build
```

---

### Error 4: "Failed to resolve import" di TypeScript

**Penyebab**: Path mapping tidak ada di `tsconfig.json`

**Solusi**:

Edit `tsconfig.json`, tambahkan:
```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  }
}
```

---

### Error 5: Geolocation tidak bekerja di emulator

**Solusi**:

1. Buka Extended Controls di emulator (icon `...`)
2. Pilih tab "Location"
3. Set coordinates manual atau gunakan GPX file
4. Click "Send"

---

### Error 6: Camera tidak bekerja di emulator

**Solusi**:

1. Buat emulator baru dengan hardware camera enabled
2. Di AVD Manager → Edit Device
3. Advanced Settings → Camera:
   - Front camera: Webcam atau Emulated
   - Back camera: Webcam atau Emulated

---

### Error 7: "Gradle sync failed" di Android Studio

**Solusi**:

1. **File → Invalidate Caches / Restart**
2. Atau manual:
   ```bash
   cd android
   ./gradlew clean
   ./gradlew build
   ```

3. Jika masih error, update Gradle:
   - File: `android/gradle/wrapper/gradle-wrapper.properties`
   - Update: `distributionUrl=https\://services.gradle.org/distributions/gradle-8.0-all.zip`

---

### Error 8: "JAVA_HOME is not set"

**Solusi Windows**:
```powershell
# Set JAVA_HOME
setx JAVA_HOME "C:\Program Files\Java\jdk-17"

# Add to PATH
setx PATH "%PATH%;%JAVA_HOME%\bin"

# Restart terminal dan verify
java -version
```

**Solusi macOS/Linux**:
```bash
# Edit ~/.zshrc atau ~/.bash_profile
export JAVA_HOME=$(/usr/libexec/java_home -v 17)
export PATH=$JAVA_HOME/bin:$PATH

# Reload
source ~/.zshrc
```

---

### Error 9: "SDK location not found"

**Penyebab**: `ANDROID_HOME` tidak di-set

**Solusi Windows**:
```powershell
setx ANDROID_HOME "C:\Users\YourUser\AppData\Local\Android\Sdk"
setx PATH "%PATH%;%ANDROID_HOME%\platform-tools"
```

**Solusi macOS/Linux**:
```bash
export ANDROID_HOME=$HOME/Library/Android/sdk  # macOS
# atau
export ANDROID_HOME=$HOME/Android/Sdk  # Linux

export PATH=$PATH:$ANDROID_HOME/platform-tools
```

---

### Error 10: Port 5173 already in use

**Solusi**:

```bash
# Windows - kill process di port 5173
netstat -ano | findstr :5173
taskkill /PID <ProcessID> /F

# macOS/Linux
lsof -ti:5173 | xargs kill -9

# Atau gunakan port lain
npm run dev -- --port 3000
```

---

### Error 11: "Failed to fetch" saat akses API

**Penyebab**: CORS atau network issue

**Solusi**:

1. Cek internet connection
2. Test API di browser: https://api.open-meteo.com/v1/forecast?latitude=-6.2&longitude=106.8&hourly=temperature_2m
3. Tambahkan error handling:
   ```typescript
   try {
     const response = await axios.get(url);
   } catch (error) {
     console.error('API Error:', error);
     // Handle error
   }
   ```

---

### Error 12: "Cannot read property of undefined"

**Penyebab**: Data belum loaded tapi sudah di-access

**Solusi**:

Gunakan optional chaining dan null checks:
```vue
<template>
  <!-- ❌ SALAH -->
  <p>{{ weatherData.hourly.time[0] }}</p>

  <!-- ✅ BENAR -->
  <p v-if="weatherData">{{ weatherData.hourly.time[0] }}</p>
  
  <!-- Atau -->
  <p>{{ weatherData?.hourly?.time?.[0] }}</p>
</template>
```

---

### 🆘 Masih Mengalami Error?

**Gunakan Working Code Sample**:

```bash
cd code-samples/tuweb02-weather-app
npm install
npm run dev
```

Bandingkan project Anda dengan working sample untuk menemukan perbedaannya.

**Dokumentasi Lengkap**: Lihat `PERBAIKAN_TUWEB02.md`

---

## 🎯 RANGKUMAN

Pada praktikum ini, Anda telah mempelajari:

### 1. **Android Development Environment**
- ✅ Instalasi JDK, Android Studio, Gradle
- ✅ Setup environment variables
- ✅ Membuat dan mengelola AVD (emulator)

### 2. **Build Android App**
- ✅ Menambahkan platform Android dengan Capacitor
- ✅ Build dan run di emulator
- ✅ Generate APK debug dan release

### 3. **Native Plugins**
- ✅ Geolocation untuk akses GPS
- ✅ Camera untuk foto
- ✅ Preferences untuk storage lokal

### 4. **REST API Integration**
- ✅ Menggunakan Axios untuk HTTP requests
- ✅ Membuat service layer
- ✅ Handling loading dan error states

### 5. **Aplikasi Terintegrasi**
- ✅ Tab-based navigation
- ✅ Dashboard dengan multiple widgets
- ✅ Integrasi semua fitur (storage, API, native)

---

## 📚 REFERENSI

1. **Capacitor Documentation**
   - https://capacitorjs.com/docs

2. **Capacitor Plugins**
   - https://capacitorjs.com/docs/plugins

3. **Android Developer Guide**
   - https://developer.android.com/guide

4. **Axios Documentation**
   - https://axios-http.com/docs/intro

---

## 📧 PENUTUP

Selamat! Anda telah menyelesaikan Praktikum 2!

**Pertemuan selanjutnya (Tuweb 3 - Pertemuan 14):**
- Project akhir: Aplikasi lengkap dengan semua fitur
- Best practices dan optimization
- Publishing ke Google Play Store

**Terus berlatih dan eksplorasi fitur-fitur lain!**

---

## 🆕 UPDATE & IMPROVEMENTS

**Tanggal Update**: 24 November 2025

### ✅ Perbaikan yang Telah Dilakukan:

1. **Ditambahkan Langkah 0**: Setup Configuration Files
   - `vite.config.ts` dengan alias `@/`
   - `tsconfig.json` dengan path mapping
   - `capacitor.config.ts` configuration

2. **Ditambahkan Section Troubleshooting**
   - 12 common errors dengan solusi lengkap
   - Tips debugging dan best practices

3. **Working Code Sample Tersedia**
   - Lokasi: `code-samples/tuweb02-weather-app/`
   - Full working project dengan semua fitur
   - Dokumentasi lengkap: `PERBAIKAN_TUWEB02.md`

### 🎯 Untuk Mahasiswa:

Jika mengalami masalah mengikuti tutorial ini:

1. **Gunakan Working Code Sample**:
   ```bash
   cd code-samples/tuweb02-weather-app
   npm install
   npm run dev
   ```

2. **Baca Troubleshooting Section** di materi ini

3. **Lihat Dokumentasi Fix**: `PERBAIKAN_TUWEB02.md`

---

**Disusun oleh:**
Anton Prafanto, S.Kom, M.T.
Dosen Program Studi Informatika
Universitas Mulawarman
Tutor Universitas Terbuka

**Mata Kuliah:** Pemrograman Berbasis Perangkat Bergerak (MSIM4401)
**Tahun:** 2025


---

# 🧑‍🏫 PENGAYAAN PRAKTIKUM PERTEMUAN 10

Bagian pengayaan ini dapat digunakan untuk sesi **4–5 jam**. Fokusnya bukan hanya “berhasil build APK”, tetapi memahami aliran teknis dari aplikasi web Ionic/Vue sampai menjadi aplikasi Android yang bisa mengakses perangkat keras.

## A. Mental Model: Dari Vue ke APK

~~~text
Vue + Ionic + TypeScript
        |
        | npm run build
        v
      dist/
        |
        | npx cap sync android
        v
android/ native project
        |
        | Gradle / Android Studio
        v
     APK / AAB
        |
        v
Android device / emulator
~~~

### Poin untuk dijelaskan
- **npm run build** menghasilkan web assets.
- **Capacitor** menjembatani web app dengan native platform.
- Folder **android/** adalah project Android native.
- **Gradle** yang benar-benar mengompilasi project Android.
- Native plugin bekerja karena ada bridge antara JavaScript/TypeScript dan API perangkat.

---

## B. Pre-flight Check Sebelum Praktikum Android

Jalankan satu per satu:

~~~bash
node --version
npm --version
ionic --version
java -version
javac -version
adb version
~~~

Jika project sudah ada:

~~~bash
npm install
npm run build
npx cap doctor
~~~

### Pertanyaan tutor
- Mengapa aplikasi bisa jalan di browser tetapi gagal di Android?
- Mengapa Java/JDK diperlukan padahal kode kita TypeScript?
- Apa beda Ionic CLI, Capacitor CLI, Android SDK, dan Gradle?

---

## C. Menambahkan Platform Android dengan Benar

Dari root project:

~~~bash
npm install @capacitor/android
npm run build
npx cap add android
npx cap sync android
npx cap open android
~~~

Setelah perubahan pada kode web:

~~~bash
npm run build
npx cap sync android
~~~

### Aturan sederhana
- **add** biasanya sekali saat membuat platform.
- **sync** dilakukan berulang setelah dependency/plugin/web asset berubah.
- **open** membuka project native di Android Studio.

---

## D. Demo Native 1 — Camera dengan Capacitor Modern

Install:

~~~bash
npm install @capacitor/camera
npx cap sync android
~~~

Buat **src/services/CameraService.ts**:

~~~ts
import {
  Camera,
  CameraResultType,
  CameraSource
} from '@capacitor/camera';

export async function takePhoto(): Promise<string | null> {
  const permission = await Camera.requestPermissions({
    permissions: ['camera']
  });

  if (permission.camera !== 'granted') {
    return null;
  }

  const photo = await Camera.getPhoto({
    quality: 80,
    allowEditing: false,
    resultType: CameraResultType.DataUrl,
    source: CameraSource.Prompt
  });

  return photo.dataUrl ?? null;
}
~~~

Gunakan di page:

~~~vue
<template>
  <ion-button @click="capture">Ambil Foto</ion-button>

  <ion-card v-if="imageUrl">
    <img :src="imageUrl" alt="Hasil kamera" />
  </ion-card>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { IonButton, IonCard } from '@ionic/vue';
import { takePhoto } from '@/services/CameraService';

const imageUrl = ref<string | null>(null);

async function capture() {
  imageUrl.value = await takePhoto();
}
</script>
~~~

### Yang harus diterangkan
- Permission dapat **granted**, **denied**, atau belum diputuskan.
- Camera API bersifat asynchronous.
- DataUrl mudah untuk demo, tetapi ukurannya besar jika disimpan banyak.
- Untuk production, file URI biasanya lebih efisien daripada Base64/DataUrl.

---

## E. Demo Native 2 — Geolocation

Install:

~~~bash
npm install @capacitor/geolocation
npx cap sync android
~~~

Service:

~~~ts
import { Geolocation } from '@capacitor/geolocation';

export interface Coordinate {
  latitude: number;
  longitude: number;
  accuracy: number;
}

export async function getCurrentCoordinate(): Promise<Coordinate> {
  const permission = await Geolocation.requestPermissions();

  if (permission.location !== 'granted' &&
      permission.coarseLocation !== 'granted') {
    throw new Error('Izin lokasi tidak diberikan.');
  }

  const position = await Geolocation.getCurrentPosition({
    enableHighAccuracy: true,
    timeout: 10000
  });

  return {
    latitude: position.coords.latitude,
    longitude: position.coords.longitude,
    accuracy: position.coords.accuracy
  };
}
~~~

Page:

~~~vue
<template>
  <ion-button @click="locate">Ambil Lokasi</ion-button>

  <ion-list v-if="coordinate">
    <ion-item>Latitude: {{ coordinate.latitude }}</ion-item>
    <ion-item>Longitude: {{ coordinate.longitude }}</ion-item>
    <ion-item>Akurasi: {{ coordinate.accuracy }} meter</ion-item>
  </ion-list>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { IonButton, IonItem, IonList } from '@ionic/vue';
import {
  getCurrentCoordinate,
  type Coordinate
} from '@/services/LocationService';

const coordinate = ref<Coordinate | null>(null);

async function locate() {
  coordinate.value = await getCurrentCoordinate();
}
</script>
~~~

### Diskusi penting
Akurasi GPS 5 meter dan 500 meter sama-sama memberikan latitude/longitude, tetapi kualitas informasi berbeda. Maka field **accuracy** perlu diperhatikan.

---

## F. Demo Native 3 — Foto + Lokasi + Waktu

Contoh ini paling dekat dengan ide aplikasi pada materi UT.

~~~ts
import { takePhoto } from '@/services/CameraService';
import { getCurrentCoordinate } from '@/services/LocationService';

export interface FieldRecord {
  id: string;
  capturedAt: string;
  imageDataUrl: string;
  latitude: number;
  longitude: number;
  accuracy: number;
}

export async function createFieldRecord(): Promise<FieldRecord> {
  const image = await takePhoto();

  if (!image) {
    throw new Error('Foto tidak tersedia.');
  }

  const location = await getCurrentCoordinate();

  return {
    id: crypto.randomUUID(),
    capturedAt: new Date().toISOString(),
    imageDataUrl: image,
    latitude: location.latitude,
    longitude: location.longitude,
    accuracy: location.accuracy
  };
}
~~~

### Aliran yang dapat digambar di papan
1. User menekan tombol.
2. App meminta permission camera.
3. Camera dibuka.
4. Foto dikembalikan ke aplikasi.
5. App meminta permission location.
6. GPS memberikan koordinat.
7. Timestamp dibuat.
8. Ketiga data digabung menjadi satu record.

### Challenge
Tambahkan input **catatan** dan **nama lokasi** ke FieldRecord.

---

## G. Demo REST API 1 — Loading, Success, Error

Buat **src/services/UserApi.ts**:

~~~ts
import axios from 'axios';

export interface ApiUser {
  id: number;
  name: string;
  email: string;
  phone: string;
}

const client = axios.create({
  baseURL: 'https://jsonplaceholder.typicode.com',
  timeout: 7000
});

export async function fetchUsers(): Promise<ApiUser[]> {
  const response = await client.get<ApiUser[]>('/users');
  return response.data;
}
~~~

Page:

~~~vue
<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Data User</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content>
      <div class="ion-padding" v-if="loading">
        Mengambil data...
      </div>

      <ion-text color="danger" v-else-if="errorMessage">
        <p class="ion-padding">{{ errorMessage }}</p>
      </ion-text>

      <ion-list v-else>
        <ion-item v-for="user in users" :key="user.id">
          <ion-label>
            <h2>{{ user.name }}</h2>
            <p>{{ user.email }} · {{ user.phone }}</p>
          </ion-label>
        </ion-item>
      </ion-list>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue';
import {
  IonPage, IonHeader, IonToolbar, IonTitle,
  IonContent, IonText, IonList, IonItem, IonLabel
} from '@ionic/vue';
import { fetchUsers, type ApiUser } from '@/services/UserApi';

const users = ref<ApiUser[]>([]);
const loading = ref(false);
const errorMessage = ref('');

async function loadUsers() {
  loading.value = true;
  errorMessage.value = '';

  try {
    users.value = await fetchUsers();
  } catch {
    errorMessage.value = 'REST API tidak dapat diakses.';
  } finally {
    loading.value = false;
  }
}

onMounted(loadUsers);
</script>
~~~

---

## H. Demo REST API 2 — Route Parameter /user/:id

Router:

~~~ts
{
  path: '/user/:id',
  component: () => import('@/views/UserDetailPage.vue')
}
~~~

Navigasi dari list:

~~~vue
<ion-item
  v-for="user in users"
  :key="user.id"
  :router-link="'/user/' + user.id">
  {{ user.name }}
</ion-item>
~~~

Ambil id:

~~~ts
import { useRoute } from 'vue-router';

const route = useRoute();
const id = Number(route.params.id);
~~~

### Poin penjelasan
Route parameter adalah contoh bagaimana **UI list → URL → detail page → request API** membentuk aliran aplikasi.

---

## I. Local Persistence dengan Capacitor Preferences

Install:

~~~bash
npm install @capacitor/preferences
npx cap sync
~~~

Service:

~~~ts
import { Preferences } from '@capacitor/preferences';

const KEY = 'msim4401_profile';

export interface LocalProfile {
  name: string;
  email: string;
}

export async function saveProfile(profile: LocalProfile) {
  await Preferences.set({
    key: KEY,
    value: JSON.stringify(profile)
  });
}

export async function loadProfile(): Promise<LocalProfile | null> {
  const result = await Preferences.get({ key: KEY });

  if (!result.value) return null;

  return JSON.parse(result.value) as LocalProfile;
}

export async function clearProfile() {
  await Preferences.remove({ key: KEY });
}
~~~

### Perbandingan untuk diskusi
- **Preferences**: key-value sederhana.
- **SQLite**: data relasional lebih kompleks, query, tabel.
- **REST API**: sumber data berada di server.
- **Reactive state**: data aktif selama app berjalan.

---

## J. Konsep State Login: Dari Vuex ke Pinia

Materi UT menggunakan centralized state untuk menjaga status login saat berpindah view. Untuk project Vue modern, konsep yang sama dapat ditulis dengan Pinia.

~~~ts
import { defineStore } from 'pinia';
import { computed, ref } from 'vue';

export const useAuthStore = defineStore('auth', () => {
  const userName = ref('');
  const fullName = ref('');

  const isLoggedIn = computed(() => userName.value !== '');

  function login(user: string, name: string) {
    userName.value = user;
    fullName.value = name;
  }

  function logout() {
    userName.value = '';
    fullName.value = '';
  }

  return {
    userName,
    fullName,
    isLoggedIn,
    login,
    logout
  };
});
~~~

### Hal yang tidak berubah secara konseptual
Centralized store tetap digunakan untuk menyimpan data lintas halaman; yang berubah hanya library dan gaya API.

---

## K. Router Guard untuk Melindungi Halaman

~~~ts
router.beforeEach((to) => {
  const auth = useAuthStore();

  const protectedRoutes = ['/home', '/camera', '/profile'];

  if (protectedRoutes.includes(to.path) && !auth.isLoggedIn) {
    return '/login';
  }

  return true;
});
~~~

### Pertanyaan
Mengapa menyembunyikan tombol menu saja tidak cukup untuk keamanan navigasi? Karena user masih bisa mengetik URL langsung; route guard memberi kontrol tambahan di sisi navigasi aplikasi.

---

## L. Permission dan AndroidManifest

Jika plugin membutuhkan permission yang belum otomatis tercatat, cek:

**android/app/src/main/AndroidManifest.xml**

~~~xml
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
~~~

> Gunakan permission seminimal mungkin. Jangan menambahkan permission yang tidak dipakai aplikasi.

---

## M. Build APK melalui Command Line

Windows:

~~~bash
npm run build
npx cap sync android
cd android
gradlew.bat assembleDebug
~~~

macOS/Linux:

~~~bash
npm run build
npx cap sync android
cd android
./gradlew assembleDebug
~~~

Umumnya debug APK berada di:

~~~text
android/app/build/outputs/apk/debug/app-debug.apk
~~~

Install:

~~~bash
adb devices
adb install -r android/app/build/outputs/apk/debug/app-debug.apk
~~~

### Penjelasan flag -r
Mengganti aplikasi yang sudah terinstal tanpa perlu uninstall manual, selama signature sesuai.

---

## N. Debugging: Browser vs Android Device

### 1. Log dari TypeScript

~~~ts
console.log('coordinate', coordinate.value);
console.error('failed', error);
~~~

### 2. ADB Logcat

~~~bash
adb devices
adb logcat
~~~

Filter sederhana:

~~~bash
adb logcat | findstr Capacitor
~~~

Pada macOS/Linux:

~~~bash
adb logcat | grep Capacitor
~~~

### 3. Chrome Remote Debugging
- Aktifkan Developer Options.
- Aktifkan USB Debugging.
- Hubungkan perangkat.
- Buka Chrome di desktop.
- Gunakan halaman inspect devices untuk WebView aplikasi.

### Tiga kategori error
1. **Web layer**: Vue/TypeScript/HTTP.
2. **Bridge layer**: Capacitor/plugin.
3. **Native layer**: permission, Gradle, SDK, AndroidManifest.

---

## O. Troubleshooting Table

| Gejala | Kemungkinan penyebab | Pemeriksaan |
|---|---|---|
| Camera tidak muncul | permission ditolak | cek requestPermissions dan Settings Android |
| Geolocation timeout | GPS mati / emulator belum punya lokasi | set location emulator |
| npx cap sync gagal | dependency tidak lengkap | npm install lalu cap doctor |
| Gradle gagal | JDK/SDK tidak cocok | java -version, SDK Manager |
| adb tidak melihat device | USB debugging/driver | adb devices |
| API jalan di browser tapi gagal device | network/security/CORS endpoint | cek URL, internet device, log |
| Perubahan UI tidak muncul di APK | lupa build/sync | npm run build lalu cap sync |

---

# 🧪 MINI PROJECT: FIELD LOG

Target: mahasiswa membuat aplikasi yang menyimpan sementara daftar observasi.

Setiap record:

~~~ts
interface Observation {
  id: string;
  title: string;
  note: string;
  imageDataUrl: string;
  capturedAt: string;
  latitude: number;
  longitude: number;
}
~~~

Fitur minimal:
- [ ] Tambah judul dan catatan.
- [ ] Ambil foto.
- [ ] Ambil lokasi.
- [ ] Simpan timestamp.
- [ ] Tampilkan list.
- [ ] Tampilkan detail.
- [ ] Simpan draft ke Preferences.
- [ ] Build APK dan install ke perangkat.

### Pertanyaan pengembangan
- Bagaimana jika camera permission ditolak?
- Bagaimana jika GPS gagal?
- Bagaimana jika API tidak punya internet?
- Kapan data sebaiknya disimpan ke SQLite?
- Apa yang sebaiknya tidak disimpan sebagai Base64?

---

# ⏱️ SKENARIO 270 MENIT

| Durasi | Aktivitas |
|---|---|
| 0–30 | Arsitektur Android, Capacitor, build pipeline |
| 30–60 | JDK, Android Studio, SDK, emulator/device |
| 60–90 | Add/sync/open Android |
| 90–125 | Camera plugin |
| 125–160 | Geolocation |
| 160–190 | Foto + lokasi + timestamp |
| 190–220 | REST API + route detail |
| 220–240 | Persistence/state |
| 240–260 | Build APK + adb |
| 260–270 | Debugging dan review |

---

# ✅ CHECKLIST AKHIR PERTEMUAN 10

Mahasiswa harus mampu:

- [ ] Menjelaskan jalur build dari Vue/Ionic sampai APK.
- [ ] Menambahkan platform Android.
- [ ] Melakukan cap sync.
- [ ] Meminta permission dengan benar.
- [ ] Menggunakan Camera.
- [ ] Menggunakan Geolocation.
- [ ] Mengambil data REST API.
- [ ] Menangani loading/error.
- [ ] Menggunakan route parameter.
- [ ] Menyimpan data lokal sederhana.
- [ ] Menjelaskan centralized state.
- [ ] Menghasilkan debug APK.
- [ ] Menginstall APK dengan adb.
- [ ] Membedakan error web, bridge, dan native.

