Öğrenci Ad-Soyad: BEray Akar
Öğrenci No: 250541019

````
PROSEDÜR E_TICARET_ISLEMI()
    // 1. Giriş Kontrolü
    EĞER KULLANICI_GIRIS_YAPMADI() İSE
        YAZDIR("Lütfen giriş yapınız.")
        GIRIS_YAP()
    DEĞİLSE
        YAZDIR("Hoş geldiniz!")
    SON_EĞER
    
    // Değişken Tanımlamaları
    ÜRÜN_KATEGORİLERİ = ["Elektronik", "Giyim", "Ev", "Kozmetik"]
    SEPET = BOS_LISTE()
    DEVAM_ET = DOĞRU
    
    // 2. Ürün Seçme ve Sepete Ekleme Döngüsü
    TEKRARLA
        // Kategorilerde Gezinme
        YAZDIR("Lütfen bir kategori seçin:")
        HER kategori İÇİN ÜRÜN_KATEGORİLERİ
            YAZDIR("- " & kategori)
        SON_HER
        
        SECILEN_KATEGORI = KULLANICIDAN_GIRIS_AL()
        SECILEN_URUN = URUN_SEC(SECILEN_KATEGORI)
        
        YAZDIR(SECILEN_URUN & " adlı ürünü sepete eklemek ister misiniz? (Evet/Hayır)")
        CEVAP = KULLANICIDAN_GIRIS_AL()
        
        EĞER CEVAP EŞİTTİR "Evet" İSE
            // Stok Kontrolü
            EĞER STOK_KONTROL_ET(SECILEN_URUN) İSE
                SEPETE_EKLE(SEPET, SECILEN_URUN)
                YAZDIR("Ürün sepete eklendi.")
            DEĞİLSE
                YAZDIR("Ürün stokta yok. Üzgünüz.")
            SON_EĞER
        DEĞİLSE
            YAZDIR("Ürün eklenmedi.")
        SON_EĞER
        
        YAZDIR("Başka bir ürün eklemek ister misiniz? (Evet/Hayır)")
        DEVAM_CEVAP = KULLANICIDAN_GIRIS_AL()
        
        EĞER DEVAM_CEVAP EŞİTTİR "Hayır" İSE
            DEVAM_ET = YANLIŞ
        SON_EĞER
        
    KADAR DEVAM_ET EŞİTTİR YANLIŞ
    
    // 3. Sepeti Görüntüleme ve Düzenleme
    TEKRARLA
        SEPETI_GOSTER(SEPET)
        YAZDIR("Sepetten ürün silmek ister misiniz? (Evet/Hayır)")
        SILME_CEVAP = KULLANICIDAN_GIRIS_AL()
        
        EĞER SILME_CEVAP EŞİTTİR "Evet" İSE
            YAZDIR("Lütfen silinecek ürünün adını/ID'sini girin:")
            SILINECEK_URUN = KULLANICIDAN_GIRIS_AL()
            SEPETTEN_SIL(SEPET, SILINECEK_URUN)
        SON_EĞER
        
    KADAR SILME_CEVAP EŞİTTİR "Hayır"
    
    // 4. İndirim Kodu Uygulama
    YAZDIR("İndirim kodunuz var mı? (Evet/Hayır)")
    KOD_CEVAP = KULLANICIDAN_GIRIS_AL()
    
    EĞER KOD_CEVAP EŞİTTİR "Evet" İSE
        YAZDIR("Lütfen indirim kodunuzu girin:")
        KOD = KULLANICIDAN_GIRIS_AL()
        
        EĞER KOD_GECERLI_MI(KOD) İSE
            INDİRİM_UYGULA(SEPET, KOD)
            YAZDIR("İndirim başarıyla uygulandı.")
        DEĞİLSE
            YAZDIR("Girilen kod geçersiz.")
        SON_EĞER
    SON_EĞER
    
    // 5. Ödeme Kontrolleri ve Hesaplama
    TOPLAM_TUTAR = SEPET_TUTARI_HESAPLA(SEPET)
    
    // Minimum Tutar Kontrolü
    EĞER TOPLAM_TUTAR < 50.00 İSE
        YAZDIR("Sepet tutarı 50.00 TL altında. Alışverişe devam edilemez.")
        CIKIS() // İşlemi sonlandır
    SON_EĞER
    
    YAZDIR("Sepet geçerli. Ödeme aşamasına geçiliyor.")
    
    // Kargo Ücreti Hesaplama
    EĞER TOPLAM_TUTAR >= 200.00 İSE
        KARGO_UCRETI = 0.00
        YAZDIR("Kargo ücretsiz!")
    DEĞİLSE
        KARGO_UCRETI = 29.99
        YAZDIR("Kargo ücreti: " & KARGO_UCRETI & " TL.")
    SON_EĞER
    
    // Genel Toplamı Hesaplama ve Gösterme
    GENEL_TOPLAM = TOPLAM_TUTAR + KARGO_UCRETI
    YAZDIR("Ödenecek Toplam Tutar: " & GENEL_TOPLAM & " TL")
    
    // 6. Sonlandırma
    YAZDIR("Alışveriş tamamlandı. Teşekkür ederiz!")
    
SON_PROSEDÜR
```   
