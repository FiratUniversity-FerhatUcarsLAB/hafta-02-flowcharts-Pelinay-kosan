İsim - Soy isim :Pelinay KOŞAN
Öğrenci No:250542002

sistemin kısa açıklaması (maks. 5-6 satır)
 ATM Para Çekme Sistemini pseudocode ile sistem adımlarını sözde kodlanmış şekilde yazınız
 // ATM PARA ÇEKME SİSTEMİ TEMEL ADIMLARI

FONKSİYON ParaCekmeIslemi()
BAŞLA

    YAZDIR("Lütfen kartınızı yerleştiriniz.")
    KART_YERLEŞTİR = KartOku()

    EĞER KART_YERLEŞTİR BAŞARILI İSE
        KART_TİPİ = KartBilgisiAl(KART_YERLEŞTİR)
        YAZDIR("Lütfen şifrenizi giriniz.")
        ŞİFRE = KullanıcıGirdisiAl()

        // Şifre Doğrulama
        EĞER ŞifreDoğruMu(KART_TİPİ, ŞİFRE) İSE
            DOĞRULAMA_GİRİŞİMİ = 1
            DÖNGÜ ŞİFRE_GİRİŞİ ÜÇ DEFA İLE SINIRLI
                EĞER ŞifreDoğruMu(KART_TİPİ, ŞİFRE) İSE
                    KIR (Döngüyü)
                DEĞİLSE
                    DOĞRULAMA_GİRİŞİMİ = DOĞRULAMA_GİRİŞİMİ + 1
                    EĞER DOĞRULAMA_GİRİŞİMİ > 3 İSE
                        YAZDIR("Çok fazla hatalı şifre girişi. Kart alıkonuldu.")
                        KartAlıkoy()
                        ÇIK (İşlemden)
                    DEĞİLSE
                        YAZDIR("Hatalı şifre. Lütfen tekrar deneyiniz. Kalan deneme: " + (4 - DOĞRULAMA_GİRİŞİMİ))
                        ŞİFRE = KullanıcıGirdisiAl()
                    SON_EĞER
                SON_EĞER
            SON_DÖNGÜ

            // Hesap Seçimi (Birden fazla hesap varsa)
            HESAP_LİSTESİ = HesaplarıGetir(KART_TİPİ)
            EĞER HesapSayısı(HESAP_LİSTESİ) > 1 İSE
                YAZDIR("Lütfen işlem yapmak istediğiniz hesabı seçiniz (Örn: Vadesiz, Tasarruf).")
                SEÇİLEN_HESAP = KullanıcıSeçimiAl(HESAP_LİSTESİ)
            DEĞİLSE
                SEÇİLEN_HESAP = HESAP_LİSTESİ[0] // Tek hesabı seç
            SON_EĞER

            // Çekilecek Miktarın Girilmesi
            YAZDIR("Lütfen çekmek istediğiniz miktarı giriniz.")
            İSTENEN_MİKTAR = KullanıcıGirdisiAl()

            // Kontroller
            GÜNCEL_BAKİYE = HesapBakiyesiSorgula(SEÇİLEN_HESAP)
            ATM_PARA_STOK = ATMStokKontrol()

            EĞER İSTENEN_MİKTAR > 0 VE İstenenMiktarKatlarıUygunMu(İSTENEN_MİKTAR) İSE
                EĞER İSTENEN_MİKTAR <= GÜNCEL_BAKİYE İSE
                    EĞER İSTENEN_MİKTAR <= ATM_PARA_STOK İSE

                        // Para Transferi ve Kayıt
                        İŞLEM_BAŞARILI = ParaTransferi(SEÇİLEN_HESAP, İSTENEN_MİKTAR, "Çekim") // Bankaya yetkilendirme gönder
                        EĞER İŞLEM_BAŞARILI İSE
                            YAZDIR("İşleminiz gerçekleştiriliyor. Lütfen bekleyiniz.")
                            ParaDağıt(İSTENEN_MİKTAR)
                            YAZDIR("Lütfen paranızı alınız.")
                            YAZDIR("Lütfen kartınızı alınız.")
                            KartİadeEt()
                            FişYazdır(SEÇİLEN_HESAP, İSTENEN_MİKTAR, "BAŞARILI")
                        DEĞİLSE
                            YAZDIR("Banka onayı alınamadı veya işlem başarısız oldu. Kartınız iade ediliyor.")
                            KartİadeEt()
                            FişYazdır(SEÇİLEN_HESAP, İSTENEN_MİKTAR, "BAŞARISIZ_BANKA")
                        SON_EĞER

                    DEĞİLSE
                        YAZDIR("ATM'de yeterli para stoğu bulunmamaktadır. Lütfen daha düşük bir miktar giriniz veya başka bir ATM'yi deneyiniz.")
                        KartİadeEt()
                        FişYazdır(SEÇİLEN_HESAP, İSTENEN_MİKTAR, "BAŞARISIZ_STOK")
                    SON_EĞER
                DEĞİLSE
                    YAZDIR("Hesabınızda yeterli bakiye bulunmamaktadır. Kartınız iade ediliyor.")
                    KartİadeEt()
                    FişYazdır(SEÇİLEN_HESAP, İSTENEN_MİKTAR, "BAŞARISIZ_BAKİYE")
                SON_EĞER
            DEĞİLSE
                YAZDIR("Girilen miktar geçersiz. Kartınız iade ediliyor.")
                KartİadeEt()
                FişYazdır(SEÇİLEN_HESAP, İSTENEN_MİKTAR, "BAŞARISIZ_MİKTAR_HATASI")
            SON_EĞER

        DEĞİLSE
            // (Şifre denemesi zaten döngü içinde yapıldı. Buraya düşülmez, döngü sonu kontrolü esas alınır.)
            BOŞ_ADIM()
        SON_EĞER

    DEĞİLSE
        YAZDIR("Kart okuma hatası veya kart geçersiz. İşlem sonlandırılıyor.")
        // Kart iade edilmeye çalışılır, edilemezse hata mesajı verilir.
        KartİadeEt()
    SON_EĞER

SON_FONKSİYON
