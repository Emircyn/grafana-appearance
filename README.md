# Önemli!!
Eğer değişiklikleri görmüyorsanız tüm adımlar için geçerli
```bash
systemctl restart grafana-server
```
***Bu komut Grafana servisini yeniden başlatır.***


# Simgeler (Favicon)

**Favicon**, tarayıcı sekmesinde uygulama başlığının yanında görünen simgedir.  
Kendi favicon’unuzu kullanmak için, **fav32.png** ve **apple-touch-icon.png** dosyalarını istediğiniz görüntülerle değiştirebilirsiniz.  

Bunun için aşağıdaki komutu kullanabilirsiniz:

```bash
cp img/fav32.png /usr/share/grafana/public/img/fav32.png
cp img/fav32.png /usr/share/grafana/public/img/apple-touch-icon.png
```
# Logo

**Giriş sayfasındaki logo**, kullanıcıların dikkatini çeken ilk unsurdur.  
Bu logoyu değiştirmek için aşağıdaki adımları izleyin:

- `grafana_icon.svg` dosyasını kendi logonuzla değiştirin.

### Komut:
```bash
cp img/logo.svg /usr/share/grafana/public/img/grafana_icon.svg
```

# Giriş Arka Planı

**Arka plan görüntüsü**, hem açık hem de koyu temalar için özelleştirilebilir.  
Arka plan görüntüsünü özelleştirirken, her iki tema için de dosyaları değiştirmeniz gerekir. Aynı resmi kullanabilirsiniz, ancak her iki dosyanın da değiştirilmesi gereklidir.

### Komutlar:
```bash
cp img/background.svg /usr/share/grafana/public/img/g8_login_dark.svg
cp img/background.svg /usr/share/grafana/public/img/g8_login_light.svg
```
# Uygulama Başlığı

**Tarayıcı sekmesinde görünen uygulama başlığı (application title)** aşağıdaki komutla değiştirilebilir:

### Komut:
```bash
find /usr/share/grafana/public/build/ -name *.js -exec sed -i 's|"AppTitle","Grafana")|"AppTitle","MoniStream")|g' {} \;
```
Eğer başlıklar değişmezse;
## Başlıkları Elle Değiştirme Adımları

### Başlıkları Kontrol Etmek için Komut:
Aşağıdaki komutu kullanarak "Welcome to Grafana" ifadesini içeren dosyaların listesini alabilirsiniz:

```bash
grep -r -l /usr/share/grafana/public/build 'Welcome to Grafana'
```
Bu komut, belirtilen dizindeki dosyaları tarar ve "Welcome to Grafana" ifadesini içeren dosyaların isimlerini listeler.

### Nano ile Dosyaları Açma:
Çıktıdan aldığınız dosya isimlerini kullanarak, her dosyayı ***nano*** ile açabilirsiniz.
### Örneğin:
```bash
nano /usr/share/grafana/public/build/app.js
```
Bu komut, app.js dosyasını nano editörü ile açacaktır.

## Yazıyı Değiştirme

***nano*** açıldıktan sonra, ***"Welcome to Grafana"*** yazısını bulun ve şu şekilde değiştirin:

- ***Ctrl + W*** tuşlarına basarak arama kutusuna ***"Welcome to Grafana"*** yazın ve Enter tuşuna basın.
- Bulduğunuz yazıyı ***"Welcome to MoniStream"*** olarak değiştirin.

## Dosyayı Kaydedip Çıkma:

Değişiklikleri kaydetmek için:

- ***Ctrl + O*** tuşlarına basın.
- ***Enter*** tuşuna basarak kaydedin.
- Çıkmak için ***Ctrl + X*** tuşlarına basın.

#### ***grep*** komutundan aldığınız diğer dosyaları nano ile açarak aynı işlemi tekrarlayın.

# Giriş Sayfası Altbilgisi

**Altbilgideki bağlantılar** (isimler/URL’ler) özelleştirilebilir veya tamamen kaldırılabilir.  
Aşağıdaki komutlar, altbilgiyi düzenlemek veya bağlantıları kaldırmak için kullanılabilir:

### Bağlantıları Kaldırmak İçin:

```bash
find /usr/share/grafana/public/build/ -name *.js -exec sed -i 's|{target:"_blank",id:"documentation",text:(0,r.t)("nav.help/documentation","Documentation"),icon:"document-info",url:"https://grafana.com/docs/grafana/latest/?utm_source=grafana_footer"},{target:"_blank",id:"support",text:(0,r.t)("nav.help/support","Support"),icon:"question-circle",url:"https://grafana.com/products/enterprise/?utm_source=grafana_footer"},{target:"_blank",id:"community",text:(0,r.t)("nav.help/community","Community"),icon:"comments-alt",url:"https://community.grafana.com/?utm_source=grafana_footer"}||g' {} \;
```
```bash
find /usr/share/grafana/public/build/ -name *.js -exec sed -i 's|{target:"_blank",id:"version",text:`${e.edition}${s}`,url:t.licenseUrl}||g' {} \;
```
```bash
find /usr/share/grafana/public/build/ -name *.js -exec sed -i 's|{target:"_blank",id:"version",text:`v${e.version} (${e.commit})`,url:i?"https://github.com/grafana/grafana/blob/main/CHANGELOG.md":void 0}||g' {} \;
```
```bash
find /usr/share/grafana/public/build/ -name *.js -exec sed -i 's|{target:"_blank",id:"updateVersion",text:"New version available!",icon:"download-alt",url:"https://grafana.com/grafana/download?utm_source=grafana_footer"}||g' {} \;
```

eğer kaldırılmamışsa css ile kaldıracağız.

# CSS Dosyası Oluşturma
### ***/usr/share/grafana/public/build/css*** Klasörünü Oluşturun

İlk olarak, `css` klasörünü oluşturmanız gerekiyor. Terminalde şu komutu kullanarak bu klasörü oluşturabilirsiniz:

```bash
mkdir -p /usr/share/grafana/public/build/css
```
### style.css Dosyasını Oluşturma

Sonra, style.css adlı bir dosya oluşturun. Aşağıdaki komut ile style.css dosyasını oluşturabilir ve düzenleyebilirsiniz:
```bash
nano /usr/share/grafana/public/build/css/style.css
```
```CSS

body.login-page footer{
  /*footerı görünmez yapar*/
  display:none!important;

}
@media only screen and (min-width: 544px) {
body.login-page .css-1px3c36{
/*Login sayfasındaki logunun büyüklüğü istediğiniz gibi oynayabilirisiniz.*/
  max-width:150px!important;
}

}
```

#### ***CSS*** dosyasını oluşturduktan sonra, oluşturduğunuz ***style.css*** dosyasını ***/usr/share/grafana/public/views/index.html*** dosyasına eklemek için şu adımları izleyebilirsiniz:


```bash
nano /usr/share/grafana/public/views/index.html
```
Dosyanın ```<head>``` kısmına aşağıdaki satırı ekleyin:
```html
  <link rel="stylesheet" href="/public/build/css/style.css">
```
Bu satır, oluşturduğunuz style.css dosyasını HTML dosyasına dahil eder.
 
