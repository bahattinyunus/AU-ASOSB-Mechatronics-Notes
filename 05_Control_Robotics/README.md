# Kontrol Sistemleri & Robotik: Robot Doktorluğu ve Sistem Cerrahlığı

> *"Otonom sistemler (AI) dünyayı yönetecek, peki o sistemler hastalandığında, delirdiğinde veya travma geçirdiğinde onlara kim bakacak?"*

Bizler, **Robot Doktorlarıyız**. Otonom bir fabrikadaki robot kolu aniden durduğunda, sorun her zaman "buglı kod" değildir. Belki bir dişli sıyırmıştır, belki triger kayışı gevşemiştir, belki de enkoderin optik okuyucusu tozlanmıştır. Bir AI yazılımında hata (bug) olduğunda sunucuyu yeniden başlatabilirsiniz; ama bir robot kolu 200kg yükle kontrolsüzce bir yere çarptığında onu "tamir" etmelisiniz. Bu, dijital değil fiziksel bir müdahaledir.

## 🛠️ Metal Yaka Perspektifi: Robot Yoğun Bakım Ünitesi (Robot ER)

### 1. Diagnosis (Teşhis Koyma Sanatı)
Robotun ekranında beliren hata kodu: "Eksen 4 - Aşırı Akım Hatası (Overcurrent Error)".
*   **Beyaz Yaka Yaklaşımı:** Kodu inceler, belki akım limitlerini yazılımla artırır. Bu tehlikelidir, motoru yakabilir.
*   **Metal Yaka Yaklaşımı:** Robotun yanına gider. Eksen 4'ün motoruna elini koyar. "Çok mu ısınmış?". Freni manuel olarak açıp ekseni eliyle hareket ettirmeye çalışır. "Sıkışma var mı?". Belki de 4. eksendeki elektromanyetik fren balatası yapışmıştır ve motor freni yenmeye çalışırken aşırı akım çekiyordur. İşte bu, yazılımla çözülemeyen, dokunarak ve hissederek çözülen bir arızadır.

### 2. Kalibrasyon: Robotun Sıfır Noktası
Robotun uzayda nerede olduğunu bilmesi gerekir. Her robotun bir "Home" veya "Zero" pozisyonu vardır. Bir çarpışma (Collision) sonrası veya kayış değişiminden sonra bu "sıfır noktası" kayar. Robotu (Mastering/Zeroing) yeniden kalibre etmek, bir virtüözün enstrümanını akort etmesi gibidir. Çok hassas, büyük sabır isteyen ve mükemmel bir "kulak" (tecrübe) gerektiren bir sanattır.

## 📚 Konu Başlıkları ve Derinlemesine Saha Uygulamaları

### Kontrol Teorisi: Denge ve Kararlılık
*   **PID Kontrol:** Bu sadece bir formül değildir (Oransal, İntegral, Türev). Sistemin karakteridir.
    *   **P (Proportional):** Şimdiki hataya tepki verir. Çok yüksekse sistem titrer.
    *   **I (Integral):** Geçmiş hataları toplar, hedefe tam oturmayı sağlar. Çok yüksekse sistem hantal kalır (Overshoot).
    *   **D (Derivative):** Geleceği tahmin eder, fren yapar.
    *   **Tuning (Ayar):** Robot titriyor mu? D kazancını azalt. Hedefe varamıyor mu? I kazancını artır. Bu matematiksel bir işlemden çok, makineyle dans etmek gibidir.

### Robot Kinematiği: Hareketin Geometrisi
*   **İleri Kinematik:** "Motorlara şu açıları veriyorum, robotun ucu (TCP) uzayda hangi (X,Y,Z) noktasına gider?"
*   **Ters Kinematik:** "Robotun ucunun şu (X,Y,Z) noktasına gitmesini istiyorum, motorların her birinin açısı kaç derece olmalı?" (Bu hesabı yapmak zordur, AI yapar ama doğrulamak sizin işinizdir.)
*   **Tekillik (Singularity):** Robotun matematiksel olarak kilitlendiği, sonsuz hıza çıkmaya çalıştığı kör noktalar. Robot bu noktaya yaklaşırsa kontrolsüzce savrulur. Bir Metal Yaka, robotu programlarken bu "ölüm bölgelerinden" (Singularity Zones) uzak tutmayı bilir. Çünkü bu, operatörün hayatını korumak demektir.

### Endüstriyel Otomasyon: Fabrikanın Beyni
*   **PLC (Programlanabilir Mantık Denetleyicisi):** Endüstrinin kalbi. PC gibi mavi ekran vermez, virüs bulaşmaz, tozdan etkilenmez, 7/24 çalışır. Ladder diyagramı ile mantık kurmak.
*   **SCADA:** Fabrikanın kokpiti. Binlerce sensörden gelen veriyi tek ekrandan izlemek. Kırmızı bir alarm yandığında, sahada hangi motorun, hangi sensörün arızalandığını nokta atışı bulmak.

---

> **Ustanın Bilgelik Notu:** "Robotun gücüne asla güvenme, sadece Acil Durdurma (Emergency Stop) butonuna güven. Robotun gözü yoktur (kamera takmadıysan), hissi yoktur (tork sensörü yoksa) ve vicdanı yoktur. Yörüngesinin önüne geçersen seni ezer geçer ve bir hata oluştuğunu bile anlamadan işine devam eder. Robotla şakalaşma."
