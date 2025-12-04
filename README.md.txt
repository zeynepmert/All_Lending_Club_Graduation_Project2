

-----------------------------------------------------------------------------------------

TR
📌 Lending Club Kredi Analizi ve Tahmin Modelleri Projesi

Bu proje, Kaggle üzerinde açık kaynak olarak sunulan All Lending Club Loan Data veri seti kullanılarak gerçekleştirilmiştir.
Veri seti bağlantısı:
👉 https://www.kaggle.com/datasets/wordsforthewise/lending-club

Üç kişilik bir ekip tarafından yürütülen bu çalışma; veri temizleme, özellik mühendisliği, keşifçi veri analizi (EDA), KPI & içgörü üretimi, tahmin modelleri kurulumu ve dashboard geliştirme aşamalarını kapsamaktadır.

📊 1. Proje Verisi

Projede iki farklı ana veri kaynağı kullanılmıştır:

✔ 1. Accepted Loans Dataset (Kabul Edilen Krediler)

145 sütun

2,260,702 satır

Daha detaylı analiz edilebilmesi için 7 alt tabloya bölünmüştür:

Alt tablolar:

loan_base

borrower_info

credit_history

payments

delinquency_risk

hardship

settlement

Bu tablolar, ortak id anahtarı üzerinden birleştirilerek ilişkilendirilmiştir.

✔ 2. Rejected Loans Dataset (Reddedilen Krediler)

9 sütun

27,648,742 satır

Accepted ve Rejected veri setleri daha sonra modelleme aşaması için bir araya getirilmiş, tutarlı bir ortak yapı oluşturulmuştur.

🔍 2. Proje Aşamaları

Bu proje, uçtan uca bir kredi risk analizi ve modelleme pipeline’ı olarak geliştirilmiştir. Aşamalar aşağıdaki gibidir:

### 2.1. Veri Temizleme & Özellik Mühendisliği

Eksik değerlerin yakalanması ve doldurulması

Binary missing_flag değişkenlerinin oluşturulması

Tarih değişkenlerinin ayrıştırılması

Kategorik değişkenlerin one-hot encoding ile kodlanması

Gereksiz veya bilgi taşımayan değişkenlerin çıkarılması

Accepted + Rejected veri setlerinin yapısal olarak birleştirilmesi

Train/test ayrımı & scaling işlemleri

Veri kalite kontrolleri

### 2.2. Keşifçi Veri Analizi (EDA)

Demografik analizler

Kredi ürün özellikleri

Kredi performans dağılımları

Zaman serisi analizleri

Kredi risk göstergeleri

Aykırı değer analizleri

Segment bazlı incelemeler

### 2.3. KPI & Insights Üretimi

Kredi portföyüne dair:

Temerrüt oranları

Segment bazlı kabul/red oranları

Gelir & borç ilişkisi

Payment behavior analizi

Risk seviyelerine göre portföy dağılımı

Erken uyarı göstergeleri

Sonuçlar görselleştirilmiş ve dashboard geliştirmesi için altyapı oluşturulmuştur.

### 2.4. Modelleme Aşaması

Bu proje kapsamında 3 farklı makine öğrenimi modeli geliştirilmiştir:

1️⃣ Kredi Kabul / Red Tahmin Modeli

Logistic Regression temelli model

Data cleaning → feature engineering → encoding → scaling → stratified train/test split

Performans metrikleri: Accuracy, ROC-AUC, F1-score, Recall, Precision

Model çıktıları CSV formatında kaydedilmiştir.

2️⃣ Lending Club Kredi Risk Analizi ve Stres Testi Simülasyonu

Kredi risk dağılımı modellemesi

Makro senaryolara göre stres testi

Default oranı simülasyonları

Segment bazlı etki analizi

3️⃣ Model 3 (model3_adi)

📌 Bu bölüm sen ayrıntısını verdiğinde burayı düzenleyebilirim.
(Not: Modelin amacını, yaklaşım türünü ve çıktılarını birkaç cümleyle yazarsan, final versiyona ekleyeyim.)

### 2.5. Dashboard Geliştirme

Power BI ile kredi portföyü dashboard’u

Segment bazlı KPI'lar

Zaman serisi trendleri

Risk göstergeleri

Kullanıcı etkileşimli filtreler

Model sonuçlarının görsel sunumu

🧠 3. Genel Proje Yapısı
All_Lending_Club_Graduation_Project2/
notebooks
│
├── 01_Created_subtable/
│   ├── accepted_loans/
│   ├── rejected_loans/
│
├── 02_EDA/
│   ├── visualizations.ipynb
│
├── 03_KPI&Insights/
│
├── 04_Models/
│   ├── logistic_regression/
│   ├── stress_test/
│   ├── model_3/
│   ├──
│
├── dashboard/
    └── All_lending_club_dashboard.pbix


🧾 4. Sonuç

Bu proje kapsamında:

✔ 30 milyon satırı aşan büyük bir veri işlenmiş
✔ Accepted & Rejected veri setleri birleştirilmiş
✔ Geniş kapsamlı veri temizleme ve özellik mühendisliği yapılmış
✔ EDA ve KPI analizleri gerçekleştirilmiş
✔ 3 farklı makine öğrenimi modeli geliştirilmiş
✔ Kullanıcı dostu bir dashboard hazırlanmıştır

Proje, Lending Club kredi portföyü üzerinde hem tahmin modelleri hem de risk analizi sunan uçtan uca bir veri bilimi çalışmasıdır.