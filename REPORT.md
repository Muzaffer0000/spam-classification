# Spam ve Normal E-posta Sınıflandırması — Proje Raporu

## 1. Amaç

Bu çalışmada amaç, etiketli e-posta örneklerini **normal (ham)** ve **spam** olarak sınıflandırmaktır. Aynı eğitim ve test verisi üzerinde dört makine öğrenmesi algoritması eğitilmiş, performans ölçütleri karşılaştırılmış ve en iyi sonuç veren model seçilmiştir.

## 2. Veri seti

- **Kaynak:** [UCI Machine Learning Repository — Spambase](https://archive.ics.uci.edu/dataset/94/spambase)
- **Örnek sayısı:** 4.601
- **Girdi özellikleri:** 57 sayısal özellik
- **Hedef etiketi:** 0 = normal, 1 = spam
- **Sınıf dağılımı:** 2.788 normal, 1.813 spam

**Veri seti sınırlaması:** Spambase, e-postaların ham metin gövdelerini değil, e-postalardan önceden çıkarılmış sayısal özellikleri içerir. Bu nedenle çalışma, ham metin üzerinde sözcük temizleme veya metin vektörleştirme yapmaz; hazır özelliklerden spam sınıflandırması yapar.

## 3. Uygulama yöntemi

Veri, sınıf oranları korunarak eğitim ve test kümelerine ayrılmıştır. Verinin yüzde 80'i (3.680 örnek) modelleri eğitmek, yüzde 20'si (921 örnek) daha önce görülmemiş örneklerde değerlendirmek için kullanılmıştır. Sonuçların tekrarlanabilmesi için **random_state=42** kullanılmıştır.

Lojistik Regresyon ve Destek Vektör Makinesi öncesinde özellikler ölçeklenmiştir. Ölçekleme, eğitim ve test verisinin birbirine karışmaması için modellerin işlem hattı içinde uygulanmıştır. Dört model de aynı veri bölünmesinde değerlendirilmiştir.

## 4. Karşılaştırılan algoritmalar

1. **Gaussian Naive Bayes:** Özellikler arasındaki bağımsızlık varsayımını kullanarak sınıf olasılıklarını hesaplar.
2. **Lojistik Regresyon:** Özelliklerden sınıf olasılığını öğrenen doğrusal bir sınıflandırıcıdır.
3. **Destek Vektör Makinesi (RBF):** Sınıflar arasındaki ayrımı bulur; RBF çekirdeği doğrusal olmayan sınırlar öğrenmesine yardımcı olur.
4. **Random Forest:** Farklı örnek ve özelliklerle eğitilen çok sayıda karar ağacının tahminlerini birleştirir.

## 5. Değerlendirme ölçütleri

Spam sınıfı pozitif sınıf (1) olarak kabul edilmiştir.

- **Accuracy (doğruluk):** Tüm test e-postalarının ne kadarının doğru sınıflandırıldığını gösterir.
- **Precision (spam kesinliği):** Modelin spam dediği e-postaların ne kadarının gerçekten spam olduğunu gösterir.
- **Recall (spam yakalama oranı):** Gerçek spam e-postaların ne kadarının yakalandığını gösterir.
- **F1 skoru:** Precision ve recall değerlerini birlikte özetler. Modelleri seçerken spam sınıfının F1 skoru esas alınmıştır.
- **Confusion matrix (karmaşıklık matrisi):** Gerçek sınıflarla model tahminlerini çaprazlayan tablodur. Satırlar gerçek sınıfı, sütunlar tahmini gösterir.

## 6. Model karşılaştırma sonuçları

| Model | Accuracy | Precision (spam) | Recall (spam) | F1 (spam) |
|---|---:|---:|---:|---:|
| Gaussian Naive Bayes | 83,39% | 71,78% | 95,32% | 81,89% |
| Lojistik Regresyon | 92,94% | 92,09% | 89,81% | 90,93% |
| Destek Vektör Makinesi (RBF) | 92,73% | 92,77% | 88,43% | 90,55% |
| **Random Forest** | **94,57%** | **95,10%** | **90,91%** | **92,96%** |

Bu veri bölünmesinde en yüksek spam F1 skoru Random Forest modelinde elde edilmiştir. Random Forest ayrıca en yüksek accuracy ve spam precision değerlerini vermiştir. Naive Bayes spam'lerin daha büyük bölümünü yakalamıştır (recall %95,32), ancak spam precision değeri daha düşük olduğu için daha fazla normal e-postayı yanlışlıkla spam olarak işaretlemiştir.

## 7. En iyi modelin confusion matrix'i

Sınıf sırası **normal, spam**; satırlar gerçek, sütunlar tahmin olacak şekildedir:

| Gerçek / Tahmin | Tahmin normal | Tahmin spam |
|---|---:|---:|
| Gerçek normal | 541 (TN) | 17 (FP) |
| Gerçek spam | 33 (FN) | 330 (TP) |

- **TN = 541:** Normal e-postalar doğru biçimde normal sınıflandırılmıştır.
- **FP = 17:** Normal e-postalar yanlışlıkla spam olarak işaretlenmiştir.
- **FN = 33:** Spam e-postalar normal olarak tahmin edilmiş, yani kaçırılmıştır.
- **TP = 330:** Spam e-postalar doğru biçimde yakalanmıştır.

Model, 921 test örneğinin 871'ini doğru sınıflandırmıştır: (541 + 330) / 921 = %94,57 doğruluk.

## 8. Sonuç ve sınırlamalar

Bu deneyde dört algoritma aynı eğitim/test ayrımında karşılaştırılmış; spam F1 skoru ve accuracy bakımından en iyi sonuç Random Forest ile elde edilmiştir. Seçilen model test kümesinde 17 yanlış spam alarmı ve 33 kaçırılan spam üretmiştir. Bu sayılar, yalnızca kullanılan Spambase veri seti ve sabit eğitim/test bölünmesi için geçerlidir; başka veri kümelerinde sonuçlar değişebilir.

Çalışmanın önemli sınırlaması, veri setinin ham e-posta metnini değil önceden çıkarılmış sayısal özellikleri içermesidir. Ayrıca sonuçlar tek bir eğitim/test bölünmesine dayanmaktadır; farklı e-posta kaynaklarına doğrudan genellenmemelidir.

## Kaynakça

Hopkins, M., Reeber, E., Forman, G., & Suermondt, J. (1999). *Spambase*. UCI Machine Learning Repository. https://doi.org/10.24432/C53G6X
