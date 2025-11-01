# 🏦 ING HUBS Datathon 2025 – Bank Customer Churn Prediction

> “Her ayrılan müşteri bir sessizlik bırakır. Biz o sessizliği veriye dönüştürdük.”

---

## 🎯 Problem Tanımı

Bankacılık sektöründe müşteri kaybı (churn), gelir ve sadakat açısından en kritik problemlerden biridir.  
Bu proje kapsamında hedefimiz:
- Müşteri kaybına neden olan davranışsal ve finansal faktörleri **erken tespit etmek**,  
- Potansiyel olarak ayrılma eğilimindeki müşterileri **proaktif stratejilerle elde tutmak**,  
- Banka için **ölçeklenebilir, açıklanabilir ve uygulanabilir** bir tahmin modeli geliştirmek.

---

## 💡 İş Değeri

| Metrik | Açıklama |
|:-------|:----------|
| 💸 **Müşteri kaybetme maliyeti** | Yeni müşteri edinmek, mevcut müşteriyi tutmaktan **5–7 kat** daha pahalı. |
| 🚨 **Erken uyarı sistemi** | Churn riski yüksek müşteriler erken tespit edilerek hedefli kampanyalar planlanabilir. |
| 📈 **Elde tutma etkisi** | %5’lik müşteri elde tutma artışı, kârlılığı **%25–95** arasında artırabilir (Harvard Business Review). |
| 🤝 **Veri destekli kararlar** | Sadakat stratejileri artık sezgiyle değil, **veriyle yönlendiriliyor.** |

---

## 📂 Veri Seti Özeti

| Dataset | Satır Sayısı | Sütun | Açıklama |
|:---------|:-------------|:------|:----------|
| **customers.csv** | 176,293 | 8 | Demografik, iş tipi, bölge, yaş, tenure bilgileri |
| **customer_history.csv** | 5,359,609 | 7 | Müşteri işlem geçmişi, EFT ve kredi kartı verileri |
| **reference_data.csv** | 133,287 | 3 | Churn etiketli train referansı |
| **reference_data_test.csv** | 43,006 | 2 | Test referansı |
| **Toplam** | **≈ 5.71 milyon** | 20+ | Banka müşterilerinin çok boyutlu davranış verisi |

---

## 🧹 Veri Ön İşleme

| Aşama | Açıklama |
|:------|:----------|
| 🔍 **Eksik değer yönetimi** | Sayısal değişkenlerde *medyan* ve *KNN imputasyonu*, kategoriklerde *mod* kullanıldı. Eksiklik bayrakları (`is_missing`) eklendi. |
| 📏 **Uç değer baskılama (Winsorization)** | Finansal değişkenlerde uç değerler, bilgi kaybı olmadan istatistiksel sınırlar içine çekildi. |
| 🔢 **Özellik ölçekleme** | Zaman serisi tabanlı değişkenlerde *robust scaling* uygulandı. |
| 🧠 **Türetilmiş özellikler (Feature Engineering)** | Finansal davranış, kanal çeşitliliği, inaktivite trendleri, yaşam döngüsü evreleri gibi domain tabanlı yeni değişkenler eklendi. |

---

## 🧩 Özellik Mühendisliği

| Yeni Özellik | Amaç | Kaynak |
|:--------------|:------|:--------|
| 🕒 **Exponential Decay Features** | Zamana bağlı işlem azalış trendini yakalamak | TDS Time Series FE |
| 💤 **Inactivity Streaks** | Arka arkaya inaktif ay sayısı → churn riski sinyali | ScienceDirect 2023 |
| ⚙️ **Engagement Diversity (Entropy)** | Kanal çeşitliliği → sadakat korelasyonu | Shannon Entropy + MDPI 2024 |
| 🔁 **Customer Lifecycle Stage** | Onboarding, Growth, Mature, Decline fazları | Springer 2024 |
| 📈 **Velocity & Acceleration** | İşlem hacmindeki momentum değişimi | Trend Analysis (TDS) |
| 🧮 **Cohort-Based Features** | Benzer tenure grubuna göre normalizasyon | SpringerOpen 2024 |

---

## 🧠 Modelleme Yaklaşımı

| Model | Tip | Açıklama |
|:------|:-----|:----------|
| 🐈‍⬛ **CatBoost (Tuned)** | Gradient Boosting | Kategorik değişkenlerde yüksek performans, en güçlü baz model |
| ⚡ **LightGBM (Tuned)** | Gradient Boosting | Dengesiz sınıf verisinde hızlı ve optimize yapı |
| 🌳 **XGBoost (Tuned)** | Gradient Boosting | Parametre optimizasyonu sonrası stabil skor |
| 🔄 **LSTM (Baseline)** | Time Series NN | Davranış trendlerini doğrulamak için referans |
| 🎯 **Ensemble (Optuna Weighted)** | Hybrid Model | Tüm modellerin güçlü yönlerini ağırlıklı birleştirir |

---

## 📊 Model Performans Sonuçları

| Model | AUC | F1 | Precision | Recall | OOF Score | Ağırlık (%) |
|:-------|:----:|:--:|:----------:|:--------:|:-----------:|
| CatBoost (Tuned) | 0.729 | 0.683 | 0.695 | 0.672 | 1.1958 | 42.6 |
| LightGBM (Tuned) | 0.724 | 0.678 | 0.688 | 0.669 | — | 33.7 |
| XGBoost (Tuned) | 0.721 | 0.671 | 0.682 | 0.661 | — | 22.8 |
| LSTM (Baseline) | 0.701 | 0.653 | 0.650 | 0.656 | — | 0.9 |
| **Ensemble (Final)** | **0.730** | **0.689** | **0.701** | **0.678** | **1.1958** | 100 |

🧮 **Optuna optimizasyonu (1000 deneme)** ile ağırlıklar belirlenmiş ve OOF skorunda **+1.2% performans artışı** sağlanmıştır.  

---

## 🛠️ Kullanılan Araçlar ve Teknolojiler

| Araç | Amaç | İkon |
|:------|:------|:------|
| **Python** | Veri analizi ve modelleme | 🐍 |
| **Pandas / NumPy** | Veri işleme ve hesaplama | 📊 |
| **CatBoost / LightGBM / XGBoost** | Modelleme | 🌲 |
| **Optuna** | Hiperparametre optimizasyonu | 🎯 |
| **Matplotlib / Seaborn** | Görselleştirme | 📈 |
| **Scikit-learn** | Modelleme altyapısı ve metrik hesaplama | ⚙️ |
| **Power BI** | İş tarafı sunumları, dashboard | 💼 |
| **Kaggle Notebooks** | Reprodüksiyon ortamı | 💻 |

---

## 🧭 İş Stratejisi ve Etki

> “Model sadece bir tahmin aracı değil, müşteri kaybını önleyecek erken uyarı sistemidir.”

- 🎯 **Erken uyarı sistemi**: churn riski yüksek segmentler otomatik etiketlenebilir.  
- 💌 **Kampanya hedefleme**: düşük sadakatli segmentler için özel retention stratejileri.  
- 🧠 **Veri odaklı karar**: müşteri davranışı ve yaşam döngüsüne göre dinamik öneriler.  
- 💰 **Kârlılık artışı**: churn’ü %5 azaltmak → potansiyel %30 gelir artışı.

---

## 👥 Ekip

| Üye | Rol | Alan |
|:----|:----|:-----|
| **Ozan Möhürcü** | Data Scientist | Modelleme, Feature Engineering, Validation |
| **Ömer Tanır** | Machine Learning Engineer | Optuna, Ensemble, Model Optimization |

---

## 🧾 Lisans ve Katkı

Bu proje **ING HUBS Datathon 2025** kapsamında geliştirilmiştir.  
Kod ve sonuçlar açık kaynak paylaşımı için optimize edilmiştir.

---

> *“Veriyle sessiz müşteri kayıplarını görünür kıldık.  
Her ayrılış bir sinyaldi, biz o sinyali erken duyduk.”*

---
