# KupasTarif Engine – Business Logic Repository

Core calculation dan business logic engine untuk aplikasi KupasTarif. Repository ini berisi semua algoritma perhitungan tarif, validasi, dan data processing.

## 📁 Struktur

```
engine/
├── 01data.js           # Data & database management
├── 02valid.js          # Validation logic
├── 03fare.js           # Fare calculation
├── 04cost.js           # Cost calculation & analysis
├── 05extra.js          # Extra charges & add-ons
├── 06api.js            # API integration & external services
├── 07cache.js          # Caching mechanism
├── README.md           # Documentation
└── engine.txt          # Raw engine documentation
```

## 🧮 Module Overview

### 01data.js – Data Management
Mengelola data struktur aplikasi:
- Data tarif dari berbagai provider
- Database pricing rules
- Historical data storage
- Data validation schemas

### 02valid.js – Validation
Validasi input dan business logic:
- Validasi lokasi (coordinates)
- Validasi jarak (distance bounds)
- Validasi waktu perjalanan
- Validasi data pengemudi
- Validasi penumpang profile

### 03fare.js – Fare Calculation
Kalkulasi tarif utama:
- Base fare calculation
- Distance-based pricing
- Time-based surcharges
- Dynamic pricing algorithms
- Multi-provider fare comparison

### 04cost.js – Cost Analysis
Analisis biaya operasional:
- Fuel cost calculation
- Maintenance cost estimation
- Insurance cost breakdown
- Depreciation calculation
- Profit/loss analysis

### 05extra.js – Extra Charges
Biaya tambahan:
- Surge pricing
- Peak hour multipliers
- Tolls & road taxes
- Waiting time charges
- Cancellation fees
- Promotion/discount application

### 06api.js – API Integration
Integrasi dengan service eksternal:
- Google Maps API (routing, distance)
- Weather API (conditions impact)
- Real-time pricing updates
- Provider API integration
- Data synchronization

### 07cache.js – Caching
Optimasi performance:
- Calculation result caching
- API response caching
- Cache invalidation strategy
- Cache size management
- TTL (Time-To-Live) configuration

## 🔄 Data Flow

```
User Input
    ↓
02valid.js (Validasi)
    ↓
01data.js (Load Data)
    ↓
03fare.js (Hitung Tarif)
    ↓
04cost.js (Analisis Biaya)
    ↓
05extra.js (Tambah Extra)
    ↓
06api.js (External Data)
    ↓
07cache.js (Cache Result)
    ↓
Output ke UI
```

## 💾 Caching Strategy

```javascript
// Cache hierarchy
1. Memory cache (07cache.js) – fastest
2. IndexedDB (browser) – persistent
3. API calls – slowest, cached aggressively
4. Geolocation data – cached with short TTL
```

## 🔌 Usage in SPA

Module di-import di halaman yang relevan:

```javascript
// Contoh di pages/result.js
import { calculateFare } from '../../../engine/03fare.js';
import { calculateCost } from '../../../engine/04cost.js';
import { validateInput } from '../../../engine/02valid.js';

// Validation
const validation = await validateInput(data);

// Calculation
const fare = await calculateFare(route, distance, time);
const cost = await calculateCost(fare, vehicle);

// Display result
displayResult({ fare, cost, validation });
```

## 🎯 Key Features

### Multi-Provider Support
- Gojek pricing model
- Grab pricing model
- Indriver model
- Custom pricing rules

### Smart Caching
- Automatic cache busting
- Cache warming for frequent routes
- Smart prefetch untuk predictable patterns

### Real-time Updates
- Live price monitoring
- Dynamic surge pricing
- Weather impact calculation

### Analytics
- Fare history tracking
- Cost trend analysis
- Provider comparison
- Profit maximization hints

## 📊 Performance Optimization

- Lazy loading modules
- Async calculation processing
- Worker threads untuk heavy computation
- Memoization untuk repeated calculations

## 🔐 Data Privacy

- No external data transmission (unless API call)
- Local calculation preferentially
- Cache isolated per user (browser)
- No personal data logging

## 📱 Platform Support

- Web browser (modern)
- Android app via Capacitor
- Offline-capable architecture
- IndexedDB support required

## 🧪 Testing

Module dapat ditest independen:

```javascript
import { calculateFare } from './03fare.js';

const testResult = calculateFare(
  { origin: [0, 0], destination: [1, 1] },
  5.2,  // distance in km
  840   // time in seconds
);

console.log(testResult);
```

## 🔗 Related Repositories

- **apk** (root): https://github.com/kupastarif/apk
- **spa** (UI): https://github.com/kupastarif/spa

## 📄 Additional Documentation

- `engine.txt` – Detailed technical documentation
- Inline code comments for algorithm explanations

---

**Created**: July 2026  
**Maintained by**: Kupas⚡Tarif Team

---

**Note**: Semua kalkulasi dilakukan secara transparan untuk memberikan edukasi kepada driver ojek online tentang bagaimana sistem pricing bekerja.
