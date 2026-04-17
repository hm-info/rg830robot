## <span style="color: #000000; font-weight: bold;">1. RG830 Robot Yazılım Manuel </span>

RG830 da proje alt yapısı macro mantığına göre yazıldı.Her aksesuar ın kendine ait macrosu bulunmakta.Aksesuarların yüzeye veya kanala atacağı duruma göre makrolar şekillenmektedir.Çerçeveyi karşımıza aldığımızda Üst ön  yüzeyden başlayarak saat yönünde

1 (Top Fron)- 2 (Right Front)- 3 (BottomFront)- 4 (Left Front) 

5 (Top Channel)- 6 (Right Channel)- 7 (Bottom Channel)- 8 (Left Channel) 

şeklinde isimlendirilmektedir. Montaj yapılacak yüzeyin macrosu yukarıda verdiğim yüzey numarasına göre yapılmaktadır.

**Örnek:**  
- 102 Makrosu ---> 1 numaralı aksesuar 2. yüzeye
- 204 Makrosu ---> 2 numaralı aksesuar 4. yüzeye
- 2805 Makrosu ---> 28 numaralı aksesuar 5. yüzeye 

Macrolar Robot tarafında HOME klasöründe profilin derinlik ölçüsüne göre ayrılarak yazılmıştır.

![RG830](_media/Macro.png)

**A:** 1 numara 70mm lik profil, 2 numara 76mm lik profil, 3 numara 88mm lik profil

**B:** Profil isminin altına sıralanan her aksesuarın kendine ait makrolarını göstermektedir.

## <span style="color: #000000; font-weight: bold;">2. Yeni Nokta Tanıtma ve İsim  </span>

- 1.YÖNTEM

![RG830](_media/D_NoktaTanıtma.png)

**1:** Tanıtım yapmak istediğimiz satıra pendant üzerinde dokunarak o satırın işaretlenmesini sağla.

**2:** Komut isimlerini açar.

**3:** Eklemek istediğimiz komutlar burada listelenir. Hareket komutlarından MoveL ye basarak ekleme yaptığımızda işaretli noktanın altına yada üstüne soru sorarak ekleme yaptırır.

FlexPendant üzerinden MoveL komutu eklendiğinde, ilgili satırda koordinatların '*' (yıldız) simgesi belirecektir. Bu aşamada konum kaydı yapılırken, robot o an seçili olan Tool (Takım) ve Wobj (İş Parçası) verilerini referans alarak koordinatları atar. Hatalı tanımlamaları önlemek adına; komut ekleme işleminden önce, kullanılacak olan Tool ve Wobj seçimlerinin doğru yapıldığından emin olunmalıdır.

![RG830](_media/D_HareketKomutu.png)

**1:** Listeyi açar

**2:**  Robot ile ilgili hareket,tool,wobj seçeneklerini açar

**3:** Tool ve Wobj seçimi ni yaptığımız kısım

Bu işlemlerden sonra bu komutu başka yerlerde kullanabilmek için '*' olan kısma isim vermemiz gerekmektedir bu sebeplede "robtarget" olarak bir değişken tanımlamamız gerekmekte bu değişkene de isim vererek yıldızlı alanda ki koordinat bilgilerini atamamız gerekmektedir. Bu işlem Robot Studio programı üzerinden gerçekleştirilebilir.

![RG830](_media/D_HareketKomutIsimVerme.png)

**1:** FlexPendant da görünen satırın Robot studio ekranında görünen hali

**2:**  FlexPendant da görünen yıldızlı kısma isimli atamanın ( Örnek olarak EgitimNok )yapıldığı değişken tanımlama kısmı

**3:** FlexPendant da görünen yıldızlı alana tanımlanan değişken isminin kullanılması. 

3 numaradaki gibi isimlendirme yapıldıktan sonra 3 numara ile aynı olduğundan 1 numarayı karmaşayı önlemek için programdan silebiliriz.

Artık program içinde EgitimNok değişkeni isim olarak çağırılıp kullanılabilir.

- 2.YÖNTEM

![RG830](_media/D_HareketKomutu2.png)

**A:** Tanıtılacak noktaya verilen isim

**B:** Depolama tipinin seçimi

**C:** Değişkeni hangi modüle kaydedeceğini seçiyoruz
 
 OK dedikten sonra seçtiğimiz modülün içerisine konum tanımlamasını öncesinde seçilen tool ve wobj ye göre kaydeder. Bu değişkeni **1.YÖNTEM** de görülen 3.kırmızı çerçeve deki yazılış tarzıyla kullanabiliriz.

## <span style="color: #000000; font-weight: bold;">3. Nokta üzerinden Offsetleme Hız ve Zone verilmesi </span>

![RG830](_media/D_Offsetleme.png)

**A:** Tanımlanan noktanın en sade hali. Nokta Modify edilirken bu en sade hali üzerinden yapılır. Offsetli yazım üzerinden izin verilmez.

**B:** temel bir referans noktasına (EgitimNok) bağlı olarak robotu belirli mesafelerde ötelemek için kullanılan fonksiyondur. Yeni bir nokta öğretmek yerine, mevcut bir noktadan sapma yaparak hareket üretmeyi sağlar.

**C:** X,Y,Z offset değerleri mm olarak

**D:** Robotun uç noktasının (TCP) saniyede kaç milimetre hızla hareket edeceğini belirler.

**E:** Robotun hedef noktaya ne kadar yaklaşacağını veya noktayı ne kadar "yumuşatarak" geçeceğini belirleyen köşe (path) parametresidir:

## <span style="color: #000000; font-weight: bold;">4. Magazinlere Yeni Yol Eklenmesi Durumu </span>

Sistemdeki aksesuar alma ve bırakma koordinatları, kat ve aksesuar numaralarına göre yapılandırılmış bir Array  mimarisi içerisinde saklanmaktadır.Sisteme yeni bir aksesuar eklenmesi durumunda, mevcut hiyerarşinin korunması için bu dizilere sıralı ekleme yapılması gerekmektedir.

- Yeni Konum Ekleme Prosedürü:

**Değişken Tanımlama:** Programın Variables modülünde yer alan mevcut aksesuar dizisine gidilmelidir.

**Dizi Genişletme:** Mevcut kat ve aksesuar sırası takip edilerek yeni koordinat verisi diziye dahil edilmelidir.

**Nokta Öğretme:** Diziye eklenen yeni indis için robotun fiziksel konumu öğretilmeli ve robtarget verisi güncellenmelidir.

Variables içerisindeki array leri aşağıdaki görselde görebilirsiniz. 

![RG830](_media/D_AlmaBirakmaArray.png)

- yeni eklenen yol için öğretme işlemini yaparken aşağıdaki görselde bulunan sırayı takip ederek eklediğiniz aksesuar ı seçtikten sonra modify diyerek noktayı güncelleyebilirsiniz. Bu işlemi yaparken tool seçiminin ToolGrip olmasını ve Wobj nin de tanıtım yapılan magazine göre seçilmesi gerekmektedir.

![RG830](_media/AlmaBirakmaNokta.png) 

Sistemde yer alan her bir aksesuarın varlık/yokluk kontrolü için kendine ait bir kontrol sensörü bulunmaktadır. Aksesuar kontrol noktasının doğru tanımlanması için şu prosedür izlenmelidir:

- Hizalama ve Konumlandırma:

Robot, ilgili istasyondan kalıbı aldıktan sonra, tutuş düzlemini ve oryantasyonunu bozmadan (doğrusal bir rotada) çıkış yapmalıdır. Aksesuar, sensörün tam karşısında ve algılama mesafesi dahilinde kalacak şekilde konumlandırılmalıdır. Robotun bu kontrol noktasındaki pozisyonu, sensörün aksesuarı en kararlı şekilde gördüğü konum olarak belirlenmeli ve kaydedilmelidir.

- Yazılımsal Yapı:

Alma-bırakma noktalarında olduğu gibi, aksesuar kontrol noktaları da her aksesuar grubuna özel olarak isimlendirilmiş Array (Dizi) yapıları içerisinde tanımlanmıştır. Sıralı ekleme yapılmalıdır yeni yol için. Bu sayede her aksesuar tipi için ayrı ve bağımsız kontrol koordinatları oluşturulabilir. Program içerisinde Variables modülündeki LMagazineAccessoryControl ve RMagazineAccessoryControl kısımlarına eklemeler yapılmalıdır. Aşağıda Aksesuar Kontrol için Array leri görebilirsiniz.

![RG830](_media/D_AksesuarKontrolArray.png)

- Kayıt İşlemi:
Hassas konumlandırma tamamlandıktan sonra, nokta kayıt adımları aşağıdaki görsel yönergeler takip edilerek gerçekleştirilmelidir.

![RG830](_media/AksesuarKontrolL.png)  ![RG830](_media/AksesuarKontrolR.png) 

