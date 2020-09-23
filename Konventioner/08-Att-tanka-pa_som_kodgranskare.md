# 8. Att tänka på som kodgranskare

* **Kritisera kod och inte människor – var snäll mot utvecklaren, inte mot koden.**  
Så långt det är möjligt, skriv dina kommentarer i en positiv anda och inrikta dig på att förbättra koden. Relatera kommentar till teamstandarder, specifikationer och prestandaökningar.

 
* **Behandla människor som vet och kan mindre än du med respekt, vördnad och tålamod.**

* **Ställ frågor istället för att göra uttalanden.**  
Ett uttalande är anklagande. "Du har inte följt standarden här" är en attack vare sig avsiktligt eller inte. Frågan "Vad var resonemanget bakom denna approach? är ett sätt att få veta mer. Självklart kan frågan inte sägas med en sarkastisk eller nedlåtande ton; men görs det på rätt sätt, kan den få utvecklaren att efterfråga en bättre lösning.

* **Försök att undvika ”varför”-frågor.**  
Det är stor skillnad på "Varför följde du inte standarden här?” och “Vad var resonemanget bakom att avvika från standarden här?”.

* **När du föreslår en ändring, beskriv varför.**

* **Använd egna exempel.**  
Låt kodaren veta att hen inte är den enda personen som gjort misstaget. Det kan kan vara ett bra sätt att göra kritiken lite mer komfortabel. "Jag lärde mig det här den hårda vägen när…” eller “Jag brukade göra precis på det här sättet…” kan vara bra sätt att uttrycka sig på.

* **Alla kommentarer kräver inte åtgärder.**  
Kommentarer kan även vara tankeväckande och behöver inte vara något som ska lösas eller ens svaras på. Men, då är det viktigt att du noterar det tydligt i texten.
 
* **Har du hamnat som kodgranskare av misstag?**  
Om du bjudits in att vara kodgranskare och koden i fråga är utanför din kompetens - kommentera det i ärendet och ta bort dig själv som granskare. Kan du granska delar av koden så gör du det.

* **Kom ihåg att berömma.**  
Syftet med kodgranskningar är inte att fokusera på att berätta hur kodaren kan bli bättre, och inte nödvändigtvis att de gjort ett bra jobb. Men den mänskliga naturen är sådan att vi vill erkännas för våra framgångar, och inte bli ihågkomna pga brister. Eftersom utveckling är ett kreativt arbete som utvecklare lägger ner sin själ i, är det också nära deras hjärta. Detta gör att det behövs mer beröm än kritik.
 
* **Se till att du har bra kodstandarder att referera.**  
Granskning har sin grund i företags- och branchstandarder. Standarder syftar till att ha en enig syn för att kunna producera kod med kvalité och som är underhållningsbar. Om en diskussion uppstår, om något som inte finns definierat, då har du arbeta att göra med att lägga till nya delar. Du bör ständigt fråga dig om det som diskuterats finns standardiserat.  

Men, bara för att det är en standard nu behöver det inte betyda att den alltid gäller. Uppdatera standarder i takt med att nya metoder införs och nya ramverk mm släpps.

* **Kom ihåg att inte hasta igenom en kodgranskning - men, du bör göra den snabbt.**  
Tacka nej till att granska kod om du är upptagen med annat, på så sätt kan någon annan hjälpa till istället. Sträva efter att gå igenom hela koden så mycket som möjligt vid ett och samma tillfälle. På det sättet kan man undeviker man onödiga iterationer (gransking, kommentar, ändring, gransking, kommentar, ändring osv).
 
* **Kom ihåg att du har ett ansvar för koden du granskar.**  
När du granskar en pull request och godkänner så signerar du på att du har tagit ditt ansvar att granska och säkerställa att koden följer uppsatta regler.
