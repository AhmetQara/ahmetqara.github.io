
 ## Deauthentication Attack (yetkisizlendirme atağı)
 
 ![resim](https://user-images.githubusercontent.com/18248422/175813642-e7cc6bd0-048f-4969-83b8-63e4c8b852bc.png)

 aireplay-ng-deauth <#gönderilecek PaketSayısı> -a <saldırılacak ağın MAC adresi> <arayüz>

 bu atak saldırılacak ağdaki tüm cihazlara yapılır ve başarılı olma şansı spesifik bir cihaza yapılmasına göre daha düşüktür. Eğer tek bir cihaza spesifik atak yapmak istiyorsak o zaman;

![resim](https://user-images.githubusercontent.com/18248422/175813649-c8a1c99c-fcff-42a1-a125-2051a8e61661.png)

  bu şekilde ek olarak "-c <hedefin mac adresi>" belirterek saldırı yapacağımız ağda bulunan spesifik bir hedefe saldırı yapıp onu yetkisizlendirip ağdan atabiliriz ve başarı şansımız daha yüksek olur.     

Deauthentication Attack mantığı şu şekilde çalışır:

![resim](https://user-images.githubusercontent.com/18248422/175813659-bc3ed673-4b23-4a37-ab69-27c48a24c766.png)

WEP şifreleme türünün çalışma mantığı

![resim](https://user-images.githubusercontent.com/18248422/175813665-8d922ab0-076a-4437-9998-54e42f4b5726.png)

 Yukarda ki resimde kırmızı yazılı ve işaretli kısımda gördüğümüz üzere modem WEP ile şifrelendiğinde cihazlar arası request--response alışverişi yaparken “IV(initialization vector) + KEY (PASSWORD)” adında iki değişken kullanır. Bu ikisi birleştirilip öyle şifrelenir. İşte bu alışveriş esnasında her bir request-response esnasında mesela telefondan modeme “IV+KEY(PASSWORD)” şeklinde değil ama “IV” kısmı gidiyor. Dışardan bir kişide bazı yöntemleri kullanarak bu “IV” kısmını görebiliyor “KEY(PASSWORD)” kısmını göremiyor. İşte bu noktada şöyle bir açık ortaya çıkıyor; bu “IV” kısmı sadece 24 bitlik küçük karakterlerden oluşuyor o yüzden belli bir yerden sonra tekrar etmeye başlıyor. Bu tekrar etme durumundan dolayı belli başlı programlar kullanılarak devamlı tekrar eden patternları, şemaları birbirleriyle eşleştirerek şifrelerle “KEY(PASSWORD)” eşleştirilip şifre kırılabiliyor.
 
![resim](https://user-images.githubusercontent.com/18248422/175813673-f511b8b8-402b-4f91-8436-cfdec7fd9c04.png)

 bu şekilde hedef bir ağ belirterek wepcrack adında bir dosyaya toplanan paketleri kaydettiriyoruz.
  
 ![resim](https://user-images.githubusercontent.com/18248422/175813683-98b5e5fe-5708-4c44-a766-babdb535a609.png)

ardından bu wepcrack-01.cap uzantılı dosyayı aircrack-ng ile çalıştırıyoruz ve bize “IV-PASSWORD” kısmında ki “IV” leri toplamaya başlıyor. O anda ağda ne kadar çok trafik olursa o kadar hızlı toplar. İşte bu noktada bu ağa fakeauth yöntemiyle kendimizi bağlanmış gibi gösterip ardından o ağda trafik ağı üreterek süreci hızlandırabiliriz. 
 
 
### Fakeauth Attack 

Bu atak kendimizi seçeceğimiz hedef bir ağa sanki bağlanmışız gibi göstermemizi sağlar.

![resim](https://user-images.githubusercontent.com/18248422/175813696-65647fc8-bf9d-4ff5-bfe2-1a390e56da0a.png)

Yukarıda olduğu gibi önce -a <bağlanacağımız hedef MAC adresi> ardından -h <kendi cihazımızın MAC adresi> ve <wlan0mon> şeklinde bağlanacağımız arayüz ismi (wi-fi adapter vb) belirtip kendimizi o ağa bağlanmış gibi gösterebiliriz.

Ağa bu şekilde bağlanmış gibi gösterdikten sonra;

![resim](https://user-images.githubusercontent.com/18248422/175813720-bcb73b5b-305e-4709-90d4-f67e85215b7e.png)

bu şekilde yine aireplay-ng ile “--arpreplay -b <hedef MAC> -h <kendi MAC adresimiz> wlan0mon” komutu ile o ağda örneğin WEP algoritmasını kullanan bir ağ ise bu algoritmada ağ içinde paket alışverişi esnasında üretilen “IV-PASSWORD” şeklinde ki “IV” kısmını okuyabilir hale gelir ve de bu “IV” kısmı bi süre sonra tekrar eden algoritmalar oldukları için aircrack-ng yöntemiyle kolayca “PASSWORD” kısmına erişip şifreyi kırabiliriz.

## creted by [@ahmetkara](https://github.com/ahmetQara)
