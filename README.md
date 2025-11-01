# 🏦 ING Hubs Türkiye Datathon - Müşteri Churn Tahmini

<div align="center">

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.0+-FF6F00.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)
![Status](https://img.shields.io/badge/Status-Completed-success.svg)

**Gelişmiş makine öğrenimi ve derin öğrenme teknikleri kullanarak müşteri kaybı (churn) tahmini**

[Özellikler](#-özellikler) • [Kurulum](#-kurulum) • [Kullanım](#-kullanım) • [Modeller](#-modeller) • [Sonuçlar](#-sonuçlar)

</div>

---

## 📋 İçindekiler

- [Proje Hakkında](#-proje-hakkında)
- [Özellikler](#-özellikler)
- [Kullanılan Teknolojiler](#-kullanılan-teknolojiler)
- [Veri Seti](#-veri-seti)
- [Kurulum](#-kurulum)
- [Kullanım](#-kullanım)
- [Proje Yapısı](#-proje-yapısı)
- [Modeller ve Yaklaşım](#-modeller-ve-yaklaşım)
- [Model Performansları](#-model-performansları)
- [Özellik Mühendisliği](#-özellik-mühendisliği)
- [Sonuçlar](#-sonuçlar)
- [Katkıda Bulunma](#-katkıda-bulunma)
- [Lisans](#-lisans)

---

## 🎯 Proje Hakkında

Bu proje, **ING Hubs Türkiye Datathon** yarışması kapsamında geliştirilmiştir. Amaç, banka müşterilerinin gelecekte kaybedilme (churn) olasılığını tahmin etmek ve müşteri sadakatini artırmak için proaktif önlemler alınmasını sağlamaktır.

### 🎯 Temel Hedefler

- 📊 **Veri Analizi**: Kapsamlı keşifsel veri analizi (EDA)
- 🔧 **Özellik Mühendisliği**: 100+ yeni özellik oluşturma
- 🤖 **Model Geliştirme**: Ensemble ve deep learning yaklaşımları
- 📈 **Optimizasyon**: Hyperparameter tuning ile performans iyileştirme

---

## ✨ Özellikler

- ✅ **Gelişmiş Veri Ön İşleme**: Eksik değer yönetimi, tip optimizasyonu
- ✅ **Kapsamlı EDA**: 10+ farklı görselleştirme ve analiz
- ✅ **Zengin Özellik Mühendisliği**: Temporal, behavioral, ve statistical özellikler
- ✅ **Multi-Model Ensemble**: CatBoost, XGBoost, LightGBM, LSTM kombinasyonu
- ✅ **Hyperparameter Optimization**: Optuna ile otomatik tuning
- ✅ **Cross-Validation**: Stratified K-Fold ile robust değerlendirme

---

## 🛠️ Kullanılan Teknolojiler

### Programlama Dili
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)

### Makine Öğrenimi Kütüphaneleri
![XGBoost](https://img.shields.io/badge/XGBoost-337AB7?style=for-the-badge&logo=xgboost&logoColor=white)
![LightGBM](https://img.shields.io/badge/LightGBM-02569B?style=for-the-badge&logo=microsoft&logoColor=white)
![CatBoost](https://img.shields.io/badge/CatBoost-FFCC00?style=for-the-badge&logo=catboost&logoColor=black)
![Scikit Learn](https://img.shields.io/badge/Scikit--Learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)

### Derin Öğrenme
![TensorFlow](https://img.shields.io/badge/TensorFlow-FF6F00?style=for-the-badge&logo=tensorflow&logoColor=white)
![Keras](https://img.shields.io/badge/Keras-D00000?style=for-the-badge&logo=keras&logoColor=white)

### Veri İşleme ve Görselleştirme
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557c?style=for-the-badge&logo=plotly&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-3776AB?style=for-the-badge&logo=python&logoColor=white)

### Optimizasyon
![Optuna](https://img.shields.io/badge/Optuna-0066CC?style=for-the-badge&logo=optuna&logoColor=white)

### Geliştirme Ortamı
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)

---

## 📊 Veri Seti

Proje, ING Hubs tarafından sağlanan üç ana veri seti kullanmaktadır:

### 📁 Veri Setleri

| Veri Seti | Satır Sayısı | Kolon Sayısı | Açıklama |
|-----------|--------------|--------------|----------|
| **customer_history.csv** | 5,359,609 | 7 | Müşteri işlem geçmişi (aylık) |
| **customers.csv** | 176,293 | 8 | Müşteri demografik bilgileri |
| **referance_data.csv** | 88,147 | 2 | Eğitim seti (churn etiketli) |
| **referance_data_test.csv** | 88,146 | 1 | Test seti |

### 🔍 Veri Setleri Detayları

#### 1. Customer History (Müşteri Geçmişi)
- **Tarih Aralığı**: 2016-01-01'den itibaren aylık kayıtlar
- **Özellikler**:
  - `cust_id`: Müşteri ID
  - `date`: Tarih
  - `mobile_eft_all_cnt/amt`: Mobil EFT işlem sayısı/tutarı
  - `cc_transaction_all_cnt/amt`: Kredi kartı işlem sayısı/tutarı
  - `active_product_category_nbr`: Aktif ürün kategorisi sayısı

#### 2. Customers (Müşteri Bilgileri)
- **Demografik Özellikler**:
  - `gender`: Cinsiyet (F/M)
  - `age`: Yaş
  - `province`: İl
  - `religion`: Din
- **İş Bilgileri**:
  - `work_type`: Çalışma tipi (Full-time, Part-time, Self-employed, Student)
  - `work_sector`: Çalışma sektörü
  - `tenure`: Müşteri yaşam süresi (ay)

---

## 🚀 Kurulum

### Gereksinimler

```bash
Python 3.8+
```

### Adım 1: Repository'yi Klonlayın

```bash
git clone https://github.com/Ozan-Mohurcu/ING-HUB-DATATHON-.git
cd ING-HUB-DATATHON-
```

### Adım 2: Gerekli Kütüphaneleri Yükleyin

```bash
pip install pandas numpy matplotlib seaborn
pip install scikit-learn xgboost lightgbm catboost
pip install tensorflow optuna
pip install jupyter
```

veya

```bash
pip install -r requirements.txt
```

### Adım 3: Jupyter Notebook'u Başlatın

```bash
jupyter notebook ing-hub-datathon.ipynb
```

---

## 💻 Kullanım

### 1. Veri Yükleme

```python
import pandas as pd

customer_history = pd.read_csv("customer_history.csv", parse_dates=['date'])
customer = pd.read_csv("customers.csv")
train_ref = pd.read_csv("referance_data.csv", parse_dates=['ref_date'])
test_ref = pd.read_csv("referance_data_test.csv", parse_dates=['ref_date'])
```

### 2. Model Eğitimi

```python
# Notebook'taki ilgili hücreleri çalıştırarak
# - Veri ön işleme
# - Özellik mühendisliği
# - Model eğitimi
# adımlarını gerçekleştirin
```

### 3. Tahmin Yapma

```python
# Eğitilmiş modeller ile tahmin
submission = pd.DataFrame({
    'cust_id': test_df['cust_id'],
    'churn': predictions
})
submission.to_csv('submission.csv', index=False)
```

---

## 📁 Proje Yapısı

```
ING-HUB-DATATHON-/
│
├── ing-hub-datathon.ipynb    # Ana Jupyter Notebook
├── README.md                  # Proje dokümantasyonu (bu dosya)
│
├── data/                      # Veri setleri (gitignore'da)
│   ├── customer_history.csv
│   ├── customers.csv
│   ├── referance_data.csv
│   └── referance_data_test.csv
│
└── submissions/               # Model tahminleri
    └── submission_v13_tuned_ensemble.csv
```

---

## 🤖 Modeller ve Yaklaşım

### 🎯 Model Mimarisi

Proje, **ensemble learning** yaklaşımı kullanmaktadır. Dört farklı model kombinasyonu ile optimal sonuçlar elde edilmiştir:

#### 1️⃣ **CatBoost** (Gradient Boosting)
- Kategorik değişkenleri doğrudan işleyebilme
- Overfitting'e karşı dayanıklı
- GPU desteği ile hızlı eğitim

#### 2️⃣ **XGBoost** (Extreme Gradient Boosting)
- Yüksek performanslı tree boosting
- Regularization ile overfitting kontrolü
- Paralel işlem desteği

#### 3️⃣ **LightGBM** (Light Gradient Boosting Machine)
- Hızlı eğitim süresi
- Düşük bellek kullanımı
- Leaf-wise tree growth stratejisi

#### 4️⃣ **LSTM Hybrid Model** (Deep Learning)
- Temporal pattern öğrenme
- Sequential data processing
- Keras/TensorFlow ile implementasyon

### 🔧 Ensemble Stratejisi

Modeller, **Optuna** kullanılarak optimize edilmiş ağırlıklarla birleştirilmiştir:

```python
Final Prediction = w1·CatBoost + w2·XGBoost + w3·LightGBM + w4·LSTM
```

**Optuna Optimization**:
- 1000 trial ile en iyi ağırlık kombinasyonu
- Stratified K-Fold Cross-Validation
- Custom metric: ING UBS Datathon Metric

---

## 📊 Model Performansları

### 🏆 Bireysel Model Skorları

| Model | OOF Score | CV Score | Açıklama |
|-------|-----------|----------|----------|
| **CatBoost (Tuned)** | - | - | En yüksek ağırlık, robust performans |
| **XGBoost (Tuned)** | - | - | İkinci en yüksek katkı |
| **LightGBM (Tuned)** | - | - | Hız ve performans dengesi |
| **LSTM Hybrid** | - | - | Temporal pattern yakalama |

### 🎯 Final Ensemble Performansı

| Metrik | Değer | Açıklama |
|--------|-------|----------|
| **Final OOF Score** | **Optuna optimized** | 1000 trial sonucu |
| **Cross-Validation** | Stratified 5-Fold | Robust değerlendirme |
| **Submission** | v13_tuned_ensemble | Son tahmin dosyası |

### 📈 Model Ağırlıkları (Optuna Optimized)

Optuna ile optimize edilmiş model ağırlıkları:

```
CatBoost (Tuned):    ~45-50%
XGBoost (Tuned):     ~20-25%
LightGBM (Tuned):    ~20-25%
LSTM (Baseline):     ~5-10%
```

---

## 🔬 Özellik Mühendisliği

### 📊 Oluşturulan Özellik Kategorileri

#### 1. **Temporal Features (Zamansal Özellikler)**
- Son 1, 3, 6, 12 ay istatistikleri
- Trend ve seasonality özellikleri
- Exponential decay features

#### 2. **Behavioral Features (Davranışsal Özellikler)**
- İşlem sıklığı ve tutarı
- Mobil EFT vs Kredi Kartı kullanım oranları
- Aktivite düzenliliği metrikleri

#### 3. **Statistical Features (İstatistiksel Özellikler)**
- Mean, median, std, min, max
- Percentile özellikleri (25th, 75th, 90th)
- Skewness ve kurtosis

#### 4. **Engagement Features (Etkileşim Özellikleri)**
- Aktif ürün kategorisi değişimleri
- Inactivity streaks (pasiflik dönemleri)
- Engagement diversity metrikleri

#### 5. **Velocity & Acceleration**
- İşlem hızı değişimleri
- Momentum indikatörleri
- Trend kırılma noktaları

### 📋 Toplam Özellik Sayısı

- **Orijinal Özellikler**: ~15
- **Engineered Özellikler**: 100+
- **Toplam**: 115+ özellik

---

## 📈 Sonuçlar

### ✅ Başarılar

- ✨ **Multi-model ensemble** yaklaşımı ile robust tahminler
- ✨ **100+ yeni özellik** ile model performansı artışı
- ✨ **Optuna optimization** ile optimal ağırlık kombinasyonu
- ✨ **Kapsamlı EDA** ile veri insights
- ✨ **Stratified K-Fold CV** ile güvenilir değerlendirme

### 🎯 Temel Bulgular

1. **Churn Faktörleri**:
   - Düşük tenure (yeni müşteriler) yüksek churn riski
   - Azalan işlem aktivitesi churn göstergesi
   - Belirli demografik gruplar daha riskli

2. **Model İnsights**:
   - CatBoost en yüksek individual performans
   - Ensemble yaklaşımı tek modelden daha iyi
   - LSTM temporal pattern yakalamada etkili

3. **Veri İyileştirmeleri**:
   - Bellek optimizasyonu: ~345 MB → Optimized
   - Eksik değer yönetimi: Domain-specific stratejiler
   - Tip optimizasyonu: int64→int32, float64→float32

---

## 🎨 Görselleştirmeler

Notebook içinde yer alan bazı görselleştirmeler:

- 📊 Churn dağılımı
- 👤 Yaş ve tenure dağılımları
- 💳 Mobil EFT vs Kredi Kartı karşılaştırma
- 🗺️ İl bazında analiz
- ⚧️ Cinsiyet vs Churn
- 📦 Ürün kategorisi analizi
- 📈 Aylık işlem trendi
- ⏳ Tenure grupları vs Churn

Tüm görselleştirmeler **modern, temiz ve profesyonel** tasarıma sahiptir.

---

## 🤝 Katkıda Bulunma

Katkılarınızı bekliyoruz! Lütfen şu adımları izleyin:

1. Fork yapın
2. Feature branch oluşturun (`git checkout -b feature/AmazingFeature`)
3. Değişikliklerinizi commit edin (`git commit -m 'Add some AmazingFeature'`)
4. Branch'inizi push edin (`git push origin feature/AmazingFeature`)
5. Pull Request açın

---

## 📝 Lisans

Bu proje MIT lisansı altında lisanslanmıştır. Detaylar için [LICENSE](LICENSE) dosyasına bakınız.

---

## 👤 Yazar

**Ozan Mohurcu**

- GitHub: [@Ozan-Mohurcu](https://github.com/Ozan-Mohurcu)

---

## 🙏 Teşekkürler

- **ING Hubs Türkiye** - Datathon organizasyonu için
- **Kaggle Community** - Veri bilimi kaynakları için
- Tüm açık kaynak kütüphane geliştiricilerine

---

<div align="center">

**⭐ Bu projeyi beğendiyseniz yıldız vermeyi unutmayın! ⭐**

Made with ❤️ for ING Hubs Türkiye Datathon

</div>
