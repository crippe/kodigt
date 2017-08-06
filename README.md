# Checklista för C# utvecklare  🛠  beta 0.6.7


### Vad är det här?
***
Ansatsen för det här dokumentet är att ge riktlinjer för kodning i programmeringsspråket C#. Konventionerna utgår från egna erfarenheter, Microsoft-dokumentation, StyleCop-regler samt många andra artiklar kring C#-praxis. Det förekommer punkter som inte har någon särskild motivering. Bakgrunden till dessa val är att det är bättre att bestämma en standard, och vara konsekvent, än att det blir godtyckligt.

Dokumentet kan fungera som underlag när man vill sätta upp kodpraxis i team. Tänker man samma? Mest av allt är det en kom-ihåg-lista att gå igenom innan man gör kodgranskningar och migrerar ihop kod. Det är inte en komplett redogörelse för språket C#, SOLID, designmönster eller TDD. De finns andra mer djuplodade böcker och kurser för det. Den tar inte heller upp några riktlinjer för frontend-utveckling med JavaScript-ramverk, CSS etcetera.

### Varför kodpraxis?
***
Det kanske är så att vissa ser att kodningsriktlinjer begränsar kreativitet och tar för mycket tid i anspråk att följa. Men det är värt ansträngningen. Huvudskälet till att använda en konsekvent uppsättning kodningskonventioner är att standardisera struktur och kodstil för en applikation så att du och andra lätt kan läsa, förstå och underhålla koden.

Fördelar med riklinjer:
* Konventioner behövs för att öka medvetenheten om att kod i allmänhet läses tio gånger mer än den ändras.
* Konventioner behövs för att åskådligöra potentiella fallgropar för vissa konstruktioner i C#.
* Riktlinjer behövs för att göra oss bekanta med konventioner i .NET Framework, t.ex. IDisposable, LINQ-uttryck och Exceptions.
* Konventioner leder också till att minska gapet mellan erfarna kollegor och juniora utvecklare. Det är också en stor hjälp för nya teammedlemmar.

### Innehåll
***
* [Introduktion](01-Introduktion.md)
* [Mindset](02-Mindset.md)
* [Namnkonventioner](03-Namnkonventioner.md)
* [Layoutkonventioner](04-Layoutkonventioner.md)
* [Kommentarkonventioner](05-Kommentarkonventioner.md)
* [Språkkonventioner och checklista](06-Sprakkonventioner_och_checklista.md)  
    * [Generellt](06-Sprakkonventioner_och_checklista.md#generellt)  
    * [ASP.NET MVC](06-Sprakkonventioner_och_checklista.md#aspnet-mvc)
