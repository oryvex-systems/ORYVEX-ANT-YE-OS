# ORYVEX ŞANTİYE OS

İnşaat firmaları için proje, saha, maliyet, satın alma, depo, taşeron, hakediş ve yapay zekâ destekli şantiye yönetim sistemi.

Canlı alan adı: `revakhali.info`

Kaynak senkronizasyonu ORYVEX ana deposundaki `apps/oryvex-revakhali/` dizininden GitHub Actions ile yapılır.

Yayın: GitHub Pages (`gh-pages`).

Son senkronizasyon tetiklemesi: Resmi Süreç Merkezi, gelişmiş Dijital Şantiye Defteri ve mahal bazlı imalat ilerleme modülü devreye alındı. Şantiye-M, YDS/UYDS ve yetki belgesi süreç takibi; hava, mahal, saha ilerlemesi, teknik personel, fiili işçi, makine-teçhizat, görüşme/karar, ziyaret, güvenlik ve fotoğraf alanları Supabase veri modeline eklendi. Blok/kat/bölüm/mahal seviyesinde planlanan, önceki, bugünkü ve kümülatif imalat miktarı ile ilerleme yüzdesi tutuluyor. Resmi API doğrulanmadan otomatik Bakanlık gönderimi yapılmaz; resmi sisteme geçiş ve dışa aktarılabilir kayıt mantığı esas alınır. Misafir test modu geçici olarak aktiftir.