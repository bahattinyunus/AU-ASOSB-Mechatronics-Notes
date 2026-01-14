# Elektrik & Elektronik: Devre Cerrahlığı ve Fiziksel Hata Ayıklama

> *"Elektronikte duman bir kez çıktıysa, o komponentin ruhu bedeni terk etmiştir ve geri döndürülemez."*

Elektronik, mekatronik sistemin sinir sistemidir. Yazılım (beyin) emirleri verir, mekanik (kas) bu emirleri uygular; ancak bu emirleri taşıyan, ileten, güçlendiren ve gücü sağlayan elektroniktir. Bir yazılımcı hata yaptığında genellikle zararsız bir hata mesajı veya "bip" sesi duyar. Ancak bir elektronik mühendisi hata yaptığında şiddetli bir **patlama** sesi duyar, ardından o karakteristik ve geniz yakan yanık silikon kokusunu alır.

Bu modül, sadece teorik devre şemaları çizmekten ziyade, "çalışmayan" veya "yanmış" bir devreyi hayata döndürme sanatına odaklanır. Biz buna **Fiziksel Hata Ayıklama (Physical Debugging)** veya daha havalı bir tabirle **Devre Cerrahlığı** diyoruz.

## 🛠️ Metal Yaka Perspektifi: Devre Cerrahlığı Prensipleri

### 1. Dumanı Asla Geri Koyamazsın
Elektronik dünyasında "Ctrl+Z" veya "Undo" tuşu yoktur. Bir MOSFET'i yanlış tetikleyip yaktıysan, o artık yanmıştır. Bu yüzden "önce ölç, sonra enerji ver" kuralı bizim değişmez kanunumuzdur.
*   **Cerrahın Neşteri (Havya):** İyi bir lehim, parlak, pürüzsüz ve konik yapısıyla bir sanat eseridir. "Soğuk lehim" ise sistemin gizli kanseridir; bazen temas eder çalışır, bazen etmez durur. En zor bulunan, saç baş yolduran arızalar genellikle çatlak bir lehimin eseridir.

### 2. Görünmez Düşman: Elektriksel Gürültü (Noise)
Dijital simülasyon dünyasında sadece net 1 ve net 0 vardır. Fiziksel dünyada ise 0.9V, 3.3V, 5.1V, anlık dikenler (spikes), parazitler ve dalgalanmalar vardır.
*   **Osiloskop (Zamanın Mikroskobu):** Elektronikçinin gerçek gözüdür. Multimetre size voltajın ortalamasını gösterir ve bu bazen yalandır. Osiloskop ise size sinyalin gerçeğini, anlık bozulmaları, gürültüyü ve dalga formunu gösterir. PWM sinyalinin köşeleri ne kadar dik? I2C hattında "ringing" var mı? Bunu sadece osiloskopla görebilirsiniz.

## 📚 Konu Başlıkları ve Derinlemesine Saha Uygulamaları

### Temel Analiz ve Hata Avı Sanatı
*   **Ohm ve Kirchhoff Yasaları:** Bunlar sadece sınav geçmek için değil, arızayı eliyle koymuş gibi bulmak içindir. Bir kabloda veya bağlantı noktasında beklenmedik bir voltaj düşümü (Voltage Drop) varsa, orada istenmeyen bir direnç vardır. Kablo gevşemiştir, klemens oksitlenmiştir veya lehim çatlamıştır.
*   **Kısa Devre Takibi:** Bir kartın beslemesi kısa devre mi gösteriyor? Hangi parçanın yandığını bulmak için laboratuvar tipi güç kaynağı ile akımı sınırlayıp voltaj vermek ve ısınan parçayı (termal kamera veya dikkatli bir parmak testi ile) bulmak, gerçek bir dedektiflik işidir.

### Analog Elektronik: Sinyal İşleme
*   **Op-Amp'lar (Operasyonel Yükselteçler):** Sensörden gelen cılız milivolt seviyesindeki sinyali, mikrodenetleyicinin okuyabileceği seviyeye yükseltmek. AI'a giden veri buradan geçer. Eğer bu kat bozuksa veya gürültülü ise, AI çöp veriyle eğitilir ve kararlar alır.
*   **Filtreler ve Gürültü Bastırma:** Fabrika ortamı elektriksel olarak "çok kirlidir". Büyük motorların sürücüleri şebekeye parazit yayar. Kondansatörler (Bypass/Decoupling) ve bobinlerle bu sinyalleri temizlemek, sistemin kararlılığı için hayati önem taşır.

### Güç Elektroniği: Sistemin Kasları ve Gücü
*   **MOSFET ve IGBT:** Bunlar sistemin dijital anahtarlarıdır. Ancak evdeki ışık anahtarı gibi değil; saniyede 20.000 (20kHz) veya daha fazla kez açılıp kapanırlar. Eğer "Gate" bacağını yeterince hızlı ve güçlü süremezseniz, MOSFET "doğrusal bölgeye" girer, ısınır ve patlar.
*   **H-Köprüsü Sürücüler:** Motoru hem ileri hem geri sürmek için kullanılan devre. Eğer yazılım hatasıyla köprünün iki tarafını (üst ve alt anahtarı) aynı anda açarsanız (Shoot-through), köprüyü milisaniyeler içinde havaya uçurursunuz. Donanımsal "dead-time" eklemenin neden hayat kurtardığını burada öğreniriz.

### Sensörler: Makinenin Duyu Organları
*   Sıcaklık (NTC/PTC), Mesafe (Ultrasonik/Lidar), Konum (Encoder), İvme (IMU).
*   **Saha Arıza Senaryosu:** Encoder kablosunun ekranlaması (shield) topraklanmazsa ne olur? Motorun manyetik alanı kabloya parazit basar, işlemci robotun 1000 tur attığını sanar ama robot yerinden bile oynamamıştır. Sonuç: Robot aniden son hızla duvara çarpar. Bu sorunu yazılımla çözemezsiniz, donanımla çözmelisiniz.

---

> **Ustanın Bilgelik Notu:** "Multimetren senin kılıcın, osiloskobun ise kalkanındır. Yanında bunlar olmadan asla elektronik savaşına (sahaya) çıkma. Ve asla unutma: Bir elektronikçinin en iyi sensörü kendi burnudur; çünkü yanık silikon kokusu asla yalan söylemez ve unutulmaz."
