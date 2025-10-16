Öğrenci Ad-Soyad: Beray Akar
Öğrenci No: 250541019




Sistem, öncelikle kullanıcının onu **Aktif Edip Etmediğini Kontrol Ederek** çalışmaya başlar; aktif değilse anında kapanır. Eğer sistem aktifse, bir **sürekli döngüye** girerek düzenli aralıklarla sensör okumaları yapar. Bu döngüde, evin içindeki **hareket sensörleri** ve kapı/pencerelerdeki **açılma sensörleri** izlenir. Bu sensörlerden herhangi biri bir ihlal sinyali verirse (hareket algılanırsa veya bir kapı açılırsa), sistem alarm sürecini başlatır. Ancak hemen alarm çalmaz; öncelikle bir **yanlış alarm kontrolü** yaparak ev sahibinin gerçekten evde olup olmadığını kontrol eder. Eğer ev sahibi evdeyse, durum yanlış alarm kabul edilir ve sistem sessizce izleme döngüsüne döner. Eğer ev sahibi evde değilse, tehdit gerçek kabul edilir, **kamera kaydı başlatılır** ve tehdidin ciddiyetine göre bir **alarm seviyesi belirlenir**. Ardından, kritik bir adım olarak, ev sahibine anında **çoklu kanallardan (SMS, uygulama, e-posta)** bildirim gönderilir ve alarm çalmaya başlar. Sistem, bu aksiyonlardan sonra belirli bir süre **bekler** ve kullanıcının uygulamadan alarmı **sıfırlama** emri verip vermediğini kontrol eder. Sıfırlama emri gelirse alarm durdurulur ve sistem normal izleme moduna döner; aksi takdirde alarm durumu devam eder ve bildirimler tekrar gönderilir, böylece kesintisiz bir güvenlik sağlanmış olur.
