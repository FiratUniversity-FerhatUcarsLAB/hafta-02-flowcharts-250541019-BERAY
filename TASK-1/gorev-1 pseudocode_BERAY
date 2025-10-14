Öğrenci Ad-Soyad: Beray Akar
Öğrenci No: 250541019

FUNCTION ATM_Withdraw():
    SHOW "Kartınızı takınız"
    READ card
    IF ValidateCard(card) == FALSE:
        SHOW "Geçersiz kart"
        EJECT card
        RETURN

    ASK "PIN giriniz"
    READ pin
    IF Authenticate(card, pin) == FALSE:
        INCREMENT failedAttempts
        IF failedAttempts >= MAX_PIN_ATTEMPTS:
            BlockCard(card)
            SHOW "Kart bloke oldu"
            EJECT card
            RETURN
        SHOW "Hatalı PIN"
        RETURN

    SHOW "İşlem türünü seçin: 1-Çekim 2-Bakiye 3-İptal"
    READ choice
    IF choice == 2:
        SHOW GetBalance(card)
        EJECT card
        RETURN
    IF choice == 3:
        SHOW "İşlem iptal edildi"
        EJECT card
        RETURN

    ASK "Çekmek istediğiniz tutarı girin"
    READ amount

    IF NOT IsAmountValid(amount):
        SHOW "Geçersiz tutar"
        EJECT card
        RETURN

    account = GetAccount(card)
    IF amount > account.balance:
        SHOW "Yetersiz bakiye"
        OFFER "Başka işlem yapmak ister misiniz?"
        EJECT card
        RETURN

    IF amount > account.dailyRemainingLimit:
        SHOW "Günlük limit aşıldı"
        EJECT card
        RETURN

    IF NOT CashAvailableInATM(amount):
        SHOW "ATM'de yeterli nakit yok"
        EJECT card
        RETURN

    DispenseCash(amount)
    DeductFromAccount(account, amount)
    LogTransaction(card, account, amount, SUCCESS)
    ASK "Fiş ister misiniz? (E/H)"
    READ receiptChoice
    IF receiptChoice == 'E':
        PrintReceipt(card, amount, account.balance)
    SHOW "Paranızı alın"
    EJECT card
    RETURN
