Credit Approval / Rejection Prediction Model

Phase 1: Data Preparation and Merging

In this project, the final dataset used for model training was created by combining two different source datasets: accepted (approved credit applications) and rejected (declined credit applications).
The process consists of selecting data subsets, aligning column structures, and merging the datasets into a single modeling dataset.

1. Datasets Used
Accepted Dataset (Approved Credit Applications)

Contains a total of 2,260,702 rows.

80% of this dataset was selected for model development.

This subset represents the positive class (approved) in the final modeling dataset.

Rejected Dataset (Rejected Credit Applications)

Contains a total of 27,648,742 rows.

A portion equal to 3.5 times the size of the selected accepted subset was sampled.

This sampling was performed to reduce class imbalance and to achieve a more balanced data distribution for training.

2. Aligning Variables Across Datasets

The accepted and rejected datasets do not share the same column structure. Therefore:

Columns present in the accepted dataset but missing in the rejected dataset were identified.

Corresponding variables in the rejected dataset were transformed to match the accepted dataset in terms of:

data type,

format,

calculation logic,

and naming.

Numerical transformations, categorical mappings, and column renaming operations were applied.

All matched variables were saved using the same column names as in the accepted dataset.

Additionally, an approval_status column was added to both datasets:

Assigned 1 for accepted applications

Assigned 0 for rejected applications

This ensured a consistent and unified structure between the two datasets for downstream modeling.

3. Merging the Datasets

After ensuring column alignment:

Both datasets were standardized to have the same schema.

The accepted and rejected subsets were then vertically concatenated (row-wise).

This produced a single combined dataset containing both approved and rejected credit applications.

4. Final Outcome

The resulting dataset is:

Balanced in terms of class distribution,

Structurally consistent, with unified variable naming and formatting,

Fully prepared for machine learning model training.

This merged dataset serves as the foundation for all subsequent data preprocessing, feature engineering, and modeling stages in the project.

Phase 2: Data Cleaning, Feature Engineering, and Modeling Preparation

In this phase, the final merged dataset was processed through missing-value handling, feature engineering, categorical encoding, column reduction, train/test splitting, and numerical scaling. The goal was to prepare the dataset for training a logistic regression model in a fully optimized and clean structure.

1. Missing Value Handling

Some numerical variables contained missing information represented with –1. To ensure the model correctly interprets these cases, a two-step strategy was applied.

(a) Added Missing-Flag Columns

Binary “missing_flag” columns were created for the following variables:

inq_last_6mths_missing

delinq_2yrs_missing

annual_inc_missing

These flags help the model distinguish between actual zero values and missing information.

(b) Median Imputation

Values equal to –1 were:

replaced with NaN, and

filled with the median of each column.

Median imputation is robust against outliers and preserves the variable distribution.

2. Feature Engineering
Extraction of Date Components

The variable Application_Date was decomposed into:

app_year

app_month

app_day

The original date column was then removed.

3. Categorical Variable Encoding

Categorical variables were encoded using:

One-Hot Encoding

Applied to:

State

home_ownership

The parameter drop_first=True was used to avoid the dummy variable trap.

4. Removal of Non-Contributing Features

Based on correlation analysis and modeling relevance, the following variables were dropped:

annual_inc_missing

delinq_2yrs_missing

inq_last_6mths_missing

home_ownership_UNKNOWN

app_day

Risk_Score

home_ownership_MORTGAGE

Employment_Length

These features did not provide meaningful predictive contribution.

5. Train/Test Split
Target Variable

Approval_Status

Feature Set

Columns removed from X:

Approval_Status

app_year

app_month

Stratified Train/Test Split

The dataset was split into:

80% training

20% testing

with:

stratify=y

This ensured both sets preserved the original accepted/rejected class distribution, providing more reliable evaluation.

6. Scaling
Why Scaling?

Numerical variables operate on different scales. Scaling ensures the logistic regression model learns stable and comparable weights.

Scaling Rules

✔️ Only numerical variables were scaled

❌ One-hot encoded variables were not scaled

❌ Missing-flag variables were not scaled

✔️ Scaling was done after the train/test split (to prevent data leakage)

Scaler Used

StandardScaler()

Training set: fit_transform

Test set: transform

Phase 3: Logistic Regression Model Training

The logistic regression model was trained using:

log_reg = LogisticRegression(max_iter=500, class_weight='balanced')


max_iter = 500 → Ensures full convergence

class_weight = 'balanced' → Addresses class imbalance

Performance Metrics Calculated

Accuracy

F1-Score

ROC-AUC

Confusion Matrix

Classification Report

All results were both printed and saved as CSV files:

model_metrics.csv

classification_report.csv

Project Results

This project successfully processed two large-scale datasets (accepted & rejected credit applications) to build a clean, balanced, and model-ready dataset. Key accomplishments include:

✔️ Constructed a large, class-balanced modeling dataset
✔️ Correct missing-value detection using missing flags and median imputation
✔️ Proper encoding of categorical variables
✔️ Stratified train/test split preserving class ratios
✔️ Safe scaling only on numerical features (no leakage)
✔️ Successful training and evaluation of a logistic regression model

Overall, a solid baseline machine learning model was created to predict credit approval outcomes with a fully engineered and validated dataset.


Stage 4: Model Evaluation and Interpretation of Results

The final stage of the project involves evaluating the predictive performance of the logistic regression model and interpreting the results within the context of credit approval decision-making. The metrics obtained provide a comprehensive understanding of how effectively the model distinguishes between applications that should be approved and those that should be rejected.

Accuracy: 0.969

The model achieves an overall accuracy of 96.9%, indicating that the vast majority of predictions are correct. While this is a very high score, accuracy alone is not always a reliable performance indicator in credit risk modeling, especially in the presence of class imbalance. Therefore, additional metrics are examined to obtain a more complete performance assessment.

Confusion Matrix Analysis
              Pred 0        Pred 1
True 0      1,258,246        7,754
True 1         41,924      319,876


The confusion matrix reveals the following insights:

True Negatives (1,258,246): Applications that were correctly predicted as rejected.

False Positives (7,754): Applications incorrectly predicted as approved.
These represent credit risk exposure and are typically the most costly error for lenders.

True Positives (319,876): Applications correctly predicted as approved.

False Negatives (41,924): Applications incorrectly predicted as rejected.
These represent lost business opportunities.

Overall, the model makes significantly fewer false approvals (FP) than false rejections (FN), indicating a risk-averse and conservative behavior—often desirable in financial institutions prioritizing credit risk management.

Precision (Class 1 – Approved): 0.98

The model demonstrates exceptionally high precision, correctly identifying 98% of all applications it labels as approved. This means the likelihood of incorrectly approving a risky customer is very low. In credit modeling, such a high precision score is considered extremely valuable.

Recall (Class 1 – Approved): 0.88

The recall score shows that the model successfully captures 88% of all applications that should genuinely be approved, while missing approximately 12%. Although this is generally acceptable, increasing recall would further reduce the number of potentially profitable customers incorrectly rejected.

F1-Score (Class 1): 0.93

With an F1-score of 0.93, the model achieves a strong balance between precision and recall. This indicates that the model simultaneously emphasizes minimizing credit risk and maintaining good customer approval coverage.

ROC-AUC: 0.988

A ROC-AUC score of 0.988 demonstrates the model’s near-perfect ability to distinguish between high-risk and low-risk credit applications. In credit risk modeling, a value above 0.85 is considered strong; therefore, 0.988 indicates an exceptionally robust model.

Overall Interpretation

The logistic regression model performs at a very high level across all major evaluation metrics. Key conclusions include:

Excellent risk discrimination capability (high ROC-AUC)

Very low rate of incorrect approvals, ensuring strong protection against credit losses

Balanced performance with high precision and strong F1-score

Moderately high recall, indicating some room for improvement to reduce unnecessary rejections

Final Assessment

The model offers a highly reliable and risk-sensitive solution for predicting credit approval decisions. Its conservative structure minimizes the likelihood of approving risky customers while maintaining strong overall predictive accuracy. With targeted improvements to recall, the model could further enhance business value by retaining more eligible applicants without compromising risk management.

--------------------------------------------------------------------------------------------

Aşama 1: Veri Hazırlık ve Birleştirme

Bu projede modelleme sürecinde kullanılacak nihai veri setini oluşturmak için accepted (kabul edilen krediler) ve rejected (reddedilen krediler) olmak üzere iki farklı kaynak veri setinden yararlanılmıştır. Süreç, veri alt kümelerinin seçilmesi, kolonların birbiriyle uyumlu hale getirilmesi ve veri setlerinin birleştirilmesi adımlarından oluşmaktadır.

1. Kullanılan Veri Setleri
Accepted Dataset (Kabul Edilen Krediler)

Toplam 2.260.702 satırdan oluşmaktadır.

Model için ilk aşamada accepted verilerinin %80’i seçilmiştir.

Bu alt küme, nihai veri setinin “pozitif” sınıfını temsil etmektedir.

Rejected Dataset (Reddedilen Krediler)

Toplam 27.648.742 satırdan oluşmaktadır.

Accepted verilerinin %80’lik kısmının yaklaşık 3.5 katı kadar rejected verisi seçilmiştir.

Bu seçim, model eğitimindeki sınıf dengesizliğini azaltmak ve daha homojen bir veri dağılımı elde etmek amacıyla yapılmıştır.

2. Değişkenlerin Uyumlu Hale Getirilmesi

Accepted ve rejected veri setlerinde yer alan sütunlar birebir aynı değildir.
Bu nedenle:

Accepted veri setinde bulunan fakat rejected veri setinde bulunmayan değişkenler belirlenmiştir.

Rejected veri setine ait kolonlar, accepted veri setindeki karşılıklarıyla türü, formatı ve hesaplama mantığı aynı olacak şekilde dönüştürülmüştür.

Bazı kolonlar için sayısal dönüşümler, kategorik sınıflandırmalar veya yeniden isimlendirmeler yapılmıştır.

Tüm eşleşen kolonlar accepted veri seti ile aynı isimlerde kaydedilmiştir.

Ayrica her iki datasetine de aproval_status sutunu eklenmistir. Bu deger accepted veri setinde 1 ile; rejected veri setinde 0 ile doldurulmustur. 

Bu adımın amacı, iki veri setinin de model için ortak ve uyumlu bir şema ile temsil edilmesini sağlamaktır.

3. Veri Setlerinin Birleştirilmesi

Kolon eşleştirme tamamlandıktan sonra:

Accepted ve rejected veri setleri aynı kolon yapısına sahip olacak şekilde standartlaştırılmıştır.

Ardından bu iki veri seti dikey olarak (row-wise) birleştirilmiştir.

Bu sayede hem kabul edilen hem reddedilen kredi başvurularını içeren, dengeli ve bütünleşik bir veri seti oluşturulmuştur.

4. Nihai Sonuç

Bu aşamalar sonunda, model eğitiminde kullanılacak tek ve birleşik bir veri seti elde edilmiştir.
Bu veri seti:

Sınıf dağılımı açısından dengelidir,

Tüm kolonlar iki veri kaynağı arasında tutarlı olacak şekilde düzenlenmiştir,

Model eğitimine hazır hale getirilmiştir.


Aşama 2: Veri Temizleme, Özellik Mühendisliği ve Modelleme İçin Hazırlık

Bu aşamada, birleştirilen nihai veri seti üzerinde eksik değer işlemleri, yeni değişken türetme, kategorik değişkenlerin encode edilmesi, gereksiz sütunların temizlenmesi, train/test ayrımı ve sayısal değişkenlerin ölçeklendirilmesi gerçekleştirilmiştir. Amaç, veri setini lojistik regresyon modelinin eğitimine tamamen hazır hale getirmektir.

1. Eksik Değer Yönetimi (Missing Value Handling)

Dataset’te bazı sayısal değişkenlerde eksik değerler -1 ile temsil edilmiştir. Bu değerlerin doğru şekilde yakalanabilmesi ve modelin eksik bilgiyi öğrenebilmesi için iki adımlı bir strateji uygulanmıştır:

(a) Missing Flag Kolonları Eklendi

Aşağıdaki değişkenler için binary “missing_flag” sütunları oluşturulmuştur:

inq_last_6mths_missing

delinq_2yrs_missing

annual_inc_missing

Bu sütunlar, modelin bir gözlemde eksik bir bilgi olup olmadığını doğru şekilde yorumlamasını sağlar.

(b) Median ile Doldurma

Eksik değerler (yani –1 olanlar):

NaN ile değiştirildi

Kolonların median değerleri ile dolduruldu

Bu yöntem, uç değerlerden etkilenmeyen ve dağılımı bozmayan en güvenilir yaklaşımdır.

2. Özellik Mühendisliği (Feature Engineering)
Tarih Değişkenlerinin Ayrıştırılması

Application_Date değişkeni:

yıl → app_year

ay → app_month

gün → app_day

şeklinde parçalanmıştır.

Ardından orijinal tarih kolonu çıkarılmıştır.

3. Kategorik Değişkenlerin Kodlanması (Encoding)

Kategorik kolonlarda aşağıdaki yöntem kullanılmıştır:

One-Hot Encoding

Aşağıdaki değişkenler için pd.get_dummies() kullanıldı:

State

home_ownership

drop_first=True seçeneği ile dummy tuzağı engellendi.

Model İçin Gereksiz Kolonların Çıkarılması

Analiz ve korelasyon incelemeleri sonucunda aşağıdaki değişkenler veri setinden çıkarılmıştır:

annual_inc_missing

delinq_2yrs_missing

inq_last_6mths_missing

home_ownership_UNKNOWN

app_day

Risk_Score

home_ownership_MORTGAGE

Employment_Length

Bu değişkenler modelde anlamlı katkı sağlamadığı için kaldırılmıştır.

4. Train/Test Ayrımı
Hedef değişken (Target)

Approval_Status

Model değişkenleri (Features)

Aşağıdaki sütunlar çıkarıldı:

Approval_Status

app_year

app_month

Stratified Train/Test Split

Veri:

%80 train

%20 test

şeklinde bölünmüştür.

stratify=y parametresi kullanılmıştır.
Böylece hem train hem test setinde accepted/rejected oranı aynı tutulmuştur, bu da daha güvenilir performans ölçümü sağlar.

5. Ölçeklendirme (Scaling)
Neden Scaling?

Sayısal kolonların ölçeklerinin farklı olması lojistik regresyon modelinde ağırlıkların yanlış öğrenilmesine neden olabilir.

Ölçeklendirme Kuralları

⚠️ Sadece sayısal değişkenler scale edilmiştir.

❌ One-hot kolonları scale edilmemiştir.

❌ Missing_flag kolonları scale edilmemiştir.

✔️ Scaling train/test split’ten sonra yapılmıştır (data leakage’i önlemek için).

Kullanılan scaler

StandardScaler()

Train için fit_transform, test için transform uygulanmıştır.

Aşama 3: Lojistik Regresyon Modelinin Eğitilmesi

Bu aşamada lojistik regresyon modeli:

log_reg = LogisticRegression(max_iter=500, class_weight='balanced')


parametreleri ile eğitilmiştir.

max_iter = 500 → Modelin tam olarak yakınsaması için artırıldı.

class_weight = 'balanced' → Sınıf dengesizliğinde modelin iki sınıfa da eşit önem vermesi için kullanıldı.

Model eğitildikten sonra şu metrikler hesaplanmıştır:

Accuracy

F1-Score

ROC-AUC

Confusion Matrix

Classification Report

Tüm metrikler hem ekrana yazdırılmış hem de CSV formatında kaydedilmiştir:

model_metrics.csv

classification_report.csv

Proje Sonuçları

Bu proje kapsamında, iki büyük ölçekli veri kaynağından (accepted & rejected) oluşturulan birleşik veri seti üzerinde kapsamlı veri temizleme, özellik mühendisliği ve modelleme süreçleri yürütülmüştür. Sonuç olarak:

✔️ Çok büyük hacimli ve sınıfı dengelenmiş bir modelleme veri seti oluşturulmuştur.
✔️ Eksik değerler doğru şekilde işaretlenip medyan ile doldurulmuştur.
✔️ Kategorik değişkenler uygun yöntemlerle encode edilmiştir.
✔️ Train/test split’te stratify kullanılarak sınıf dağılımı korunmuştur.
✔️ Yalnızca sayısal değişkenlere scaling uygulanmış, data leakage tamamen önlenmiştir.
✔️ Lojistik regresyon modeli başarıyla eğitilmiş ve performans metrikleri raporlanmıştır.

Bu aşama ile birlikte kredi başvurularının kabul/red durumunu tahmin eden temel bir makine öğrenimi modeli oluşturulmuş ve değerlendirilmiştir.


Aşama 4: Model Değerlendirmesi ve Sonuçların Yorumlanması

Bu aşamada, lojistik regresyon modelinin tahmin performansı değerlendirilmiş ve kredi başvurularının kabul/red kararları bağlamında elde edilen sonuçlar yorumlanmıştır. Hesaplanan metrikler, modelin hangi başvuruların onaylanması veya reddedilmesi gerektiğini ne kadar etkili ayırt ettiğine dair kapsamlı bir bakış sunmaktadır.

Accuracy (Doğruluk): 0.969

Modelin doğruluk oranı %96.9 olup, yapılan tahminlerin büyük çoğunluğunun doğru olduğunu göstermektedir. Bu oldukça yüksek bir skor olmakla birlikte, kredi riski modellemesinde doğruluk tek başına güvenilir bir ölçüt değildir. Sınıf dağılımındaki olası dengesizlikler nedeniyle diğer metriklerin de değerlendirilmesi önemlidir.

Confusion Matrix Analizi
              Tahmin 0        Tahmin 1
Gerçek 0     1,258,246         7,754
Gerçek 1        41,924       319,876


Confusion matrix aşağıdaki içgörüleri sağlamaktadır:

True Negative (1,258,246): Reddedilmesi gereken başvuruların doğru tahmin edilmesi.

False Positive (7,754): Aslında reddedilmesi gerekirken yanlışlıkla onaylanan başvurular.
Bu hata türü kredi riski açısından en maliyetli hatadır.

True Positive (319,876): Onaylanması gereken başvuruların doğru tahmin edilmesi.

False Negative (41,924): Aslında onaylanması gerekirken reddedilen başvurular.
Bu durum iş kaybı ve gelir kaybına yol açabilir.

Genel olarak model, yanlış onay verme hatalarını (FP) daha düşük seviyede tutarak riskten kaçınan (conservative) bir davranış sergilemektedir. Bu yaklaşım, kredi riski yönetimini önceliklendiren kurumlar için genellikle tercih edilir.

Precision (Kesinlik) – Sınıf 1 (Onay): 0.98

Model, “Onay” dediği başvuruların %98’inde doğru karar vermektedir.
Bu, hatalı kredi onaylama olasılığının son derece düşük olduğunu gösterir.

Kredi risk modellerinde bu kadar yüksek precision değeri son derece güçlü bir sonuçtur.

Recall (Duyarlılık) – Sınıf 1 (Onay): 0.88

Model, gerçekten onaylanması gereken başvuruların %88’ini doğru şekilde yakalamaktadır.
Yaklaşık %12’lik bir kesim ise gereksiz şekilde reddedilmiştir.

Bu genel olarak kabul edilebilir bir sonuçtur, ancak recall değerinin iyileştirilmesi potansiyel müşteri kayıplarını azaltabilir.

F1-Score (Sınıf 1): 0.93

F1-score, precision ve recall’un dengeli bir şekilde değerlendirilmesini sağlar.
0.93 gibi yüksek bir skor, modelin hem yanlış onaylamayı hem de yanlış reddetmeyi başarılı şekilde yönettiğini ortaya koymaktadır.

ROC-AUC: 0.988

ROC-AUC değeri 0.988 olup, modelin riskli ve risksiz başvuruları ayırt etme kapasitesinin neredeyse kusursuz olduğunu göstermektedir.

Kredi modellerinde 0.85–0.90 arası bile güçlü kabul edilirken, 0.988 değeri üstün bir performansa işaret etmektedir.

Genel Değerlendirme

Model, tüm önemli performans metriklerinde çok yüksek bir başarı göstermektedir:

Risk ayrıştırma kapasitesi çok güçlüdür (yüksek ROC-AUC).

Yanlış kredi onaylama oranı oldukça düşüktür, bu da risk yönetimi açısından avantaj sağlar.

Precision ve F1-score dengeli ve yüksek seviyededir.

Recall değeri makul düzeydedir, ancak daha fazla müşteri kazanımı için iyileştirilebilir.

Sonuç

Geliştirilen lojistik regresyon modeli, kredi başvurularının kabul/red kararlarını tahmin etmek için güvenilir, sağlam ve risk odaklı bir çözüm sunmaktadır. Model, riskli başvuruların onaylanma olasılığını minimuma indirirken genel tahmin kapasitesini de yüksek seviyede tutmaktadır. Recall’ın artırılmasıyla birlikte model, hem risk yönetimi hem de müşteri kazanımı açısından daha da optimize edilebilir bir yapıya sahiptir.
