# Ödev 2 — Model iyileştirme ve ROC analizi

## Amaç

İlk ödevdeki spam/normal e-posta sınıflandırma deneyini geliştirmek; model parametrelerini eğitim verisinde çapraz doğrulamayla ayarlamak ve algoritmaları ROC eğrileri ile ROC-AUC kullanarak karşılaştırmak.

## Veri ve deney düzeni

UCI Spambase veri kümesi kullanılmıştır. Veri setinde 4.601 örnek ve e-postalardan çıkarılmış 57 sayısal özellik bulunur; ham e-posta metni içermez. Etiket 0 normal, 1 spam anlamına gelir.

Veri, sınıf oranları korunarak `random_state=42` ile yüzde 80 eğitim ve yüzde 20 test olarak ayrılmıştır. Parametre araması yalnızca eğitim kümesinde beş katlı StratifiedKFold çapraz doğrulamasıyla yapılmıştır. Ölçekleme gereken modellerde StandardScaler, veri sızıntısını önlemek için Pipeline içinde kullanılmıştır. Test kümesi nihai değerlendirme için ayrılmıştır.

Karşılaştırılan algoritmalar:
- Gaussian Naive Bayes
- Lojistik Regresyon
- RBF çekirdekli Destek Vektör Makinesi
- Random Forest

Arama hedefi çapraz doğrulamada spam F1 skorudur. Arama aralıkları ve kod `notebooks/model_iyilestirme_roc.ipynb` içindedir.

## Sonuçlar

Colab'da notebook çalıştırıldığında dört ayarlanmış modelin ROC eğrileri aynı test kümesinde oluşturuldu. Grafikte görünen ROC-AUC değerleri (üç ondalık basamağa yuvarlanmış):

| Ayarlanmış model | ROC-AUC |
|---|---:|
| Gaussian Naive Bayes | 0,945 |
| Lojistik Regresyon | 0,968 |
| SVM (RBF) | 0,979 |
| Random Forest | 0,984 |

En iyi ayarlanmış model, test spam F1 skoruna göre **Random Forest** oldu. Confusion matrix'ten hesaplanan ölçümleri:

- Accuracy: 870/921 = **%94,46**
- Spam precision: 331/350 = **%94,57**
- Spam recall: 331/363 = **%91,18**
- Spam F1: **%92,85**
- ROC-AUC: grafikte yaklaşık **0,984**

Ayar araması test F1 skorunu mutlaka yükseltmez. Bu çalıştırmada ayarlanmış Random Forest'ın spam F1'i %92,85'tir; ilk ödevdeki temel Random Forest sonucu %92,96 idi. Bu küçük fark, eğitimde çapraz doğrulamayla seçilen ayarların ayrılmış test kümesinde daha iyi sonuç garantilemediğini gösterir. Amaç, ayarları test verisine bakarak seçmeden karşılaştırma yapmaktır. Ayrıntılı temel/ayarlanmış metrik tablosu Colab notebook çıktısındadır.

**ROC-AUC yorumu:** AUC 1'e yaklaştıkça model normal ve spam e-postaları farklı eşiklerde daha iyi ayırt eder. Grafiğin sol üst köşesine yakın olması tercih edilir. Kesikli çapraz çizgi rastgele tahmin seviyesini (AUC=0,5) gösterir.

## Confusion matrix ve hata analizi

En iyi ayarlanmış modelin notebook'ta gösterilen confusion matrix'ini buraya aktarın:

| Gerçek / Tahmin | Tahmin normal | Tahmin spam |
|---|---:|---:|
| Gerçek normal | TN: — | FP: — |
| Gerçek spam | FN: — | TP: — |

FP, normal bir e-postaya yanlışlıkla spam denmesidir. FN, spam e-postanın normal sanılıp kaçırılmasıdır. TN ve TP doğru sınıflandırmalardır.

## Değerlendirme

Temel ve ayarlanmış modelleri test spam F1 ve ROC-AUC açısından karşılaştırın. Ayar aramasının sonucu her ölçütte iyileştireceği garanti değildir; sonucu notebook'un gerçek çıktısına göre yorumlayın. Spam'i kaçırmanın mı yoksa normal e-postaya yanlış alarm vermenin mi daha maliyetli olduğuna göre precision ve recall dengesini de açıklayın.

## Sınırlama

UCI Spambase ham e-posta gövdelerini değil, önceden çıkarılmış sayısal özellikleri içerir. Bu deney metin temizleme, kelime vektörleştirme veya yeni e-postalardan özellik çıkarma yapmaz. Sonuçlar bu veri seti, veri bölünmesi ve denenmiş parametre aralıklarıyla sınırlıdır.
