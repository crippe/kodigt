# Checklista för C# utvecklare
![RCA computer room 1959](Konventioner/Bilder/RCA-computer-room-1959.jpg)

***
### Vad är det här?
Ansatsen för det här dokumentet är att ge riktlinjer för att utveckla i programmeringsspråket C#. Konventionerna utgår från egna erfarenheter, Microsoft-dokumentation, StyleCop-regler samt många andra artiklar kring C#-praxis. Det förekommer punkter som inte har någon särskild motivering. Bakgrunden till dessa val är att det är bättre att bestämma en standard, och vara konsekvent, än att det blir godtyckligt.

Dokumentet kan fungera som underlag när man vill sätta upp kodpraxis i team. Tänker man samma? Mest av allt är det en kom-ihåg-lista att gå igenom innan man gör kodgranskningar och migrerar ihop kod. Det är inte en komplett redogörelse för språket C#, SOLID, designmönster eller TDD. De finns andra mer djuplodade böcker och kurser för det. Den tar inte heller upp några riktlinjer för frontend-utveckling med JavaScript-ramverk, CSS etcetera.

***
### Varför kodpraxis?
Det kanske är så att vissa ser att kodningsriktlinjer begränsar kreativitet och tar för mycket tid i anspråk att följa. Men det är värt ansträngningen. Huvudskälet till att använda en konsekvent uppsättning kodningskonventioner är att standardisera struktur och kodstil så att du och andra lätt kan läsa, förstå och underhålla koden.

Fördelar med kodpraxis:
* Konventioner behövs för att öka medvetenheten om att kod i allmänhet läses tio gånger mer än den ändras.
* Konventioner behövs för att åskådligöra potentiella fallgropar för vissa konstruktioner i C#.
* Riktlinjer behövs för att göra oss bekanta med konventioner i .NET Framework, t.ex. IDisposable, LINQ-uttryck och Exceptions.
* Konventioner leder också till att minska gapet mellan erfarna och juniora utvecklare. Det är också en stor hjälp för nya teammedlemmar.
* Riktlinjer leder till minskad kostnad då underhåll av applikation går snabbare och är enklare.

***
### Licens  
Du får mer än gärna skapa en egen version av detta dokument (alla inkluderade filer). <a href="Licens.md" target="_blank">Licensen</a> låter dig skapa, anpassa och distribuera den ändrade versionen så länge du refererar till originalversionen här.  Och om du har några bra idéer, rekommendationer eller korrigeringar, posta kommentarer här <a href="https://github.com/crippe/kodigt/issues/new" target="_blank">https://github.com/crippe/kodigt/issues/new</a>. 

***
### Innehåll
1. [Introduktion](Konventioner/01-Introduktion.md) 
1. [Inspiration](Konventioner/02-Inspiration.md)  
1. <a href="Konventioner\03-Drivande_principer.md" target="_blank">Drivande principer</a>
1. [Namnkonventioner](Konventioner/04-Namnkonventioner.md)  
1. [Layoutkonventioner](Konventioner/05-Layoutkonventioner.md)
    *  <a href="Konventioner\05-Layoutkonventioner.md#generellt" target="_blank">Generellt</a>
    *  <a href="Konventioner\05-Layoutkonventioner.md#storlekar-och-antal" target="_blank">Storlekar och antal</a>
1. [Kommentarkonventioner](Konventioner/06-Kommentarkonventioner.md)  
1. [C#-konventioner och checklista](Konventioner/07-CSharp-konventioner_och_checklista.md)  
    * [Generellt](Konventioner/07-CSharp-konventioner_och_checklista.md#generellt)  
    * [ASP.NET MVC](Konventioner/07-CSharp-konventioner_och_checklista.md#aspnet-mvc)
