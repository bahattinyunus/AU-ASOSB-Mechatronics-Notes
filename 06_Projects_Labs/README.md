# Projeler & Laboratuvarlar: İspat Meydanı ve Hurdalık (The Proving Ground)

> *"Teoride, teori ile pratik aynıdır. Pratikte ise, dağlar kadar farklıdır."*

Burası steril bir sınıf veya sessiz bir kütüphane değil; burası bir **hurdalıktır**. Burası, bilgisayar ekranında mükemmel çalışan algoritmaların donanımla buluşunca patladığı, simülasyonda kusursuz oturan tasarımların montajda deliklerinin birbirini karşılamadığı yerdir. Ve gerçek öğrenme tam olarak bu anda, yani işler ters gittiğinde başlar.

Bir "Metal Yaka" teknisyeninin portföyü, "başarıyla tamamlanmış ve rafa kaldırılmış projeler" listesi değil; "karşılaşılan sorunlar, patlayan parçalar ve bunlara bulunan dahiyane çözümler" kataloğudur.

## 🛠️ Metal Yaka Perspektifi: Proje Kültürü ve Başarısızlık

### 1. Başarısızlık Günlüğü (Builder's Log)
Çalışan ve ışıldayan bir robotun videosunu herkes çeker ve LinkedIn'e koyar. Bizim için değerli olan o son video değil, o robotu çalıştırana kadar kaç tane motor sürücü yaktığın, kaç gece kodun çöktüğü, kaç tane dişli kırdığın ve en önemlisi; **bu sorunları nasıl analiz edip aştığındır**.
*   **Değersiz Not:** "Robotu yaptım, çalıştı."
*   **Altın Değerinde Not:** "Motor dönmüyordu. Multimetre ile pinleri ölçtüm, sinyal sürücüye geliyordu ama çıkış yoktu. Datasheet'e baktım, 'Enable' pinini High yapmayı unutmuşum. Düzelttim çalıştı. Bir daha asla Enable pinini unutmam." -> İşte bu tecrübedir.

### 2. "Hello World" Değil, "Blink LED" Hiç Değil
Bir ekrana "Hello World" yazdırmak yazılımcının işidir. Bizim dünyamızda "Hello World", fiziksel bir LED'i yakıp söndürmektir. Ama bu da yetmez. Bizim gerçek projemiz, bir motoru (kas) yük altında, ısınmadan, istenilen pozisyona, istenilen hızda götürmek ve orada sabit tutmaktır. Bu basit eylem; fizik, matematik, elektronik ve yazılımın mükemmel senfonisidir.

## 📚 Proje Kategorileri & Metal Yaka Seviye Sistemi

### Seviye 1: Çırak (Bileşenleri Tanıma ve Saygı Duyma)
*   **Çizgi İzleyen Robot:** Dışarıdan bakınca basit bir oyuncak gibi görünür. Ama PID kontrol mantığını (Orantısal tepki vermeyi) öğrenmek için dünyadaki en iyi okuldur. Sensör gürültüsüyle, motorun eylemsizliğiyle ve sürtünmeyle ilk kavgamızı burada veririz.
*   **Akıllı Sera Otomasyonu:** Sensör okumanın (sıcaklık/nem) ve röle kontrolünün (su motoru aç/kapa) temelleri. Histerezis (Hysteresis) mantığını, yani motorun sürekli "aç-kapa" yapıp yanmasını engellemeyi öğreniriz.

### Seviye 2: Kalfa (Sistemi Kurma ve Sorun Çözme)
*   **Kendini Dengeleyen Robot (Self-Balancing Robot):** Ters sarkaç problemi. Gerçek zamanlı kontrol döngüsü ve IMU (Jiroskop/İvmeölçer) sensör füzyonu (Kalman/Complementary Filtreleri) olmadan bu robot asla ayakta duramaz. Yerçekimiyle dans etmeyi öğretir.
*   **Masaüstü CNC / 3D Yazıcı Yapımı:** Kendi takım tezgahını yapmak. Step motor kontrolü, lineer rulmanlar, şase rijitliği (esnemezliği) ve güç kaynağı hesabı. Bir makinenin nasıl eksenlendiğini (X, Y, Z) öğretir.

### Seviye 3: Usta / Baş Teknisyen (Entegrasyon ve Vizyon)
*   **Görüntü İşlemeli Robot Kol (Pick & Place):** Bir kamera (OpenCV) masadaki nesneyi görür, koordinatını çıkarır, ters kinematik ile robot kolu oraya gider ve parçayı alır. Yazılımın (Görüntü İşleme), Elektroniğin (Sensörler) ve Mekaniğin (Robot Kolu) kusursuz senfonisidir.
*   **Otonom Mobil Robot (AMR) & SLAM:** Lidar sensörü ile robotun bilmediği bir odada kendi haritasını çıkarması ve yolunu bulması. ROS (Robot Operating System) ustalığı gerektirir. Geleceğin lojistik fabrikalarının temelidir.

---

> **Ustanın Bilgelik Notu:** "Çalışmayan projenizi asla çöpe atmayın. O bir başarısızlık değil, henüz çözülmemiş bir bulmacadır. Dünyanın en iyi mühendisleri, en çok parça bozanlardır; çünkü her bozdukları parçada o malzemenin limitlerini, o kodun açığını ve fiziğin kurallarını yaşayarak öğrenmişlerdir. Boza boza yapmayı öğreneceksiniz."
