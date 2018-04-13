# 1)	Crowbar- Parola kırma aracı

Crowbar sızma testleri esnasında kullanılan bir parola kırma aracıdır. Diğer parola kırma araçlarına göre farklı bazı protokoller kullanmaktadır. Örneğin bazı digger araçlar SSH parola kırma için kullanıcı adı-şifre kullanmasına rağmen crowbar SSH anahtarı kullanmaktadır.

Crowbar OpenVPN , Remote Desktop Protocol with NLA support, SSH private key authentication ve VNC key authentication larda kullanılabilmektedir.

Kurulum

İlk olarak bağımlı olan gerekli şeyleri kurmak için,

## apt-get -y install openvpn freerdp-x11 vncviewer

Daha sonra son versiyonunu indirip kullanabilirsiniz.

Ben github üzerinden https://github.com/galkan/crowbar link üzerinde indirdim.

Kullanım

Önemli bazı parametler :

-h: Yardım menüsünü gösterir. 

-b: Yukarıda belirtilen crowbarın desteklediği servisleri kullanmak için başına yazılır. Örn: -b openvpn, -b rdp

-c: Sadece tek bir şifre yazacağımız zaman kullandığımız parameter. Eğer bir txt dosyasından parolaları okumak istediğimizde -C ve dosyanın yolu şeklinde kullanıyoruz.

-p: Port numarasını ifade eder.

-s: Hedef ip adresi veya aralığını gösterir. Eğer bunu bir dosyadan okumak istersen -S ve o ip listesinin olduğu dosyanın yolunu vermemiz gerekir.

-v: Denenen bütün kullanıcı adı - şifre leri gösterir.

-u : Sadece tk bir kullanıcı adı yazacağımız zaman kullanılan parametredir. Eğer bir txt dosyasından kullanıcı adlarını okumak istediğimizde -U ve dosya yolunu kullanmamız gerekmektedir.
Örnek kullanım kodu :

### ./crowbar.py -b rdp -u decoder -C/root/Desktop/rdp_pass.lst -s 10.5.41.212/32 -v

![ekran resmi 2018-04-12 16 39 39](https://user-images.githubusercontent.com/37982203/38737013-84fa6426-3f36-11e8-82f1-c6aa9016b8c7.png)
![ekran resmi 2018-04-12 16 39 52](https://user-images.githubusercontent.com/37982203/38737016-8a342b2a-3f36-11e8-8078-02790002c579.png)




