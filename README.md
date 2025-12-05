> ## 🇹🇷 Türkçe Versiyon  
📌 Lending Club Kredi Analizi ve Tahmin Modelleri Projesi

Bu proje, Kaggle üzerinde açık kaynak olarak sunulan All Lending Club Loan Data veri seti kullanılarak gerçekleştirilmiştir.  
Veri seti bağlantısı:  
👉 https://www.kaggle.com/datasets/wordsforthewise/lending-club

Üç kişilik bir ekip tarafından yürütülen bu çalışma; veri temizleme, özellik mühendisliği, keşifçi veri analizi (EDA), KPI & içgörü üretimi, tahmin modelleri kurulumu ve dashboard geliştirme aşamalarını kapsamaktadır.

📊 1. Proje Verisi

Projede iki farklı ana veri kaynağı kullanılmıştır:

✔ **1. Accepted Loans Dataset (Kabul Edilen Krediler)**  
145 sütun  
2,260,702 satır  

Daha detaylı analiz edilebilmesi için 7 alt tabloya bölünmüştür:

- loan_base  
- borrower_info  
- credit_history  
- payments  
- delinquency_risk  
- hardship  
- settlement  

Bu tablolar, ortak id anahtarı üzerinden birleştirilerek ilişkilendirilmiştir.

✔ **2. Rejected Loans Dataset (Reddedilen Krediler)**  
9 sütun  
27,648,742 satır  

Accepted ve Rejected veri setleri daha sonra modelleme aşaması için bir araya getirilmiş, tutarlı bir ortak yapı oluşturulmuştur.

---

🔍 **2. Proje Aşamaları**

Bu proje, uçtan uca bir kredi risk analizi ve modelleme pipeline’ı olarak geliştirilmiştir. Aşamalar aşağıdaki gibidir:

### 2.1. Veri Temizleme & Özellik Mühendisliği
- Eksik değerlerin yakalanması ve doldurulması  
- Binary missing_flag değişkenlerinin oluşturulması  
- Tarih değişkenlerinin ayrıştırılması  
- Kategorik değişkenlerin one-hot encoding ile kodlanması  
- Gereksiz veya bilgi taşımayan değişkenlerin çıkarılması  
- Accepted + Rejected veri setlerinin yapısal olarak birleştirilmesi  
- Train/test ayrımı & scaling işlemleri  
- Veri kalite kontrolleri  

### 2.2. Keşifçi Veri Analizi (EDA)
- Demografik analizler  
- Kredi ürün özellikleri  
- Kredi performans dağılımları  
- Zaman serisi analizleri  
- Kredi risk göstergeleri  
- Aykırı değer analizleri  
- Segment bazlı incelemeler  

### 2.3. KPI & Insights Üretimi
Kredi portföyüne dair:
- Temerrüt oranları  
- Segment bazlı kabul/red oranları  
- Gelir & borç ilişkisi  
- Payment behavior analizi  
- Risk seviyelerine göre portföy dağılımı  
- Erken uyarı göstergeleri  

Görselleştirilmiş sonuçlar dashboard geliştirmesi için kullanılmıştır.

---

### 2.4. Modelleme Aşaması

Bu proje kapsamında 3 farklı makine öğrenimi modeli geliştirilmiştir:

1️⃣ **Kredi Kabul / Red Tahmin Modeli**  
- Logistic Regression temelli model  
- Data cleaning → feature engineering → encoding → scaling → stratified split  
- Performans: Accuracy, ROC-AUC, F1-score, Recall, Precision  
- Çıktılar CSV olarak kaydedilmiştir.

2️⃣ **Lending Club Kredi Risk Analizi ve Stres Testi Simülasyonu**  
- Risk dağılımı modellemesi  
- Makro senaryolara göre stres testi  
- Default oranı simülasyonları  
- Segment etki analizi  

3️⃣ **Kredi Tutarı Sınıflandırma Modeli**  
- Kredi tutarını segmentlere ayırma (düşük–orta–yüksek)  
- Random Forest tabanlı çok sınıflı tahmin  
- Segment bazlı değerlendirme ve hata analizi  

---

### 2.5. Dashboard Geliştirme
- Power BI ile kredi portföyü dashboard'u  
- Segment bazlı KPI'lar  
- Zaman serisi trendleri  
- Risk göstergeleri  
- Etkileşimli filtreleme  
- Model sonuçlarının görsel sunumu  

---

🧠 **3. Genel Proje Yapısı**

All_Lending_Club_Graduation_Project2/  
│  
├── notebooks/  
│   ├── 01_Created_subtable/  
│   ├── 02_EDA/  
│   ├── 03_KPI&Insights/  
│   ├── 04_Models/  
│   └── .ipynb_checkpoints/  
│  
├── dashboard/  
│   └── All_lending_club_dashboard.pbix  
│  
└── README.md

---

🧾 **4. Sonuç**

Bu proje kapsamında:  
✔ 30 milyon satırı aşan veri işlenmiştir  
✔ Accepted & Rejected veri setleri birleştirilmiştir  
✔ Geniş kapsamlı veri temizleme & özellik mühendisliği yapılmıştır  
✔ EDA ve KPI analizleri gerçekleştirilmiştir  
✔ 3 farklı makine öğrenimi modeli geliştirilmiştir  
✔ Kullanıcı dostu bir dashboard oluşturulmuştur  

Proje, Lending Club kredi portföyünde hem tahmin hem de risk analizi sunan uçtan uca bir veri bilimi çalışmasıdır.


---

> ## 🇬🇧 English Version  
📌 Lending Club Credit Analysis and Predictive Modeling Project

This project was carried out using the publicly available **All Lending Club Loan Data** dataset on Kaggle.  
Dataset link:  
👉 https://www.kaggle.com/datasets/wordsforthewise/lending-club

Conducted by a team of three, this study includes data cleaning, feature engineering, exploratory data analysis (EDA), KPI & insight generation, predictive model development, and dashboard creation.

📊 **1. Project Data**

Two main datasets were used in the project:

✔ **1. Accepted Loans Dataset**  
145 columns  
2,260,702 rows  

This dataset was split into seven subtables:

- loan_base  
- borrower_info  
- credit_history  
- payments  
- delinquency_risk  
- hardship  
- settlement  

These tables were merged using a shared ID key.

✔ **2. Rejected Loans Dataset**  
9 columns  
27,648,742 rows  

The Accepted and Rejected datasets were later combined at the modeling stage to create a consistent structure.

---

🔍 **2. Project Stages**

This project was developed as an end-to-end credit risk analysis and modeling pipeline.

### 2.1. Data Cleaning & Feature Engineering
- Missing value detection & imputation  
- Creating binary missing_flag variables  
- Parsing date variables  
- One-hot encoding of categorical data  
- Removing irrelevant variables  
- Merging Accepted + Rejected datasets  
- Train/test split & scaling  
- Data quality checks  

### 2.2. Exploratory Data Analysis (EDA)
- Demographics  
- Loan product characteristics  
- Loan performance distributions  
- Time-series analysis  
- Credit risk indicators  
- Outlier detection  
- Segment-based analysis  

### 2.3. KPI & Insights Generation
Portfolio insights include:
- Default rates  
- Segment-based approval/rejection rates  
- Income–debt relationships  
- Payment behavior analysis  
- Portfolio distribution by risk level  
- Early warning indicators  

These outputs were visualized and used for dashboard development.

---

### 2.4. Modeling Stage

Three machine learning models were developed:

1️⃣ **Credit Approval / Rejection Prediction Model**  
- Logistic Regression–based  
- Cleaning → feature engineering → encoding → scaling → stratified split  
- Metrics: Accuracy, ROC-AUC, F1-score, Recall, Precision  
- Outputs stored as CSV  

2️⃣ **Credit Risk Analysis & Stress Test Simulation**  
- Risk distribution modeling  
- Macroeconomic scenario stress tests  
- Default rate simulations  
- Segment-level impact analysis  

3️⃣ **Loan Amount Classification Model**  
- Segments loan amounts into low–medium–high  
- Random Forest multiclass classifier  
- Segment performance evaluation & error analysis  

---

### 2.5. Dashboard Development
- Power BI portfolio dashboard  
- Segment-based KPIs  
- Time-series trends  
- Risk indicators  
- Interactive filters  
- Visualization of model outputs  

---

🧠 **3. Overall Project Structure**

All_Lending_Club_Graduation_Project2/  
│  
├── notebooks/  
│   ├── 01_Created_subtable/  
│   ├── 02_EDA/  
│   ├── 03_KPI&Insights/  
│   ├── 04_Models/  
│   └── .ipynb_checkpoints/  
│  
├── dashboard/  
│   └── All_lending_club_dashboard.pbix  
│  
└── README.md

---

🧾 **4. Conclusion**

In this project:  
✔ Over 30 million rows of data were processed  
✔ Accepted & Rejected datasets were merged  
✔ Extensive data cleaning & feature engineering were completed  
✔ EDA and KPI analyses were performed  
✔ Three machine learning models were developed  
✔ A user-friendly dashboard was delivered  

This project serves as an end-to-end data science workflow providing both predictive modeling and risk analysis for the Lending Club loan portfolio.
