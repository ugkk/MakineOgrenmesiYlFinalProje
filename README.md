# MakineOgrenmesiYlFinalProje
Bu projede HIGGS veri seti kullanılarak makine öğrenmesi pipeline'ı uygulanmıştır. Proje kapsamında,
- Aykırı değer temizliği (IQR yöntemi),
- Özellik ölçekleme (StandartScaler),
- ANOVA F-score ile öznitelik seçimi (k = 10, 15, 20),
- Nested Cross-Validation (outer 5-fold, inner 3-fold) ile hem öznitelik sayısı hem hiperparametre seçimi (Flowchart A ve B),
- KNN, SVM, MLP ve XGBoost modelleri ile sınıflandırma gerçekleştirilmiştir.

HIGGS veri seti üzerinde dört farklı sınıflandırma algoritması (KNN, SVM, MLP, XGBoost) kullanılarak özellik seçimi (ANOVA F-score yöntemiyle) ve hiperparametre optimizasyonu (nested cross-validation ile) gerçekleştirilmiştir. Projede toplam 100.000 örnek kullanılmış ve veri ön işleme adımları olarak IQR yöntemiyle aykırı değer temizliği ve StandardScaler ile ölçekleme uygulanmıştır.

# Model Performanslarının Karşılaştırması


 XGBoost, en yüksek performansı gösteren model olarak öne çıkmıştır. Bu modelin başarısı, özellikle büyük veri setleri ve yüksek boyutlu öznitelikler üzerinde güçlü genelleme kabiliyeti ve düzenli öğrenme algoritmaları sayesinde açıklanabilir. Ayrıca, XGBoost’un tree boosting mekanizması sayesinde overfitting riski azaltılmıştır.KNN modeli, nispeten daha basit bir algoritma olmasına rağmen etkili sonuçlar vermiştir. Ancak, modelin performansı veri büyüklüğüne ve k komşuluk parametresine oldukça duyarlıdır. Kullanılan n_neighbors değerlerinin optimize edilmesi performansı artırmıştır. MLP (Multi-Layer Perceptron) modelinde ise derin öğrenmenin hesaplama yükü ciddi bir performans darboğazı oluşturmuştur. Özellikle GridSearchCV ile hiperparametre taraması yapılırken veri boyutunun büyük olması ve max_iter=300 gibi iterasyon sayılarının fazlalığı nedeniyle işlem süreleri uzamış, bazı parametre kombinasyonları sonuç alınamadan sonlandırılmıştır. Buna rağmen temel bir MLP yapısı ile anlamlı sonuçlar elde edilmiştir. SVM modeli ise büyük veri setleri ile çalışırken ciddi zaman ve kaynak tüketimi göstermiştir. Özellikle probability=True ayarı altında yapılan eğitimler, Platt Scaling sebebiyle ek eğitimler gerektirmiş ve işlem sürelerini artırmıştır. Bu nedenle probability=False ile sadeleştirilmiş versiyonu kullanılmıştır. 


 # XGBoost – En Yüksek Doğruluk Oranı
XGBoost modeli, genellikle yüksek boyutlu veri setlerinde üstün doğruluk performansı gösterir.Bu çalışmada da en iyi doğruluk oranı bu modelle elde edilmiştir.Boosting mekanizması sayesinde zayıf sınıflandırıcılar bir araya getirilerek güçlü bir model oluşturulmuştur.Aynı zamanda overfitting'e karşı güçlüdür, bu da doğruluk oranını artırıcı etki yapar.

# MLP (Multi-Layer Perceptron) – Orta Seviye Doğruluk
MLP modeli doğruluk açısından genellikle iyi performans gösterse de bu çalışmada işlem yükü nedeniyle bazı hiperparametre denemeleri yapılamamıştır.Doğruluğu yüksek olabilir ancak eğitim süresi uzun olduğu için tüm potansiyeli ortaya çıkamamış olabilir.Batch-learning (toplu öğrenme) kullanımı işlem süresini uzatırken doğruluğu sınırlı düzeyde optimize etmiştir.

# SVM – Nispeten Düşük Doğruluk (Veri Setine Bağlı)
SVM, küçük veya orta ölçekli veri kümelerinde yüksek doğruluk gösterse de bu çalışmada veri setinin büyüklüğü nedeniyle hesaplama açısından verimli olamamıştır. Bu nedenle doğruluk seviyesi optimum değerlere ulaşamamış olabilir. Ayrıca probability=False olarak çalıştırılması, modelin ayrıntılı kalibrasyonundan ödün verilmesi anlamına gelir.

# KNN – Orta Seviye ve Stabil Doğruluk
KNN modeli, doğru seçilen k değeri ile oldukça stabil ve tatmin edici doğruluk oranları sunabilir.
Ancak büyük veri setlerinde her tahmin için tüm veri üzerinde işlem yapması gerektiğinden doğruluk/performans dengesinde zorluk yaşanabilir. Bu çalışmada k=3, 12 gibi değerlerle optimize edilmiş ve başarı elde edilmiştir.

MLP ve SVM gibi algoritmalarda işlem sürelerinin uzun olması dikkat çekmektedir. Bu durum, gelecekte veri seti küçültme (örnekleme), paralel işlem ya da daha verimli mimarilerin (örneğin LightGBM, CatBoost) tercih edilmesi ile geliştirilebilir.  





