# Felsökningsrapport

## Fel: Överlappande bokningar

### Vilket fel undersökte du?

Programmet tillät överlappande bokningar, vilket innebar att samma mötesrum kunde bokas av flera personer under samma tid.

### Hur återskapade du felet?

Jag startade programmet och skapade två bokningar i rummet Aspen den 20 oktober. Den första bokningen var mellan 10.00 och 11.00 och den andra mellan 09.30 och 10.30. 

### Vilket resultat fick du?

Programmet godkände båda bokningarna trots att tiderna överlappade. 

### Vilket resultat skulle du ha fått?

Programmet skulle ha nekat den andra bokningen eftersom rummet redan var bokat under en del av den valda tiden.

### Vilken del av koden orsakade felet?
Felet fanns i BookingService.cs i villkoret hasOverlap som kontrollerar om bokningar överlappar. Jag tittade på jämförelsen booking.StartTime >= existing.StartTime eftersom jag såg att den var felaktig. Jag uppmärksammade att den nya bokningens sluttid inte kontrollerades.

### Varför gav koden ett felaktigt resultat?

Felet uppstod eftersom programmet bara kontrollerade om den nya bokningens starttid låg inom en befintlig bokning. Det kontrollerade inte om den nya bokningens sluttid överlappade den befintliga bokningen. Därför kunde vissa överlappande bokningar godkännas.

### Vad ändrade du?

Jag ändrade villkoret i BookingService.cs så att programmet jämför både start- och sluttiderna för bokningarna. Jag ersatte booking.StartTime >= existing.StartTime med booking.EndTime > existing.StartTime. På så sätt kan programmet upptäcka om två bokningar överlappar och förhindra att de godkänns.

### Hur kontrollerade du att ändringen fungerade?

Efter att jag hade ändrat koden körde jag testerna i Test Explorer. Jag kontrollerade att alla fyra testfallen för överlappande bokningar blev godkända. Innan ändringen misslyckades två av dessa testfall. Efter rättningen kunde programmet hantera de olika tidsintervallen korrekt. Jag körde sedan alla tester igen och fick totalt 12 av 14 godkända tester. De två tester som fortfarande misslyckades gällde avbokningsfunktionen och inte överlappande bokningar.

### Vilket automatiserat test skyddar mot att felet återkommer?

Testet Create_WhenBookingOverlapsExistingBooking_ReturnsFailure i BookingServiceTests.cs kontrollerar att programmet nekar bokningar som överlappar en befintlig bokning. Testet körs med fyra olika tidsintervall och kontrollerar att bokningen misslyckas och att rätt felmeddelande visas.