# ORYVEX CORE DATA MODEL V1
## CAMİ PRO + ŞANTİYE OS Ortak Çekirdeği

Bu doküman iki ürünün aynı saha veri dilini kullanmasını zorunlu kılar.

## Ortak ana nesneler
- Organization
- Project
- ProjectMember
- WorkPackage
- ProjectPoz
- ProjectMahal
- Person
- Certificate
- Crew
- CrewMember
- Subcontractor
- Equipment
- Material
- Supplier
- PurchaseOrder
- StockMovement
- DailyLog
- ProgressRecord
- ProgressPayment
- Invoice
- Collection
- CostEntry
- CashMovement
- Risk
- Notification
- Document
- DocumentReview
- OfficialRecord
- AuditLog

## Ortak ID kuralı
Aynı işin CAMİ PRO ve ŞANTİYE OS tarafında ikinci bir kimliği oluşturulmaz. Project ID ve WorkPackage ID temel çapraz referanstır.

## Ortak durum zincirleri

### Tedarik
Teklif Bekliyor → Bağlantı Yapıldı → Kapora Ödendi → Üretimde → Sevkte → Şantiyede → Tamamlandı

### İmalat
Planlandı → Başladı → Devam Ediyor → Tamamlandı → Kontrol Edildi → Kabul Edildi → Hakedişe Uygun

### Hakediş
Hakedişe Hazır → Kontrol Bekliyor → Hakedişe Alındı → Onaylandı → Faturalandı → Tahsil Edildi

### Resmî kayıt
Hazırlanıyor → Eksik Veri → Kontrol Bekliyor → Aktarıma Hazır → Kullanıcı Tarafından Aktarıldı → Doğrulandı → Hata/Tekrar

## Ürün ayrımı
CAMİ PRO cami mimarisi, tezyinat, stok cami projeleri, tasarım kütüphanesi ve camiye özel metraj/poz bilgisini genişletir.

ŞANTİYE OS genel inşaat operasyonu, farklı yapı türleri ve saha yönetimini genişletir.

Ortak çekirdek alan adları değiştirilmez. Ürüne özel alanlar çekirdek tabloları bozmak yerine ek tablo/extension mantığıyla eklenir.

## Senkronizasyon ilkesi
ORYVEX merkezi ileride iki sistem arasında olay/veri senkronizasyonu kurarsa aşağıdaki ana event adları kullanılır:
- project.created
- work_package.created
- purchase_order.updated
- stock.moved
- daily_log.created
- progress.accepted
- progress_payment.approved
- invoice.issued
- collection.received
- risk.created
- official_record.ready

## Güvenlik
Her ürün organization/project membership ve RLS üzerinden erişim verir. Bir firmanın proje, tedarikçi, taşeron, finans veya doküman verisi diğer firmaya açılmaz.

## Ana kural
**Veri bir kez girilir; plan, saha, tedarik, hakediş, finans ve resmî kayıt aynı veriden beslenir.**