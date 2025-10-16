Öğrenci Ad-Soyad: Beray Akar
Öğrenci No: 250541019

PROSEDÜR ParaCekmeIslemi()
    // Adım 1: Kartın Takılması ve Doğrulama
    EKRAN_GOSTER("Lütfen kartınızı takınız.")
    KART_OKU()
    
    EĞER KartGecerli() İSE
        EKRAN_GOSTER("Lütfen PIN'inizi giriniz.")
        PIN_GIRISI = KULLANICIDAN_AL()
        
        EĞER PIN_DOGRU_MU(PIN_GIRISI) İSE
            // Adım 2: İşlem Seçimi ve Miktar Girişi
            EKRAN_GOSTER("Yapmak istediğiniz işlemi seçin: 1-Para Çekme, 2-Bakiye Sorgulama, ...")
            ISLEM_SECIMI = KULLANICIDAN_AL()
            
            EĞER ISLEM_SECIMI EŞİTTİR 1 İSE
                EKRAN_GOSTER("Lütfen çekmek istediğiniz miktarı giriniz.")
                CEKILECEK_MIKTAR = KULLANICIDAN_AL()
                
                // Adım 3: Kontroller
                EĞER CEKILECEK_MIKTAR > KART_BAKIYESI İSE
                    EKRAN_GOSTER("Yetersiz bakiye. Lütfen farklı bir miktar giriniz.")
                
                AKSİ TAKDİRDE EĞER CEKILECEK_MIKTAR > ATM_KASASI_NAKDİ İSE
                    EKRAN_GOSTER("ATM'de yeterli nakit yok. Lütfen farklı bir miktar giriniz.")
                    
                AKSİ TAKDİRDE
                    // Adım 4: İşlemi Gerçekleştirme
                    
                    // Banka sistemine bakiye güncelleme talebi gönder
                    YENI_BAKIYE = KART_BAKIYESI - CEKILECEK_MIKTAR
                    BAKIYE_GUNCELLE(YENI_BAKIYE)
                    
                    // ATM nakit miktarını güncelle
                    ATM_KASASI_NAKDİ = ATM_KASASI_NAKDİ - CEKILECEK_MIKTAR
                    
                    // Adım 5: Para ve Kartı Teslim Etme
                    PARA_VER(CEKILECEK_MIKTAR)
                    EKRAN_GOSTER(CEKILECEK_MIKTAR & " TL teslim edildi. Lütfen paranızı alınız.")
                    
                    KART_CIKAR()
                    EKRAN_GOSTER("Lütfen kartınızı alınız.")
                    
                    // Adım 6: Makbuz
                    EĞER KULLANICI_MAKBUZ_ISTIYOR_ISE
                        MAKBUZ_BAS("İşlem Başarılı. Miktar: " & CEKILECEK_MIKTAR & " TL. Yeni Bakiye: " & YENI_BAKIYE & " TL.")
                    
                    EKRAN_GOSTER("İşleminiz tamamlanmıştır. Teşekkür ederiz.")
                SON_EĞER // Miktar Kontrolleri
            
            SON_EĞER // İşlem Seçimi
            
        AKSİ TAKDİRDE
            EKRAN_GOSTER("Hatalı PIN. İşlem iptal edildi.")
            KART_CIKAR()
        SON_EĞER // PIN Doğrulama
        
    AKSİ TAKDİRDE
        EKRAN_GOSTER("Kart geçersiz veya okunamadı. Lütfen kartınızı alınız.")
    SON_EĞER // Kart Geçerliliği
    
SON_PROSEDÜR
