
## Aircrack Ng WPA/WPA2 Attack (Hack)

![resim](https://user-images.githubusercontent.com/18248422/176179455-3dbc443b-6377-4748-9c00-4998eb5db348.png)

 WEP'de olduğu gibi benzer yöntemlerle önce handshake yakalayıp ardından bu handhake'i elimizde bulunan bir wordlist ile karşılaştıracağız ve bu şekilde şifreyi kırmaya çalışacağız.

Önce aşağıda ki komutlarla bir .cap dosyası elde ediyoruz.

![resim](https://user-images.githubusercontent.com/18248422/176179468-eea2ffdc-a06a-4fd6-aa84-dfaa7f8e88ba.png)

Eğer bu komut çalışırken bir handshake yakalayamazsak bu komut çalıştığı esnada bu modeme birileri çıkıp geri bağlanmamış demektir. Bu durumda deauth attack yaparak bu ağda bulunan bir cihazı kısa süreliğine ağdan atarsak geri bağlandığı esnada hanshake yakalayabiliriz. Deauth attack için şu komutu kullanabiliriz

![resim](https://user-images.githubusercontent.com/18248422/176179524-51441726-f7cf-4f19-84e8-65a165c0b757.png)

Bu komutta 1000 tane paket gönderiyor fakat bu kadarına gerek olmayacaktır küçük bir paket gönderimi çoğu zaman iş görecektir.

Artık içerisinda hanshake bilgisi bulunan bir .cap dosyası elde ettiğimize göre artık wordlist ile karşılaştırma yapabiliriz. İnternetten bir wordlist indirebilir veya kendimiz belli karakterler ve uzunluk belirleyerek bir wordlist oluşturabiliriz. Kendimiz bir wordlist oluşturmak için crunch kullanacağız;

![resim](https://user-images.githubusercontent.com/18248422/176179547-ad36a20d-4a90-49ca-a6af-e446a44022a5.png)

bu şekilde bir wordlist dosyası oluşturduktan sonra aşağıda ki şekilde bir komut yazarak

![resim](https://user-images.githubusercontent.com/18248422/176179593-4f7c1cac-6a80-4c87-aff0-fd06e7057d9f.png)

elimizde ki .cap dosyası ile wordlist'i karşılaştırıp şifreyi kırmaya çalışacağız.
