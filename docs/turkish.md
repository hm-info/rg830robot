# RG830 Robot Manual
## Acil Durdurma
Robot enerjilendiği zaman robot üzerindeki acil butonlar ve harici diğer etkileyen acil durumları kaldırılmalı daha sonrasında Motor On butonuna basılmalıdır.

![KT803](_media/AcilDurdurma.png)

## Çalışma Modları
- **Otomatik Mod :** Üretim Modu
- **Manuel Mod :** Jog modda hareket ve kontroller yapılabilir.

![RG830](_media/ModSecim.png)

## Jog Hareket ile Robot Eksen Kontrol 
- Robot manuel moddayken, hareket birimlerini devreye almak için FlexPendant'ın sağ tarafında bulunan 'Motor On' (Motorları Aktif Etme) butonuna basılmalıdır.

![RG830](_media/MotorOnButon.png)

- Sol Üst menü çubuğundan Joging sayfasına girip eksenler ile ilgili durumları görebilirsiniz.
- Robotta 1-6 arası eksenleri tek tek hareket ettirebiliriz. İlk basımda 1-3 arası ikinci basışta 4-6 arası eksen kontrollerinin yönlerini ilgili eksen numarasının altında görebilirsiniz.

![RG830](_media/1_6EksenSecim.png)

- Robot, lineer olarak X, Y ve Z eksenlerinde hareket ettirilebilir. Bu hareketler, arayüzde seçilen İş Nesnesi (Wobj) referans alınarak gerçekleştirilir ve hareket yönü, ilgili Wobj'nin yönelimine göre tayin edilir.

![RG830](_media/LineerHareketSecim.png)

- Tool seçimine göre orientation hareket. 

![RG830](_media/OrientationHareketSecim.png)

## Robot Eksen Kalibrasyonu
- Robotun ilk kurulumu esnasında, her eksen için ayrı ayrı kalibrasyon işlemi gerçekleştirilmelidir. Kalibrasyon sırasında, her eksene ait sıfır noktası işaretleri (çentikler) birbirini tam karşılayacak şekilde, yüksek hassasiyetle hizalanmalıdır.


![RG830](_media/EksenCentikleri.png)

- Robot üzerindeki tüm eksenler fiziksel olarak kalibrasyon çentikleriyle hizalandıktan sonra, ilgili değerleri FlexPendant üzerinden kaydetmek için aşağıdaki görsel adımları takip edebilirsiniz. Bu işlem, robotun ilk kurulumunda veya sistemden 'Robot kalibrasyonu kayboldu' uyarısı alındığında uygulanmalıdır.

![RG830](_media/RobotEksenKalibrasyonu.png)

## TCP (Tool Center Point) Tanıtımı

TCP, robotun uç işlevcisinin (tutucu, vidalama, delme vb.) iş yapacağı tam merkez noktasıdır. Robot kontrol ünitesi varsayılan olarak sadece robotun bilek merkezini (6. eksen flanş merkezi) bilir. Ancak gerçek operasyonlarda işi yapan robotun bileği değil, ona takılan "Tool" (Takım) olduğu için, bu takımın uç noktasının robota matematiksel olarak tanıtılması gerekir.

TCP Tanıtmanın Amacı Nedir?
Hassas Hareket: TCP doğru tanımlandığında, robot tüm yönelim (oryantasyon) hareketlerini bu nokta etrafında yapar. Yani robotun bileği hareket etse bile, takımın ucu (TCP)  sabit kalır.

Lineer Doğruluk: Robotun X, Y veya Z eksenlerinde doğrusal hareket etmesi istendiğinde, bu hareket bilek merkezine göre değil, tanımlanan TCP noktasına göre hesaplanır.

Yörünge Takibi: Delme, Vidalama, Tutma robotun iş parçası üzerindeki yolu kusursuz takip edebilmesi için TCP'nin milimetrik hassasiyette olması şarttır.

- TCP tanıtımı yaparken sabit  mümkünse sivri bir cisme farklı açılardan yaklaşım yaparak tanıtma işlemi gerçekleştirilir.

## Wobj (Work Object) Tanıtma

**Wobj (Work Object) :** robotun çalışma alanındaki parçaları veya düzenekleri tanımlamak için kullanılan, kullanıcı tarafından belirlenmiş bir koordinat sistemidir. ABB robot sistemlerinde Wobj tanımlama işlemi, ilgili yüzey üzerinde 3-Nokta Metodu kullanılarak gerçekleştirilir.

- 3-Nokta Metodu ile Tanımlama
Koordinat sistemini oluşturmak için operatör tarafından sırasıyla şu üç referans noktası öğretilir:

X1 (Orijin Noktası): Tanımlanacak olan yüzeyin başlangıç (sıfır) noktasıdır. Koordinat sisteminin merkezi bu nokta olarak kabul edilir.

X2 (X Ekseni Yönü): X ekseninin doğrultusunu belirleyen ikinci noktadır. X1 ile X2 arasındaki hat, sistemin pozitif X yönünü oluşturur.

Y1 (Y Ekseni Yönü): Y ekseninin doğrultusunu belirleyen üçüncü noktadır. Bu nokta, X eksenine dik olan pozitif Y yönünü tarif eder.

Robotu herbir tanıtma noktasına  (X1,X2,Y1) ayrı ayrı götürerek üzerine 4 numaralı görselde ki şekilde Modify Position diyerek o noktanın koordinatlarını öğretebilirsiniz. Tüm öğretmeler tamamlandıktan sonra 5 numaralı görseldeki gibi Ok diyerek işlemi tamamlayabiliriz.

Otomatik Z Ekseni ve Düzlemsellik

Öğretilen bu üç noktanın oluşturduğu düzlem, sistem tarafından matematiksel olarak hesaplanarak Z eksenini otomatik olarak tayin eder.

Eğimli Yüzeylerde Hareket: Tanımlanan yüzey eğimli olsa dahi, robot bu yüzeye ait Wobj referansıyla hareket ettiğinde, yüzeyin eğimini baz alarak kusursuz bir lineer (doğrusal) hareket sergiler.

Hassasiyet: X ve Y noktaları arasındaki mesafe ne kadar uzak ve noktalar ne kadar hassas seçilirse, oluşturulan Wobj'nin doğruluğu o derece yüksek olur.

**NOT :** Wobj tanımlama işlemi sırasında kullanılan Tool'un (Takım) TCP değerlerinin doğruluğu, oluşturulan iş nesnesinin hassasiyetini doğrudan etkilemektedir.

- Wobj tanıtım işleminin nasıl yapılacağını aşağıdaki görsellerden takip edebilirsiniz.

![RG830](_media/WobjTanıtım.png)


