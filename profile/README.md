# ANKA: Hibrit BLE 5.0 ve Wi-Fi FTM Tabanlı Şebekesiz Afetzede Konumlandırma Sistemi

<p align="center">
  <img src="https://img.shields.io/badge/TÜBİTAK-2209--B%20Destekli-blue?style=for-the-badge" alt="TÜBİTAK 2209-B" />
  <img src="https://img.shields.io/badge/Platform-Android-green?style=for-the-badge&logo=android" alt="Android" />
  <img src="https://img.shields.io/badge/Framework-Flutter-02569B?style=for-the-badge&logo=flutter" alt="Flutter" />
  <img src="https://img.shields.io/badge/Standard-IEEE%20802.11mc%20%7C%20BLE%205.0-orange?style=for-the-badge" alt="Standards" />
</p>

---

## 📌 Proje Özeti
Deprem ve benzeri büyük afetlerde hücresel baz istasyonlarının ve internet altyapısının çökmesi, kritik **ilk 72 saatte** enkaz altındaki kişilerin tespitini güçleştirmektedir. 

**ANKA**, harici hiçbir donanım veya altyapıya ihtiyaç duymadan, yalnızca standart akıllı telefon donanımlarını kullanarak:
1. **Sensör Füzyonu** ile enkaz durumunu otomatik algılar.
2. Düşük güç tüketimli **BLE 5.0 Mesh** ağı ile çok zıplamalı (multi-hop) "Hayat Sinyali" yayını yapar.
3. Kurtarma ekibi 1 zıplama mesafesine ulaştığında devreye giren **Wi-Fi FTM (Fine Time Measurement / ToF)** teknolojisi ile metre altı doğrulukta nokta atışı mesafe tahmini sunar.

> Bu proje, **TÜBİTAK 2209-B Sanayiye Yönelik Lisans Araştırma Projeleri Desteği Programı** kapsamında, **Sakarya Üniversitesi** ve **ARGEDE Bilişim** iş birliği ile yürütülmektedir.

---

## 🏗️ Mimari ve Çalışma Prensibi

```
[ Enkaz Modu Tetikleme ]
  ├── İvmeölçer (Şiddetli darbe + Hareketsizlik)
  ├── Işık Sensörü (Ortam lux ≈ 0)
  ├── Yakınlık Sensörü (Sürekli blokaj)
  └── Şebeke Kontrolü (Hücresel & Wi-Fi sinyali yok)
            │
            ▼
[ BLE 5.0 Mesh Ağı (D2D Yayılımı) ]
  └── Paket: [ ID | Pil % | Hane Kişi Sayısı | Zıplama (Hop) | RSSI ]
            │
            ▼ (1 Zıplama Mesafesine Girildiğinde)
[ Wi-Fi FTM (IEEE 802.11mc ToF Modülü) ]
  └── Kurtarma ekibi arayüzünde metre hassasiyetinde mesafe hesabı
```

### 📱 Geliştirilen Modüller

| Modül | Görev | Hedef Platform / Teknoloji |
| :--- | :--- | :--- |
| **Anka: Hayat Sinyali** | Enkaz altı sensör füzyonu, arka plan Foreground Service yönetimi, BLE Peripheral yayını. | Flutter / Android Native (Foreground Service) |
| **Anka: Yardım Eli** | BLE Central taraması, mesh tablosu görselleştirme, Wi-Fi RTT/FTM mesafe takibi. | Flutter / Android Ranging APIs (Wi-Fi RTT) |

---

## 🛠️ Teknolojik Altyapı
- **Mobil Arayüz:** Flutter / Dart
- **Yerel Servisler:** Android Native (Java/Kotlin) BLE Advertising & Scanning API
- **Mesafe Ölçümü:** Android `WifiRttManager` (IEEE 802.11mc FTM protokolü)
- **Arka Plan Yönetimi:** Android Foreground Service (Kalıcı bildirim mekanizması)

---

## 🚀 Kurulum ve Çalıştırma

### Gereksinimler
- Flutter SDK `>=3.x`
- Android Studio & Android SDK (API Seviyesi 28 / Android 9.0 ve üzeri gereklidir)
- Wi-Fi RTT (FTM) ve BLE 5.0 Peripheral modunu destekleyen en az 2 adet fiziksel Android cihaz

### Projeyi Klonlama
```bash
git clone [https://github.com/anka-project/anka-android.git](https://github.com/anka-project/anka-android.git)
cd anka-android
```

### Bağımlılıkları Yükleme
```bash
flutter pub get
```

### Derleme ve Çalıştırma
```bash
# Hayat Sinyali (Afetzede Modülü) için
flutter run -t lib/main_victim.dart

# Yardım Eli (Kurtarma Ekibi Modülü) için
flutter run -t lib/main_rescuer.dart
```

---

## 👥 Proje Ekibi & Danışmanlar
- **Yürütücü / Araştırmacı:** Berat Resuloğlu
- **Araştırmacı:** Esma Gülsüm Bilgin
- **Akademik Danışman:** Prof. Dr. Cüneyt Bayılmış *(Sakarya Üniversitesi)*
- **Sanayi Danışmanı:** Anıl Enis Köksal *(ARGEDE Bilişim Teknolojileri)*

---

## 📄 Lisans
Bu proje lisanslanma aşamasındadır. Detaylar için `LICENSE` dosyasına göz atabilirsiniz.
