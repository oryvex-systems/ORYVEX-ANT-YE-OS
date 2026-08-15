# ORYVEX STANDARDI 003
## Saha, Şantiye-M ve Resmî Entegrasyon Standardı
### CAMİ PRO + ŞANTİYE OS Ortak Çekirdek

## 1. Ana ilke

**Veri bir kez girilir, her yerde kullanılır.**

CAMİ PRO ve ŞANTİYE OS aynı saha veri modelini kullanır. Günlük şantiye kaydı, personel, ekipman, imalat, tedarik, stok, hakediş, finans ve resmî kayıt süreçleri birbirinden kopuk tutulmaz.

Sistem zinciri:

PLAN → GÜNLÜK SAHA → PERSONEL / USTA → EKİPMAN → MALZEME → İMALAT → KONTROL → HAKEDİŞ → TAHSİLAT → RESMÎ KAYIT / AKTARIM

## 2. Ortak veri kimlikleri

Her projede aşağıdaki temel kimlikler zorunludur:
- Project ID
- Site ID / Şantiye ID
- Work Package ID
- Poz ID
- Mahal ID
- Person ID
- Usta / Yetki Belgesi ID
- Equipment ID
- Material ID
- Supplier ID
- Purchase Order ID
- Daily Log ID
- Progress Record ID
- Hakediş ID
- Payment / Tahsilat ID
- Official Transfer Record ID

Aynı veri CAMİ PRO ve ŞANTİYE OS arasında yeniden oluşturulmaz; ortak ID ile ilişkilendirilir.

## 3. Günlük şantiye kaydı standardı

Her günlük saha kaydında en az:
- Tarih
- Şantiye
- Şantiye şefi
- Hava / çalışma koşulları
- Yapılan faaliyet
- İş paketi / poz
- Mahal
- Planlanan miktar
- Gerçekleşen miktar
- Birim
- Çalışan personel / usta
- Alt işveren / ekip
- Kullanılan ekipman
- Kullanılan malzeme
- Fotoğraf / belge
- İş güvenliği notu
- Sorun / gecikme
- Teknik açıklama
- Kontrol / onay durumu
- Resmî kayıt aktarım durumu
alanları bulunur.

## 4. Personel ve yetkili usta standardı

Her personel/usta kaydında:
- Ad soyad
- Kimlik / sistem içi ID
- Meslek
- Yetki / belge türü
- Belge numarası
- Belge geçerlilik durumu
- İşveren / taşeron
- Şantiye
- İşe başlama tarihi
- İşten ayrılma tarihi
- Atandığı iş paketleri
- Günlük faaliyet bağlantıları
- Eksik belge / risk durumu
bulunur.

AI, planlanan iş için gerekli nitelikli/yetkili ekip atanmadığında uyarı verir.

## 5. Ekipman standardı

Her ekipman için:
- Ekipman ID
- Tür
- Marka / model
- Kapasite
- Operatör
- Belge / periyodik kontrol
- Şantiye
- Kullanıldığı iş paketi
- Günlük çalışma süresi
- Arıza / bakım durumu
- Aynı zamandaki diğer atamalar
izlenir.

AI kaynak çakışmasını kontrol eder.

## 6. Malzeme ve tedarik standardı

Her malzeme hareketi şu zincire bağlanır:
İhtiyaç → Talep → Teklif → Sipariş → Kapora/Avans → Üretim → Sevk → Şantiye Girişi → Stok → Sarf → İmalat

Her malzeme için:
- Malzeme ID
- Poz / iş paketi
- İhtiyaç tarihi
- Gerekli miktar
- Sipariş miktarı
- Gelen miktar
- Kullanılan miktar
- Stok
- Fire
- Tedarikçi
- Termin
- Son sipariş tarihi
- Ödeme planı
- Kapora
- Kalan ödeme
- Sevkiyat
- Kabul
alanları tutulur.

## 7. İmalat gerçekleşme standardı

Gerçekleşme ayrı bir olay kaydıdır.

Durum zinciri:
Planlandı → Başladı → Devam Ediyor → Tamamlandı → Kontrol Edildi → Kabul Edildi → Hakedişe Uygun

Her gerçekleşme kaydı günlük saha kaydına, iş paketine, personele, ekipmana ve malzeme sarfına bağlıdır.

## 8. Hakedişe dönüş standardı

Hakediş yalnız uygun gerçekleşmeden üretilir.

Aşağıdakiler ayrı tutulur:
- Yapılan miktar
- Kontrol edilen miktar
- Kabul edilen miktar
- Hakedişe uygun miktar
- Hakedişe giren miktar
- Onaylanan miktar
- Faturalanan tutar
- Tahsil edilen tutar

Poz bazında farklı hakediş kuralları tanımlanabilir.

## 9. Finans standardı

Her saha hareketinin finansal etkisi hesaplanır.

Takip edilir:
- Avans
- Kapora
- Tedarikçi ödemesi
- İşçilik
- Taşeron ödemesi
- Genel gider
- Hakediş
- Kesinti
- Avans mahsup
- Fatura
- Tahsilat
- Finansman açığı

30 / 60 / 90 günlük nakit görünümü zorunludur.

## 10. Şantiye-M / resmî kayıt köprüsü

CAMİ PRO ve ŞANTİYE OS doğrudan kamu sistemi API'si varmış gibi davranmaz.

Üç katmanlı yaklaşım kullanılır:

### Katman A — Resmî kayda hazır veri
Sistem resmî süreçlerde ihtiyaç duyulabilecek saha, personel, ekipman ve günlük faaliyet verilerini yapılandırılmış biçimde toplar.

### Katman B — Aktarım / kontrol merkezi
Kayıtlar şu durumlarla izlenir:
- Hazırlanıyor
- Eksik veri
- Kontrol bekliyor
- Aktarıma hazır
- Kullanıcı tarafından aktarıldı
- Doğrulandı
- Hata / tekrar gerekli

### Katman C — Resmî entegrasyon konektörü
Yetkili API, web servis veya resmî entegrasyon yöntemi sağlanırsa yalnız Connector katmanı değiştirilir. Ana CAMİ PRO / ŞANTİYE OS veri modeli değişmez.

## 11. AI kontrol motoru

AI şu kontrolleri yapar:
- Ön iş tamamlanmadan faaliyet başlangıcı
- Aynı mahalde fiziksel çakışma
- Aynı ekip / makine çift atama
- Yetkisiz / eksik belgeli usta riski
- Malzeme yetişmeme riski
- Stok açığı
- Finansman açığı
- Günlük kayıt eksikliği
- Tamamlanan ancak hakedişe dönüşmeyen iş
- Hakediş onay gecikmesi
- Resmî kayıt aktarım eksikliği
- Kritik yol ve teslim tarihi etkisi

AI kritik kararı otomatik uygulamaz; öneri + gerekçe + etki üretir.

## 12. 30 / 60 / 90 günlük görünüm

### 30 gün
- Kesin saha faaliyetleri
- Personel / usta ihtiyacı
- Günlük kayıt yükümlülükleri
- Kesin ödemeler

### 60 gün
- Satın alma
- Tedarik
- Ekip / ekipman
- Finans hazırlığı

### 90 gün
- Uzun terminli ürünler
- Kritik taşeronlar
- Belge / izin riskleri
- Stratejik finans riski

## 13. CAMİ PRO ve ŞANTİYE OS görev ayrımı

### CAMİ PRO
Cami projelerine özel teknik, mimari, tezyinat, metraj, proje ve uygulama kararlarını derinleştirir.

### ŞANTİYE OS
Genel inşaat projelerinde saha operasyonu, ekip, günlük kayıt, görev, tedarik, gerçekleşme ve resmî kayıt süreçlerini merkezileştirir.

### Ortak çekirdek
- İş paketi
- Günlük saha
- Personel / usta
- Ekipman
- Malzeme
- Satın alma
- Gerçekleşme
- Hakediş
- Finans
- Risk
- Resmî kayıt durumu

## 14. Değişiklik ve versiyonlama

Bu standart yaşayan dokümandır. Mevzuat veya resmî sistem değiştiğinde önce entegrasyon katmanı gözden geçirilir. Ana saha veri modeli mümkün olduğunca korunur.

Her revizyon sürüm numarası ve tarih ile kaydedilir.

## 15. Ana sistem cümlesi

**Veri bir kez girilir. Plan, saha, tedarik, hakediş, finans ve resmî kayıt aynı veriden beslenir.**

**İnsan sahayı yönetir; AI bağlantıları kontrol eder; sistem kayıt kaybını ve geç fark edilen riski önler.**