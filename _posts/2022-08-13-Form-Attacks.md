
## Form Attacks

### Submit Form

 Form ile saldırı;
 
 Web sitelerinde genelde form doldurup gönderme (submit etme) kısmı olur. Eğer bu tarz bir form doldurup submit etme varsa o alanda kod çalıştırıp çalıştıramadığımızı kontrol etmeliyiz.
 
 ![resim](https://user-images.githubusercontent.com/18248422/179507810-2274eaed-19b0-4861-8d82-fac781541cef.png)
 
 mesela bu örnekte submit kısmına ping yazıp gönderiyoruz ayrıca “ping 10.0.2.15” gibi bir komut yazdıktan sonra “ping 10.0.2.15; ls” yazıp gönderince “ls” komutunun  da çalıştığını görüyoruz (resimde kırmızı ile işaretli kısımda ls komutunun sonucu olan dosya listesini görüyoruz). Demek ki burada sadece ping değil başka komutlarda çalıştırabiliriz. İşte burda komut olarak mesela “reverse shell”  yani ters bağlantı komutu çalıştırabiliriz. İnternette reverse shell diye arattığımızda bir çok kaynak ve cheat sheet bulabiliriz.
 
 ![resim](https://user-images.githubusercontent.com/18248422/179507860-21d27aab-8709-46fc-b1b2-181f3ccbd87e.png)

 işte bunun gibi farklı farklı dillerde reverse shell komutları mevcut.
 
 ### Reverse Shell
 
  Reverse shell yani ters bağlantı, komut çalıştırabildiğimiz bir sunucudan kendi cihazımıza bir bağlantı açmamıza olanak sağlar. Backdoor mantığına benzerdir ama tam olarak aynı değil. Backdoor da karşıda bir kullanıcının bir .exe veya bir dosya çalıştırması, bir siteye vs. girmesi bi şeylere tıklaması gerekirken, reverse shell de biz kendimiz kod çalıştırabileceğimiz bir açık bulduğumuzda o zaafiyetten faydalanıp kendimize bağlantı yaptırarak içeriye daha kolay sızabilmek için açık bir kapı bırakmış oluyoruz. 
 
 Şimdi komutumuzu yani reverse shell komutunu girmeden önce netcad ile bir port açıp dinlemeye başlayalım.
 
 ![resim](https://user-images.githubusercontent.com/18248422/179507917-044034c1-a5e8-414f-85a2-259d60a688a3.png)
 
 bu şekilde netcad çalıştırarak “5050” portunu dinlemeye başlıyoruz.
 
 Ardından mesela php için yazılmış olan reverse shell komutunu siteye girelim;
 
![resim](https://user-images.githubusercontent.com/18248422/179508004-05fefc39-73dd-4cc8-9d53-b34c4744afe3.png)

  tabi bu komutta olan ip adresine kendi ip adresimizi ve port kısmına ise netcad ile dinlemeye başladığımız “5050” portunu giriyoruz. 
 
 ![resim](https://user-images.githubusercontent.com/18248422/179508054-c7bb3ac4-994a-4fed-a71b-76f985d73b5a.png)

 Gerekli düzenlemeleri yapınca komut bu hale geldi. Artık bu komutu gidip site üzerinde ki form da çalıştırmak üzere submit edebiliriz. 
 
 ![resim](https://user-images.githubusercontent.com/18248422/179508062-2eee4bfb-608d-4dfe-b1d4-902cbb76364b.png)
 
  bu şekilde yazıp submit ediyoruz.
 
 komutumuzu yazıp submit edince, terminalimizde nc ile açıp dinlemeye başladığımız 5050 portuna bağlantı geldi. Gördüğünüz gibi bu komut sayesinde bu siteden kendimize bir shell açıp içeriye girmeyi başardık artık websitesinin bütün dosyalarına erişebiliyoruz. Reverse shell işlemi başarılı olmuş oldu.
 
 ![resim](https://user-images.githubusercontent.com/18248422/179508086-8760d472-1ed1-47ce-bcc8-7fbaaf7c63a5.png)
 
 ### Upload Form
 
 ![resim](https://user-images.githubusercontent.com/18248422/179508138-475d51e6-ad3c-4726-a323-b46fa01af968.png)
 
bu tarz upload edebileceğimiz kısımlara kendi backdoor trojanımızı yüklemeye çalışarak da hacklemeyi deneyebiliriz.

 Şimdi sırf bu tarz durumlarda hızlıca bir backdoor oluşturup dinleyebilmek için yazılmış bir tool kullanacağız.
 
 Kullanacağımız tool adı weevely;
 
 ![resim](https://user-images.githubusercontent.com/18248422/179508160-48e436d6-0af1-460e-8be4-dcb1c8ee4051.png)
 
  "weevely" olarak komutu yazdığımızda nasıl kullanacağını bu şekilde anlatıyor. 
 
 Şimdi bir örnek ile backdoor oluşturup siteye upload edelim.
 
 ![resim](https://user-images.githubusercontent.com/18248422/179508183-c0283cd8-656d-4c8c-b241-61475bda8e30.png)
 
 "weevely generate <password> <path>/<filename>" şeklinde backdoor umuz oluştu.
 
 Şimdi root kısmına oluşturduğumuz connection.php backdoor unu siteye upload edelim.
 
  ![resim](https://user-images.githubusercontent.com/18248422/179508211-e1e6e2f7-febd-4d42-82ea-c8db4777873f.png)
 
 bu şekilde upload ettikten sonra oluşturup upload ettiğimiz “connection.php” dosyasının nereye kaydolduğunu da gösteriyor. Burada nereye yüklediğini ve gerçekten de yüklenmiş mi diye kontrol edip o url adresi almamız gerekiyor. 
 
  ![resim](https://user-images.githubusercontent.com/18248422/179508313-43f662e0-2abc-455c-8279-ed5989aaa7b3.png)

  burada “../../” kısmında da görüldüğü gibi iki klasör geriye gitmiş. Bizde tarayıcımızda iki klasör geriye gidilmiş haline bu “/hackable/uploads/connection.php” kısmını yapıştırırsak “connection.php” dosyamızın bulunduğu url adresine girmiş oluruz.
 
  ![resim](https://user-images.githubusercontent.com/18248422/179508328-4c7294b4-4c55-4199-b9bb-97a31d40b37c.png)

  tarayıcının adres kısmına bunu yazıp girdik ve bir hatayla karşılaşmadık demek ki yüklenmiş. Şimdi bu adresi weevely ile kullanalım.

 Şimdi weevely framework une geri dönüp bu upload ettiğimiz dosya sayesinde bağlantıyı açıp sızalım. 
 
 ![resim](https://user-images.githubusercontent.com/18248422/179508345-82c0f2f2-208f-4c03-a10c-579846a2dead.png)

 weevely yazıp url adresi ve backdoor'u oluştururken yazdığımız password'u yazıp çalıştırdıktan sonra, artık bağlantıyı kurduk ve cihazı hackledik. İşte bu kadar! Artık içerdeyiz.
 
 Önemli NOT: Eğer yüklenecek sayfa php uzantısını kabul etmiyorsa;
  
 ![resim](https://user-images.githubusercontent.com/18248422/179508381-b3fba26d-41bc-4565-9ec7-fab0891ff638.png)

  ### XSS
  
  ![resim](https://user-images.githubusercontent.com/18248422/179508426-1b8e1ae9-709a-4617-8699-5f0e23613a32.png)
  
  örneğin bir websitesinde bu şekilde bir mesaj gönderme kısmı varsa, mesaj kısmında bu örnekte olduğu gibi beef açıp, mesaj kısmında hook.js scriptini yazıp mesajı göndererek çalıştırıp, websitesini ziyaret edenleri hackleyebiliriz.
 
  ## creted by [@ahmetkara](https://github.com/ahmetQara)

 
