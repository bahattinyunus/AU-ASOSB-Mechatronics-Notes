# Programlama & Gömülü Sistemler: Silikon Vadisi Değil, Silikon Beyin Cerrahlığı

> *"Kod, silikonun ruhudur. Ancak kötü yazılmış bir kod, silikonu ısıtır, yorar, kafasını karıştırır ve sonunda sistemi öldürür."*

Yapay Zeka (AI) çağında, "Sıfırdan Sürücü (Driver) Yazmak" artık insan için bir meziyet değildir; bunu bir AI modeli saniyeler içinde hatasız yapabilir. Yeni çağın meziyeti, o kodu alıp STM32'nin 128KB'lık kısıtlı hafızasına sığdırmak (Optimization), sonsuz döngüye girip sistemi kilitlemesini engellemek (Watchdog Implementation) ve milisaniyelik gecikmelere bile tahammülü olmayan donanımla "kekelemeden" konuşturmaktır.

Biz artık "kod yazıcı" (Coder) değiliz; biz **"Gömülü Sistem Entegratörü"** ve **"Donanım Fısıldayıcısı"**yız.

## 🛠️ Metal Yaka Perspektifi: Kod Enjeksiyonu ve Optimizasyon

### 1. İstemi Mühendisliği (Prompt Engineering)
C++ sözdizimini (syntax), noktalı virgülleri veya pointer aritmetiğini ezberlemek hamallıktır. Önemli olan "ne istediğini" çok net bir teknik dille ifade edebilmektir.
*   **Yanlış İstemi:** "Bana I2C kodu yaz." -> AI size çalışan ama güvensiz, bloke edici (blocking) bir kod verir.
*   **Doğru İstemi/Mühendislik:** "STM32F407 işlemci için, HAL kütüphanesini kullanarak, DMA (Doğrudan Bellek Erişimi) modunda çalışan, hataya dayanıklı (fault-tolerant), timeout mekanizması olan ve kesme (interrupt) tabanlı bir I2C sensör okuma sürücüsü oluştur." -> İşte bu, bir Metal Yaka mühendisinin işidir.

### 2. Gerçek Zamanlı (Real-Time) Kısıtlar ve Disiplin
Bir web sitesi açılırken 1 saniye gecikirse, kullanıcı sayfayı yeniler ve söylenir. Ancak 100km/s hızla giden bir robotun fren sistemi 10 milisaniye geç tetiklenirse, birisi ölebilir veya fabrika durabilir.
*   **RTOS (Gerçek Zamanlı İşletim Sistemi):** Windows veya Android gibi değildir. Mavi ekran verme lüksü yoktur. RTOS, işlemcinin zamanını mikrosaniyeler mertebesinde dilimleyen, görevleri (tasks) aciliyet sırasına göre dizen ve asla gecikmeye izin vermeyen mutlak bir trafik polisidir.

## 📚 Konu Başlıkları ve Derinlemesine Saha Uygulamaları

### C/C++: Donanımın Ana Dili ve Tehlikeleri
*   **Pointer'lar ve Bellek Yönetimi:** Bellek adreslerine doğrudan erişim (0x20000000). Eğer dikkatsizce yanlış bir adrese veri yazarsanız (Buffer Overflow), sistemi anında çökertirsiniz. Bu, elektronikteki "kısa devre"nin yazılım dünyasındaki karşılığıdır: **Segmentation Fault**. Bir Metal Yaka, pointer'ları bir cerrahın bistürisi gibi dikkatli kullanır.
*   **Bit Manipülasyonu:** 32-bitlik bir kontrol register'ının tamamını değiştirmek yerine, sadece 3. bitini '1' yapmak (Bitwise Operations: `CreateMask |= (1 << 3)`). Çünkü o 3. bit, motoru açan anahtardır veya lazeri ateşleyen tetiktir. Diğer bitlere dokunursanız sistemi bozarsınız.

### Mikrodenetleyiciler: Makinenin Beynini Yönetmek
*   **Kesmeler (Interrupts):** İşlemcinin kapı zilidir. İşlemci o anda dünyanın en önemli matematik işlemini yapıyor olsa bile, "Acil Stop" butonuna basıldığında (External Interrupt) veya sensörden veri geldiğinde her şeyi bırakıp o sinyale bakmak zorundadır. Doğru kurgulanmazsa, işlemci sürekli zillere bakmaktan asıl işini yapamaz hale gelir (Interrupt Storm).
*   **DMA (Direct Memory Access):** İşlemciyi yormadan veriyi bir yerden bir yere taşıyan "dijital hamal". Sensörden hafızaya terabaytlarca veri akarken CPU'nun (Merkezi İşlem Birimi) yükü %0 olur. Çünkü o sırada CPU, robotun bir sonraki hamlesini hesaplamakla meşguldür.

### Haberleşme Protokolleri: Makine Dili Konuşmak
*   **I2C ve SPI:** Kart üzerindeki çiplerin kendi aralarındaki fısıldaşmaları. Biri yavaş ama kalabalık (I2C), diğeri hızlı ama kablolu (SPI). Hangisini ne zaman kullanacağınızı bilmek sistem mimarisidir.
*   **UART/USART:** Bilgisayarla veya GPS modülüyle konuşmak. Asenkron olduğu için zamanlama (Baud Rate) tutmazsa, ekranda anlamsız karakterler (Hieroglyphs) görürsünüz.
*   **CAN-Bus (Controller Area Network):** Otomobilin ve modern fabrikanın sinir ağı. Elektriksel gürültüye karşı inanılmaz dirençlidir. Kabloyu kesseniz bile kalan hattan veri göndermeye çalışır. Bir Tesla'nın otonom sürüşü de, bir tankın taret kontrolü de bu protokole emanettir.

---

> **Ustanın Bilgelik Notu:** "`delay(1000)` komutunu kodunda kullanmak, bir gömülü sistem mühendisi için suçtur. İşlemciyi 1 tam saniye boyunca (ki bu işlemci için 1 asır gibidir) uyutamazsınız; o sırada dünya dönmeye devam ediyor, sensörler veri gönderiyor, motor dönüyor. `millis()` kullanın, Timer kullanın, RTOS kullanın ama işlemciyi asla boşa bekletmeyin (Non-blocking code)."
