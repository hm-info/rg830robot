**MÜŞTERİYE ÖNEMLİ NOTLAR:**

1-) Her zaman default kalıplarda aksesuar olacak !!!!!

2-) Hava gittiğinde aksesuarlar aşağıya inebiliyor, tekrar gelince yukarı çıkıypor. Bu esnada iki adet aksesuar çıkıp kalıbı zorlayabilir,
    Hava gittiğinde aşağı inen aksesuarları kontrol etmeliler !!!!!

3-) Acil stoptan sonra sistemi ayaklandırmak için reset ışığı yanana kadar hat panosundaki reset butonuna basacaklar.

4-) Yatar kalkar sehpalar yukarı ya da aşağı hareket ederken acil stopa basılırsa biraz kayma yapsa dahi sonrasında durur.

5-) Acil stoplar hem robot panosunun çıkışlarını keser hem hat panosunun çıkışlarını keser ve iki sistemi de acil stop senaryosuna sokar.
    Gerçekten acil bir durum olmadıkça(Çerçevenin iki sehpa arasında kalması gibi vs.) stop düğmeleri ile sistemler ayrı ayrı durdurulabilir.

6-) Çit içine girildikten sonra sistem resetten düşer. 
    Dışarı çıkıp kapıyı kilitleme komutu ile kapı kilitledikten sonra ilk olarak hat panosundaki reset butonuna ışık yanana kadar basınız.
    
7-) Hat çalışırken robotu durdurmak isterseniz ya da robot çalışırken hattı durdurmak isterseniz: Kendi panosundaki stop butonlarına basınız.

## <span style="color: #000000; font-weight: bold;">1. Makine İlk Açılışta Robot Gripper Kalıp Durumu</span>

- Sistem ilk açıldığında resetleme sonrası gripperda kalıp olup olmadığının teyitini ister.

![RG830](_media/o_GripperFree.png)

*YES:* Elinde olan kalıbı kendi numarasındaki yere bırakarak tekrar home pozisyonuna döner ve iş dosyası ile haberleşmeyi bekler.

*NO:*  Home pozisyonunda iş dosyası ile haberleşmeyi bekler.

**NOT:** İş dosyası manuel olarak eklenirse aşağıdaki üç maddelik anlatım ile yapılacaktır. Otomatik sistem çalışırken kendisi sistemden çekeceğinden bu işlemleri yapmaya gerek kalmayacak.

- İş dosyasının okunabilmesi için exe dosyası açılmalıdır.
- Hazırlanan iş Dosyası Robot File klasörünün içine konulmalıdır.
- Start butonuna basıldığında Robot File klasöründeki iş dosyası okunarak Plc den robota veri aktarımı gerçekleşir bilgi aktarımı tamamlandıktan sonra Robot iş dosyasını çalışmaya başlar.

## <span style="color: #000000; font-weight: bold;">2. Robot Bypass ve Hattın Bağımsız Çalışma Modu</span>

Robotun operasyona dahil edilmeyeceği durumlarda, hattın kesintisiz çalışmaya devam edebilmesi için aşağıdaki yapılandırma uygulanmalıdır:

*Parametre Ayarı:* Robot kontrol ekranı üzerinden "RobotActive" parametresi "0" olarak ayarlanmalıdır. Bu ayar yapıldığında robot operasyonu otomatik olarak Bypass edilir. Robot devre dışı kalarak hattın tek başına çalışmasına olanak tanır.

*İş Akışı (Çerçeve Transferi):* işlenen çerçeveler doğrudan hat üzerinden ilerleyerek robot çıkışında bulunan aktarma sehpasına yönlendirilir.

## <span style="color: #000000; font-weight: bold;">3. Kapıların açılma İzin Prosedürü</span>

 *Kapı Açma İzin Senaryosu:*

 - Kapı siviçleri üzerindeki :

    Beyaz buton: Kapı açma isteği

    Siyah buton: Kapı kilitleme komutu
    
- Hatta bulunan 3 adet yatar kalkar sehpa yukarı ya da aşağı hareket etmediği zaman kapı açma isteği onaylanır.
- Eğer kapı arkasındaki mandala basarsanız mekanik olarak kapı kilidi açılır. Bunu sadece ve sadece çok acil ve hızlı aksiyon alınması    gereken durumlarda kullanınız.
- Kapı açıldıktan sonra tekrar kilitlemek için kapıların ikisini de kapatıp siyah butona basınız.Ardından ekrandan "kapıların kilitli olduğu ve alanda kimsenin olmadığı" sorgusunu onaylayarak sistemleri kaldığı yerden devam ettirebilirsiniz.

Operatör tarafından **"Kapı Açma İzin Butonu"**na basıldığında; robot, mekanik güvenliği ve parça bütünlüğünü korumak adına aktif işlemini tamamladıktan sonra duruşa geçer.

*İşlem Tamamlama Senaryoları:*

Sistem aşağıdaki işlemlerden biri yürüyor ise süreci kesmez, işlemin bitmesini bekler:

- Vidalama: Aktif vidalama işlemi tork değerine ulaşana kadar devam eder.

- Vida Besleme: Vida çekme veya transfer işlemi tamamlanır.

- Delme: Delme ucu iş parçasından güvenli şekilde geri çekilir.

Aktif döngü (cycle) güvenli noktada tamamlandığında, sistem otomatik olarak kapı kilitlerini açar ve operatöre giriş onayı verir.

## <span style="color: #000000; font-weight: bold;">4. Acil Stop-Reset / Stop-Reset senaryoları / Acil Stop-Start / Stop-Start Senaryoları </span>

*4.1 Acil Stop-Reset Senaryosu:*

Acil Stop butonuna basılması durumunda güvenlik protokolü gereği aktif iş çevrimi (cycle) iptal edilir ve sistem güvenli duruş moduna geçer. Bu işlemden sonra sistemi ilk açıldığı haline döndürmek için aşağıdaki adımları takip edebilirsiniz.

*Sistemi Tekrar Aktif Hale Getirme Adımları:*

![RG830](_media/o_AlarmRstButon.png)

- *A:* Operatör panelinden Alarmlar (Reset) temizlenir.
- *Hat tarafı panosundan reset ışığı yanana kadar reset butonuna basınız.*
- *B:* Reset e basılır . Robot Po to Main yapar arkasından **C** soru paneli açılır
- *C:* Gripper üzerinde kalıp var,yok sorgusu yapılır. Daha sonrasında **D** soru paneli açılır
- *D:* Acilden sonra aynı iş dosyası ile mi yoksa farklı bir iş dosyası ile mi çalışacağına dair soru paneli açılır.

  *YES:* Hafızadaki iş dosyası ile devam eder.

  *NO:*  Farklı iş dosyasının yüklenmesini bekler. Belli bir süre iş dosyasını okuyamazsa, dosya okuyamadığına dair hata mesajı verir.

*4.2 Stop-Reset Senaryosu:*

Sistemde *E (Stop Butonu)*'na basıldığında, PLC ve robot koordineli bir "bekleme moduna" geçer. Bu sürecin teknik işleyişi şu şekildedir:

 - *PLC*, stop sinyali alındığında, mevcut çalışma adımını (state) dondurarak sistemi "Stop State" moduna alır.

 - *Robot*, Stop sinyali geldiği anda Robot Vidalama işlemi , Vida besleme işlemi , delme işlemi yapmıyorsa Plc den gelen sinyal ile hızını sıfıra çeker ve hareket edeceği satırda bekler

 - *Sistemi Yeniden Başlatma :* Sistemde bir alarm durumu yoksa yukarıdaki *B* adımından,alarm durumu varsada *Acil Stop - Reset* senaryosundaki adımları uygulayarak devam ettirebilirsiniz. 

 *4.3 Acil Stop - Start Senaryosu*

- Acil stopa basılırsa hem hat panosu hem robot panosu bütün çıkışlarını keser.
- Çit içine girilecekse kapı açma izin butonuna (Beyaz Buton) basılır.
- İçeri girdikten sonra, tekrar dışarı çıkınca kapıyı kapatıp siyah butona basarak kapıyı kilitleme komutu veriniz.
- Acil stopları kaldırıp hat panosundan reset ışığı yanana kadar reset butonuna basınız.

![RG830](_media/o_Confirm.png)

- Ekrandan içeride kimsenin olmadığını onayladıktan sonra sistem kaldığı yerden devam eder.

*4.4 Stop - Start Senaryosu*

- Çit içine girmeden sistemi durdurmak isterseniz stop butonuna basınız ve devam etmek istediğiniz zaman start butonuna basınız.
- Çit içine girilecekse kapı açma izin butonuna (Beyaz Buton) basılır; 
- Çit içine girdikten sonra, tekrar dışarı çıkınca kapıyı kapatıp siyah butona basarak kapıyı kilitleme komutu veriniz.
- Hat panosundan reset ışığı yanana kadar reset butonuna basınız.

![RG830](_media/o_Confirm.png)

- *G:* Ekrandan içeride kimsenin olmadığını onayladıktan sonra sistem kaldığı yerden devam eder.


## <span style="color: #000000; font-weight: bold;">5. Hat ile Çalışacağı Zaman, Hattan Çerçeve Ne Zaman Gelecek, Hattaki Çerçeve ile Gelen Çerçeve Aynı mı?</span>

Hattın senkronize çalışabilmesi için çerçeve transferi ve iş dosyası oluşturma süreci şu kriterlere göre ilerler:

*Çerçeve Geliş Koşulu:* Hat sonundaki çıkış sehpasında (Z) hazır bir çerçeve bulunması durumunda robot plc sinden yeni çerçeve isteğini bekler.

*İş Dosyası Oluşturma:* Robotun işlemine başlayabilmesi için (Z) sehpasındaki çerçevenin iş dosyasının oluşturulmuş ve sisteme tanımlanmış olması gerekir.

*Hattaki çerçeve ile gelen çerçeve Kontrolü:* (Z) sehpasındaki mevcut çerçeve ile plc yazılımından gelen iş dosyasındaki çerçeve ID leri birbiriyle eşleşmelidir. Eşleşme varsa robot işlemi başlatır, Eşleşme yoksa yanlış iş dosyası alarmı verir

## <span style="color: #000000; font-weight: bold;">6. Çerçeve Sıkıştırmada Alarm Durumları</span>

Sistem hazır olduğunda çerçeve çıkış sensörüne geldiğinde çerçeveyi sıkıştırmak için Eksen yaklaştığında yeteri kadar sıkamadığında ölçüm ile ilgili olarak **"Frame Measuring Error, Wrong Frame Sizes !"** hatası verir tekrar sıkması için **(F) Start Buton**'una basıp tekrar sıkıştırma işlemi yapılır.

## <span style="color: #000000; font-weight: bold;">7. Drilling Tool Not Ok Alarm Durumu</span>

*Sistem, operasyon güvenliğini sağlamak adına her iş başlangıcında bir kez olmak üzere otomatik takım kontrolü gerçekleştirir. Sürecin işleyişi ve hata durumunda yapılması gerekenler aşağıda belirtilmiştir:*

- Robot, delme takımının (tool) fiziksel bütünlüğünü doğrulamak amacıyla takım ucunu önceden tanımlanmış bir kontrol siviçine (switch) temas ettirir.

- Tool ucu sensöre temas edip sinyal aldıktan sonra işlem akışı devam eder.

- Takım kontrol noktasına ulaştığı halde siviçten doğrulama sinyali alınamazsa, robot otomatik olarak hareketi durdurur. Güvenli bir bekleme pozisyonuna (kontrol noktasının üst kısmı) geçerek operatör panelinde durum alarmını aktif hale getirir.

*Müdahale ve Arıza Giderme:*

- *Takım Hasarı:* Eğer delme ucu fiziksel olarak zarar görmüş veya kırılmışsa, yeni bir takım ucu ile değiştirilmelidir.

- *Sensör Kontrolü:* Takım ucunda bir sorun gözlemlenmiyorsa, ilgili kontrol sensörünün (switch) işlevselliği ve kablo bağlantıları kontrol edilmelidir.

- *Sistemi Tekrar Devreye Alma:* Gerekli fiziksel düzeltmeler yapıldıktan ve arıza kaynağı giderildikten sonra, operatör paneli üzerinden **Start Butonuna (F)** basılarak işlem döngüsü kaldığı yerden devam ettirilir.

## <span style="color: #000000; font-weight: bold;">8. Accessory Not Ok Alarm Durumu</span>

Aksesuar montaj sürecinin sağlıklı ilerleyebilmesi için parçanın magazinden başarıyla alınması ve kalıp içerisinde hassas şekilde konumlanması kritik önem taşımaktadır. Bu doğrultuda, montaj aşamasına geçilmeden önce parçanın varlığı ve konumu sensörler aracılığıyla denetlenir.

Robot tarafından kontrol noktasına getirilen aksesuarın sensör tarafından algılanmaması durumunda sistem "AccessoryNotOk" alarmı üretir; robot, operatör müdahalesine imkan tanımak için kontrol noktasından bir miktar yükselerek bekleme moduna geçer. Bu durumda izlenmesi gereken çözüm yolları aşağıda belirtilmiştir:

*Manuel Müdahale ile Devam Etme*

- Eğer aksesuar magazinden çıkmış fakat kalıp tarafından tam alınamadığı için magazin üzerinde kalmışsa:

Operatör, emniyet kapısını açarak (sistem Acil Stop moduna geçecektir) hattın içerisine girer. Magazindeki aksesuarı alarak, geliş yönüne dikkat ederek el ile manuel olarak kalıba yerleştirir.Hattan çıkıp emniyet kapısını kapattıktan sonra sistemi resetleyip panel üzerinden **F (Start Buton)**'una basarak süreci kaldığı yerden devam ettirir.

*Alma İşleminin Tekrarlanması (Aksesuar Magazindeyse)*

- Eğer aksesuar magazinde kalmışsa ve operatör bu parçanın robot tarafından tekrar alınmasını istiyorsa:

Hattan çıktıktan ve emniyet kilidini devreye aldıktan sonra panel üzerindeki **B (Reset Butonu)**'na basılır. Bu işlemle birlikte robot, aynı aksesuarı alma döngüsünü en baştan tekrarlayacaktır.

*Magazinden Aksesuar Çıkmaması Durumu*

- Eğer magazinden hiç aksesuar çıkmadığı için robot boş dönmüş ve bekleme noktasına gelmişse:

Hata giderildikten sonra panel üzerinden **B (Reset Butonu)***'na basılarak aksesuar alma işlemi yeniden başlatılır.

## <span style="color: #000000; font-weight: bold;">9. Çeneye Vida Çekilememe Durumu</span>

Robot, vidalama işlemi öncesinde sistemden vida besleme talebinde bulunur. Vida beslemesinin başarısız olması durumunda operatör aşağıdaki adımları izlemelidir:

*Ön Kontrol:*

- Operatör, öncelikle vidalama ucunu gözle kontrol ederek vidanın gönderilip gönderilmediğini teyit etmelidir.

*Vida Gönderimi Başarılı İse (Görsel Onay):*

- Eğer vida uca ulaşmışsa ve herhangi bir sorun gözlemlenmiyorsa:

Hattın içerisine girildiği için öncelikle sistem emniyet devreleri resetlenmelidir.Ardından panel üzerindeki **F (Start Butonu)**'na basılarak işlem kaldığı yerden devam ettirilmelidir.

*Vida Beslenemedi İse (Hata Onayı):*

- Eğer görsel kontrolde vidanın uca ulaşmadığı teyit edilirse:

Hattın içerisine girildiği için öncelikle sistem emniyet devreleri resetlenmelidir. Ardından panel üzerindeki **B (Reset Butonu)**'na basılarak vida çekme işlemi yeniden tetiklenmelidir.

## <span style="color: #000000; font-weight: bold;">10. Aktüel Aksesuar Montajını Geçmek için PassNextAccessory</span>

![RG830](_media/o_PassNextAccessory.png)

Robotun delme, vidalama veya diğer operasyonları sırasında herhangi bir sorunla karşılaşılması durumunda, mevcut iş akışını bozmadan sürece müdahale etmek için aşağıdaki adımlar izlenmelidir:

*İşlemin Durdurulması:*
- Panel üzerinden E (Stop Butonu)'na basılmalıdır. Bu işlem robotu bekleme moduna alır.

*Dikkat:* Bu aşamada B (Reset Butonu)'na basılırsa, tüm işlem durumu (state) sıfırlanır ve süreç en başa döner.

## <span style="color: #000000; font-weight: bold;">11. İşlemin Yeniden Başlatılması ve Seçenekler</span>

- Durdurma işleminden sonra F (Start Butonu)'na basıldığında, ekranda bir karar sayfası açılır. Operatör bu aşamada şu iki seçenekten birini tercih etmelidir:

*G:* Robotun, kaldığı yerden işlemlerine devam etmesini sağlar.

*H:* Robotun, mevcut işlemini iptal ederek bir sonraki aksesuar döngüsüne geçmesini sağlar.

*Kritik Uyarı:* **H** seçeneği tercih edildiğinde robot kendisini güvenli bir şekilde kurtardıktan sonra Gripper da kalıp varsa bırakma noktasına gidecektir. Bırakma işlemi sırasında kalıpta aksesuar bulunmadığından emin olunmalıdır.

## <span style="color: #000000; font-weight: bold;">12. Aksesuar Montaj Alarm Tanımları ve Çözüm Adımları</span>

Aşağıda belirtilen alarmlar montaj esnasında meydana gelebilecek alarm mesajlarıdır.

**Screw Drop failed !** 9.madde bu alarm durumunu özetler.
**Screw did not move to jaw or Screw detector broken !** "Vida Besleme Bekleme Zaman Aşımı" hatasıdır. Sistem vida besleme modundayken belirli bir süre geçmesine rağmen vidanın hedefe ulaştığına dair sinyal Vida kontrol sensöründen alınamadığında tetiklenir. Bu hataya sebep olabilecek hatalar aşağıdaki gibi olabilir: 

- **Besleme Haznesi Boş:** Vida dizici vibratörde veya besleme ünitesinde vida kalmamış olabilir.

- **Mekanik Sıkışma:** Vida, besleme hortumu içinde veya ağız kısmında sıkışmış, sensöre ulaşamamış olabilir.

- **Hava Basıncı Sorunu:** Vidayı itmek için kullanılan hava basıncı yetersizdir.

- **Sensör Arızası:** ScrewCame sensörü vidayı görmüyor veya fiziksel olarak yerinden oynamış olabilir.


## <span style="color: #000000; font-weight: bold;">13. Eksen Hareket halindeyken Sıkışması Durumu</span>

Robot bazen fiziksel bir engele çarpmadığı halde, gitmek istediği noktaya matematiksel olarak ulaşamaz veya eklem limitlerine takılır. Bu durumlarda operatörün kurtarması için izleyeceği adımlar şunlardır:

## <span style="color: #000000; font-weight: bold;">13.1. Sorunu Teşhis Etme (Hata Mesajı Okuma)</span>

- Ekranda aşağıdaki mesajlardan birini görüyorsanız robot "geometrik" bir çıkmaza girmiştir:

*"Axis Limit":* *Robot bir ekleminin dönebileceği son noktaya gelmiştir.

*"Singularity"* (Tekillik): Robotun bilek eksenleri (4 ve 6) aynı hizaya gelmiş, robot yönünü şaşırmıştır.

*"Out of Reach":* Robotun kolu o noktaya yetişemiyor veya o rotayı takip edemiyordur.

## <span style="color: #000000; font-weight: bold;">13.2. Robotu Manuel Modda Kurtarma (Jogging)</span>

![RG830](_media/ModSecim.png)

Kontrol ünitesinden anahtarı saga çevirerek **B (Manuel Mod)**'a alın

![RG830](_media/1_6EksenSecim.png)

- Robot bu hataları verdiğinde genellikle "Linear" (Doğrusal) modda hareket etmeyi reddeder. Robotu rahatlatmak için:

*Hareket Modunu Değiştirin:* FlexPendant üzerinden hareket modunu "Axis" (Eksen) moduna getirin. **A** tuşuna basıldığında **B** kısmının 1-3 ve 4-6 arasında eksen olarak değiştiğini göreceksiniz. 

*Eksenleri Manuel Döndürün:* Limit hatası varsa: Sınıra dayanan ekseni ters yöne doğru joystick ile çevirin.Hangi eksen arasında çalışılacaksa o alanda **B** kalınmalı ve Jogging sayfasındaki joystick yönlerinin nasıl çalıştığını gösteren görsele bakarak hareket ettirilmelidir.

*Tekillik (Singularity) varsa:* 5. ekseni (bilek bükme) hafifçe yukarı veya aşağı hareket ettirerek eksenlerin aynı hizadan çıkmasını sağlayın.

*Güvenli Bir Noktaya Çekin:* Robotu, sorun yaşadığı noktadan yaklaşık 5-10 cm uzaklaştırıp boşluğa (güvenli alana) alın.

## <span style="color: #000000; font-weight: bold;">13.3. İşlemi "Atlatma" ve Devam Ettirme (Program Pointer Taşıma)</span>

![RG830](_media/o_PointerTaşıma.png)

- Operatörün asıl yapması gereken, robotu o "hatalı noktadan" kurtarıp bir sonraki güvenli işlem adımına manuel olarak yönlendirmektir.şu adımları izleyin:

*Program Editor Sayfasını Açın:* FlexPendant'ta  kısmına girin **A**'dan menü çubuğuna ve **B**'ye basarak Program Editör sayfasını açın.

*Bir Sonraki Adımı Seçin:* Kod içerisinde robotun takıldığı satırın bir altındaki veya bir sonraki işlem başlangıcı olan (Örn: MoveL veya MoveJ) satıra dokunarak seçili hale getirin. Görsel **C**. Arada komut satırları varsa komut satırlarını atlamayın. Plc tarafında state lerde takılma yaşamamak için. 

*İmleci Taşıyın (PP to Cursor):* **D** "Debug" menüsünden **E** "PP to Cursor" (Program İmlecini Seçili Satıra Taşı) seçeneğine basın.

Bu işlemlerden sonra önce manuel olarak çalıiştırılarak işlemin devam edilebilir olduğu izlemek sağlıklı olacaktır. Manuel olarak adım adım ilerlemek için Flexpendant üzerinden görseldeki **F** Motor On butonunu **basılı tutun** Görsel **H** da olduğu gibi siz basılı tutarken Motor On yazısının olduğunu görün manuel de işlemleri bu şekilde ilerletebilirsiniz. Sonrasında Görsel **G** adım adım her satırı işletmek için kullanılır her basışta kendi içinde bir satır okuyarak ilerler. Görsel **G** de adım adım gitmek istemiyorsanız Görsel **I** ya bastığınız da tüm satırları adım adım taramaya başlar. Robot çalışırken durdurmak istediğiniz zaman Görsel **J** Stop butonu na basabilir yada Görsel **F** Motor On butonundan elinizi çekebilirsiniz. Robotu çalıştırdıktan sonra robot sonraki adıma kendisi gidebildiyse bu aşamadan sonra Robotu Otomatik Moda alarak tekrar çalıştırabilirsiniz.

*Otomatik Mod ve Start:* Görseldeki **K** yönüne anahtarı çevirin Flexpendant ekranına gelen soruları onaylayın ve Sistemi "Auto" moduna alın, görseldeki **L** kısmına basarak motorları aktif hale getirin ve sistemdeki alarmları kaldırdıktan sonra Start vererek işlemlerinize devam edin

*Hız Kontrolü:* Robot ilk hareketini yaparken hızı %10-%25 seviyesinde tutarak yörüngesini izleyin. bir sorun gözlemlenmez ise hızı tekrar %100 e alabilirsiniz. Hız ayar sayfası için sırasıyla görseldeki **M-N** kısımlarına tıklayarak **O** hız sayfasını açabilirsiniz.

## <span style="color: #000000; font-weight: bold;">14. Ekrandaki Parametreler hakkında , vidalama eksen hızları hakkında detaylı bilgi</span>

![RG830](_media/o_ParameterScrew.png) 

![RG830](_media/o_ParameterScrew2.png) 

![RG830](_media/o_ParameterScrew3.png)

**A:** Vidalama eksen grubunun Home pozisyonunu **(Parametre Değer:53)** belirler.

Sistem aşağıdaki durumlarda otomatik olarak ekseni bu pozisyona getirir:

Çevrim Sonu: Bir vida çakma işlemi başarıyla tamamlandığında, yeni bir vida almak veya parçanın geçişine izin vermek için.

Reset İşlemi: Makine sıfırlandığında (Reset) veya başlangıç konumuna döndüğünde.

Vida Boşaltma (Unload): Sistemdeki mevcut vidanın tahliyesi sonrası güvenli bekleme noktasına geçişte.

**B:** Vidalama eksen grubunun işlem bittikten sonra veya Reset durumunda Home a geri dönerken kullandığı hızdır. **(Parametre Değer:50)**

**C:** Bu parametre, vidalama ucunun referans alınan fiziksel sıfır noktasını belirler. Tüm çalışma mesafeleri, dalma derinlikleri ve yaklaşma pozisyonları bu "0" noktası referans alınarak hesaplanır. **(Parametre Değer:82)**

**D:** Bu parametre, vidalama grubunun çalışma (Set) pozisyonuna giderken kullandığı hızdır. **(Parametre Değer:42)**

**E:** Bu parametre, vidalama grubunun geri dönüş (Reset) pozisyonuna giderken kullandığı hızdır. **(Parametre Değer:42)**

**F:** Aksesuar kalinligi , vida kafasi kaç mm disarida kalacak yani Vidabaşı ve çerçeve arasındaki mesafenin offseti ne kadar olacağı bilgisidir. **(Parametre Değer:1)**

**G:** Vidanın besleme hortumundan gelip çeneler tarafından tutulduğu pozisyondur. Sistem, vida besleme işlemi sırasında ekseni bu noktaya getirir. Vidanın besleme ünitesinden gelip çeneye girdiği, ancak henüz parçaya vidalanmadığı ara durak noktasıdır. **(Parametre Değer:55)**

**H:** Robotun Aktif çalışır durumda ise **(Parametre Değer:1)** olmalı Robotta bir sorun var veya byPass (Madde 2 deki durum) etmek istiyorsam **(Parametre Değer:0)** olmalıdır.

**I:** Sağ magazinde kaç aksesuar bulunduğu ile ilgili parametre **(Parametre Değer:29)**

**J:** Sol magazinde kaç aksesuar bulunduğu ile ilgili parametre **(Parametre Değer:19)**

**K:** Vidalama Tool unun '0' noktasi ile Gripperin '0' noktasi arasindaki yükseklik farki **(Parametre Değer:1.5)**

**L:** Robot hattan ayrı olarak denemeler yapılacağı zaman **(Parametre Değer:1)**, hat ile senkron çalışacağı zaman **(Parametre Değer:0)** olmalıdır.

**M:** Robotun X düzlemindeki erişim mesafesine göre robotun aksesuarları sağa yada sola yönelimli olarak işleyebilmesi adına girilen limit değer. **(Parametre Değer:1500)**

**N:** Robotun Y düzlemindeki erişim mesafesine göre robotun delme işlemini yönelimli olarak yapabilmesi adına girilen limit değer. **(Parametre Değer:1950)**


**Ö:** Bu parametre, çerçeve taşıma ekseninin (AxisFrm) bir çerçeveyi yakalarken veya bir engelle karşılaştığında durmasını sağlayan tork (güç) limitini belirler. Sistem, eksen hareket halindeyken bu limit değerine ulaşıp ulaşmadığını sürekli izler. **(Parametre Değer:....)**

**R:** Bu değer daha çok hassas ölçüm (metroloji) aşamasında devreye girer. Çerçeveye çok sert basıp profilin esnemesini veya ezilmesini engellemek için torku düşük bir seviyede tutar. **(Parametre Değer:0.5)**


**T:** Parçayı yakalamak veya ölçmek için hareket ederken bu koordinatı ana hedef noktası olarak kullanır. Yazılım, her yeni iş emrinde bu değeri otomatik olarak güncelleyerek eksenin "parçayı nerede bulması gerektiğini" belirler.

**U:** Ölçüm işlemi sırasında temel yakalama pozisyonuna (CatchPos) eklenen düzeltme değeridir. **(Parametre Değer:20)**


## <span style="color: #000000; font-weight: bold;">15. Alarmlar</span>

[ALM:....] : Bütün ileri gidemedi ya da geri gidemedi alarmları aslında pistonun sıkışmış olması anlamına gelmektedir.
             Manuel sayfadan ters yönde hareket ettirerek sıkışmayı giderdikten sonra Reset Alarms butonuna basınız.

[ALM:5010] : Vida düşürme hatası. Hava hortumunu kontrol edin.
	     Eğer vida hortum içinde ise Start butonuna basarak kaldığı yerden devam edin. Aksi takdirde Reset butonuna basarak tekrar vida çekmeyi deneyin.

[ALM:3022] : Aksesuar alma başarısız oldu. Kalıbı kontrol edin, gerçekten alamadıysa;
             Tekrar denemek isterseniz kalıbı ve aksesuar çıkış noktasını boşaltıp Reset butonuna basınız,
             Ya da aksesuarı manuel olarak kalıba yerleştirip Start butonuna basarak, prosesi hızlandırabilirsiniz.

[ALM:3029] : Delme tool algılanamadı. Eğer kırıldı ise değiştirin,
             Eğer bir sorun yoksa Start butonuna basarak devam edebilirsiniz.

[ALM:3120] : Vidalama grup eksen hatası, Reset alarms butonuna basarak alarmı resetlemeyi deneyin, aksi takdirde sistemi kontrol edin

[ALM:3100] : Vidalama eksen hatası, Reset alarms butonuna basarak alarmı resetlemeyi deneyin, aksi takdirde sistemi kontrol edin

[ALM:3794] : Sağ magazin 3.kat 1.aksesuar(20) algılanmadı. Ya alma noktasına aksesuar yerleştirin ve Reset Alarms butonuna basınız. Ya da Reset Alarms butonuna basarak tekrar aksesuar hazırlamayı dene.

[ALM:3795] : Sağ magazin 3.kat 2.aksesuar(21) algılanmadı. Ya alma noktasına aksesuar yerleştirin ve Reset Alarms butonuna basınız. Ya da Reset Alarms butonuna basarak tekrar aksesuar hazırlamayı dene.

[ALM:3796] : Sağ magazin 3.kat 3.aksesuar(22) algılanmadı. Ya alma noktasına aksesuar yerleştirin ve Reset Alarms butonuna basınız. Ya da Reset Alarms butonuna basarak tekrar aksesuar hazırlamayı dene.

[ALM:3797] : Sağ magazin 3.kat 4.aksesuar(23) algılanmadı. Ya alma noktasına aksesuar yerleştirin ve Reset Alarms butonuna basınız. Ya da Reset Alarms butonuna basarak tekrar aksesuar hazırlamayı dene.

[ALM:3798] : Sağ magazin 3.kat 5.aksesuar(24) algılanmadı. Ya alma noktasına aksesuar yerleştirin ve Reset Alarms butonuna basınız. Ya da Reset Alarms butonuna basarak tekrar aksesuar hazırlamayı dene.

[ALM:3799] : Sağ magazin 3.kat 6.aksesuar(25) algılanmadı. Ya alma noktasına aksesuar yerleştirin ve Reset Alarms butonuna basınız. Ya da Reset Alarms butonuna basarak tekrar aksesuar hazırlamayı dene.

[ALM:3800] : Sağ magazin 3.kat 7.aksesuar(26) algılanmadı. Ya alma noktasına aksesuar yerleştirin ve Reset Alarms butonuna basınız. Ya da Reset Alarms butonuna basarak tekrar aksesuar hazırlamayı dene.

[ALM:3801] : Sağ magazin 3.kat 8.aksesuar(27) algılanmadı. Ya alma noktasına aksesuar yerleştirin ve Reset Alarms butonuna basınız. Ya da Reset Alarms butonuna basarak tekrar aksesuar hazırlamayı dene.

[ALM:3802] : Sağ magazin 3.kat 9.aksesuar(28) algılanmadı. Ya alma noktasına aksesuar yerleştirin ve Reset Alarms butonuna basınız. Ya da Reset Alarms butonuna basarak tekrar aksesuar hazırlamayı dene.

[ALM:3803] : Sağ magazin 3.kat 10.aksesuar(29) algılanmadı. Ya alma noktasına aksesuar yerleştirin ve Reset Alarms butonuna basınız. Ya da Reset Alarms butonuna basarak tekrar aksesuar hazırlamayı dene.

[ALM:5235] : Çerçeve sabitleme işlemi başarısız oldu. Çerçeve ölçülerini kontrol ediniz eğer doğru ise Reset alarms butonuna basarak tekrar deneyin