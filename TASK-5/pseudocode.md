Öğrenci Ad-Soyad: Beray Akar
Öğrenci No: 250541019

PROSEDÜR GUVENLIK_SISTEMI_CALISTIR()
    
    // Değişken Tanımlamaları
    SISTEM_AKTIF = YANLIŞ // Başlangıçta sistem devre dışı kabul edilir
    ALARM_DURUMU = YANLIŞ
    
    // 1. Sistem Aktivasyon Kontrolü
    EĞER KULLANICI_SISTEMI_AKTIF_ETTI_MI() EŞİTTİR DOĞRU İSE
        SISTEM_AKTIF = DOĞRU
        YAZDIR("Güvenlik Sistemi Aktif Edildi.")
    DEĞİLSE
        YAZDIR("Güvenlik Sistemi Devre Dışı. Lütfen aktif edin.")
        DUR() // Sistem aktif değilse prosedür sona erer
    SON_EĞER
    
    // 2. Sensör Okuma Sürekli Döngüsü
    TEKRARLA SÜREKLİ // Sonsuz döngü: Sistem çalıştığı sürece sensörleri dinler
        
        BEKLE(1 saniye) // Her kontrolden önce kısa bir bekleme
        
        // Sadece sistem aktifken kontrol et
        EĞER SISTEM_AKTIF EŞİTTİR DOĞRU İSE
            
            TEHDIT_ALGILANDI = YANLIŞ
            
            // 3. Hareket Sensörü Kontrolü
            EĞER HAREKET_ALGILANDI_MI() EŞİTTİR DOĞRU İSE
                YAZDIR("UYARI: Hareket algılandı.")
                TEHDIT_ALGILANDI = DOĞRU
                ALARM_SEVIYESI = 1 // Düşük Seviye Alarm (Ön Kontrol)
            SON_EĞER
            
            // 4. Kapı/Pencere Sensörü Kontrolü
            EĞER KAPI_VEYA_PENCERE_ACIK_MI() EŞİTTİR DOĞRU İSE
                YAZDIR("UYARI: Kapı/Pencere açıldı.")
                TEHDIT_ALGILANDI = DOĞRU
                ALARM_SEVIYESI = 2 // Orta Seviye Alarm (Daha ciddi)
            SON_EĞER
            
            // Tehdit Algılanırsa Tepki Ver
            EĞER TEHDIT_ALGILANDI EŞİTTİR DOĞRU İSE
                
                // 5. Yanlış Alarm Kontrolü (Ev sahibi evde mi?)
                EĞER EV_SAHIBI_EVDE_MI() EŞİTTİR DOĞRU İSE
                    YAZDIR("Ev sahibi evde. Yanlış alarm varsayımı.")
                    TEHDIT_ALGILANDI = YANLIŞ
                    ALARM_SIFIRLA()
                DEĞİLSE
                    // 6. Alarm Seviyesi Belirleme ve Bildirim
                    
                    // 7. Kamera Aktivasyonu
                    KAMERA_KAYIT_BASLAT()
                    YAZDIR("Kamera kaydı başlatıldı.")
                    
                    EĞER ALARM_SEVIYESI EŞİTTİR 2 İSE
                        YAZDIR("Orta seviye tehdit. Alarm çalacak.")
                        ALARM_CALDIR()
                    SON_EĞER
                    
                    // 8. Bildirim Gönderme
                    BILDIRIM_GONDER(ALARM_SEVIYESI, "SMS", "Potansiyel güvenlik ihlali!")
                    BILDIRIM_GONDER(ALARM_SEVIYESI, "App", "Potansiyel güvenlik ihlali!")
                    BILDIRIM_GONDER(ALARM_SEVIYESI, "Email", "Potansiyel güvenlik ihlali!")
                    
                    ALARM_DURUMU = DOĞRU
                    
                    // 9. Bekle ve Tekrar Kontrol Et (Bildirim sonrası bekleme)
                    BEKLE(30 saniye)
                    
                    // 10. Alarm Sıfırlama veya Devam Ettirme
                    EĞER KULLANICI_SIFIRLAMA_TALEBI_GONDERDI_MI() EŞİTTİR DOĞRU İSE
                        ALARM_SIFIRLA()
                        ALARM_DURUMU = YANLIŞ
                        KAMERA_KAYIT_DURDUR()
                        YAZDIR("Kullanıcı isteği üzerine alarm sıfırlandı.")
                    DEĞİLSE
                        YAZDIR("Alarm devam ediyor. Yeni bildirim gönderiliyor.")
                        // Döngü başa döner, 30 saniye sonra tekrar kontrol eder.
                    SON_EĞER
                SON_EĞER // Ev sahibi kontrolü
            SON_EĞER // Tehdit algılama kontrolü
        SON_EĞER // Sistem aktif kontrolü
        
    SON_TEKRARLA // Sürekli döngü sonu

SON_PROSEDÜR
