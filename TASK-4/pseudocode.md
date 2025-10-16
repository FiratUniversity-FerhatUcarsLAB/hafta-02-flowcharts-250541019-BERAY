Öğrenci Ad-Soyad: Beray Akar
Öğrenci No: 250541019


BEGIN

    PRINT "TC Kimlik Numaranızı giriniz: "
    READ tc_no

    IF NOT IsValid(tc_no) THEN
        PRINT "Geçersiz TC Kimlik Numarası!"
        EXIT
    ENDIF

    PRINT "Giriş başarılı."

    REPEAT
        PRINT "İşlem Seçiniz:"
        PRINT "1 - Randevu Al"
        PRINT "2 - Tahlil Sonucu Gör"
        READ secim

        IF secim == 1 THEN
            PRINT "Poliklinik listesi:"
            DISPLAY ["Dahiliye", "Kardiyoloji", "Ortopedi", "Cildiye"]

            PRINT "Poliklinik seçiniz: "
            READ poliklinik

            PRINT "Doktor listesi getiriliyor..."
            DISPLAY GetDoctors(poliklinik)
            READ doktor

            PRINT "Uygun saatler listeleniyor..."
            DISPLAY GetAvailableHours(doktor)
            READ saat

            PRINT "Randevunuz onaylandı."
            SEND_SMS(tc_no, doktor, saat)

        ELSE IF secim == 2 THEN
            IF NOT HasTestRecord(tc_no) THEN
                PRINT "Tahlil kaydınız bulunamadı."
            ELSE
                IF IsResultReady(tc_no) THEN
                    PRINT "Sonuçlarınız hazır."
                    SHOW_RESULTS(tc_no)

                    PRINT "PDF olarak indirmek ister misiniz? (Evet/Hayır): "
                    READ cevap
                    IF cevap == "Evet" THEN
                        DOWNLOAD_PDF(tc_no)
                    ENDIF
                ELSE
                    PRINT "Sonuçlarınız henüz hazır değil. Lütfen bekleyiniz."
                ENDIF
            ENDIF
        ELSE
            PRINT "Geçersiz seçim, lütfen 1 veya 2 giriniz."
        ENDIF

        PRINT "Başka bir işlem yapmak ister misiniz? (Evet/Hayır): "
        READ devam

    UNTIL devam == "Hayır"

    PRINT "İyi günler dileriz."

END
