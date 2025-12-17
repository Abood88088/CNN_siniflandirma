# 🧠 CNN Tabanlı Görüntü Sınıflandırma (Lamba – Saat)

Bu proje, **BLG407 Makine Öğrenmesi** dersi kapsamında,
tarafımdan **telefon kamerası ile çekilmiş özgün görüntüler**
kullanılarak geliştirilmiş bir **CNN tabanlı görüntü sınıflandırma sistemi**dir.

Amaç, **Lamba** ve **Saat** nesnelerini yüksek doğrulukla ayırt edebilen
farklı derin öğrenme yaklaşımlarını karşılaştırmalı olarak incelemektir.

Projede üç farklı model uygulanmıştır:

- **Model1 → Transfer Learning (ResNet50)**
- **Model2 → Temel CNN (From Scratch)**
- **Model3 → Geliştirilmiş CNN (Data Augmentation + Callback)**

---

## 👤 Öğrenci Bilgileri

| Bilgi | İçerik |
|------|--------|
| **Ad** | ABDUL RAHMAN |
| **Soyad** | KHANOUM |
| **Öğrenci No** | 2212721317 |
| **Ders** | BLG407 – Makine Öğrenmesi |
| **GitHub** | https://github.com/Abood88088/CNN_siniflandirma |

---

## 🗂️ 1. Veri Seti Bilgileri

Bu projede kullanılan veri seti **tamamen özgündür** ve
tarafımdan **cep telefonu kamerası** ile çekilmiştir.

| Özellik | Açıklama |
|------|---------|
| Toplam Görüntü | **100 adet** |
| Sınıflar | Lamba (50) – Saat (50) |
| Görüntü Boyutu | 128 × 128 |
| Veri Kaynağı | Telefon kamerası |
| Bölme Oranı | %70 Train – %15 Validation – %15 Test |
| Veri Türü | RGB |

### 📁 Klasör Yapısı
```text
dataset/
├── lamba/
└── saat/
```
### 📊 Deney Karşılaştırma Tablosu

Aşağıdaki tablo, farklı hiperparametre ve yöntemlerle elde edilen
test doğruluklarını özetlemektedir.

| Deney No | Batch Size | Filtre Sayısı | Dropout | Learning Rate | Veri Artırımı | Test Doğruluğu | Not                  |
| -------- | ---------- | ------------- | ------- | ------------- | ------------- | -------------- | -------------------- |
| 1        | 32         | 32-64-128     | 0.2     | 0.001         | Hayır         | %68            | Temel deneme         |
| 2        | 64         | 32-64-128     | 0.3     | 0.001         | Evet          | %74            | Veri artırımı etkili |
| 3        | 64         | 64-128-256    | 0.4     | 0.0005        | Evet          | %78            | Daha derin yapı      |

⚙️ 2. Model1 – Transfer Learning (ResNet50)
🔍 Model Açıklaması

Model1’de, ImageNet veri seti üzerinde önceden eğitilmiş
ResNet50 mimarisi kullanılmıştır.
Amaç, küçük veri setlerinde transfer learning yaklaşımının etkisini
incelemektir.

🧱 Mimari

-ResNet50 (dondurulmuş katmanlar)

-GlobalAveragePooling2D

-Dense (128, ReLU)

-Dropout (0.3)

-Dense (2, Softmax)

📊 Sonuçlar

| Metrik                     | Değer      |
| -------------------------- | ---------- |
| Eğitim Epoch               | 20         |
| En İyi Validation Accuracy | %92.86     |
| **Test Accuracy**          | **%81.25** |
| Test Loss                  | 0.6328     |

<img width="832" height="537" alt="image" src="https://github.com/user-attachments/assets/6273ac86-6d2a-4a61-bb54-94100875e281" />
<img width="838" height="556" alt="image" src="https://github.com/user-attachments/assets/4cfcebdb-114f-434f-aa45-0bae0919e4e1" />


📝 Değerlendirme

Transfer learning sayesinde sınırlı veriyle
kabul edilebilir ve dengeli bir performans elde edilmiştir.
Model1, proje için güçlü bir başlangıç noktası olmuştur.

🧱 3. Model2 – Temel CNN (From Scratch)
🔍 Model Açıklaması

Model2, transfer learning kullanılmadan
tamamen sıfırdan oluşturulmuş temel bir CNN mimarisidir.

Amaç, basit bir CNN yapısının bu veri setindeki başarısını ölçmektir.

🧠 Mimari

-Conv2D (32) + MaxPooling

-Conv2D (64) + MaxPooling

-Conv2D (128) + MaxPooling

-Dense (128, ReLU)

-Dropout (0.3)

-Softmax (2 sınıf)

📊 Sonuçlar

| Metrik                     | Değer      |
| -------------------------- | ---------- |
| En Yüksek Eğitim Accuracy  | %100       |
| En İyi Validation Accuracy | %100       |
| **Test Accuracy**          | **%93.75** |
| Test Loss                  | 0.2244     |

<img width="819" height="579" alt="image" src="https://github.com/user-attachments/assets/639789bd-af1c-4cdb-a071-d44ce3785333" />
<img width="790" height="574" alt="image" src="https://github.com/user-attachments/assets/52e33cb9-b9ce-4856-923c-a216028d8707" />

📝 Değerlendirme

Model2, sade mimarisine rağmen oldukça başarılı sonuçlar üretmiştir.
Bu durum, doğru veri hazırlığı ve uygun hiperparametrelerin
küçük veri setlerinde bile etkili olabileceğini göstermektedir.


🚀 4. Model3 – Geliştirilmiş CNN (Optimize Edilmiş)
🔍 Model Açıklaması

Model3, Model2 temel alınarak geliştirilmiş;
veri artırımı, dinamik öğrenme oranı ve
callback mekanizmaları ile optimize edilmiştir.

⚙️ Kullanılan Yöntemler

*Data Augmentation (rotation, zoom, horizontal flip)

*EarlyStopping

*ReduceLROnPlateau

*Dengeli Dropout (0.25)

🧠 Mimari

*Conv2D (32 → 64 → 128)

*MaxPooling

*Dense (128)

*Dropout (0.25)

*Softmax

📊 Sonuçlar
| Metrik                     | Değer      |
| -------------------------- | ---------- |
| En Yüksek Eğitim Accuracy  | %100       |
| En İyi Validation Accuracy | %100       |
| **Test Accuracy**          | **%95.00** |
| Test Loss                  | 0.1730     |

<img width="740" height="617" alt="image" src="https://github.com/user-attachments/assets/992d881a-05db-4ca3-8db6-f119db76a58a" />
<img width="802" height="575" alt="image" src="https://github.com/user-attachments/assets/e9ccce03-7d36-482a-9daf-b14c240e8984" />

📝 Değerlendirme

Model3, uygulanan optimizasyonlar sayesinde
en dengeli ve genelleştirilebilir performansı sunmuştur.
Bu nedenle proje kapsamında nihai model olarak seçilmiştir.

📈 5. Genel Karşılaştırma
| Model  | Test Accuracy | Yorum                                   |
| ------ | ------------- | --------------------------------------- |
| Model1 | %81.25        | Transfer learning ile dengeli başlangıç |
| Model2 | %93.75        | Basit CNN ile güçlü performans          |
| Model3 | **%95.00**    | En iyi genelleme ve nihai model         |

📁 6. Proje Dosya Yapısı
CNN_siniflandirma/
├── dataset/
│   ├── lamba/
│   └── saat/
│
├── images/
│   ├── model1_acc.png
│   ├── model1_loss.png
│   ├── model2_acc.png
│   ├── model2_loss.png
│   ├── model3_acc.png
│   └── model3_loss.png
│
├── Model1.ipynb
├── Model2.ipynb
├── Model3.ipynb
└── README.md



