Örenci Ad-Soayd: Beray Akar
Örenci No: 250541019

BAŞLA

// Hasta kimlik doğrulama
TC_NO = kullanıcı_girdisi("TC Kimlik Numaranızı giriniz: ")
EĞER TC_NO geçerli değilse
    "Geçersiz TC Kimlik Numarası!" yazdır
    DUR
DEĞİLSE
    "Giriş başarılı." yazdır

TEKRARLA
    "İşlem Seçiniz:"
    "1 - Randevu Al"
    "2 - Tahlil Sonucu Gör"
    SECIM = kullanıcı_girdisi()

    EĞER SECIM == 1 ise
        // Randevu Modülü
        POLIKLINIK_LISTESI = ["Dahiliye", "Kardiyoloji", "Ortopedi", "Cildiye"]
        HER poliklinik İÇİN POLIKLINIK_LISTESI
            poliklinik yazdır
        SECILEN_POLIKLINIK = kullanıcı_girdisi("Poliklinik seçiniz: ")

        DOKTOR_LISTESI = doktor_getir(SECILEN_POLIKLINIK)
        HER doktor İÇİN DOKTOR_LISTESI
            doktor yazdır
        SECILEN_DOKTOR = kullanıcı_girdisi("Doktor seçiniz: ")

        SAATLER = uygun_saatler(SECILEN_DOKTOR)
        HER saat İÇİN SAATLER
            saat yazdır
        SECILEN_SAAT = kullanıcı_girdisi("Randevu saati seçiniz: ")

        "Randevunuz onaylandı." yazdır
        SMS_GONDER(TC_NO, SECILEN_DOKTOR, SECILEN_SAAT)

    EĞER SECIM == 2 ise
        // Tahlil Modülü
        EĞER tahlil_var(TC_NO) değilse
            "Tahlil kaydınız bulunamadı." yazdır
        DEĞİLSE
            EĞER sonuc_hazir(TC_NO) ise
                "Tahlil sonuçlarınız hazır." yazdır
                SONUC_GOSTER(TC_NO)
                "PDF olarak indirmek ister misiniz?" yazdır
                CEVAP = kullanıcı_girdisi()
                EĞER CEVAP == "Evet" ise
                    PDF_INDIR(TC_NO)
            DEĞİLSE
                "Sonuçlarınız henüz hazır değil, lütfen bekleyiniz." yazdır

    "Başka bir işlem yapmak ister misiniz?" yazdır
    DEVAM = kullanıcı_girdisi()
UNTIL DEVAM == "Hayır"

"İyi günler dileriz." yazdır

BİTİR
