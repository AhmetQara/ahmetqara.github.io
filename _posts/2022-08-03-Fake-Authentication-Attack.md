## Fake Authentication Attack

![resim](https://user-images.githubusercontent.com/18248422/175950672-562a2bca-170f-4ede-b3c3-9b3576c0eb86.png)
 
Bu şekilde hedef bir ağ belirterek wepcrack adında bir dosyaya toplanan paketleri kaydettiriyoruz.

![resim](https://user-images.githubusercontent.com/18248422/175950740-5d515209-44b0-40f5-8953-d02af89bf25f.png)

ardından bu wepcrack-01.cap uzantılı dosyayı aircrack-ng ile çalıştırıyoruz ve bize “IV-PASSWORD” kısmında ki “IV” leri toplamaya başlıyor. O anda ağda ne kadar çok trafik olursa o kadar hızlı toplar. İşte bu noktada bu ağa fakeauth yöntemiyle kendimizi bağlanmış gibi gösterip ardından o ağda trafik ağı üreterek süreci hızlandırabiliriz. 
 
### Fakeauth Attack 

Bu atak kendimizi seçeceğimiz hedef bir ağa sanki bağlanmışız gibi göstermemizi sağlar.

![resim](https://user-images.githubusercontent.com/18248422/175950786-de219a27-5db4-4c7f-a19e-0b894aeace77.png)

 Yukarıda olduğu gibi önce -a <bağlanacağımız hedef MAC adresi> ardından -h <kendi cihazımızın MAC adresi> ve <wlan0mon> şeklinde bağlanacağımız arayüz ismi (wi-fi adapter vb) belirtip kendimizi o ağa bağlanmış gibi gösterebiliriz.

 Ağa bu şekilde bağlanmış gibi gösterdikten sonra;

 ![resim](https://user-images.githubusercontent.com/18248422/175950845-508b676c-4fec-4f9b-83f5-32f6acf60b4b.png)

 bu şekilde yine aireplay-ng ile “--arpreplay -b <hedef MAC> -h <kendi MAC adresimiz> wlan0mon” komutu ile o ağda örneğin WEP algoritmasını kullanan bir ağ ise bu algoritmada ağ içinde paket alışverişi esnasında üretilen “IV-PASSWORD” şeklinde ki “IV” kısmını okuyabilir hale gelir ve de bu “IV” kısmı bi süre sonra tekrar eden algoritmalar oldukları için aircrack-ng yöntemiyle kolayca “PASSWORD” kısmına erişip şifreyi kırabiliriz.

## creted by [@ahmetkara](https://github.com/ahmetQara)
