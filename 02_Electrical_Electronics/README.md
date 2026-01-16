# 02. Elektrik & Elektronik: Devre Cerrahlığı, Dumanın Ruhu ve Fiziksel Hata Ayıklama

![High Voltage](https://img.shields.io/badge/DANGER-High%20Voltage-red?style=for-the-badge&logo=electricity)
![Skill](https://img.shields.io/badge/Skill-Soldering-blue?style=for-the-badge&logo=espressif)

> *"Yazılımda hata yaparsan ekranda bir uyarı çıkar; elektronikte hata yaparsan bir patlama sesi duyarsın ve o korkunç yanık silikon kokusunu alırsın. Ve unutma, duman bir kez çıktıysa, o komponentin ruhu bedeni terk etmiştir; geri döndürülemez."*

---

## ⚡ Metal Yaka Perspektifi: Devre Cerrahlığı

Mezun olduğunuzda kimse sizden Kirchhoff kanunlarını kağıt üzerinde ispatlamanızı istemeyecek. Sizden beklenen; durmuş bir üretim hattındaki panoyu açıp, yüzlerce kablo ve onlarca kart arasından arızalı olan o **tek bir komponenti** bulmanız ve sistemi hayata döndürmenizdir.

Yazılım "Sanal Beyin" ise, Elektronik "Sinir Sistemi" ve "Kardiyovasküler Sistem"dir.
*   **Voltaj:** Kan Basıncıdır.
*   **Akım:** Kan Akışıdır.
*   **Kablo Kesiti:** Damar genişliğidir.
*   **Kısa Devre:** Aort damarının parçalanmasıdır.

Bu modül, sadece teorik şemaları değil, **"Çalışmayan"** veya **"Yanmış"** bir devreyi teşhis etme (diagnosis) ve onarma sanatını; yani **Devre Cerrahlığını** anlatır.

---

## 🛠️ 1. Duman Prensibi ve Geri Dönülmezlik

Elektronik dünyasında "Ctrl+Z" (Geri Al) tuşu yoktur.
*   Bir MOSFET'i yanlış tetikleyip yaktıysan, o artık kömürdür.
*   Bir kondansatörü ters bağlayıp patlattıysan, o artık bir şarapneldir.
*   **Kural:** "Önce Ölç, Sonra Enerji Ver."

### Görünmez Düşman: Gürültü (Noise) ve EMI
Dijital dünyada mantık temizdir (0 veya 1). Fiziksel dünyada ise kaos vardır.
*   **Senaryo:** Motor çalışınca sensör saçmalıyor. Motor durunca düzeliyor.
*   **Teşhis:** Motor kablosu, bir yayın anteni gibi etrafa elektromanyetik parazit (EMI) yayıyor. Sensör kablosu da bir anten gibi bu paraziti topluyor.
*   **Çözüm:** Ekranlı (Shielded) kablo kullanmak, ekranı **tek noktadan** topraklamak, Ferrit boncuk takmak. Yazılımla bunu çözemezsin.

---

## 🧰 2. Teşhis Aletleri: Cerrahın Çantası

### A. Multimetre: Stetoskop
*   **Voltaj:** Devrede can var mı?
*   **Direnç:** Kablo kopuk mu (sonsuz ohm), kısa devre mi (0 ohm)?
*   **Diiyot Modu:** Yarı iletkenler (Transistör, Regülatör) sağlam mı? PN jonksiyonu 0.6V-0.7V gösteriyor mu?

### B. Osiloskop: Zamanın Mikroskobu ve Röntgen
Multimetre size yalan söyler. Multimetre size voltajın "ortalamasını" gösterir.
*   3.3V sandığınız DC gerilim, belki de saniyede 1 milyon kez 0V ile 5V arasında dalgalanıyordur (Ripple).
*   PWM sinyalinin kare dalgası bozulmuş mu? Köpekbalığı yüzgecine mi benziyor? (Kapasitif yük sorunu).
*   Haberleşme hattında (I2C/UART) parazit var mı?
*   **Osiloskopsuz elektronikçi, kör bir nişancı gibidir.**

### C. Laboratuvar Güç Kaynağı: Yaşam Destek Ünitesi
*   **Akım Sınırlama (Current Limiting):** Kartı tamir ettikten sonra direkt prize takarsan tekrar patlayabilir. Güç kaynağını 0.1 Amper'e ayarla. Eğer kısa devre varsa, güç kaynağı voltajı keser (CC Mode) ve kartı korur.

### D. Termal Kamera: Isı Haritası
*   Kısa devre olan parça, enerjiyi ısıya çevirir. Karta enerji verip termal kamerayla bakarsan, arızalı parça **"Ben Buradayım!"** diye parlar.

---

## 📚 Modül İçeriği ve Saha Rehberi

| Dosya | Açıklama | Saha Uygulaması |
| :--- | :--- | :--- |
| **[`02_Oscilloscope_Guide.md`](./02_Oscilloscope_Guide.md)** | Osiloskop Rehberi | Sinyal yakalama, PWM analizi, Gürültü tespiti. |
| **[`02_Soldering_Art.md`](./02_Soldering_Art.md)** | Lehim Sanatı | Soğuk lehim tespiti, Flux kullanımı, SMD lehimleme. |
| **[`03_Component_Failure.md`](./03_Component_Failure.md)** | Komponent Arıza Kataloğu | Bir parça neden ve nasıl yanar? Görsel otopsi. |
| **[`04_Grounding_Noise.md`](./04_Grounding_Noise.md)** | Topraklama ve Gürültü | Şase döngüleri (Ground Loops), ekranlama, parazit. |

---

## 🩸 Güç Elektroniği: Sistemin Kasları

Sistem sadece 5V ve 3.3V'dan ibaret değildir. Motorları süren 24V, 48V veya 380V güç katı vardır.
*   **H-Köprüsü (H-Bridge):** Motoru ileri-geri süren 4 anahtarlı yapı.
*   **Shoot-Through (Kısa Devre Vuruşu):** Aynı hattaki üst ve alt anahtarı (MOSFET) aynı anda açarsan, güç kaynağını kısa devre edersin (Bom!). Donanımsal **"Dead-Time"** (Ölü Zaman) koymak zorundasın.

---

> **Ustanın Bilgelik Notu:**  
> "İyi bir elektronikçi, devrenin şemasına değil, kokusuna ve sıcaklığına güvenir. Yanık bir direnç, sebep değil sonuçtur. O direnci yakan asıl suçluyu (genellikle kısa devre olmuş bir kondansatör veya transistör) bulmadan sakın yenisini takma."
