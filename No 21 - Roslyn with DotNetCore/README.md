# .Net Core Üzerinde Roslyn Pratikleri Yapmak

Amacım uzun süredir _(Tanıtıldığı Ekim 2011 yılından bu yana)_ hayatımızda olan .Net Compiler Platform'unu _(Kod adı Roslyn)_ pratik kod parçaları ile tanımak. Roslyn ile çalışma zamanında kod çalıştırmak ve hatta kodu analiz etmek mümkün. Özellikle kod satır sayısı çok yüksek olan uygulamalarda clean code pratiklerinin uygulanması gibi durumlarda epey kullanışlı. Hatta şöyle de düşünülebilir. C# bilgimiz var ve .Net Framework kütüphanesine hakimiz. Bazı otomatize sistem işleri için Powershell veya Bash script öğrenmek yerine C#'ı script dili olarak kullanabilmemiz mümkün. .Net Core desteği olması da bunu Cross Platform yapabilmemize izin veriyor. Bu sebepten çalışmadaki amaçlarımdan birisi de dotnet-script komut satırı aracını kullanarak içerisine C# script kodları içeren csx uzantılı kodları çalıştırmak. Bu CSX uzantılı _(CSharp Script dosyası anlamına geliyor)_ dosyalar Powershell veya bash için yazılmış script dosyaları gibi düşünülebilir.

## Birinci Önrek için Ön Hazırlıklar ve Çalıştırma

Heimdall _(Ubuntu 20.04)_ üzerindeki pratikler için uygulamaya Microsoft.CodeAnalysis.CSharp.Scripting paketinin eklenmesi lazım.

```bash
dotnet new console -o HelloRoslyn
dotnet add package Microsoft.CodeAnalysis.CSharp.Scripting

dotnet watch run
```
>Kodun çalışması ile ilgili bilgiler yorum satırlarında mevcut ;)

Region1 çalışmasına ait örnek ekran görüntüsü,

![Screenshot_01.png](./assets/Screenshot_01.png)

Region2 çalışmasına ait örnek ekran görüntüsü,

![Screenshot_02.png](./assets/Screenshot_02.png)

Region3 çalışmasına ait örnek ekran görüntüsü,

![Screenshot_03.png](./assets/Screenshot_03.png)

## İkinci Örnek için Ön Hazırlıklar ve Çalıştırma

İlk örneklerde C# kodlarının dinamik olarak yine bir C# uygulaması içerisinden çalıştırılması söz konusu. Bu sefer Nuget paket desteği de sunan dotnet-script ile script dosyalarının çalıştırılması gündemde.

```bash
# Önce gerekli komus satırı aracı yüklenir
dotnet tool install -g dotnet-script

# Yüklü olan dotnet tool setine aşağıdaki komutla bakılabilir
dotnet tool list -g

# Örnek script dosyası
touch dirwatcher.csx

# Çalıştırmak içinse
dotnet script dirwatcher.csx
```

![Screenshot_04.png](./assets/Screenshot_04.png)

## Bölümün Bomba Soruları

- Console uygulamasının kodunun ikinci region bloğunda yer alan kod çalışma zamanında hangi durumlarda exception vererek sonlanır _(Kısaca Patlar)_
- CSX örneği ilk çalıştırıldığında cevap vermesi neden çok uzun sürmüştür.
- CSX örneğindeki Nuget paketi sizce nereye inmiştir?

## Ödevler

- Bir web sayfasında Multiline TextBox kontrolüm olsun. İçine yazdığım basit C# kodlarının sonucunu anında başka bir kutucukta görebileyim. Web'deki pencerede C# script'leri yazdığımızı düşünelim.
- dotnet-script init komutunu deneyip ne işe yaradığını anlamaya çalışın.