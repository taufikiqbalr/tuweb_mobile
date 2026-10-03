# MATERI TUWEB 3 - PERTEMUAN 14
# PROJECT AKHIR: APLIKASI MOBILE TERINTEGRASI LENGKAP

> **Catatan penyusunan:** file final ini merupakan adaptasi dari **TUWEB_4.md** sesuai pemetaan pada README repository. Isi utama project “Kampus Kita” dipertahankan, lalu diperkaya dengan jembatan konsep ke materi UT tentang aplikasi terintegrasi: autentikasi, state lintas halaman, penyimpanan lokal, Camera, Geolocation, router, offline workflow, serta build APK.

---

## 📋 INFORMASI MATA KULIAH

**Mata Kuliah**: Pemrograman Berbasis Perangkat Bergerak (MSIM4401)
**Pertemuan**: 14 (TUWEB 3 - Project Akhir)
**Pokok Bahasan**: Pengembangan Aplikasi Mobile Terintegrasi Lengkap dari Awal sampai Deployment
**Pendekatan**: Project-Based Learning

---

## 🎯 TUJUAN PEMBELAJARAN

Setelah menyelesaikan praktikum ini, mahasiswa diharapkan mampu:

1. Merancang dan mengembangkan aplikasi mobile lengkap dari awal hingga akhir
2. Mengintegrasikan berbagai teknologi (Vue, Ionic, REST API, Native Plugins)
3. Menerapkan best practices dalam pengembangan mobile
4. Melakukan testing dan debugging aplikasi secara menyeluruh
5. Mengoptimasi performa dan user experience aplikasi
6. Mendeploy aplikasi ke perangkat Android
7. Mempersiapkan aplikasi untuk publikasi di Google Play Store
8. Membuat dokumentasi dan user guide aplikasi

---

## 📚 PRASYARAT

Sebelum memulai praktikum ini, pastikan Anda telah:

- ✅ Menyelesaikan Tuweb 1 (Pertemuan 6)
- ✅ Menyelesaikan Tuweb 2 (Pertemuan 10)
- ✅ Memahami Vue.js, Ionic Framework, dan Capacitor
- ✅ Mampu build aplikasi menjadi APK
- ✅ Memiliki ide aplikasi atau mengikuti studi kasus yang disediakan

---

## 🎨 STUDI KASUS: APLIKASI "KAMPUS KITA"

### Overview Aplikasi

**Kampus Kita** adalah aplikasi mobile untuk mahasiswa yang mengintegrasikan berbagai fitur penting:

1. **Informasi Akademik** - Jadwal kuliah, nilai, dan pengumuman
2. **Manajemen Tugas** - To-do list dengan reminder
3. **Info Cuaca & Lokasi** - Cuaca kampus dan navigasi
4. **Profil Mahasiswa** - Data diri dengan foto
5. **Berita & Artikel** - Feed berita kampus dari API
6. **Catatan** - Note-taking dengan rich text

### Fitur Utama:

✅ **Offline-first**: Data disimpan lokal, sync saat online
✅ **Real-time**: Notifikasi dan update terbaru
✅ **Native Features**: Camera, GPS, Storage
✅ **Modern UI**: Material Design dengan animasi
✅ **Responsive**: Adaptif untuk berbagai ukuran layar

---

## 🏗️ ARSITEKTUR APLIKASI

### Struktur Folder

```
kampus-kita/
├── android/                    # Android platform
├── ios/                        # iOS platform (opsional)
├── public/                     # Static assets
├── src/
│   ├── assets/                 # Images, icons
│   ├── components/             # Reusable components
│   │   ├── common/             # Button, Card, dll
│   │   ├── layout/             # Header, Footer
│   │   └── features/           # Feature-specific
│   ├── composables/            # Vue composables (hooks)
│   ├── models/                 # TypeScript interfaces
│   ├── router/                 # Routing configuration
│   ├── services/               # API services
│   │   ├── api/                # HTTP clients
│   │   ├── storage/            # Local storage
│   │   └── native/             # Native plugins
│   ├── stores/                 # State management (Pinia)
│   ├── utils/                  # Helper functions
│   ├── views/                  # Pages/Views
│   ├── theme/                  # CSS/SCSS files
│   ├── App.vue                 # Root component
│   └── main.ts                 # Entry point
├── tests/                      # Unit & E2E tests
├── .env                        # Environment variables
├── capacitor.config.ts         # Capacitor config
├── ionic.config.json           # Ionic config
├── package.json                # Dependencies
├── tsconfig.json               # TypeScript config
└── vite.config.ts              # Vite bundler config
```

---

## 🚀 PRAKTIKUM 1: SETUP PROJECT & ARCHITECTURE

### Langkah 1: Membuat Project Baru

```bash
# Buat project dengan template tabs
ionic start kampus-kita tabs --type=vue --capacitor

cd kampus-kita
```

---

### Langkah 2: Install Dependencies

```bash
# State Management
npm install pinia

# HTTP Client
npm install axios

# Date Utilities
npm install date-fns

# Validation
npm install yup

# Rich Text Editor
npm install @tiptap/vue-3 @tiptap/starter-kit

# Capacitor Plugins
npm install @capacitor/geolocation @capacitor/camera @capacitor/preferences @capacitor/local-notifications @capacitor/share @capacitor/network

# Sync
npx cap sync
```

---

### Langkah 3: Setup State Management (Pinia)

File: `src/stores/index.ts`

```typescript
import { createPinia } from 'pinia';

export const pinia = createPinia();
```

File: `src/main.ts` (update)

```typescript
import { createApp } from 'vue'
import App from './App.vue'
import router from './router';
import { pinia } from './stores';

import { IonicVue } from '@ionic/vue';

/* Core CSS required for Ionic components */
import '@ionic/vue/css/core.css';
/* ... other ionic css ... */

const app = createApp(App)
  .use(IonicVue)
  .use(router)
  .use(pinia);

router.isReady().then(() => {
  app.mount('#app');
});
```

---

### Langkah 4: Membuat Models/Interfaces

File: `src/models/index.ts`

```typescript
// User Model
export interface User {
  id: string;
  nim: string;
  name: string;
  email: string;
  prodi: string;
  semester: number;
  photo?: string;
}

// Task Model
export interface Task {
  id: string;
  title: string;
  description: string;
  deadline: Date;
  priority: 'low' | 'medium' | 'high';
  completed: boolean;
  category: 'kuliah' | 'tugas' | 'ujian' | 'lainnya';
  createdAt: Date;
}

// Schedule Model
export interface Schedule {
  id: string;
  mataKuliah: string;
  dosen: string;
  ruangan: string;
  hari: string;
  jamMulai: string;
  jamSelesai: string;
}

// Note Model
export interface Note {
  id: string;
  title: string;
  content: string;
  category: string;
  tags: string[];
  createdAt: Date;
  updatedAt: Date;
}

// News/Article Model
export interface Article {
  id: number;
  title: string;
  excerpt: string;
  content: string;
  image: string;
  author: string;
  publishedAt: Date;
  category: string;
}

// Weather Model
export interface Weather {
  city: string;
  temperature: number;
  description: string;
  humidity: number;
  windSpeed: number;
  icon: string;
}
```

---

### Langkah 5: Setup Environment Variables

File: `.env`

```env
VITE_APP_NAME=Kampus Kita
VITE_API_BASE_URL=https://api.kampuskita.ac.id/v1
VITE_WEATHER_API_URL=https://api.open-meteo.com/v1
VITE_NEWS_API_URL=https://newsapi.org/v2
```

File: `src/config/index.ts`

```typescript
export const config = {
  appName: import.meta.env.VITE_APP_NAME || 'Kampus Kita',
  apiBaseUrl: import.meta.env.VITE_API_BASE_URL,
  weatherApiUrl: import.meta.env.VITE_WEATHER_API_URL,
  newsApiUrl: import.meta.env.VITE_NEWS_API_URL,
};
```

---

## 📦 PRAKTIKUM 2: MEMBUAT SERVICES LAYER

### Langkah 1: HTTP Client Setup

File: `src/services/api/httpClient.ts`

```typescript
import axios, { AxiosInstance, AxiosRequestConfig, AxiosResponse } from 'axios';
import { config } from '@/config';

class HttpClient {
  private instance: AxiosInstance;

  constructor(baseURL: string) {
    this.instance = axios.create({
      baseURL,
      timeout: 10000,
      headers: {
        'Content-Type': 'application/json',
      },
    });

    this.setupInterceptors();
  }

  private setupInterceptors() {
    // Request Interceptor
    this.instance.interceptors.request.use(
      (config) => {
        // Bisa tambahkan token di sini
        const token = localStorage.getItem('authToken');
        if (token) {
          config.headers.Authorization = `Bearer ${token}`;
        }
        return config;
      },
      (error) => {
        return Promise.reject(error);
      }
    );

    // Response Interceptor
    this.instance.interceptors.response.use(
      (response) => response,
      (error) => {
        // Handle errors globally
        if (error.response?.status === 401) {
          // Redirect to login
          console.log('Unauthorized, redirecting to login...');
        }
        return Promise.reject(error);
      }
    );
  }

  async get<T>(url: string, config?: AxiosRequestConfig): Promise<T> {
    const response: AxiosResponse<T> = await this.instance.get(url, config);
    return response.data;
  }

  async post<T>(url: string, data?: any, config?: AxiosRequestConfig): Promise<T> {
    const response: AxiosResponse<T> = await this.instance.post(url, data, config);
    return response.data;
  }

  async put<T>(url: string, data?: any, config?: AxiosRequestConfig): Promise<T> {
    const response: AxiosResponse<T> = await this.instance.put(url, data, config);
    return response.data;
  }

  async delete<T>(url: string, config?: AxiosRequestConfig): Promise<T> {
    const response: AxiosResponse<T> = await this.instance.delete(url, config);
    return response.data;
  }
}

export const apiClient = new HttpClient(config.apiBaseUrl);
export const weatherClient = new HttpClient(config.weatherApiUrl);
```

---

### Langkah 2: Storage Service

File: `src/services/storage/storageService.ts`

```typescript
import { Preferences } from '@capacitor/preferences';

export class StorageService {
  /**
   * Simpan data
   */
  static async set(key: string, value: any): Promise<void> {
    await Preferences.set({
      key,
      value: JSON.stringify(value),
    });
  }

  /**
   * Ambil data
   */
  static async get<T>(key: string): Promise<T | null> {
    const { value } = await Preferences.get({ key });
    return value ? JSON.parse(value) : null;
  }

  /**
   * Hapus data
   */
  static async remove(key: string): Promise<void> {
    await Preferences.remove({ key });
  }

  /**
   * Hapus semua data
   */
  static async clear(): Promise<void> {
    await Preferences.clear();
  }

  /**
   * Cek apakah key ada
   */
  static async has(key: string): Promise<boolean> {
    const { value } = await Preferences.get({ key });
    return value !== null;
  }
}

// Storage Keys
export const STORAGE_KEYS = {
  USER: 'user',
  TASKS: 'tasks',
  NOTES: 'notes',
  SCHEDULES: 'schedules',
  SETTINGS: 'settings',
  THEME: 'theme',
};
```

---

### Langkah 3: News Service

File: `src/services/api/newsService.ts`

```typescript
import { Article } from '@/models';

// Mock data untuk demo (karena NewsAPI butuh key)
const mockArticles: Article[] = [
  {
    id: 1,
    title: 'Pendaftaran Mahasiswa Baru Tahun 2025',
    excerpt: 'Universitas membuka pendaftaran mahasiswa baru untuk tahun akademik 2025/2026.',
    content: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit...',
    image: 'https://picsum.photos/400/250?random=1',
    author: 'Admin Kampus',
    publishedAt: new Date('2025-01-01'),
    category: 'Pengumuman',
  },
  {
    id: 2,
    title: 'Seminar Nasional Teknologi Informasi',
    excerpt: 'Prodi Informatika mengadakan seminar nasional dengan tema AI dan Machine Learning.',
    content: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit...',
    image: 'https://picsum.photos/400/250?random=2',
    author: 'Prodi Informatika',
    publishedAt: new Date('2025-01-15'),
    category: 'Event',
  },
  {
    id: 3,
    title: 'Beasiswa Prestasi Semester Genap 2024',
    excerpt: 'Informasi beasiswa prestasi untuk mahasiswa berprestasi.',
    content: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit...',
    image: 'https://picsum.photos/400/250?random=3',
    author: 'Kemahasiswaan',
    publishedAt: new Date('2025-01-20'),
    category: 'Beasiswa',
  },
];

export class NewsService {
  /**
   * Get all articles
   */
  static async getArticles(): Promise<Article[]> {
    // Simulasi API call dengan delay
    await new Promise(resolve => setTimeout(resolve, 1000));
    return mockArticles;
  }

  /**
   * Get article by ID
   */
  static async getArticleById(id: number): Promise<Article | null> {
    await new Promise(resolve => setTimeout(resolve, 500));
    return mockArticles.find(article => article.id === id) || null;
  }

  /**
   * Get articles by category
   */
  static async getArticlesByCategory(category: string): Promise<Article[]> {
    await new Promise(resolve => setTimeout(resolve, 500));
    return mockArticles.filter(article => article.category === category);
  }
}
```

---

### Langkah 4: Weather Service

File: `src/services/api/weatherService.ts`

```typescript
import { weatherClient } from './httpClient';
import { Weather } from '@/models';

export class WeatherService {
  /**
   * Get weather by coordinates
   */
  static async getWeather(lat: number, lon: number): Promise<Weather> {
    try {
      const response = await weatherClient.get<any>('/forecast', {
        params: {
          latitude: lat,
          longitude: lon,
          current_weather: true,
          hourly: 'temperature_2m,relative_humidity_2m,windspeed_10m',
          timezone: 'Asia/Jakarta'
        }
      });

      return {
        city: 'Samarinda', // Bisa pakai reverse geocoding API
        temperature: response.current_weather.temperature,
        description: this.getWeatherDescription(response.current_weather.weathercode),
        humidity: response.hourly.relative_humidity_2m[0],
        windSpeed: response.current_weather.windspeed,
        icon: this.getWeatherIcon(response.current_weather.weathercode),
      };
    } catch (error) {
      console.error('Error fetching weather:', error);
      throw error;
    }
  }

  /**
   * Get weather by city name (preset)
   */
  static async getWeatherByCity(city: string): Promise<Weather> {
    const cities: { [key: string]: { lat: number; lon: number } } = {
      'samarinda': { lat: -0.5, lon: 117.15 },
      'balikpapan': { lat: -1.24, lon: 116.89 },
      'jakarta': { lat: -6.2, lon: 106.8 },
    };

    const coords = cities[city.toLowerCase()];
    if (!coords) {
      throw new Error('City not found');
    }

    return this.getWeather(coords.lat, coords.lon);
  }

  private static getWeatherDescription(code: number): string {
    const descriptions: { [key: number]: string } = {
      0: 'Cerah',
      1: 'Cerah Sebagian',
      2: 'Berawan Sebagian',
      3: 'Berawan',
      45: 'Berkabut',
      48: 'Berkabut Tebal',
      51: 'Gerimis Ringan',
      61: 'Hujan Ringan',
      63: 'Hujan Sedang',
      65: 'Hujan Lebat',
      95: 'Badai Petir',
    };
    return descriptions[code] || 'Unknown';
  }

  private static getWeatherIcon(code: number): string {
    // Mapping ke ionicons
    const icons: { [key: number]: string } = {
      0: 'sunny',
      1: 'partly-sunny',
      2: 'cloudy',
      3: 'cloudy',
      51: 'rainy',
      61: 'rainy',
      63: 'rainy',
      65: 'rainy',
      95: 'thunderstorm',
    };
    return icons[code] || 'cloud';
  }
}
```

---

## 🗂️ PRAKTIKUM 3: STATE MANAGEMENT DENGAN PINIA

### Langkah 1: User Store

File: `src/stores/userStore.ts`

```typescript
import { defineStore } from 'pinia';
import { ref } from 'vue';
import { User } from '@/models';
import { StorageService, STORAGE_KEYS } from '@/services/storage/storageService';

export const useUserStore = defineStore('user', () => {
  const user = ref<User | null>(null);
  const isAuthenticated = ref(false);

  // Load user from storage
  const loadUser = async () => {
    const savedUser = await StorageService.get<User>(STORAGE_KEYS.USER);
    if (savedUser) {
      user.value = savedUser;
      isAuthenticated.value = true;
    }
  };

  // Save user
  const setUser = async (userData: User) => {
    user.value = userData;
    isAuthenticated.value = true;
    await StorageService.set(STORAGE_KEYS.USER, userData);
  };

  // Update user
  const updateUser = async (updates: Partial<User>) => {
    if (user.value) {
      user.value = { ...user.value, ...updates };
      await StorageService.set(STORAGE_KEYS.USER, user.value);
    }
  };

  // Logout
  const logout = async () => {
    user.value = null;
    isAuthenticated.value = false;
    await StorageService.remove(STORAGE_KEYS.USER);
  };

  return {
    user,
    isAuthenticated,
    loadUser,
    setUser,
    updateUser,
    logout,
  };
});
```

---

### Langkah 2: Tasks Store

File: `src/stores/tasksStore.ts`

```typescript
import { defineStore } from 'pinia';
import { ref, computed } from 'vue';
import { Task } from '@/models';
import { StorageService, STORAGE_KEYS } from '@/services/storage/storageService';

export const useTasksStore = defineStore('tasks', () => {
  const tasks = ref<Task[]>([]);

  // Computed
  const totalTasks = computed(() => tasks.value.length);
  const completedTasks = computed(() => tasks.value.filter(t => t.completed).length);
  const pendingTasks = computed(() => tasks.value.filter(t => !t.completed).length);
  const todayTasks = computed(() => {
    const today = new Date().toDateString();
    return tasks.value.filter(t => new Date(t.deadline).toDateString() === today);
  });

  // Load tasks
  const loadTasks = async () => {
    const savedTasks = await StorageService.get<Task[]>(STORAGE_KEYS.TASKS);
    if (savedTasks) {
      tasks.value = savedTasks;
    }
  };

  // Save tasks
  const saveTasks = async () => {
    await StorageService.set(STORAGE_KEYS.TASKS, tasks.value);
  };

  // Add task
  const addTask = async (task: Omit<Task, 'id' | 'createdAt'>) => {
    const newTask: Task = {
      ...task,
      id: Date.now().toString(),
      createdAt: new Date(),
    };
    tasks.value.push(newTask);
    await saveTasks();
  };

  // Update task
  const updateTask = async (id: string, updates: Partial<Task>) => {
    const index = tasks.value.findIndex(t => t.id === id);
    if (index !== -1) {
      tasks.value[index] = { ...tasks.value[index], ...updates };
      await saveTasks();
    }
  };

  // Delete task
  const deleteTask = async (id: string) => {
    tasks.value = tasks.value.filter(t => t.id !== id);
    await saveTasks();
  };

  // Toggle complete
  const toggleComplete = async (id: string) => {
    const task = tasks.value.find(t => t.id === id);
    if (task) {
      task.completed = !task.completed;
      await saveTasks();
    }
  };

  return {
    tasks,
    totalTasks,
    completedTasks,
    pendingTasks,
    todayTasks,
    loadTasks,
    addTask,
    updateTask,
    deleteTask,
    toggleComplete,
  };
});
```

---

### Langkah 3: Notes Store

File: `src/stores/notesStore.ts`

```typescript
import { defineStore } from 'pinia';
import { ref } from 'vue';
import { Note } from '@/models';
import { StorageService, STORAGE_KEYS } from '@/services/storage/storageService';

export const useNotesStore = defineStore('notes', () => {
  const notes = ref<Note[]>([]);

  // Load notes
  const loadNotes = async () => {
    const savedNotes = await StorageService.get<Note[]>(STORAGE_KEYS.NOTES);
    if (savedNotes) {
      notes.value = savedNotes;
    }
  };

  // Save notes
  const saveNotes = async () => {
    await StorageService.set(STORAGE_KEYS.NOTES, notes.value);
  };

  // Add note
  const addNote = async (note: Omit<Note, 'id' | 'createdAt' | 'updatedAt'>) => {
    const newNote: Note = {
      ...note,
      id: Date.now().toString(),
      createdAt: new Date(),
      updatedAt: new Date(),
    };
    notes.value.unshift(newNote);
    await saveNotes();
  };

  // Update note
  const updateNote = async (id: string, updates: Partial<Note>) => {
    const index = notes.value.findIndex(n => n.id === id);
    if (index !== -1) {
      notes.value[index] = {
        ...notes.value[index],
        ...updates,
        updatedAt: new Date(),
      };
      await saveNotes();
    }
  };

  // Delete note
  const deleteNote = async (id: string) => {
    notes.value = notes.value.filter(n => n.id !== id);
    await saveNotes();
  };

  return {
    notes,
    loadNotes,
    addNote,
    updateNote,
    deleteNote,
  };
});
```

---

## 🎨 PRAKTIKUM 4: MEMBUAT UI COMPONENTS

### Langkah 1: Task Card Component

File: `src/components/features/TaskCard.vue`

```vue
<template>
  <ion-card :class="{ 'task-completed': task.completed }">
    <ion-card-content>
      <ion-grid>
        <ion-row class="ion-align-items-center">
          <ion-col size="1">
            <ion-checkbox
              :checked="task.completed"
              @ionChange="$emit('toggle', task.id)"
            ></ion-checkbox>
          </ion-col>
          <ion-col>
            <h3 :class="{ 'text-line-through': task.completed }">
              {{ task.title }}
            </h3>
            <p class="task-description">{{ task.description }}</p>
            <div class="task-meta">
              <ion-chip :color="priorityColor" size="small">
                {{ task.priority }}
              </ion-chip>
              <ion-chip size="small">
                <ion-icon :icon="calendarOutline"></ion-icon>
                {{ formatDate(task.deadline) }}
              </ion-chip>
              <ion-chip :color="categoryColor" size="small">
                {{ task.category }}
              </ion-chip>
            </div>
          </ion-col>
          <ion-col size="auto">
            <ion-button fill="clear" @click="$emit('delete', task.id)">
              <ion-icon :icon="trashOutline" color="danger"></ion-icon>
            </ion-button>
          </ion-col>
        </ion-row>
      </ion-grid>
    </ion-card-content>
  </ion-card>
</template>

<script setup lang="ts">
import { computed } from 'vue';
import { format } from 'date-fns';
import { id as idLocale } from 'date-fns/locale';
import { Task } from '@/models';
import {
  IonCard,
  IonCardContent,
  IonGrid,
  IonRow,
  IonCol,
  IonCheckbox,
  IonChip,
  IonIcon,
  IonButton,
} from '@ionic/vue';
import { calendarOutline, trashOutline } from 'ionicons/icons';

interface Props {
  task: Task;
}

const props = defineProps<Props>();
defineEmits<{
  (e: 'toggle', id: string): void;
  (e: 'delete', id: string): void;
}>();

const priorityColor = computed(() => {
  const colors = {
    low: 'success',
    medium: 'warning',
    high: 'danger',
  };
  return colors[props.task.priority];
});

const categoryColor = computed(() => {
  const colors = {
    kuliah: 'primary',
    tugas: 'secondary',
    ujian: 'danger',
    lainnya: 'medium',
  };
  return colors[props.task.category];
});

const formatDate = (date: Date) => {
  return format(new Date(date), 'dd MMM yyyy', { locale: idLocale });
};
</script>

<style scoped>
.task-completed {
  opacity: 0.6;
}

.text-line-through {
  text-decoration: line-through;
}

h3 {
  margin: 0 0 5px 0;
  font-size: 16px;
}

.task-description {
  margin: 0 0 10px 0;
  font-size: 14px;
  color: #666;
}

.task-meta {
  display: flex;
  gap: 5px;
  flex-wrap: wrap;
}
</style>
```

---

### Langkah 2: News Card Component

File: `src/components/features/NewsCard.vue`

```vue
<template>
  <ion-card button @click="$emit('click', article.id)">
    <img :src="article.image" :alt="article.title" />
    <ion-card-header>
      <ion-chip :color="categoryColor" size="small">
        {{ article.category }}
      </ion-chip>
      <ion-card-title>{{ article.title }}</ion-card-title>
      <ion-card-subtitle>
        {{ article.author }} • {{ formatDate(article.publishedAt) }}
      </ion-card-subtitle>
    </ion-card-header>
    <ion-card-content>
      {{ article.excerpt }}
    </ion-card-content>
  </ion-card>
</template>

<script setup lang="ts">
import { computed } from 'vue';
import { format } from 'date-fns';
import { id as idLocale } from 'date-fns/locale';
import { Article } from '@/models';
import {
  IonCard,
  IonCardHeader,
  IonCardTitle,
  IonCardSubtitle,
  IonCardContent,
  IonChip,
} from '@ionic/vue';

interface Props {
  article: Article;
}

const props = defineProps<Props>();
defineEmits<{
  (e: 'click', id: number): void;
}>();

const categoryColor = computed(() => {
  const colors: { [key: string]: string } = {
    'Pengumuman': 'primary',
    'Event': 'secondary',
    'Beasiswa': 'success',
  };
  return colors[props.article.category] || 'medium';
});

const formatDate = (date: Date) => {
  return format(new Date(date), 'dd MMM yyyy', { locale: idLocale });
};
</script>

<style scoped>
img {
  width: 100%;
  height: 200px;
  object-fit: cover;
}

ion-card-title {
  font-size: 18px;
  margin-top: 10px;
}
</style>
```

---

## 📱 PRAKTIKUM 5: MEMBUAT HALAMAN APLIKASI

### Halaman Dashboard (Home)

File: `src/views/HomePage.vue`

```vue
<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Kampus Kita</ion-title>
        <ion-buttons slot="end">
          <ion-button @click="refreshData">
            <ion-icon :icon="refreshOutline"></ion-icon>
          </ion-button>
        </ion-buttons>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-refresher slot="fixed" @ionRefresh="handleRefresh($event)">
        <ion-refresher-content></ion-refresher-content>
      </ion-refresher>

      <div class="ion-padding">
        <!-- Welcome Section -->
        <ion-card color="primary">
          <ion-card-content>
            <h2>Halo, {{ userName }}! 👋</h2>
            <p>{{ greeting }}</p>
          </ion-card-content>
        </ion-card>

        <!-- Quick Stats -->
        <h3>Ringkasan Hari Ini</h3>
        <ion-grid>
          <ion-row>
            <ion-col size="6">
              <ion-card color="success">
                <ion-card-content class="stat-card">
                  <ion-icon :icon="checkmarkDoneOutline" style="font-size: 32px;"></ion-icon>
                  <h3>{{ tasksStore.completedTasks }}</h3>
                  <p>Tugas Selesai</p>
                </ion-card-content>
              </ion-card>
            </ion-col>
            <ion-col size="6">
              <ion-card color="warning">
                <ion-card-content class="stat-card">
                  <ion-icon :icon="timeOutline" style="font-size: 32px;"></ion-icon>
                  <h3>{{ tasksStore.pendingTasks }}</h3>
                  <p>Tugas Pending</p>
                </ion-card-content>
              </ion-card>
            </ion-col>
          </ion-row>
        </ion-grid>

        <!-- Weather Widget -->
        <h3>Cuaca Kampus</h3>
        <ion-card v-if="weather">
          <ion-card-content>
            <ion-grid>
              <ion-row class="ion-align-items-center">
                <ion-col size="4">
                  <ion-icon :icon="getWeatherIcon(weather.icon)" style="font-size: 64px; color: #FFA500;"></ion-icon>
                </ion-col>
                <ion-col>
                  <h2>{{ weather.temperature }}°C</h2>
                  <p>{{ weather.description }}</p>
                  <small>Kelembaban: {{ weather.humidity }}%</small>
                </ion-col>
              </ion-row>
            </ion-grid>
          </ion-card-content>
        </ion-card>

        <!-- Today's Tasks -->
        <h3>Tugas Hari Ini</h3>
        <div v-if="tasksStore.todayTasks.length > 0">
          <TaskCard
            v-for="task in tasksStore.todayTasks"
            :key="task.id"
            :task="task"
            @toggle="tasksStore.toggleComplete"
            @delete="handleDeleteTask"
          />
        </div>
        <ion-card v-else>
          <ion-card-content class="ion-text-center">
            <p>Tidak ada tugas untuk hari ini</p>
          </ion-card-content>
        </ion-card>

        <!-- Latest News -->
        <h3>Berita Terbaru</h3>
        <NewsCard
          v-for="article in latestNews"
          :key="article.id"
          :article="article"
          @click="viewArticle"
        />
      </div>
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
  IonButtons,
  IonButton,
  IonIcon,
  IonCard,
  IonCardContent,
  IonGrid,
  IonRow,
  IonCol,
  IonRefresher,
  IonRefresherContent,
  alertController,
} from '@ionic/vue';
import {
  refreshOutline,
  checkmarkDoneOutline,
  timeOutline,
  sunnyOutline,
  cloudyOutline,
  rainyOutline,
} from 'ionicons/icons';
import { useUserStore } from '@/stores/userStore';
import { useTasksStore } from '@/stores/tasksStore';
import { WeatherService } from '@/services/api/weatherService';
import { NewsService } from '@/services/api/newsService';
import { Weather, Article } from '@/models';
import TaskCard from '@/components/features/TaskCard.vue';
import NewsCard from '@/components/features/NewsCard.vue';

const router = useRouter();
const userStore = useUserStore();
const tasksStore = useTasksStore();

const weather = ref<Weather | null>(null);
const latestNews = ref<Article[]>([]);

const userName = computed(() => userStore.user?.name || 'Mahasiswa');
const greeting = computed(() => {
  const hour = new Date().getHours();
  if (hour < 12) return 'Selamat pagi! Semangat kuliah hari ini!';
  if (hour < 18) return 'Selamat siang! Tetap semangat!';
  return 'Selamat malam! Jangan lupa istirahat ya!';
});

const getWeatherIcon = (icon: string) => {
  const icons: { [key: string]: any } = {
    sunny: sunnyOutline,
    cloudy: cloudyOutline,
    rainy: rainyOutline,
  };
  return icons[icon] || cloudyOutline;
};

const loadData = async () => {
  try {
    // Load weather
    weather.value = await WeatherService.getWeatherByCity('samarinda');

    // Load news
    const articles = await NewsService.getArticles();
    latestNews.value = articles.slice(0, 3);
  } catch (error) {
    console.error('Error loading data:', error);
  }
};

const refreshData = () => {
  loadData();
};

const handleRefresh = async (event: any) => {
  await loadData();
  event.target.complete();
};

const handleDeleteTask = async (id: string) => {
  const alert = await alertController.create({
    header: 'Konfirmasi',
    message: 'Yakin ingin menghapus tugas ini?',
    buttons: [
      { text: 'Batal', role: 'cancel' },
      {
        text: 'Hapus',
        role: 'destructive',
        handler: () => {
          tasksStore.deleteTask(id);
        },
      },
    ],
  });
  await alert.present();
};

const viewArticle = (id: number) => {
  router.push(`/article/${id}`);
};

onMounted(() => {
  loadData();
});
</script>

<style scoped>
h2 {
  margin: 0;
  font-size: 24px;
  color: white;
}

h3 {
  margin: 30px 0 15px 0;
  color: #333;
}

.stat-card {
  text-align: center;
  padding: 15px;
  color: white;
}

.stat-card h3 {
  font-size: 36px;
  margin: 10px 0 5px 0;
  color: white;
}

.stat-card p {
  margin: 0;
  opacity: 0.9;
}
</style>
```

---

## ⚡ PRAKTIKUM 6: OPTIMASI & BEST PRACTICES

### 1. Lazy Loading Components

```typescript
// router/index.ts
const routes = [
  {
    path: '/tasks',
    component: () => import('@/views/TasksPage.vue'), // Lazy load
  },
];
```

### 2. Image Optimization

```vue
<!-- Gunakan loading lazy dan placeholder -->
<img
  :src="imageUrl"
  loading="lazy"
  :alt="alt"
  @error="handleImageError"
/>
```

### 3. Debounce Search

File: `src/utils/debounce.ts`

```typescript
export function debounce<T extends (...args: any[]) => any>(
  func: T,
  wait: number
): (...args: Parameters<T>) => void {
  let timeout: ReturnType<typeof setTimeout>;
  return function(...args: Parameters<T>) {
    clearTimeout(timeout);
    timeout = setTimeout(() => func(...args), wait);
  };
}
```

### 4. Error Boundary

File: `src/utils/errorHandler.ts`

```typescript
import { toastController } from '@ionic/vue';

export async function showError(message: string) {
  const toast = await toastController.create({
    message,
    duration: 3000,
    position: 'top',
    color: 'danger',
  });
  await toast.present();
}

export function handleError(error: any) {
  console.error('Error:', error);
  showError(error.message || 'Terjadi kesalahan');
}
```

---

## 🧪 PRAKTIKUM 7: TESTING

### Unit Test dengan Vitest

Install:
```bash
npm install -D vitest @vue/test-utils happy-dom
```

File: `tests/unit/tasksStore.spec.ts`

```typescript
import { describe, it, expect, beforeEach } from 'vitest';
import { setActivePinia, createPinia } from 'pinia';
import { useTasksStore } from '@/stores/tasksStore';

describe('Tasks Store', () => {
  beforeEach(() => {
    setActivePinia(createPinia());
  });

  it('should add task', async () => {
    const store = useTasksStore();
    await store.addTask({
      title: 'Test Task',
      description: 'Test Description',
      deadline: new Date(),
      priority: 'high',
      completed: false,
      category: 'tugas',
    });

    expect(store.tasks.length).toBe(1);
    expect(store.tasks[0].title).toBe('Test Task');
  });

  it('should toggle task completion', async () => {
    const store = useTasksStore();
    await store.addTask({
      title: 'Test Task',
      description: 'Test Description',
      deadline: new Date(),
      priority: 'high',
      completed: false,
      category: 'tugas',
    });

    const taskId = store.tasks[0].id;
    await store.toggleComplete(taskId);

    expect(store.tasks[0].completed).toBe(true);
  });
});
```

Run tests:
```bash
npm run test
```

---

## 📦 PRAKTIKUM 8: BUILD & DEPLOYMENT

### Langkah 1: Optimize for Production

File: `vite.config.ts`

```typescript
import { defineConfig } from 'vite';
import vue from '@vitejs/plugin-vue';
import { VitePWA } from 'vite-plugin-pwa';

export default defineConfig({
  plugins: [
    vue(),
    VitePWA({
      registerType: 'autoUpdate',
      manifest: {
        name: 'Kampus Kita',
        short_name: 'KampusKita',
        description: 'Aplikasi Mahasiswa Terpadu',
        theme_color: '#3880ff',
        icons: [
          {
            src: 'icon-192.png',
            sizes: '192x192',
            type: 'image/png',
          },
          {
            src: 'icon-512.png',
            sizes: '512x512',
            type: 'image/png',
          },
        ],
      },
    }),
  ],
  build: {
    minify: 'terser',
    terserOptions: {
      compress: {
        drop_console: true, // Remove console.log in production
      },
    },
    rollupOptions: {
      output: {
        manualChunks: {
          'ionic': ['@ionic/vue'],
          'vue': ['vue', 'vue-router', 'pinia'],
        },
      },
    },
  },
});
```

---

### Langkah 2: Persiapan Release

1. **Update version di package.json**
```json
{
  "version": "1.0.0"
}
```

2. **Update app info di capacitor.config.ts**
```typescript
{
  appId: 'com.kampuskita.app',
  appName: 'Kampus Kita',
  webDir: 'dist',
  bundledWebRuntime: false
}
```

3. **Update AndroidManifest.xml**
```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.kampuskita.app"
    android:versionCode="1"
    android:versionName="1.0.0">

    <application
        android:label="Kampus Kita"
        android:icon="@mipmap/ic_launcher"
        android:roundIcon="@mipmap/ic_launcher_round">
    </application>
</manifest>
```

---

### Langkah 3: Generate Icons & Splash Screen

Install:
```bash
npm install -D @capacitor/assets
```

Siapkan file:
- `resources/icon.png` (1024x1024px)
- `resources/splash.png` (2732x2732px)

Generate:
```bash
npx capacitor-assets generate
```

---

### Langkah 4: Build APK Release

```bash
# Build web assets
npm run build

# Sync to Android
npx cap sync android

# Open Android Studio
npx cap open android
```

Di Android Studio:
1. **Build → Generate Signed Bundle / APK**
2. **APK**
3. Pilih/buat keystore
4. **Release build type**
5. **Build**

APK ada di: `android/app/release/app-release.apk`

---

### Langkah 5: Testing APK

1. **Install di perangkat**
```bash
adb install android/app/release/app-release.apk
```

2. **Test semua fitur:**
   - Login/Register
   - CRUD operations
   - API calls
   - Native features (camera, GPS)
   - Offline mode
   - Performance

---

## 📚 DOKUMENTASI PROJECT

### README.md

Buat file `README.md` di root project:

```markdown
# Kampus Kita - Aplikasi Mahasiswa Terpadu

Aplikasi mobile untuk mahasiswa yang mengintegrasikan manajemen tugas, informasi akademik, cuaca, dan fitur native.

## Fitur

- 📝 Manajemen Tugas dengan reminder
- 📰 Berita & Pengumuman Kampus
- 🌤️ Info Cuaca Real-time
- 📍 Geolocation & Navigasi
- 📷 Upload Foto Profil
- 💾 Offline-first Storage
- 🔔 Notifikasi Lokal

## Teknologi

- **Framework**: Ionic 7 + Vue 3
- **Language**: TypeScript
- **State Management**: Pinia
- **HTTP Client**: Axios
- **Build Tool**: Vite
- **Mobile**: Capacitor

## Instalasi

\`\`\`bash
# Clone repository
git clone https://github.com/username/kampus-kita.git

# Install dependencies
cd kampus-kita
npm install

# Run di browser
ionic serve

# Build untuk Android
npm run build
npx cap sync android
npx cap open android
\`\`\`

## Struktur Project

\`\`\`
src/
├── components/      # Reusable components
├── stores/          # Pinia stores
├── services/        # API & native services
├── views/           # Pages
├── models/          # TypeScript interfaces
└── utils/           # Helper functions
\`\`\`

## API

- Weather: Open-Meteo API
- News: Mock data (dapat diganti dengan API kampus)

## License

MIT License

## Author

Anton Prafanto, S.Kom, M.T.
```

---

## 🎯 CHECKLIST PROJECT COMPLETION

### Functionality ✅
- [ ] User authentication & profile
- [ ] CRUD operations (Tasks, Notes)
- [ ] API integration (Weather, News)
- [ ] Native features (Camera, GPS, Storage)
- [ ] Offline support
- [ ] Notifications
- [ ] Search & filter
- [ ] Data persistence

### UI/UX ✅
- [ ] Responsive design
- [ ] Loading states
- [ ] Error handling
- [ ] Empty states
- [ ] Smooth animations
- [ ] Consistent theme
- [ ] Accessibility

### Performance ✅
- [ ] Lazy loading
- [ ] Image optimization
- [ ] Code splitting
- [ ] Debounced search
- [ ] Minimal re-renders

### Quality ✅
- [ ] TypeScript strict mode
- [ ] ESLint configured
- [ ] Unit tests (>70% coverage)
- [ ] No console errors
- [ ] Proper error handling

### Build & Deploy ✅
- [ ] Production build successful
- [ ] APK generated
- [ ] Tested on real device
- [ ] All features working
- [ ] Performance optimized

### Documentation ✅
- [ ] README.md complete
- [ ] Code comments
- [ ] API documentation
- [ ] User guide

---

## 📝 LAPORAN PROJECT

### Template Laporan

```
LAPORAN PROJECT AKHIR
Mata Kuliah: Pemrograman Berbasis Perangkat Bergerak

IDENTITAS MAHASISWA
Nama        : [Nama Lengkap]
NIM         : [NIM]
Program Studi : Sistem Informasi
Universitas : Universitas Terbuka

INFORMASI APLIKASI
Nama Aplikasi : [Nama Aplikasi]
Deskripsi     : [Deskripsi singkat]
Platform      : Android
Framework     : Ionic + Vue.js

FITUR UTAMA
1. [Fitur 1]
2. [Fitur 2]
3. [Fitur 3]
...

TEKNOLOGI YANG DIGUNAKAN
- Frontend: Vue.js 3, TypeScript
- Framework Mobile: Ionic 7
- State Management: Pinia
- API: Axios
- Native: Capacitor
- Database: Local Storage (Preferences)

SCREENSHOT APLIKASI
[Lampirkan 5-10 screenshot]

LINK REPOSITORY
GitHub: [URL]

LINK APK
Google Drive: [URL]

LINK VIDEO DEMO
YouTube: [URL]

TANTANGAN & SOLUSI
[Jelaskan tantangan yang dihadapi dan bagaimana solusinya]

KESIMPULAN
[Kesimpulan dan pembelajaran yang didapat]
```

---

## 🎓 EVALUASI AKHIR

### Kriteria Penilaian

1. **Functionality (40%)**
   - Kelengkapan fitur
   - Fitur bekerja dengan baik
   - Error handling

2. **Code Quality (25%)**
   - Clean code
   - TypeScript usage
   - Best practices
   - Code organization

3. **UI/UX (20%)**
   - Design menarik
   - User-friendly
   - Responsive
   - Consistent

4. **Documentation (10%)**
   - README lengkap
   - Code comments
   - User guide

5. **Presentation (5%)**
   - Video demo jelas
   - Penjelasan konsep

---

## 📧 PENUTUP

Selamat! Anda telah menyelesaikan seluruh rangkaian praktikum Pemrograman Berbasis Perangkat Bergerak!

### Apa Selanjutnya?

1. **Publish ke Play Store**
   - Buat akun Google Play Developer
   - Siapkan asset (icon, screenshots, deskripsi)
   - Upload APK/AAB
   - Submit untuk review

2. **Tingkatkan Skill**
   - Pelajari animasi advanced
   - Eksplorasi plugins lainnya
   - Implementasi backend sendiri
   - Belajar iOS development

3. **Bangun Portfolio**
   - Deploy web version
   - Buat case study
   - Bagikan di LinkedIn/GitHub
   - Dapatkan feedback

**Terima kasih telah mengikuti pembelajaran ini dengan serius!**
**Semoga sukses dalam berkarya dan mengembangkan aplikasi mobile!**

---

**Disusun oleh:**
Anton Prafanto, S.Kom, M.T.
Dosen Program Studi Informatika
Universitas Mulawarman
Tutor Universitas Terbuka

**Mata Kuliah:** Pemrograman Berbasis Perangkat Bergerak (MSIM4401)
**Tahun:** 2025


---

# 🧑‍🏫 PENGAYAAN PROJECT AKHIR PERTEMUAN 14

Bagian ini membantu tutor menjelaskan project akhir secara bertahap selama **6–8 jam**, bukan langsung menampilkan aplikasi besar. Strateginya adalah mengembangkan satu use case dari versi minimal sampai versi terintegrasi.

## A. Hubungan Project “Kampus Kita” dengan Aplikasi Terintegrasi pada Materi UT

Materi UT menekankan alur aplikasi yang:
1. menyiapkan data user,
2. menampilkan login,
3. mempertahankan status login,
4. menampilkan halaman utama,
5. memanggil kamera,
6. mengambil waktu dan lokasi,
7. menyimpan/mengelola data,
8. kemudian menghasilkan aplikasi Android.

Pada project ini konsep tersebut diperluas menjadi arsitektur yang lebih modular:

~~~text
UI / Views
   |
   v
Reusable Components
   |
   v
Pinia Stores -------- Router Guard
   |
   v
Services
 |      |       |
API   Storage  Native
 |      |       |
HTTP  Local    Camera/GPS
~~~

### Pesan utama
Teknologi dapat berubah, tetapi konsepnya tetap:
- centralized state,
- pemisahan tanggung jawab,
- persistensi,
- native capability,
- asynchronous workflow,
- error handling.

---

## B. Milestone Project Agar Mudah Dijelaskan

| Milestone | Fitur | Konsep utama |
|---|---|---|
| M1 | Shell aplikasi + route | struktur project |
| M2 | Login dummy | reactive state |
| M3 | Route guard | navigation control |
| M4 | Profil tersimpan | local persistence |
| M5 | Ambil foto profil | Camera |
| M6 | Ambil lokasi | Geolocation |
| M7 | Data REST API | service layer |
| M8 | Offline queue | offline-first |
| M9 | Testing | quality |
| M10 | Build APK | deployment |

Tutor dapat berhenti di setiap milestone dan meminta mahasiswa menjelaskan “data berpindah dari mana ke mana”.

---

## C. Model Domain yang Lebih Terstruktur

Buat **src/models/index.ts**:

~~~ts
export interface StudentProfile {
  id: string;
  name: string;
  nim: string;
  email: string;
  photoDataUrl?: string;
  latitude?: number;
  longitude?: number;
}

export interface CampusTask {
  id: string;
  title: string;
  description: string;
  deadline: string;
  completed: boolean;
  synced: boolean;
}

export interface ApiState<T> {
  loading: boolean;
  data: T | null;
  error: string | null;
}
~~~

### Penjelasan
Interface bukan database dan bukan object runtime. Interface adalah kontrak TypeScript agar struktur data konsisten saat digunakan oleh component, store, dan service.

---

## D. Auth Store Minimal yang Bisa Dijalankan

**src/stores/authStore.ts**

~~~ts
import { defineStore } from 'pinia';
import { computed, ref } from 'vue';

export const useAuthStore = defineStore('auth', () => {
  const username = ref('');
  const fullName = ref('');

  const isLoggedIn = computed(() => username.value.length > 0);

  function login(user: string, name: string) {
    username.value = user;
    fullName.value = name;
  }

  function logout() {
    username.value = '';
    fullName.value = '';
  }

  return {
    username,
    fullName,
    isLoggedIn,
    login,
    logout
  };
});
~~~

Login page:

~~~vue
<script setup lang="ts">
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import { useAuthStore } from '@/stores/authStore';

const user = ref('');
const password = ref('');
const errorMessage = ref('');

const router = useRouter();
const auth = useAuthStore();

async function submitLogin() {
  errorMessage.value = '';

  if (user.value === 'user1' && password.value === 'pass1') {
    auth.login('user1', 'Mahasiswa UT');
    await router.replace('/home');
  } else {
    errorMessage.value = 'Username atau password salah.';
  }
}
</script>
~~~

### Diskusi keamanan
Contoh di atas hanya untuk pembelajaran. Password hard-coded tidak boleh dipakai pada aplikasi produksi. Authentication produksi harus melibatkan server, token/session, hashing password di backend, dan transport HTTPS.

---

## E. Route Guard

~~~ts
import { useAuthStore } from '@/stores/authStore';

router.beforeEach((to) => {
  const auth = useAuthStore();

  if (to.meta.requiresAuth && !auth.isLoggedIn) {
    return {
      path: '/login',
      query: { redirect: to.fullPath }
    };
  }

  if (to.path === '/login' && auth.isLoggedIn) {
    return '/home';
  }

  return true;
});
~~~

Definisi route:

~~~ts
{
  path: '/home',
  component: () => import('@/views/HomePage.vue'),
  meta: { requiresAuth: true }
}
~~~

### Yang dapat dijelaskan
- Guard dieksekusi sebelum navigasi selesai.
- meta menyimpan metadata route.
- query redirect dapat dipakai agar user kembali ke halaman tujuan setelah login.

---

## F. Persistensi Profile dengan Preferences

**src/services/storage/ProfileStorage.ts**

~~~ts
import { Preferences } from '@capacitor/preferences';
import type { StudentProfile } from '@/models';

const KEY = 'student_profile';

export async function saveProfile(profile: StudentProfile) {
  await Preferences.set({
    key: KEY,
    value: JSON.stringify(profile)
  });
}

export async function loadProfile(): Promise<StudentProfile | null> {
  const result = await Preferences.get({ key: KEY });

  if (!result.value) {
    return null;
  }

  return JSON.parse(result.value) as StudentProfile;
}

export async function deleteProfile() {
  await Preferences.remove({ key: KEY });
}
~~~

### Kapan Preferences cukup?
Cocok untuk:
- theme,
- token kecil,
- setting,
- profile sederhana.

Tidak cocok untuk ribuan record dengan relasi dan query kompleks. Untuk itu gunakan SQLite/database.

---

## G. Repository Pattern untuk Data Tugas

**src/repositories/TaskRepository.ts**

~~~ts
import { Preferences } from '@capacitor/preferences';
import type { CampusTask } from '@/models';

const KEY = 'campus_tasks';

export async function findAll(): Promise<CampusTask[]> {
  const result = await Preferences.get({ key: KEY });
  if (!result.value) return [];
  return JSON.parse(result.value) as CampusTask[];
}

export async function saveAll(tasks: CampusTask[]) {
  await Preferences.set({
    key: KEY,
    value: JSON.stringify(tasks)
  });
}
~~~

Store:

~~~ts
import { defineStore } from 'pinia';
import { computed, ref } from 'vue';
import type { CampusTask } from '@/models';
import * as repo from '@/repositories/TaskRepository';

export const useTaskStore = defineStore('task', () => {
  const tasks = ref<CampusTask[]>([]);

  const pending = computed(() =>
    tasks.value.filter(item => !item.completed)
  );

  async function load() {
    tasks.value = await repo.findAll();
  }

  async function add(title: string) {
    tasks.value.push({
      id: crypto.randomUUID(),
      title,
      description: '',
      deadline: new Date().toISOString(),
      completed: false,
      synced: false
    });

    await repo.saveAll(tasks.value);
  }

  async function toggle(id: string) {
    const item = tasks.value.find(task => task.id === id);
    if (!item) return;

    item.completed = !item.completed;
    item.synced = false;
    await repo.saveAll(tasks.value);
  }

  return {
    tasks,
    pending,
    load,
    add,
    toggle
  };
});
~~~

### Penjelasan arsitektur
View tidak perlu tahu apakah data disimpan di Preferences, SQLite, atau REST API. Perubahan storage dapat dilakukan pada repository/service tanpa menulis ulang UI.

---

## H. Native Service — Camera

**src/services/native/CameraService.ts**

~~~ts
import {
  Camera,
  CameraResultType,
  CameraSource
} from '@capacitor/camera';

export async function captureImage(): Promise<string> {
  const permission = await Camera.requestPermissions({
    permissions: ['camera']
  });

  if (permission.camera !== 'granted') {
    throw new Error('Izin kamera tidak diberikan.');
  }

  const photo = await Camera.getPhoto({
    source: CameraSource.Prompt,
    quality: 80,
    allowEditing: true,
    resultType: CameraResultType.DataUrl
  });

  if (!photo.dataUrl) {
    throw new Error('Foto tidak tersedia.');
  }

  return photo.dataUrl;
}
~~~

Gunakan pada profile:

~~~ts
async function changePhoto() {
  try {
    profile.value.photoDataUrl = await captureImage();
    await saveProfile(profile.value);
  } catch (error) {
    console.error(error);
  }
}
~~~

---

## I. Native Service — Geolocation

~~~ts
import { Geolocation } from '@capacitor/geolocation';

export interface GeoResult {
  lat: number;
  lng: number;
  accuracy: number;
}

export async function currentLocation(): Promise<GeoResult> {
  const permission = await Geolocation.requestPermissions();

  if (permission.location !== 'granted' &&
      permission.coarseLocation !== 'granted') {
    throw new Error('Izin lokasi tidak tersedia.');
  }

  const position = await Geolocation.getCurrentPosition({
    enableHighAccuracy: true,
    timeout: 10000
  });

  return {
    lat: position.coords.latitude,
    lng: position.coords.longitude,
    accuracy: position.coords.accuracy
  };
}
~~~

Integrasi ke profile:

~~~ts
async function updateLocation() {
  const geo = await currentLocation();

  profile.value.latitude = geo.lat;
  profile.value.longitude = geo.lng;

  await saveProfile(profile.value);
}
~~~

---

## J. Satu Use Case Terintegrasi: Check-in Kampus

Use case:
1. user login,
2. memilih menu Check-in,
3. mengambil foto,
4. mengambil lokasi,
5. menambahkan waktu,
6. menyimpan lokal,
7. mengirim ke API ketika online.

Model:

~~~ts
export interface CheckInRecord {
  id: string;
  studentId: string;
  imageDataUrl: string;
  latitude: number;
  longitude: number;
  capturedAt: string;
  syncStatus: 'pending' | 'synced' | 'failed';
}
~~~

Use case service:

~~~ts
import { captureImage } from '@/services/native/CameraService';
import { currentLocation } from '@/services/native/LocationService';

export async function createCheckIn(
  studentId: string
): Promise<CheckInRecord> {
  const image = await captureImage();
  const geo = await currentLocation();

  return {
    id: crypto.randomUUID(),
    studentId,
    imageDataUrl: image,
    latitude: geo.lat,
    longitude: geo.lng,
    capturedAt: new Date().toISOString(),
    syncStatus: 'pending'
  };
}
~~~

### Mengapa ini contoh yang baik?
Karena satu tombol melibatkan:
- UI,
- permission,
- camera,
- GPS,
- TypeScript model,
- state,
- persistence,
- potensi sync ke backend.

---

## K. HTTP Client Terpusat

**src/services/api/http.ts**

~~~ts
import axios from 'axios';

export const http = axios.create({
  baseURL: import.meta.env.VITE_API_BASE_URL,
  timeout: 10000,
  headers: {
    'Content-Type': 'application/json'
  }
});
~~~

Environment:

~~~text
VITE_API_BASE_URL=https://jsonplaceholder.typicode.com
~~~

Service:

~~~ts
import { http } from './http';

export interface NewsArticle {
  id: number;
  title: string;
  body: string;
}

export async function fetchNews(): Promise<NewsArticle[]> {
  const response = await http.get<NewsArticle[]>('/posts');
  return response.data.slice(0, 10);
}
~~~

### Poin penjelasan
Base URL, timeout, dan header tidak perlu diulang pada setiap request.

---

## L. Response State Pattern

Daripada hanya punya array data, gunakan state lengkap:

~~~ts
const loading = ref(false);
const error = ref('');
const articles = ref<NewsArticle[]>([]);

async function loadArticles() {
  loading.value = true;
  error.value = '';

  try {
    articles.value = await fetchNews();
  } catch (e) {
    error.value = 'Gagal mengambil berita.';
  } finally {
    loading.value = false;
  }
}
~~~

UI:

~~~vue
<ion-spinner v-if="loading"></ion-spinner>

<ion-text color="danger" v-else-if="error">
  {{ error }}
</ion-text>

<ion-list v-else>
  <ion-item v-for="article in articles" :key="article.id">
    {{ article.title }}
  </ion-item>
</ion-list>
~~~

---

## M. Offline Queue Sederhana

Saat request gagal, simpan operasi yang harus dikirim ulang.

~~~ts
export interface SyncCommand {
  id: string;
  type: 'CREATE_TASK' | 'UPDATE_TASK' | 'CREATE_CHECKIN';
  payload: unknown;
  createdAt: string;
}
~~~

~~~ts
import { Preferences } from '@capacitor/preferences';

const KEY = 'sync_queue';

export async function loadQueue(): Promise<SyncCommand[]> {
  const result = await Preferences.get({ key: KEY });
  return result.value
    ? JSON.parse(result.value) as SyncCommand[]
    : [];
}

export async function enqueue(command: SyncCommand) {
  const queue = await loadQueue();
  queue.push(command);

  await Preferences.set({
    key: KEY,
    value: JSON.stringify(queue)
  });
}
~~~

### Diskusi
Offline-first tidak berarti “semua disimpan lokal saja”. Offline-first berarti aplikasi tetap berguna ketika offline dan mempunyai strategi sinkronisasi ketika koneksi kembali.

---

## N. Network-aware Sync

~~~ts
import { Network } from '@capacitor/network';

export async function isOnline(): Promise<boolean> {
  const status = await Network.getStatus();
  return status.connected;
}
~~~

Listener:

~~~ts
Network.addListener('networkStatusChange', async status => {
  if (status.connected) {
    console.log('Online kembali, proses sync queue');
  }
});
~~~

### Pertanyaan
Apa yang terjadi jika dua device mengubah record yang sama saat offline? Ini masuk ke topik conflict resolution, yang dapat dijelaskan sebagai perluasan lanjutan.

---

## O. Error Handling Terpusat

**src/services/ui/ErrorPresenter.ts**

~~~ts
import { toastController } from '@ionic/vue';

export async function showError(error: unknown) {
  const message =
    error instanceof Error
      ? error.message
      : 'Terjadi kesalahan yang tidak diketahui.';

  const toast = await toastController.create({
    message,
    duration: 3000,
    color: 'danger',
    position: 'top'
  });

  await toast.present();
}
~~~

Gunakan:

~~~ts
try {
  await createCheckIn(studentId);
} catch (error) {
  await showError(error);
}
~~~

---

## P. Loading Overlay untuk Proses Multi-step

~~~ts
import { loadingController } from '@ionic/vue';

async function doCheckIn() {
  const loading = await loadingController.create({
    message: 'Mengambil foto dan lokasi...'
  });

  await loading.present();

  try {
    const record = await createCheckIn(auth.username);
    console.log(record);
  } finally {
    await loading.dismiss();
  }
}
~~~

### Mengapa perlu?
Proses kamera + GPS dapat beberapa detik. Tanpa feedback, user mengira aplikasi hang.

---

## Q. Validasi Form Sederhana Tanpa Library

~~~ts
interface ValidationResult {
  valid: boolean;
  errors: string[];
}

function validateProfile(
  name: string,
  nim: string,
  email: string
): ValidationResult {
  const errors: string[] = [];

  if (name.trim().length < 3) {
    errors.push('Nama minimal 3 karakter.');
  }

  if (nim.trim().length < 5) {
    errors.push('NIM tidak valid.');
  }

  if (!email.includes('@')) {
    errors.push('Email tidak valid.');
  }

  return {
    valid: errors.length === 0,
    errors
  };
}
~~~

Tutor dapat membandingkan validasi manual ini dengan Yup yang digunakan di bagian utama materi.

---

## R. Contoh Unit Test untuk Pure Function

~~~ts
import { describe, expect, it } from 'vitest';
import { validateProfile } from '@/utils/validateProfile';

describe('validateProfile', () => {
  it('menolak email tanpa @', () => {
    const result = validateProfile(
      'Budi',
      '12345678',
      'budi.example.com'
    );

    expect(result.valid).toBe(false);
  });

  it('menerima profile valid', () => {
    const result = validateProfile(
      'Budi Santoso',
      '12345678',
      'budi@example.com'
    );

    expect(result.valid).toBe(true);
  });
});
~~~

### Pesan pedagogis
Mulai testing dari fungsi kecil yang deterministic. Setelah mahasiswa paham, baru uji store/component.

---

## S. Test Store Pinia

~~~ts
import { beforeEach, describe, expect, it } from 'vitest';
import { createPinia, setActivePinia } from 'pinia';
import { useAuthStore } from '@/stores/authStore';

describe('authStore', () => {
  beforeEach(() => {
    setActivePinia(createPinia());
  });

  it('login mengubah status', () => {
    const store = useAuthStore();

    store.login('user1', 'Mahasiswa UT');

    expect(store.isLoggedIn).toBe(true);
    expect(store.fullName).toBe('Mahasiswa UT');
  });

  it('logout membersihkan state', () => {
    const store = useAuthStore();

    store.login('user1', 'Mahasiswa UT');
    store.logout();

    expect(store.isLoggedIn).toBe(false);
  });
});
~~~

---

## T. Checklist Arsitektur Sebelum Build

- View tidak memanggil Camera API langsung jika dapat dipisah ke native service.
- HTTP tidak ditulis berulang di setiap component.
- Store tidak menyimpan object DOM.
- Password tidak disimpan plain text.
- API base URL berada di environment variable.
- Permission hanya yang diperlukan.
- Loading dan error state tersedia.
- Route yang butuh login diberi guard.
- Local storage punya schema/data model yang jelas.
- Image besar tidak disimpan sembarangan sebagai Base64.

---

## U. Build Debug APK

~~~bash
npm run build
npx cap sync android
npx cap open android
~~~

Atau command line:

~~~bash
cd android
gradlew.bat assembleDebug
~~~

macOS/Linux:

~~~bash
cd android
./gradlew assembleDebug
~~~

Install:

~~~bash
adb install -r android/app/build/outputs/apk/debug/app-debug.apk
~~~

---

## V. Production-readiness Discussion

Sebelum menyebut aplikasi “production-ready”, diskusikan aspek berikut:

1. **Security** — authentication, authorization, secure storage.
2. **Privacy** — camera/location merupakan data sensitif.
3. **Reliability** — retry, timeout, offline handling.
4. **Observability** — logging dan crash reporting.
5. **Performance** — image size, lazy loading, network payload.
6. **Accessibility** — label, contrast, touch target.
7. **Testing** — unit/integration/device testing.
8. **Release** — signing, versioning, Play Console policy.

---

# 🧩 DEMO END-TO-END UNTUK PRESENTASI

Tutor dapat mendemonstrasikan alur berikut:

~~~text
1. Buka aplikasi
2. Login
3. Route guard membuka Home
4. Home membaca store
5. Buka Profile
6. Ambil foto
7. Ambil lokasi
8. Simpan profile lokal
9. Tambah tugas
10. Putuskan internet
11. Tambah tugas lagi
12. Tandai operasi pending
13. Hubungkan internet
14. Simulasikan sync
15. Logout
16. Coba akses /home
17. Route guard mengembalikan ke /login
18. Build APK
~~~

Setiap langkah dapat dijadikan pertanyaan:
- state berada di mana?
- data disimpan di mana?
- proses asynchronous mana?
- apa kemungkinan gagal?
- error ditampilkan di mana?

---

# ⏱️ SKENARIO 420 MENIT

| Durasi | Materi |
|---|---|
| 0–30 | Review arsitektur dari Pertemuan 6 dan 10 |
| 30–70 | Struktur project, model, router |
| 70–110 | Auth store + route guard |
| 110–150 | Profile + persistence |
| 150–190 | Camera |
| 190–230 | Geolocation |
| 230–275 | REST API + loading/error |
| 275–320 | Offline queue + network status |
| 320–350 | Reusable services + error presenter |
| 350–380 | Unit testing |
| 380–405 | Build APK |
| 405–420 | Demo end-to-end dan review |

---

# 🎓 PERTANYAAN VIVA / DISKUSI AKHIR

1. **Mengapa perlu store jika sudah ada local storage?**  
   Store untuk state reaktif saat aplikasi berjalan; local storage untuk persistensi lintas restart.

2. **Mengapa service layer penting?**  
   Memisahkan detail integrasi dari UI, meningkatkan reuse dan testability.

3. **Apakah route guard adalah sistem keamanan penuh?**  
   Tidak. Guard hanya kontrol navigasi client; authorization tetap harus dipastikan backend.

4. **Apa beda online-first dan offline-first?**  
   Online-first bergantung pada server saat operasi; offline-first mempertahankan fungsi inti secara lokal dan melakukan sinkronisasi.

5. **Mengapa Camera dan Geolocation perlu error handling khusus?**  
   User dapat menolak permission, hardware dapat tidak tersedia, atau sensor dapat gagal/timeout.

6. **Mengapa image DataUrl kurang ideal untuk jumlah besar?**  
   Ukuran data membesar dan konsumsi memori/storage tinggi.

7. **Kapan SQLite lebih tepat daripada Preferences?**  
   Saat record banyak, membutuhkan query/filter, struktur tabel, transaksi, dan relasi.

---

# ✅ DEFINITION OF DONE PROJECT AKHIR

Project dianggap selesai jika:

- [ ] Aplikasi dapat dijalankan dengan ionic serve.
- [ ] Routing dan navigation bekerja.
- [ ] Login state dipertahankan selama session.
- [ ] Route guard bekerja.
- [ ] Data penting dapat dipersist.
- [ ] REST API mempunyai loading/error state.
- [ ] Native camera bekerja.
- [ ] Native geolocation bekerja.
- [ ] Permission failure ditangani.
- [ ] Minimal satu reusable component tersedia.
- [ ] Minimal satu service layer tersedia.
- [ ] Minimal satu store tersedia.
- [ ] Minimal dua unit test lulus.
- [ ] npm run build berhasil.
- [ ] npx cap sync android berhasil.
- [ ] APK debug berhasil dibuat.
- [ ] APK diuji pada emulator/device.
- [ ] README menjelaskan instalasi dan penggunaan.
- [ ] Screenshot dan video demo tersedia.

