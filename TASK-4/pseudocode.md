. SİSTEM BAŞLAT
. “Üniversite Ders Kayıt Sistemine Hoş Geldiniz” mesajını göster
. Kullanıcı girişi ekranını aç

-----------------------------------------------------
. KULLANICI GİRİŞİ
. Kullanıcıdan Öğrenci No ve Şifre al
. Şifre doğrula
. Eğer giriş başarısızsa:
    .. Hata mesajı göster: “Hatalı giriş bilgisi”
    .. Tekrar denemek istiyor mu?
        ... Evet → tekrar giriş ekranına dön
        ... Hayır → sistemi sonlandır
. Eğer giriş başarılıysa:
    .. Öğrenci bilgilerini veritabanından getir (Ad, Fakülte, Bölüm, Dönem, Danışman)
    .. Ana menüye yönlendir

-----------------------------------------------------
. ANA MENÜ
. Ekranda şu seçenekleri göster:
    [1] Ders Kaydı Yap
    [2] Kayıtlı Dersleri Görüntüle / Sil
    [3] Transkript Görüntüle
    [4] Şifre Değiştir
    [5] Çıkış

. Kullanıcının seçimini al
. Eğer seçim == 1 → DersKaydiProsedürü
. Eğer seçim == 2 → DersSorgulaProsedürü
. Eğer seçim == 3 → TranskriptProsedürü
. Eğer seçim == 4 → SifreDegistirProsedürü
. Eğer seçim == 5 → CikisYap
. Aksi halde → “Geçersiz seçim” uyarısı göster ve ana menüye dön

-----------------------------------------------------
. DERS KAYDI PROSEDÜRÜ
. Öğrencinin aktif dönemi (örneğin 2025 Bahar) sistemden alınır
. Bu döneme ait açılmış dersleri veritabanından listele:
    (Ders Kodu, Ders Adı, Kredisi, Kontenjan, Ön Koşul, Gün/Saat)
. Ekranda “Ders Seçimi” arayüzünü göster

. Öğrenciden almak istediği dersi seçmesini iste
. Seçilen dersi kontrol et:
    .. Ön koşul dersi geçmiş mi?
        ... Hayır → Hata: “Ön koşul dersi alınmamış.”
        ... Evet → devam et
    .. Dersin kontenjanı dolu mu?
        ... Evet → “Kontenjan dolu.” mesajı göster
        ... Hayır → devam et
    .. Aynı gün ve saatte başka dersi var mı?
        ... Evet → “Ders çakışması var.” uyarısı göster
        ... Hayır → ekle

. Ders başarıyla eklendiyse:
    .. Ders öğrencinin kayıt listesine eklenir
    .. “Ders başarıyla eklendi.” mesajı göster
. Öğrenci başka ders eklemek istiyor mu?
    .. Evet → ders listesine dön
    .. Hayır → ders onay sürecine geç

. Onay ekranı:
    .. Seçilen dersleri listele (kod, ad, kredi)
    .. Toplam kredi hesapla
    .. Eğer toplam kredi > maxKredi:
        ... Uyarı: “Kredi limiti aşıldı.”
        ... Ders çıkar veya onay iptal et
    .. Eğer toplam kredi < minKredi:
        ... Uyarı: “Kredi limiti altında.”
        ... Devam etmek istiyor musun?
    .. Onayla seçeneğiyle kayıt kesinleşir
    .. Danışman onayına gönder (eğer sistemde zorunluysa)
    .. “Ders kaydınız başarıyla oluşturuldu.” mesajı göster

. Ana menüye dön

-----------------------------------------------------
. DERS SORGULAMA / SİLME PROSEDÜRÜ
. Öğrencinin mevcut dönemdeki ders kayıtlarını listele
. Kullanıcıya seçenek sun:
    [1] Belirli bir dersi sil
    [2] Ana menüye dön
. Eğer [1] seçilirse:
    .. Silmek istediği dersin kodunu sor
    .. Ders kaydını veritabanından sil
    .. “Ders kaydı silindi.” mesajı göster
. Ana menüye dön

-----------------------------------------------------
. TRANSKRİPT GÖRÜNTÜLE PROSEDÜRÜ
. Öğrencinin tüm geçmiş dönem notlarını getir
. Her ders için (Ders Adı, Kredi, Harf Notu, Dönem) bilgilerini listele
. Genel Not Ortalamasını (GANO) hesapla
. Ekrana yazdır: “Genel Ortalama: [GANO]”
. Ana menüye dön

-----------------------------------------------------
. ŞİFRE DEĞİŞTİR PROSEDÜRÜ
. Kullanıcıdan mevcut şifreyi iste
. Yeni şifreyi iki kez gir
. Eğer şifreler eşleşmiyorsa:
    .. “Şifreler uyuşmuyor.” mesajı göster
    .. Tekrar dene
. Eşleşiyorsa:
    .. Veritabanında şifreyi güncelle
    .. “Şifre başarıyla değiştirildi.” mesajı göster
. Ana menüye dön

-----------------------------------------------------
. ÇIKIŞ YAP
. “Sistemden çıkmak istiyor musunuz?” mesajı göster
. Onay verilirse oturumu sonlandır
. Oturum verilerini temizle
. “Çıkış yapıldı.” mesajı göster
. SİSTEM SONLANDIR

-----------------------------------------------------
. HATA YÖNETİMİ
. Eğer bağlantı hatası olursa:
    .. “Sunucuya bağlanılamıyor. Lütfen tekrar deneyin.” mesajı göster
. Eğer veritabanı hatası olursa:
    .. “Kayıt işlemi başarısız oldu.” mesajı göster
. Hata bilgilerini log dosyasına kaydet (zaman, kullanıcı, hata türü)

-----------------------------------------------------
. SİSTEM SONU
. Oturumu kapat
. Tüm geçici verileri sil
. Programı kapat
