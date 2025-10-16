. SİSTEM BAŞLAT
. Kullanıcı arayüzünü aç
. Ekrana “Hastane Randevu Sistemine Hoş Geldiniz” mesajı yazdır

. KULLANICI GİRİŞİ
. Eğer kullanıcı daha önce kayıtlıysa:
    .. Kullanıcıdan TC Kimlik No ve Şifre iste
    .. Şifre doğrula
    .. Eğer doğrulama başarısızsa:
        ... Hata mesajı göster: “Hatalı giriş bilgileri”
        ... 3 kez yanlış girilirse hesabı geçici olarak kilitle
        ... Ana ekrana dön
    .. Eğer doğrulama başarılıysa → Ana menüye geç
. Aksi halde (yeni kullanıcı):
    .. “Yeni Kayıt Oluştur” ekranını aç
    .. Ad, Soyad, TC Kimlik No, Telefon, E-posta, Şifre bilgilerini al
    .. Bilgileri doğrula (zorunlu alanlar, TC kimlik formatı vb.)
    .. Kullanıcıyı veritabanına kaydet
    .. Kayıt başarılı mesajı göster
    .. Ana menüye yönlendir

-----------------------------------------------------
. ANA MENÜ
. Ekranda seçenekleri göster:
    [1] Randevu Al
    [2] Randevu Görüntüle / İptal Et
    [3] Kişisel Bilgileri Güncelle
    [4] Çıkış

. Kullanıcının seçimini al
. Eğer seçim == 1 → RandevuAlProsedürü
. Eğer seçim == 2 → RandevuSorgulaProsedürü
. Eğer seçim == 3 → BilgiGuncelleProsedürü
. Eğer seçim == 4 → ÇıkışYap
. Aksi halde → “Geçersiz seçim” uyarısı göster, ana menüye dön

-----------------------------------------------------
. RANDEVU AL PROSEDÜRÜ
. Kullanıcıdan şehir seçmesini iste
. Kullanıcıdan hastane seçmesini iste
. Kullanıcıdan poliklinik (ör. Dahiliye, Göz, Kardiyoloji) seçmesini iste
. Seçilen polikliniğe ait doktor listesini getir
. Kullanıcıdan doktor seçmesini iste
. Seçilen doktorun uygun randevu tarih ve saatlerini göster
. Kullanıcıdan tarih ve saat seçmesini iste

. Kontroller:
    .. Eğer seçilen saat doluysa:
        ... Uyarı: “Seçilen saat dolu. Lütfen başka bir zaman seçiniz.”
        ... Tekrar seçim ekranına dön
    .. Eğer seçilen tarih geçmiş bir tarihse:
        ... Hata mesajı: “Geçmiş bir tarih seçilemez.”
        ... Tekrar seçim ekranına dön

. RandevuKaydet():
    .. Randevuyu veritabanına kaydet (KullanıcıID, DoktorID, Tarih, Saat)
    .. Kullanıcıya onay mesajı göster:
       “Randevunuz başarıyla oluşturuldu.”
    .. İsteğe bağlı olarak e-posta / SMS gönder:
       “Randevunuz [Tarih - Saat] tarihinde [Doktor Adı] ile onaylanmıştır.”

. Ana menüye dön

-----------------------------------------------------
. RANDEVU SORGULA / İPTAL PROSEDÜRÜ
. Kullanıcının mevcut randevularını veritabanından getir
. Randevular listelenir:
    (Tarih - Saat - Doktor - Poliklinik)
. Kullanıcıya seçenek göster:
    [1] Randevuyu İptal Et
    [2] Ana Menüye Dön

. Eğer kullanıcı [1] seçerse:
    .. İptal etmek istediği randevunun numarasını sor
    .. Randevuyu veritabanından sil
    .. “Randevu başarıyla iptal edildi.” mesajı göster
. Eğer [2] seçerse → Ana menüye dön

-----------------------------------------------------
. BİLGİ GÜNCELLE PROSEDÜRÜ
. Kullanıcı mevcut bilgilerini görüntüler
. Güncellemek istediği alanları (telefon, e-posta vb.) seçer
. Yeni bilgileri girer
. Doğrulama yapılır (ör. e-posta formatı, boş alan kontrolü)
. Güncellenen bilgiler veritabanına kaydedilir
. “Bilgileriniz başarıyla güncellendi.” mesajı göster
. Ana menüye dön

-----------------------------------------------------
. ÇIKIŞ YAP
. “Sistemden çıkmak istediğinize emin misiniz?” mesajı göster
. Onay verilirse oturumu kapat
. “Çıkış yapıldı.” mesajı yazdır
. SİSTEMİ SONLANDIR

-----------------------------------------------------
. HATA DURUMLARI
. Eğer sistem bağlantı hatası alırsa:
    .. “Sunucuya erişilemedi. Lütfen daha sonra tekrar deneyiniz.” mesajı göster
. Eğer veritabanı hatası oluşursa:
    .. “Randevu işlemi sırasında hata oluştu.” mesajı göster
. Hatalar log dosyasına kaydedilir (tarih, kullanıcı, hata tipi)

-----------------------------------------------------
. SİSTEM SONU
. Tüm geçici oturum verilerini temizle
. Oturumu kapat
. Programı sonlandır
