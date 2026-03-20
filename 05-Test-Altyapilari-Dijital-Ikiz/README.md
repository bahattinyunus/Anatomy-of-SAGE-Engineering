# 05. Test Altyapıları ve Dijital İkiz (Digital Twin)

### Özet (Abstract)
Savunma sanayiinde "hata" bir seçenek değildir. SAGE'de bir sistemin laboratuvardan çıkıp sahaya gitmeden önce binlerce kez dijital ve fiziksel testlerden geçmesi gerekir. Bu bölüm; Donanım Döngüde (HIL) simülasyonlarından, sistemlerin tüm yaşam döngüsünü kapsayan Dijital İkiz (Digital Twin) mimarisine kadar doğrulama ve geçerli kılma (V&V) süreçlerini teknik bir perspektifle inceler.

---

## 💻 Simülasyon Hiyerarşisi: MIL'den HIL'e
Bir mühimmatın geliştirme sürecinde testler katmanlar halinde ilerler.

1. **Model in the Loop (MIL):** Matematiksel modellerin (fiziğin) yazılımla test edilmesi.
2. **Software in the Loop (SIL):** Gerçek uçuş yazılımının pc ortamında koşturulması.
3. **Hardware in the Loop (HIL):** Gerçek uçuş bilgisayarının, sensörlerin ve arayıcı başlıkların "Sanal Bir Dünya"ya bağlanarak gerçek zamanlı (real-time) test edilmesi.

**HIL'in Önemi:** SAGE'de HIL testleri, mühimmatın fırlatılmadan önce karşılaşabileceği tüm fiziksel senaryoları (rüzgar, gürültü, hedef manevrası) laboratuvara getirir. Gerçek donanımın gecikme süreleri (latency) ve elektriksel gürültüleri ancak bu aşamada doğrulanabilir.

## 🌪️ Aerodinamik Rüzgar Tüneli Testleri
Hesaplamalı Akışkanlar Dinamiği (CFD) sonuçları her zaman fiziksel dünyayla %100 örtüşmeyebilir.
* **Statik ve Dinamik Katsayılar:** Kaldırma (CL), Sürükleme (CD) ve Moment (CM) katsayılarının farklı Mach sayılarında doğrulanması.
* **Captive Flight Tests:** Mühimmatın uçak altına asılarak uçurulması ve sensör verilerinin toplanması.

## 👥 Dijital İkiz (Digital Twin) Paradigması
SAGE'nin gelecek vizyonu, her bir mühimmat birimi için bulutta veya yerel sunucularda yaşayan bir "Dijital İkiz" oluşturmaktır.
* **Ömür Takibi:** Depolama koşullarının (nem, ısı) mühimmatın elektronik bileşenlerine ve katı yakıtına etkisi.
* **Prediktif Bakım:** Sensör verilerinden arıza olasılığı tahmini.

| Test Seviyesi | Kısıtlar | Çıktı |
| :--- | :--- | :--- |
| **HIL** | Real-time işletim sistemi (RTOS) gereksinimi. | Gecikme ve Jitter analizi, Yazılım olgunluğu. |
| **Rüzgar Tüneli** | Model boyutlandırma ve maliyet. | Hassas aerodinamik veri seti. |
| **Dijital İkiz** | Veri toplama ve sürekli takip. | Ömür boyu güvenilirlik tahmini. |

---

## 🧠 Açık Mühendislik Problemi (Open Engineering Problem)
**Problem: "HIL Simülasyonunda Gerçek Zamanlılık ve Veri Sadakati"**

Bir RF Arayıcı Başlığı (RF Seeker) testi için 40,000 Hz'lik analog veri çıkışı sağlayan bir simülatör tasarlıyorsunuz. Gerçek dünya fiziksel olaylarını simüle eden bilgisayarın, bu veriyi hesaplayıp seeker'a aktarması için sadece 25 mikrosaniye süresi vardır.

**Soru:** *Bilgisayarın hesaplama süresindeki milisaniyelik bir gecikme (jitter), seeker'ın kafasının karışmasına ve "kararsızlığa" (instability) girmesine neden olur. Bu gerçek zamanlılık problemini çözmek için "FPGA Tabanlı Simülasyon" ve "Paralel Hesaplama" mimarisini nasıl kurgularsınız? Deterministik olmayan bir işletim sistemi (Windows/Standart Linux) kullanmak neden imkansızdır?*
