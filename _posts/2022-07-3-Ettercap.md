## Ettercap

NOT: Günümüzde https downgrade çok işe yaramayan bir yöntem.  
  
öncelikle conf dosyasını açalım bazı ayarları değiştireceğiz;

![resim](https://user-images.githubusercontent.com/18248422/178333564-dcfedd23-8551-4393-999f-e68b9a5adec5.png)

bu iki değeri 0(sıfır) yap

![resim](https://user-images.githubusercontent.com/18248422/178333586-c2a379e2-613c-45c2-a3d6-ebb0f27155eb.png)

ardından

![resim](https://user-images.githubusercontent.com/18248422/178333626-312e0e82-45eb-42f4-8318-ef52c01fb28a.png)

linux kısmında olan bu iki satırı ise yorum satırı olmaktan çıkart

şimdi ettercap çalıştıralım;

![resim](https://user-images.githubusercontent.com/18248422/178333661-cc9b7d6e-63fb-49c0-8982-8e69b1bd1338.png)

 "ettercap -Tq ///"  komutu ile sessiz modda çalıştırıyoruz. 

![resim](https://user-images.githubusercontent.com/18248422/178333716-3a00f5c5-08d3-43cf-9c79-63bb47c8bc17.png)

bu şekilde çalışmaya başlıyor.

Çalışırken “L” basarsak bize host list verir (netdiscover taraması sonucu gibi);

![resim](https://user-images.githubusercontent.com/18248422/178333792-71010473-a405-4926-9141-636c19ccc12e.png)

şimdi ettercap'i daha spesifik bir komut ile çalıştıralım

![resim](https://user-images.githubusercontent.com/18248422/178333802-fe0f89bc-2bb8-44e9-9d3f-7568d06c434b.png)

-Tq sessiz mod

-M mode → arp:remote seçtik

-i interface

üstte ki resimde de gördüğümüz gibi gateway ve hedef ip  /// aralarına yazıyoruz şu şekilde;

 “/gateway//” ve “/hedef ip//”  (çift tırnaklar olmadan) 
 
 burada ki “///” manası aslında aralarında şunlar yazılabilir demek;

mac_address/ipv4/ipv6/port

veya “///” şeklinde boşta bırakılabilir duruma göre ilgili yerlere bizim üstte ki resime olduğu gibi ip adresleri de verilebilir.

NOT: komutu verirken 2 tane /// olduğuna dikkat edelim, birincisi gateway, ikincisi ise target için

Ve komutu çalıştırıyoruz;

![resim](https://user-images.githubusercontent.com/18248422/178333837-3b9eaa61-6e3d-42fe-abad-e2c416b90d0d.png)

çalışır hali bu. Şu anda hedef ip dinleniyor (listening/sniffing)

![resim](https://user-images.githubusercontent.com/18248422/178333863-12d5c9d9-a3ba-4955-a885-16146af7891d.png)

hedef cihazda bir http siteye girip login request gönderdim, linux'e geri dönüyorum ettercap'e bakmak için;

![resim](https://user-images.githubusercontent.com/18248422/178333886-a8923141-7a56-42b9-b4ba-f2949e401e09.png)

 ve görüldüğü gibi kullanıcı adı ve pass direk yakalayıp bize gösterdi. Buda demek oluyor ki wireshark gibi bütün paketleri değilde username, pass gibi bilgileri bize gösteren bir framework ettercap.

 NOT: Eğer belli aralıkta olan ip adreslerine saldıracaksak;
 
 ettercap -Tq -M arp:remote -i eth0 /10.0.2.1// /10.0.2.11-20//  → sonuna dikkat et, 11-20 arasında ki ip adreslerini hedefledik.
 
 saldıracağımız iki ip adresi varsa virgül ile ayırıp ikinci ip adresini ekleyebiliriz;
 
 ettercap -Tq -M arp:remote -i eth0 /10.0.2.1// /10.0.2.11, 10.0.2.12//
 
 NOT-2: Eğer iptables komutu ile port yönlendirmesi yapıp ardından sslstrip çalıştırdıysak o zaman https downgrade yapacağımıza göre “-S” komutu ile ettercap çalıştırmalıyız ki ettercap'e bu "-S" komutu ile aslında kendisinin bir ssl sertifikası kullanmamasını çünkü, biz sslstrip sayesinde zaten bir ssl sertifikası oluşturduğumuzu belirtmiş oluyoruz.
 
 Yani kısacası; -S komutunu eklemeliyiz ki ettercap kendisi bir ssl sertifikası üretmeye kalkmasın çünkü biz zaten bunu sslstrip ile yaptık.
 
 ettercap çalışırken “p” basarsak bize içinde bulunan plugin'lerin listesini verir
 
 ![resim](https://user-images.githubusercontent.com/18248422/178333937-e65fb6f4-afc1-49bf-a43b-6c5338a5cd79.png)

 buradan istediğimiz plugin adını yazıp çalıştırabiliriz. Bu yönüylede ettercap çok kullanışlı bir araçtır.
 
 ettercap ile dns spoof
 
 öncelikle ettercap'in dns dosyasına geliyoruz;
 
 ![resim](https://user-images.githubusercontent.com/18248422/178333965-d38791e4-afd6-4148-b02f-f7c5a999c430.png)
 
 ![resim](https://user-images.githubusercontent.com/18248422/178333992-4a0ba4e9-33ee-4ad0-9b84-4ce829d40cdc.png)
 
 bu şekilde yönlendirmek istediğimiz adres ve kendi ip adresimizi veriyoruz.
 
 Ardından apache server açıyoruz ki verdiğimiz adrese yönelsin (10.0.2.15 vermiştik)
 
 apache çalıştırıyoruz;
 
 ![resim](https://user-images.githubusercontent.com/18248422/178334004-ca03b801-efe6-45b9-9b52-ff974a98e58d.png)
 
 sonra ettercap çalıştırıyoruz;
 
 ettercap -Tq -M arp:remote -P dns_spoof -i eth0 /10.0.2.1// /10.0.2.11//
 
 bu şekilde çalıştırırken direk "-P dns_spoof" olarak istediğimiz bir plugin çalıştırabiliriz veya normal başlatıp “p” basıp seçebiliriz
 
 ![resim](https://user-images.githubusercontent.com/18248422/178334030-4182aa75-cf0f-4911-aba3-526f72e51352.png)
 
  dns_spoof ile çalışarak sniffing başladı. Eğer bir hata yok ise hedef şu anda “unicornitem.com” a girmeye çalışınca bizim apache server'ımıza yönlendirilecektir. 
 
  arp koruması varsa - tek yönlü arp
 
  eğer modemde arp koruması varsa o zaman aynı mac adresine sahip ikinci cihazın bağlanmasına modem izin vermez. Bu durumda tek yönlü arp saldırısı yapılır. Tek yönlü saldırı şu demektir; biz hedef cihaza gidip “ben modemim” diye kendimizi tanıtıyoruz fakat man in the middle atak da olduğu gibi gidip bir de modeme ben “hedef cihazım” demiyoruz ki modem durumu anlamasın. Bu şekilde tek yönlü atak yaparak başarılı oluruz. 
  
  Bunun ettercap kodu ise şöyle;
  
  ettercap -Tq -M arp:oneway -i eth0 /10.0.2.11// /10.0.2.1// → buraya dikkat çünkü normal saldırıya göre modem ip ile hedef ip ters yazdık.
  
  bu şekilde yaptığımızda bazen ettercap paket yakalamıyor tek yönlü olduğu için, bu durumda wireshar ile dinleyebiliriz paketleri.
 
  Daha fazlası için “ettercap -h”
 
 
 ## creted by [@ahmetkara](https://github.com/ahmetQara)

 

 
 



