Öğrenci Ad-Soyad: BEray Akar
Öğrenci No: 250541019


BAŞLA

// Kullanıcı girişi kontrolü
GİRİŞ yapıldı mı?
    EĞER HAYIR ise
        "Lütfen giriş yapınız." yazdır
        GİRİŞ YAP()
    DEĞİLSE
        "Hoş geldiniz!" yazdır

// Ürün kategorileri arasında gezinme
ÜRÜN_KATEGORİLERİ = ["Elektronik", "Giyim", "Ev", "Kozmetik"]
SEÇİLEN_ÜRÜN = BOŞ

TEKRARLA
    HER kategori İÇİN ÜRÜN_KATEGORİLERİ
        kategori yazdır
    SEÇİLEN_KATEGORİ = kategori_seç()
    SEÇİLEN_ÜRÜN = ürün_seç(SEÇİLEN_KATEGORİ)
    "Sepete eklemek ister misiniz?" yazdır
    CEVAP = kullanıcı_girdisi()

    EĞER CEVAP == "Evet" ise
        // Stok kontrolü
        EĞER stok_var(SEÇİLEN_ÜRÜN) ise
            SEPETE_EKLE(SEÇİLEN_ÜRÜN)
            "Ürün sepete eklendi." yazdır
        DEĞİLSE
            "Ürün stokta yok." yazdır
    DEĞİLSE
        "Ürün eklenmedi." yazdır

    "Başka bir ürün eklemek ister misiniz?" yazdır
    DEVAM = kullanıcı_girdisi()
UNTIL DEVAM == "Hayır"

// Sepeti görüntüleme ve düzenleme
TEKRARLA
    SEPETİ_GÖSTER()
    "Ürün silmek ister misiniz?" yazdır
    CEVAP = kullanıcı_girdisi()
    EĞER CEVAP == "Evet" ise
        SİLİNECEK = ürün_seç()
        SEPETTEN_SİL(SİLİNECEK)
UNTIL CEVAP == "Hayır"

// İndirim kodu uygulanabilir mi?
"İndirim kodunuz var mı?" yazdır
KOD_CEVAP = kullanıcı_girdisi()
EĞER KOD_CEVAP == "Evet" ise
    KOD = kod_gir()
    EĞER kod_geçerli(KOD) ise
        İNDİRİM_UYGULA(KOD)
        "İndirim uygulandı." yazdır
    DEĞİLSE
        "Kod geçersiz." yazdır

// Minimum 50 TL kontrolü
TOPLAM = sepet_tutarı()
EĞER TOPLAM < 50 ise
    "Sepet tutarı 50 TL altında. Devam edemezsiniz." yazdır
    DUR
DEĞİLSE
    "Sepet geçerli." yazdır

// Kargo ücreti hesaplama
EĞER TOPLAM >= 200 ise
    KARGO = 0
    "Kargo ücretsiz!" yazdır
DEĞİLSE
    KARGO = 29.99
    "Kargo ücreti 29.99 TL" yazdır

GENEL_TOPLAM = TOPLAM + KARGO
"Ödenecek toplam tutar: " + GENEL_TOPLAM yazdır

"Alışveriş tamamlandı. Teşekkür ederiz!" yazdır

BİTİR

