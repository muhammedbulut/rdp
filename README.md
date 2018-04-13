# 1)	Crowbar - Parola kırma aracı

Crowbar sızma testleri esnasında kullanılan bir parola kırma aracıdır. Diğer parola kırma araçlarına göre farklı bazı protokoller kullanmaktadır. Örneğin bazı digger araçlar SSH parola kırma için kullanıcı adı-şifre kullanmasına rağmen crowbar SSH anahtarı kullanmaktadır.

Crowbar OpenVPN , Remote Desktop Protocol with NLA support, SSH private key authentication ve VNC key authentication larda kullanılabilmektedir.

Kurulum

İlk olarak bağımlı olan gerekli şeyleri kurmak için,

#### apt-get -y install openvpn freerdp-x11 vncviewer

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

#### Örnek kullanım kodu :

#### ./crowbar.py -b rdp -u decoder -C/root/Desktop/rdp_pass.lst -s 10.5.41.212/32 -v



![ekran resmi 2018-04-12 16 39 52](https://user-images.githubusercontent.com/37982203/38737016-8a342b2a-3f36-11e8-8078-02790002c579.png)

![ekran resmi 2018-04-12 16 39 39](https://user-images.githubusercontent.com/37982203/38737013-84fa6426-3f36-11e8-82f1-c6aa9016b8c7.png)




#### Örnek Kullanım video linki:

https://www.youtube.com/watch?v=M15ESpW0Vf8



#   2) Patator - Parola Kırma Aracı
Patator parola tahmin etme atakları için yazılmıştır. Diğer araçlara göre hızlı olması için optimize edilmiş çoklu thread modülünü kullanan Python ile yazılmıştır. 20 'e yakın protokole paralo kırma atağı gerçekleştirebilmektedir. Bunlardan bir kaç tanesi brute-force RDP, brute-force SSH, brute force FTP …

Github üzerinden https://github.com/lanjelot/patator link üzerinde indirdim ve ayrıca kodda biraz değişiklik yaptım. Değişiklik yaptığım kodu yukarıya ekledim.


Kullanım:

./patator.py ile modülleri görebilirsiniz. Ayrıca kullanmak istediğiniz modülün daha ayrıntılı bilgisi ./patator.py module -help ile ögrenebilirsiniz. Burada parametreler ve ayrıca örnek kullanım mevcuttur.

Önemli bazı parametreler:

host=IP : hedef makinenin ip veriliyor.

user='test' : Tırnakların içine hedef makinenin kullanıcı ismi yazılıyor.

Password=FILE0 0=filename : Hedef makine üzerinde denenecek parolaları dosyadan çekmek istediğimizde FILE0 eşitliyoruz ardından sayıya kendi oluşturduğumuz dosya ismini veriyoruz.

--v: Versiyonu göstermektedir.

-h/ --help : Yardım mesajlarını göstermektedir.

--timeout=N : Yeni payload göndermeden önce N saniye beklemenizi sağlar.

-l DIR = çıktıyı DIR içine kaydetmenizi sağlar.

#### Örnek Kullanım Kodu:

#### ./patator.py rdp_login host=192.168.0.31 user='decoder' password=FILE0 0=rdp_pass.lst




![ekran resmi 2018-04-13 12 33 26](https://user-images.githubusercontent.com/37982203/38737266-5d9b92fa-3f37-11e8-848c-b9c70ffbb410.png)

![ekran resmi 2018-04-13 12 33 56](https://user-images.githubusercontent.com/37982203/38737271-6242726a-3f37-11e8-8cdd-d419fca19cff.png)

![ekran resmi 2018-04-13 12 34 05](https://user-images.githubusercontent.com/37982203/38737275-643d5f4e-3f37-11e8-94f4-278aac440cb3.png)

![ekran resmi 2018-04-13 12 34 50](https://user-images.githubusercontent.com/37982203/38737280-6a7911d2-3f37-11e8-87ce-8ecf13b8cdfd.png)


#### Örnek Kullanım video linki:

https://www.youtube.com/watch?v=KoOftYuh7fg&t=10s


# 3) Ncrack - Parola Kırma Aracı

Ncrack sızma testleri esnasında kullanılan bir parola kırma aracıdır. Geniş kapsamlı olup FTP, SSH, Telnet, HTTP, SMB, RDP, VNC gibi modülleri bulunmaktadır. Kali linuxda kullanabilinmektedir.

Kullanım

Onemli bazı parametler :

Hedef Belirleme - IP adresi, hostname gibi

Bunun için başında input anlamına -i yanında dosya türü ve yanında da dosyanın ismi belirtilir. Örn: -iX <inputfilename> XML türünde girdi dosyası

Servis Belirleme - Modül kullanımı

Yukarıda belirtilen desteklemiş olduğu servisleri <services>://target şeklinde kullanılabilir. Örnek kullanım: rdp://192.41.05.122

Zamanlama ve Performans

Ncrak eşzamanlı paralel bağlantı sayısını belirlememize yardımcı olur. Örneğin cl minimum eş zamanlı bağlantı sayısını, CL maximum eş zamanlı bağlantı sayısını ve cd <time> ise her bağlantı arasında ne kadar delay olacağını belirlememizi sağlar. -T <0-5> ile de hızımızı ayarlayabiliriz. RDP karmaşık yapılı bir protocol olduğu için bir sürü paket değişimi olacağından bu zamanlama parametreleri kullanılması önemlidir.(kaynak= man ncrack)

Kimlik Doğrulama

-U <filename>: Kullanıcı adı dosyasından okuma sağlar.
--user <username_list>: Virgülle ayrılmış kullanıcı adlarını veya sadece bir tane kullanıcı adı kullanacağımızda kullanırız.
-P<filename>: Parola dosyadan okumamızı sağlar.
--pass <password_list>: Virgülle ayrılmış parolaları veya sadece tek bir parola kullanıcağımızda kullanırız.
--password-first: Her kullanıcı adı için parola dosyasındaki parolaları tek tek dener. Default seçeneğinde bu yoktur.

Çıktı Dosyaları

Bunun için output anlamına gelen -o , yanına dosya türü ve yanına dosya ismi şeklinde kullanılır. Örnek kullanım:-oX <filename> XML türünde çıktı dosyası.

-h : Yardım özet sayfasını göstermektedir.
-V: versiyon numarasını göstermektedir.

#### Örnek kullanım kodu: 

#### ncrack -vv - -user decoder -P /root/Desktop/rdp_pass.lst rdp://192.168.0.22



![ekran resmi 2018-04-13 01 40 03](https://user-images.githubusercontent.com/37982203/38737538-3d9a63c2-3f38-11e8-8643-8c7f49f83270.png)

![ekran resmi 2018-04-13 01 40 22](https://user-images.githubusercontent.com/37982203/38737541-407133aa-3f38-11e8-9d94-ea32f1a6b1ee.png)

![ekran resmi 2018-04-13 01 58 46](https://user-images.githubusercontent.com/37982203/38737543-41dbe244-3f38-11e8-957f-18431715f5c3.png)

#### Örnek Kullanım video linki:

https://www.youtube.com/watch?v=i4UNL_XUNhg

# 4)	Medusa - Parola Kırma Aracı
Medusa büyük ölçüde paralellesmis, modüler bir parola kırma aracıdır. Birçok servise uzaktan doğrulama izni saglamaktadır. Thread tabanlı paralelleştirme testi yaptığı için eş zamanlı olarak coklu host, kullanıcı adı ve parolalarla yapılabilmektedir. Esnek kullanıcı girdisi sağlamaktadır. Modular dizayn sayesinde her servis birbirinden bağımsızdır. Bu sayede servis listesini genişletmesi için ana uygulamayı değiştirmesine gerek yoktur.

Kullanım :

Önemli bazı parametreler

-h: Hedef hostadı veya ip adresi belirlemede kullanılır. Eğer bir dosyadan okuma işlemi ile yapacaksanız -H kullanmalısınız.

-u: Hedef ip üzerinde denenecek kullanıcı adı ile birlikte kullanılır. Eğer bu işlemi dosyadan okuma ile yapacaksanız -U kullanmalısınız.

-p : Hedef ip adresi üzerinde denenecek parola ile birlikte kullanılır. Eğer bu işlemi dosyadan okuma ile yapacaksanız -P kullanmalısınız.

-O : Yanına dosya ismi ekleyerek çıktıların tutulmasını sağlayabilirsiniz.

-m/M : Çalıştırılacak modülu belirlemenizi sağlamaktadır.

-d : Medusa içinde çalıştırabileceğiniz modülleri görmenizi saglamaktadır.

-f/F : İlk bulduğunuz eşleme sonrasında aramaniyi durdurmak isterseniz kullanılmaktadır.

-V : Versiyonu göstermektedir.

-t : Toplam eşzamanlı olarak teste girebilecek login sayısını belirlememizi sağlıyor.

-T : Toplam eşzamanlı olarak teste girebilecek host adı sayısını belirlememizi sağlıyor.

#### Örnek Kod Kullanımı:

#### medusa -u decoder -P /root/Desktop/rdp_pass.lst -h 192.168.0.22 -M rdp

![ekran resmi 2018-04-13 01 42 05](https://user-images.githubusercontent.com/37982203/38737720-c6f011da-3f38-11e8-91e1-da7acb4e37a5.png)

![ekran resmi 2018-04-13 14 07 09](https://user-images.githubusercontent.com/37982203/38737722-c9fbc202-3f38-11e8-8749-68cedba46053.png)

![ekran resmi 2018-04-13 01 59 09](https://user-images.githubusercontent.com/37982203/38737726-cacbbf48-3f38-11e8-93e0-cf73603d56a5.png)

#### Örnek Kullanım video linki:

https://www.youtube.com/watch?v=QErn6wUyxps




