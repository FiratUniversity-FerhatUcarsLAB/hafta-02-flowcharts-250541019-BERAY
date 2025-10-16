BEGIN
    PRINT "Öğrenci numarasını giriniz: "
    READ ogr_no
    PRINT "Şifreyi giriniz: "
    READ sifre

    IF NOT LoginValid(ogr_no, sifre) THEN
        PRINT "Hatalı giriş! Lütfen tekrar deneyiniz."
        EXIT
    ENDIF

    PRINT "Ders listesi görüntüleniyor..."
    courseList = GetAvailableCourses()

    FOR each course IN courseList DO
        IF course.kontenjan == 0 THEN
            PRINT course.name, " dersi dolu."
            CONTINUE
        ENDIF

        IF NOT CheckPrerequisite(course, ogr_no) THEN
            PRINT course.name, " için ön koşul dersi alınmamış."
            CONTINUE
        ENDIF

        IF HasTimeConflict(course, ogr_no) THEN
            PRINT course.name, " zaman çakışması mevcut."
            CONTINUE
        ENDIF

        IF (TotalCredits(ogr_no) + course.kredi) > 35 THEN
            PRINT "Kredi limiti aşıldı."
            CONTINUE
        ENDIF

        PRINT "Bu dersi eklemek istiyor musunuz? (E/H)"
        READ choice
        IF choice == "E" THEN
            AddCourse(ogr_no, course)
        ENDIF
    ENDFOR

    PRINT "Ders çıkarma işlemi yapmak ister misiniz? (E/H)"
    READ removeChoice
    WHILE removeChoice == "E"
        PRINT "Çıkarmak istediğiniz ders kodunu girin: "
        READ removeCourse
        RemoveCourse(ogr_no, removeCourse)
        PRINT "Başka ders çıkarmak ister misiniz? (E/H)"
        READ removeChoice
    ENDWHILE

    IF GetGPA(ogr_no) < 2.5 THEN
        PRINT "Danışman onayı gereklidir."
        RequestAdvisorApproval(ogr_no)
    ENDIF

    PRINT "Kayıt özeti:"
    ShowRegisteredCourses(ogr_no)

    PRINT "Kaydı onaylıyor musunuz? (E/H)"
    READ confirm
    IF confirm == "E" THEN
        SaveRegistration(ogr_no)
        PRINT "Kayıt başarıyla tamamlandı."
    ELSE
        PRINT "Kayıt iptal edildi."
    ENDIF
END
