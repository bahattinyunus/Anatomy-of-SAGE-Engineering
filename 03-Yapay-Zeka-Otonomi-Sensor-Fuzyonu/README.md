# 03. Yapay Zeka, Otonomi ve Sensör Füzyonu

### Özet (Abstract)
Modern mühimmat sistemleri artık sadece "güdülen" değil, "karar veren" platformlardır. SAGE'nin otonomi vizyonu; karmaşık, gürültülü ve hasmane (denied-area) ortamlarda platformun görevini başarıyla tamamlamasını sağlayan algoritmik bir zırh inşa etmektir. Bu bölüm, Kalman filtrelerinden derin öğrenme tabanlı hedef tanıma sistemlerine kadar sensör füzyonunun ve yapay zekanın "Edge" (uç) cihazlardaki mimarisini inceler.

---

## 🛰️ Sensör Füzyonu ve Kalman Filtreleme
Bir mühimmatın konumu asla tek bir sensöre emanet edilmez. INS (Ataletsel Navigasyon), GPS (Küresel Konumlama) ve Seekers (Arayıcı Başlıklar) verileri birleştirilerek "En İyi Tahmin" (Best Estimate) oluşturulur.

* **Genişletilmiş Kalman Filtresi (EKF):** Dinamik sistem olmayan doğrusal (non-linear) yapıları doğrusal hale getirerek konum tahminlemeyi sağlar.
* **Gürültü Yönetimi (Noise Management):** Sensörlerden gelen beyaz gürültünün (Gaussian noise) sistemden arındırılması ve bias hatalarının anlık olarak kompanse edilmesi.
* **GNSS-Denied Area:** GPS sinyalinin köreltildiği (jamming) ortamlarda, sadece INS ve görsel navigasyon verisiyle (Optical Flow) milimetrik hassasiyette seyrüsefer yapma yeteneği.

## 🤖 Uç Noktada Yapay Zeka (Edge AI) ve Gömülü Sistemler
SAGE sistemlerindeki yapay zeka, bulut sunucularda değil, yüksek G kuvveti ve ısı altında çalışan küçük bir FPGA veya DSP üzerinde çalışmak zorundadır.

| AI Katmanı | Teknik Yaklaşım | Görev Tanımı |
| :--- | :--- | :--- |
| **Görü Algılama** | CNN (Convolutional Neural Networks) | Hedeften gelen görüntünün sınıflandırılması (Dost/Düşman/Hedef Tipi). |
| **Harekât Planlama** | Takviyeli Öğrenme (Reinforcement Learning) | Dinamik engellerden (radar alanı, hava savunma) kaçınma rotası çizme. |
| **Sürü Zekası** | Dağıtık Konsensüs Algoritmaları | Çoklu mühimmatın birbirini engellemeden hedef paylaşımı yapması. |

## 🕹️ Otonomi ve Karar Verme Mekanizmaları
Tam otonomi, mühimmatın fırlatıldıktan sonra operatörle bağını kestiğinde bile "Etik ve Teknik" kurallar çerçevesinde görevini yapabilmesidir.
* **A* ve RRT* Algoritmaları:** Gerçek zamanlı rota planlama.
* **Hedef Kilitleme (Lock-on After Launch):** Fırlatıldıktan sonra havada hedef arama ve kilitlenme yeteneği.

---

## 🧠 Açık Mühendislik Problemi (Open Engineering Problem)
**Problem: "GNSS Olmayan Ortamda Görsel Coğrafi Konumlama"**

Bir seyir füzesi, GPS sinyali tamamen kesilmiş bir vadi içerisinde 900 km/s hızla seyretmektedir. Altta bulunan kamera, yer yüzeyini taramaktadır ancak yerdeki doku (texture) düşük ışık veya yoğun bulutluluk nedeniyle belirsizdir.

**Soru:** *Kameradan gelen görüntü ile füzenin içinde yüklü olan dijital yükseklik haritası (DEM) arasındaki eşleşmeyi nasıl sağlarsınız? Standart bir görüntü eşleme (Template Matching) algoritması, yüksek hızdaki hareket (motion blur) altında çalışmayacaktır. Bu sorunu "Feature Extraction" (Özellik Çıkarımı) ve "Olasılıksal Parçacık Filtresi" (Particle Filter) kullanarak nasıl çözersiniz? Gecikme süresini (Latency) 20ms'nin altına nasıl indirirsiniz?*
