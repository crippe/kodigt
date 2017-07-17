# Checklista för C# utvecklare  🛠  beta 0.6.7
![RCA computer room 1959](https://github.com/crippe/kodigt/blob/master/wiki/images/RCA-computer-room-1959.jpg)
### Innehåll
* [Introduktion](#introduktion)
* [Mindset](#mindset)
* [Namnkonventioner](#namnkonventioner)
* [Layoutkonventioner](#layoutkonventioner)
* [Kommentarkonventioner](#kommentarkonventioner)
* [Språkkonventioner och checklista](#språkkonventioner-och-checklista)  
    * [Generellt](#generellt)  
    * [ASP.NET MVC](#aspnet-mvc)
***
### Introduktion
Alla utvecklares dröm är att få börja på ett nytt blankt blad. Med nyvunnen erfarenhet från senaste projektet vill man den här gången göra rätt från början. I realiteten har man inte den möjligheten särskilt ofta. Men ha förtröstan, det finns massor med roliga och utmanande saker att göra i en lösning som förvaltas. Refaktorera, skala bort, kapsla in, namnändra, prestandaförbättra och skriva fler tester kommer göra dig till en hjälte/hjältinna. Det kommer bli ett nöje för andra att kodgranska. Utkomsten av checklistan är förbättrad kvalité.

Bra kod är:
* Enkel, men inte förenklad
* Läsbar och lätt att förstå
* Underhållningsbar
* Oberoende/frikopplad
* Effektiv
* Självdokumenterande
* Testbar

Hur är denna artikel tänkt att fungera och användas? Vad är den och vad är den inte? Punkterna utgår oftast från en typisk webblösning med Visual Studio, C#, ASP.NET och ReSharper. Artikeln tar upp ämnen som ofta diskuteras i team eller är typiska detaljer som ofta förbises i kod. Artikeln kan också fungera som underlag när man vill sätta upp kodpraxis i team. Tänker man samma? Mest av allt är det en kom-ihåg-lista att gå igenom innan man gör kodgranskningar och migrerar ihop kod. Det är inte en komplett redogörelse för språket C#, SOLID, designmönster eller TDD. De finns andra mer djuplodade böcker och kurser för det. Den tar inte heller upp några riktlinjer för frontend-utveckling med JavaScript-ramverk, CSS etcetera.
***
### Mindset

* _"Always code as if the guy who ends up maintaining your code will be a violent psychopath who knows where you live."_  
-- John F. Woods, 1991-09-25

* _"Any fool can write code that a computer can understand. Good programmers write code that humans understand."_  
-- Martin Fowler, "Refactoring: Improving the design of existing code"

* _"The act of leaving a mess in the code should be as socially unacceptable as littering."_  
-- Robert C. “Uncle Bob” Martin

* _"Leave the code in a better state than you found it."_  
(Originalet skrevs av Robert Stephenson Smyth Baden-Powell, pappa till scoutrörelsen, och löd "Try and leave this world a little better than you found it.”)

* _"Comments are evil. The goal of comments is to compensate for our failure or to help express ourselves better. They are always sign of failure."_   
-- Robert C. “Uncle Bob” Martin, "Clean Code" 

* _"Code formatting is important because it is part of communication. It also makes the reader trust the code more."_  
-- Robert C. “Uncle Bob” Martin, "Clean Code"  

* _"We should forget about small efficiencies, say about 97% of the time: premature optimization is the root of all evil. Yet we should not pass up our opportunities in that critical 3%."_  
-- Donald Knuth, "Structured Programming With Go To Statements"  

[Secrets of Maintainable Codebases](http://www.daedtech.com/secrets-maintainable-codebases/)  
[Static Code Analysis and Quality Metrics](http://ardalis.com/static-code-analysis-and-quality-metrics)

***
### Namnkonventioner

Om inget annat sägs eller andra teamöverenskommelser finns, följ Microsofts namngivning, dokumentation och guider. Harmonisera med .NET ramverket. För att backa upp det, och vara ännu mera precis, använd [StyleCop](https://github.com/StyleCop/StyleCop) som vägledning. 

1. Använd engelska  
Alla medlemmar, parametrar och variabler bör namnges med ord från engelska språket.  

1. Domänspråk är undantag till engelska  
Använd ord, fraser och termer från företagets domän eller vad som är allmänt vedertaget i branschen. Finns det en entitet som heter `Konto` som kommer från ett backofficesystem, behåll det. Döp det inte till `Account`. Det underlättar när ytterligare en kontohanterare implementeras där namngivningen av objekt faktiskt är `Account`. Om det finns en framtagen domänspråksdokumentation i företaget, följ den framför allt annat.

    Gemensamt domänspråk är viktigt i kedjor som: `beslutsfattare/intressent ↔ affärsanalytiker ↔ produktägare ↔ arkitekt ↔ projektledare ↔ scrummaster ↔ interaktionsdesigner ↔ copywriter ↔ redaktör ↔ kundtjänst ↔ ekonomichef ↔ kientutvecklare ↔ backendutvecklare ↔ api-utvecklare`. 

    Det är oundvikligt att begrepp tas bort eller ändrar betydelse i delar av systemkedjan. Då är kommentarer i kod att rekommendera. Beskriv vad det hette tidigare och möjligen lite bakgrund, då blir det enkelt att söka/hitta och förstå koden.

    * [Ubiquitous Language](https://martinfowler.com/bliki/UbiquitousLanguage.html)
    * [Ubiquitous language without domain-driven design](https://mikealdo.github.io/2016/04/15/Ubiquitous-language-without-domain-driven-design.html)

1. Grammatiskt rätt  
Välj namn som är lätta att läsa och grammatiskt korrekt. Föredra exempelvis `HorizontalAlignment` framför `AlignmentHorizontal`.

1. Använd inte ord från programmeringsspråk  
Undvik att använda nyckelord från språk i lösningen. Använd exempelvis inte `Interface` som en variabel.

1. Använd inte prefix för fält  
Några exempel:
    * Använd inte `_` som prefix för privata fält. 
    * Använd inte `g_` eller `s_` för att skilja på statiska och icke statiska fält.
    * Använd inte typnamn (eller förkortning av det) som prefix, exempelvis `strAge`.

1. Undvik förkortningar  
Exempel: använd `OnButtonClick` framför `OnBtnClick`. Undvik också variabler med enskilda tecken som i och q. Använd `index` respektive `query` istället. Undantaget till regeln kan vara välkända förkortningar som är allmänt accepterade eller välkända i domänen. `UI` framför `UserInterface` är ett exempel.

1. Ange inte typer i namn  
Namnge medlemmar, parametrar eller variabler efter dess betydelse och inte efter vilken typ det är. Exempel: `GetLength` är ett bättre namn än `GetInt`. Använd inte `Enum`, `Class` eller `Struct` i namn.

1. Upprepa inte klassnamn i medlemmar  

    &#x274C; UNDVIK:
    ```csharp
    class Employee
    {
        Employee GetEmployee() {}
        DeleteEmployee() {}
    }
    ```
    &#x2705; GÖR SÅ HÄR:
    ```csharp
    class Employee
    {
        Employee Get() {}
        Delete() {}
    }
    ```

1. Namnge som i .NET Framework  
Namnge medlemmar på liknande sätt som medlemmar i .NET Framework-klasser. Om du exempelvis definierar en klass som ska bete sig som en samling, lägg till medlemmar som `Add`, `Remove` och `Count` framför `AddItem`, `Delete` eller `NumberOfItems`.

1. Egenskapsnamn  
    * Namnge egenskaper med substantiv, substantivfraser eller ibland adjektiva fraser. 
    * Benämn booleska egenskaper med jakande fraser, exempelvis `CanSearch` istället för `CantSearch`.
    * Använd prefix som `Is`, `Has`, `Can` och `Allows` för booleska egenskaper. Exempel: `IsVisible`, `HasChildren` och `CanExecute`.

1. Metodnamn  
Namnge metoder med verb eller verb-objekt par. Exempel `Show` respektive `ShowDialog`. Ett bra namn bör ge en antydan om **vad** en medlem gör, och om möjligt, **varför**.

    Inkludera inte `And` i namnet på en metod. Det innebär att metoden gör mer än en sak och det bryter mot "single responsibility principle”.

    En generell konvention för metoder som returnerar `Task` eller `Task<Result>` är att namnge dem med suffixet `Async` alternativt `TaskAsync`. 

1. Namnge namnrymder  
Använd produktnamn, teknikbenämningar, lager, verb och funktioner i namnrymder. Överväg att använda företagsnamn då uppköp och fusioner händer. 

    Undvik namn på typer i namnrymder, exempelvis en klass med namnet `Order`. Men ett substantiv i pluralform är vanligt, såsom `Collections` och `Helpers`.

1. Händelsenamn  
Namnge händelser med verb eller verbfraser. Till exempel: `Click`, `Deleted`, `Closing`, `Minimizing` och `Arriving`. Använd `-ing` och `-ed` för att uttrycka före och efter en händelse.

    Anta att du vill definiera händelser relaterade till radering av ett objekt. Undvik att definiera `Deleting` och `Deleted` som `StartDelete` och `EndDelete`. Namnge istället dessa som:
    * `Deleting`: Händer straxt före objektet blir raderat.
    * `Delete`: Händer när objektet behöver raderas av händelsehanteraren.
    * `Deleted`: Händer när objektet redan är raderat.

    Det är god praxis att ha `On` som prefix i metoder som handskas med händelser. Till exempel kan en metod som hanterar `Closing` namnges som `OnClosing`.

1. Pascal- eller Camel format  
    Namnge typer enligt nedan.

    | Språkelement                                    | Format                        | Exempel | StyleCop-regler |
    |-------------------------                        |------------                   |--------------------|--------------------------------------------------------------------------------|
    | Class, Struct | Pascal | `AppDomain` |  |
    | Interface | Pascal | `IBusinessService` | [SA1302: InterfaceNamesMustBeginWithI](http://stylecop.soyuz5.com/SA1302.html) |
    | Enumeration type | Pascal | `ErrorLevel` |  |
    | Enumeration values | Pascal | `FatalError` |  |
    | Event | Pascal | `Click` |  |
    | Private field | Camel | `listItem` | [SA1306: FieldNamesMustBeginWithLowerCaseLetter](http://stylecop.soyuz5.com/SA1306.html)<br>[SA1310: FieldNamesMustNotContainUnderscore](http://stylecop.soyuz5.com/SA1310.html)<br>[SA1309: FieldNamesMustNotBeginWithUnderscore](http://stylecop.soyuz5.com/SA1309.html)<br>[SA1305: FieldNamesMustNotUseHungarianNotation](http://stylecop.soyuz5.com/SA1305.html) |
    | Protected field | Pascal | `MainPanel` | [SA1307: AccessibleFieldsMustBeginWithUpperCaseLetter](http://stylecop.soyuz5.com/SA1307.html) |
    | Constant field | Pascal | `MaximumItems` | [SA1303: ConstFieldNamesMustBeginWithUpperCaseLetter](http://stylecop.soyuz5.com/SA1303.html) |
    | Constant Local variable | Camel | `maximumItems` |  |
    | Read-only static field | Pascal | `RedValue` | [SA1304: NonPrivateReadonlyFieldsMustBeginWithUpperCaseLetter](http://stylecop.soyuz5.com/SA1304.html) |
    | Local Variable | Camel | `listOfValues` | [SA1308: VariableNamesMustNotBePrefixed](http://stylecop.soyuz5.com/SA1308.html) |
    | Method | Pascal | `ToString` |  |
    | Namespace | Pascal | `System.Drawing` |  |
    | Parameter | Camel | `typeName` |  |
    | Type Parameter | Pascal | `TView` |  |
    | Property | Pascal | `BackColor` |  |

    I ReSharper är det definierat på detta sätt som standard:  
    ![ReSharper Naming Style](https://github.com/crippe/kodigt/blob/master/wiki/images/resharper-naming-style.png?raw=true)

Referenser:
* [Naming Guidelines](http://www.dofactory.com/reference/csharp-coding-standards)
* [C# Coding Standards and Naming Conventions](http://www.dofactory.com/reference/csharp-coding-standards)
* [StyleCop - Wikipedia](https://en.wikipedia.org/wiki/StyleCop)
***
### Layoutkonventioner

#### Generellt  

1. Ordning i fil  
Sträva efter att ordna medlemmar i en fil enligt StyleCop regel [SA1201: ElementsMustAppearInTheCorrectOrder](http://stylecop.soyuz5.com/SA1201.html).  
    
    | StyleCop                                                                                                                                                                                                                                                                                                                        	| ReSharper 	|
    |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|---------------------	|
    | På rotnivån ser det ut så här:<ul><li>Extern Alias Directives</li><li>Using Directives</li><li>Namespaces</li><li>Delegates</li><li>Enums</li><li>Interfaces</li><li>Structs</li><li>Classes</li></ul>  <br>Inuti en class, struct eller interface ordnas det enligt följande:<ul><li>Inuti en class, struct eller interface ordnas det enligt följande:</li><li>Fields</li><li>Constructors</li><li>Finalizers (Destructors)</li><li>Delegates</li><li>Events</li><li>Enums</li><li>Interfaces</li><li>Properties</li><li>Indexers</li><li>Methods</li><li>Structs</li><li>Classes</li></ul>   	| ![File layout - ReSharper - StyleCop](https://github.com/crippe/kodigt/blob/master/wiki/images/file-layout-resharper-stylecop.png?raw=true) 	|

    Två saker kan man fokusera på:
    1. Sortera metoder i bokstavsordning och placera alla publika först.
    1. Sortera medlemmar i klasser i bokstavsordning.

1. Klasser läggs i separata filer  

    * [SA1402: FileMayOnlyContainASingleClass](http://stylecop.soyuz5.com/SA1402.html)



1. Tomrader mellan element  
Ha alltid en tomrad mellan element. Det gäller såväl mellan metoder som kodblock. Ett block kan vara ett `if`-uttryck eller `foreach` osv.  
    
    * [SA1516: ElementsMustBeSeparatedByBlankLine](http://stylecop.soyuz5.com/SA1516.html)

1. Flera tomrader  
Undvik flera tomrader på rad.  
    
    * [SA1507: CodeMustNotContainMultipleBlankLinesInARow](http://stylecop.soyuz5.com/SA1507.html)
 
1. En deklaration per rad  
Undvik att deklarera flera variabler på en och samma rad.

    &#x274C; UNDVIK:
    ```csharp
    int i = 2, j = 3;
    ```
    &#x2705; GÖR SÅ HÄR:
    ```csharp
    int i = 2;
    int j = 3;
    ```

1. Regioner  
Undvik att använda regioner.  

    * [SA1124: DoNotUseRegions](http://stylecop.soyuz5.com/SA1124.html)
    * [C# regions is a design smell](http://enterprisecraftsmanship.com/2015/12/08/c-regions-is-a-design-smell/) 

1. Hämtning, beräkning och kontroll  
Undvik tomrad mellan datahämtning eller beräkningar, och det villkorsuttryck som ska kontrollera resultatet.

    &#x274C; UNDVIK:
    ```csharp
    var siteConfigurationPage = ContentHelper.GetSiteConfigurationPage() as ConsumerSiteConfigurationPage;

    if (siteConfigurationPage == null) return string.Empty;
    ```
    &#x2705; GÖR SÅ HÄR:
    ```csharp
    var siteConfigurationPage = ContentHelper.GetSiteConfigurationPage() as ConsumerSiteConfigurationPage;
    if (siteConfigurationPage == null) return string.Empty;
    ```

1. Tomrad innan sista retur-uttrycket  
Sträva efter att ha en tomrad innan det sista retur-uttrycket i metoder, det gäller framförallt när metoden är lite längre och mer komplicerad.

    &#x274C; UNDVIK:
    ```csharp
    // Placeholder.
    ```
    &#x2705; GÖR SÅ HÄR:
    ```csharp
    // Placeholder.
    ```

1. Indrag  
    * Använd fyra (4) mellanslag istället för tabb i filer. 
    * Använd inte enstaka mellanslag för att marginaljustera uttryck. Många varierande radstarter i koden gör att helheten blir svårare att läsa. 

    I exemplet nedan används fem olika indrag i det övre exemplet och två i det undre.

    &#x274C; UNDVIK:
    ```csharp
    public ResultType ArbitraryMethodName(FirstArgumentType firstParameter, 
                                          SecondArgumentType secondParameter,
                                          ThirdArgumentType thirdParameter)
    {
        LocalVariableType localVariable = method(firstParameter, 
                                                 secondParameter
                                                 defaultIfZero: 100);

        if (localVariable.IsSomething(thirdParameter, 
                                      SomeConstant)) 
        {   
            DoSomethingWith(localVariable); 
        } 

        return localVariable.GetSomething(); 
    }
    ```
    &#x2705; GÖR SÅ HÄR:
    ```csharp
    public ResultType ArbitraryMethodName(
        FirstArgumentType firstParameter, 
        SecondArgumentType secondParameter,
        ThirdArgumentType thirdParameter)
    {
        LocalVariableType localVariable = 
            method(firstParameter, secondParameter, defaultIfZero: 100);

        if (localVariable.IsSomething(thirdParameter, SomeConstant)) 
        {   
            DoSomethingWith(localVariable); 
        } 

        return localVariable.GetSomething(); 
    }
    ```
    * [SA1027: TabsMustNotBeUsed](http://stylecop.soyuz5.com/SA1027.html)

1. Radbryningar  
Om inte ett uttryck får rum på en rad och det inte är möjligt att refaktorera för att göra den kortare, följ dessa generella principer:
    * Bryt efter operatorer.
    * Bryt efter komma.
    * Gör alltid indrag efter radbrytning.

1. Radbrytningar i metodsignaturer  
Om raden tenderar att bli längre än praxis kan det vara mer lättläst att dela upp metodsnamnet på en rad och parametrar på nästa. Följ också konvention med indrag. 

    &#x274C; UNDVIK:
    ```csharp
    public override IAsyncResult BeginWrite(byte[] buffer, int offset, 
        int count, AsyncCallback callback, object state)
    ```
    &#x274C; UNDVIK:
    ```csharp
    public override IAsyncResult BeginWrite(byte[] buffer, int offset, 
                                            int count, AsyncCallback callback, object state)
    ```
    &#x2705; GÖR SÅ HÄR:
    ```csharp
    public override IAsyncResult BeginWrite(
        byte[] buffer, int offset, int count, AsyncCallback callback, object state)
    ```
    &#x2705; ELLER GÖR SÅ HÄR:
    ```csharp
    public override IAsyncResult BeginWrite(
        byte[] buffer, 
        int offset, 
        int count, 
        AsyncCallback callback, 
        object state)
    ```
    * [C# coding style - line length / wrapping lines](https://stackoverflow.com/questions/2151836/c-sharp-coding-style-line-length-wrapping-lines)

1. Radbrytningar i metodanrop  
Använd ungefär samma principer vid metodanrop som vid metodssignaturer.  

    &#x274C; UNDVIK:
    ```csharp
    var compareResult = string.Compare(string1, 
                                       string2, StringComparison.OrdinalIgnoreCase);
    ```
    &#x2705; GÖR SÅ HÄR:
    ```csharp
    var compareResult = string.Compare(
        string1, string2, StringComparison.OrdinalIgnoreCase);
    ```
    &#x2705; ELLER GÖR SÅ HÄR:
    ```csharp
    var compareResult = string.Compare(
        string1, 
        string2, 
        StringComparison.OrdinalIgnoreCase);
    ```
    &#x2705; ELLER GÖR SÅ HÄR:
    ```csharp
    var compareResult = 
        string.Compare(
            string1, 
            string2, 
            StringComparison.OrdinalIgnoreCase);
    ```

1. Radbrytningar av ternary operatorn  
Får uttrycket plats på en rad och är läsbart, behåll det så. I annat fall, dela upp raderna så att de börjar med `?` respektive `:`.

    &#x2139; EXEMPEL:
    ```csharp
    int result = condition
        ? SomeFunction1()
        : SomeFunction2();
    ```
    Just i detta exempel, när uttrycket är kort, är det bättre att placera allt på en rad.  

    &#x2139; EXEMPEL TVÅ:
    ```csharp
    int result = condition ? SomeFunction1() : SomeFunction2();
    ```

1. Radbrytningar av LINQ med metodsyntax  
Får uttrycket plats på en rad och är läsbart, behåll det så. I annat fall, dela upp raderna så att de börjar med `.` och extension-metod namnet. Undvik att dela upp lambda-yttryck så långt det går.

    &#x274C; UNDVIK:
    ```csharp
    var nameAndOrderIds = customers
                          .Where(c => c.Country == "Sweden")
                          .SelectMany(o => o.Orders)
                          .Where(y => y.OrderDate.Year == 2017)
                          .Select(oi => new { oi.Customer.Name, oi.OrderID });
    ```
    &#x2705; GÖR SÅ HÄR:
    ```csharp
    var nameAndOrderIds = customers
        .Where(c => c.Country == "Sweden")
        .SelectMany(o => o.Orders)
        .Where(y => y.OrderDate.Year == 2017)
        .Select(oi => new { oi.Customer.Name, oi.OrderID });
    ```

1. Radbrytningar av LINQ med frågesyntax  
Får uttrycket plats på en rad och är läsbart, behåll det så. I annat fall, placera `from` på en egen rad.

    &#x274C; UNDVIK:
    ```csharp
    var categoryProducts = from category in categories
                           join p in products on category.ID equals p.CategoryID into prodGroups
                           orderby category.Name
                           select new
                           {
                               Category = category.Name,
                               Products = from prodGroup in prodGroups
                                          orderby prodGroup.Name
                                          select prodGroup
                           };
    ```
    &#x2705; GÖR SÅ HÄR:
    ```csharp
        var categoryProducts = 
            from category in categories
            join p in products on category.ID equals p.CategoryID into prodGroups
            orderby category.Name
            select new
            {
                Category = category.Name,
                Products = 
                    from prodGroup in prodGroups
                    orderby prodGroup.Name
                    select prodGroup
            };
    ```

#### Storlekar och antal
1. Klasser    
Försök hålla klasser så små som möjligt. Använd "Single Responsibility Principal" för att avgöra storleken. Principen säger att varje objekt ska ett ansvar och att ansvaret bör vara helt inkapslat i klassen.

    * [In C# how many lines before a class should be consider to be refactored?](https://stackoverflow.com/questions/849557/in-c-sharp-how-many-lines-before-a-class-should-be-consider-to-be-refactored)
    * [How to split code into components… big classes? small classes?](https://stackoverflow.com/questions/1046367/how-to-split-code-into-components-big-classes-small-classes)
    * [.net max class size](https://stackoverflow.com/questions/14437321/net-max-class-size)

1. Metoder  
Undvik metoder som är längre än 15-20 rader. Men, det är bara ett riktmärke. Det kan finnas skäl till att en metod är längre än så. 

    * [How long should a single method be?](http://enterprisecraftsmanship.com/2017/01/19/how-long-should-a-single-method-be/)

1. Parametrar  
Antal parametrar i metodsignaturer bör vara runt fyra (4). Om det blir fler, skapa en s.k. "wrapper"-klass istället som används som parameter. Använd konstruktorn i wrapper-klassen framför att objektinitialisera den.

    * [How many parameters are too many?](http://stackoverflow.com/questions/174968/how-many-parameters-are-too-many)
    * [How many parameters in C# method are acceptable?](http://stackoverflow.com/questions/12431932/how-many-parameters-in-c-sharp-method-are-acceptable)

1. Radbredd  
Sätt radbredden till maximum om 120 tecken.

    Ju längre kodrader är ju mer distraktion utsätts du för i det ögonblick du ska börja läsa nästa rad. Se exempel nedan.

    Så här tänker ofta utvecklare när de skriver kod (rader kan vara lika långa som skärmen är bredd)  
    ![Kolumn 80](https://github.com/crippe/kodigt/blob/master/wiki/images/column-80.JPG)
    
    Så här brukar människor föredra att läsa text (kortare rader som i böcker)   
    ![Kolumn 80](https://github.com/crippe/kodigt/blob/master/wiki/images/how-people-read-3.jpg)

    * [Is an 80 Character Code Line Length Still Relevant?](https://blog.falafel.com/is-an-80-character-code-line-length-still-relevant/)
    * [How to follow the 80 character limit best practice while writing source code?](http://softwareengineering.stackexchange.com/questions/312889/how-to-follow-the-80-character-limit-best-practice-while-writing-source-code)

***
### Kommentarkonventioner

1. Undvik kommentarer   
I möjligaste mån, undvik att skriva kommentarer. Lägg istället energi på att beskriva din intention i namn på metoder,  variabler och dela upp kod på ett förståeligt sätt. 

    * [Comments in Clean Code? Think Documentation](http://www.daedtech.com/comments-clean-code-think-documentation/)
    * [Don’t document your code. Code your documentation.](https://dev.to/raddikx/dont-document-your-code-code-your-documentation)
    * [Fighting Evil in Your Code: Comments on Comments](https://www.simple-talk.com/opinion/opinion-pieces/fighting-evil-code-comments-comments/)

    **Undantag till denna rekommendation:**
1. Märkning av kod som behöver förändras med "TODO".  
TODO-kommentarer skrivs enligt mönstret:  
    **[//][mellanslag][TODO:][mellanslag][Text som börjar med stor bokstav och slutar med punkt.]** 

    &#x2139; EXEMPEL:
    ```csharp
    // TODO: En kommentar.
    ```
    * [SA1005: SingleLineCommentsMustBeginWithSingleSpace](http://stylecop.soyuz5.com/SA1005.html)

1. Beskrivning av skeenden, flöden etc som ligger utanför lösningens kontroll och som inte på ett bra och enkelt sätt kan beskrivas i kod.

1. Vid skapande av API  
Om du skapar ett ASP.NET Web API är dokumentation en del av lösningen.

    * [Creating Help Pages for ASP.NET Web API](https://docs.microsoft.com/en-us/aspnet/web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages) 
    * [Swashbuckle - Swagger for WebApi 5.5.3](https://github.com/domaindrivendev/Swashbuckle)
    * [RESTful Web API Help Documentation using Swagger UI and Swashbuckle](https://www.codeproject.com/Articles/1078249/RESTful-Web-API-Help-Documentation-using-Swagger-U)

***
### Språkkonventioner och checklista

#### Generellt
1. Återanvändning av kod  
Om ett kodblock används på mer än ett ställe, eller kommer att göra det, gör det till generiska metoder. Placera koden i relaterade klasser så andra utvecklare kan börja använda dem.
    * [Designing Code for Reusability](http://msdn.microsoft.com/en-us/library/office/aa140806(v=office.10).aspx)

1. Läsbar kod  
Skriv så att en utvecklare som börjar i teamet om sex månader förstår. Koden här är exempel på många fel på ett och samma ställe. Exemeplvis namngivning, ansvarsområde för klass, magiska siffror, upprepningar, ska 0 returneras om type är utanför intervall etcetera.  

    &#x274C; UNDVIK:
    ```csharp
    public class Class1
    {
        public decimal Calculate(decimal amount, int type, int years)
        {
            decimal r = 0;
            decimal disc = (years > 5) ? (decimal)5 / 100 : (decimal)years / 100;
            if (type == 1)
            {
                r = amount;
            }
            else if (type == 2)
            {
                r = (amount - (0.1m * amount)) - disc * (amount - (0.1m * amount));
            }
            else if (type == 3)
            {
                r = (0.7m * amount) - disc * (0.7m * amount);
            }
            else if (type == 4)
            {
                r = (amount - (0.5m * amount)) - disc * (amount - (0.5m * amount));
            }
            return r;
        }
    }
    ```
    &#x2705; EXEMPEL PÅ LÖSNING:
    ```csharp
    public class DiscountManager
    {
        private readonly IAccountDiscountCalculatorFactory factory;
        private readonly ILoyaltyDiscountCalculator loyaltyDiscountCalculator;
 
        public DiscountManager(IAccountDiscountCalculatorFactory factory, ILoyaltyDiscountCalculator loyaltyDiscountCalculator)
        {
           factory = factory;
           loyaltyDiscountCalculator = loyaltyDiscountCalculator;
        }
 
       public decimal ApplyDiscount(decimal price, AccountStatus accountStatus, int timeOfHavingAccountInYears)
       {
           decimal priceAfterDiscount = 0;
           priceAfterDiscount = factory.GetAccountDiscountCalculator(accountStatus).ApplyDiscount(price);
           priceAfterDiscount = loyaltyDiscountCalculator.ApplyDiscount(priceAfterDiscount, timeOfHavingAccountInYears);
    
          return priceAfterDiscount;
       }
    }
    ```

1. Onårbar kod  
Kontrollera om det finns kod som inte kan nås och ta bort den om så skulle vara fallet. ReSharper markerar sådan kod som nedtonad grå.

1. Varningar vid byggen  
Kontrollera och åtgärda varningar som visas när projekten byggs. Tillse att "Enable Code Analysis on Build" är ikryssat på respektive projekt.

1. using direktiv  
Sortera och ta bort `using`-direktiv som inte längre används.
    ```csharp
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    ```
    * [using Directive (C# Reference)](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/using-directive)
    
    &#x1F3F7; `using` `directive`

1. Returnera inte null  
Returnera instansierade objekt framför null i metoder. Var noga att kontrollera objekt som ändå kan vara null.
    * [How to Avoid Returning Null from a Method](http://www.codinghelmet.com/?path=howto/avoid-returning-null)
    * [Tactical Design Patterns in .NET: Control Flow -&gt; Motivation to Avoid Null Reference](https://app.pluralsight.com/player?course=tactical-design-patterns-dot-net-control-flow&author=zoran-horvat&name=tactical-design-patterns-dot-net-control-flow-m2&clip=0&mode=live)
    * [My takeaways from “Clean Code” -> Don’t Pass Null](https://medium.com/@webprolific/my-takeaways-from-clean-code-a70ca8382884)
    * [Is it Really Better to 'Return an Empty List Instead of null'? / Part 1](https://www.codeproject.com/Articles/794448/Is-it-Really-Better-to-Return-an-Empty-List-Instea), [Part 2](https://www.codeproject.com/Articles/797453/Is-it-Really-Better-to-Return-an-Empty-List-Inst), [Part 3](https://www.codeproject.com/Articles/820066/Is-it-Really-Better-to-Return-an-Empty-List-Inst), [Part 4](https://www.codeproject.com/Articles/834677/Is-it-Really-Better-to-Return-an-Empty-List-Inst)

    &#x1F3F7; `null`
1. Använd alias  
Deklarera typer på samma sätt genom hela lösningen, dvs använd inbyggda alias. Använd inte både `Int32` och `int` eller `String` och `string`.
    
    &#x274C; UNDVIK:
    ```csharp
    public class Class1
    {
        int year = 2017;
        Int32 age = 62;
 
        string name = "Stefen Andersson";
        String address = "Kommendörsgatan 34";
    }
    ```
    &#x2705; GÖR SÅ HÄR:
    ```csharp
    public class Class1
    {
        int year = 2017;
        int age = 62;
 
        string name = "Stefen Andersson";
        string address = "Kommendörsgatan 34";
    }
    ```
    * [SA1121: UseBuiltInTypeAlias](http://stylecop.soyuz5.com/SA1121.html)
    * [C# - StyleCop - SA1121: UseBuiltInTypeAlias - Readability Rules](https://stackoverflow.com/questions/6000517/c-sharp-stylecop-sa1121-usebuiltintypealias-readability-rules)

    &#x1F3F7; `string` `int` `alias`
1. Använd using-block  
Använd using-block för `IDisposable` objekt.

    &#x274C; UNDVIK:
    ```csharp
    var arialFont = new Font("Arial", emSize: 10.0f);
    try
    {
        var gdiCharSet = arialFont.GdiCharSet;
    }
    finally
    {
        if (arialFont != null)
        {
            arialFont.Dispose();
        }
    }
    ```
    &#x2705; GÖR SÅ HÄR:
    ```csharp
    using (var arialFont = new Font("Arial", emSize: 10.0f))
    {
        var gdiCharSet = arialFont.GdiCharSet;
    } 
    ```
    * [using Statement (C# Reference)](https://msdn.microsoft.com/en-us/library/yh598w02.aspx)

    &#x1F3F7; `IDisposable` `using` 
1. Exceptions  
Använd `try`-`catch` och `finally` där du vet att det finns risk att undantag uppstår och du vet att du kan göra något åt det. Undvik det annars.

    Ett exception är inte detsamma som ett fel. Om ett exception uppstår har något oväntat hänt. Ta en metod som under normala omständigheter alltid fungerar. Men om minnet tar slut kommer `OutOfMemoryException` att kastas vilket är ett exempel på något oväntat.

    Undvik att använda den generella `Exception`-klassen, skapa istället en egen som ärver från ApplicationException. Avsluta alltid egna klasser med ordet Exception (`public UserNotFoundException: Exception {}`).

    &#x274C; UNDVIK:
    ```csharp
    public User ValidateUser(string userName, string password)
    {
        if (!UserExists(userName)) throw new UserNotFoundException();
 
        if (!IsValid(userName, password)) throw new InvalidCredentialsException();
 
        return GetUser(userName);
    }
    ```
    &#x2705; GÖR SÅ HÄR:
    ```csharp
    public ValidationResult ValidateUser(string userName, string password)
    {
        if (userName == null) return new ValidationResult(ValidationStatus.UserNameIsEmpty);
        if (password == null) return new ValidationResult(ValidationStatus.PasswordIsEmpty);
 
        if (!UserExists(userName)) return new ValidationResult(ValidationStatus.UserNotFound);
 
        if (!IsValid(userName, password))
        {
            return new ValidationResult(ValidationStatus.InvalidPassword);
        }
 
        var user = GetUser(userName);
        if (user == null) throw new InvalidOperationException(GetUserShouldNotReturnNull);
 
        var validationResult = new ValidationResult(ValidationStatus.Valid, user);
 
        return validationResult;
    }
    ```

    Om du kastar vidare ett specifikt fångat undantag, kommer man bara att få reda på att felet uppstod i aktuell metod. Det ursprungliga felet kommer gå förlorat. Istället, använd endast `throw` i dessa lägen.

    &#x274C; UNDVIK:
    ```csharp
    public void RunDataOperation()
    {
        try
        {
            Intialize();
            ConnectDatabase();
            Execute();
        }
        catch (Exception exception)
        {
            throw exception;
        }
    }
    ```
    &#x2705; GÖR SÅ HÄR:
    ```csharp
    public void RunDataOperation()
    {
        try
        {
            Intialize();
            ConnectDatabase();
            Execute();
        }
        catch (Exception)
        {
            throw;
        }
    }
    ```
    * [Best practices for exceptions](https://docs.microsoft.com/en-us/dotnet/articles/standard/exceptions#best-practices-for-exceptions)
    * [Exceptions and Exception Handling (C# Programming Guide)](https://msdn.microsoft.com/en-us/library/ms173160.aspx)
    * [Design Guidelines for Exceptions](https://msdn.microsoft.com/en-us/library/ms229014(v=vs.110).aspx)
    * [C# Coding Guidelines (5) Exceptions](https://weblogs.asp.net/dixin/csharp-coding-guidelines-5-exceptions)
    * [Guidelines for Exception Handling in C#](http://intellitect.com/exceptionguidelinesforcsharp/)
    * [Why Exceptions should be Exceptional](http://mattwarren.org/2016/12/20/Why-Exceptions-should-be-Exceptional/)
    * [Exception Handling Best Practices in .NET](https://www.codeproject.com/Articles/9538/Exception-Handling-Best-Practices-in-NET)
    * [Handling Exceptions and Errors. Part 1 – Intro.](http://www.engineerspock.com/2015/09/21/handling-errors-and-exceptions-part-1-intro/)
    * [Handling Errors and Exceptions. Part 2 – Discussion.](http://www.engineerspock.com/2015/10/02/handling-errors-and-exceptions-part-2-discussion/)
    * [Handling Errors and Exceptions in C#. Part 3](http://www.engineerspock.com/2016/10/24/handling-error-and-exceptions-part-3/)
    * [Throw Often, Catch Rarely](https://helloacm.com/throw-often-catch-rarely/)
    * [C# Exception Handling Best Practices](https://stackify.com/csharp-exception-handling-best-practices/)
    * [Custom exception types](http://enterprisecraftsmanship.com/2016/12/08/custom-exception-types/)

     &#x1F3F7; `Exception` `try` `catch` `finally`
1. Lägga ihop strängar  
Det finns flera sätt att sätta ihop strängar. Här är några tumregler:
    1. Sex eller färre strängar: använd `+`, string interpolation eller `string.Format`.
    1. Över sex strängar men där man på förhand vet antal element: använd `string.Concat`.
    1. Över sex strängar och okänt antal: använd `StringBuilder`.  

    &#x2139; EXEMPEL:
    ```csharp
    // "+"
    var stringPlus = "Lorem " + "ipsum " + "dolor " + "sit " + "amet";

    // string.Format
    var stringFormat = string.Format({0} {1} {2} {3} {4}, "Lorem", "ipsum", "dolor", "sit", "amet");
            
    // String interpolation
    var person = GetPersion(id);
    var stringInterpolation = $"Name: {person.FirstName} {person.LastName}, age: {person.Age}";
            
    // string.Concat
    var stringConcat = string.Concat("Lorem ", "ipsum ", "dolor ", "sit ", "amet, ", "consectetur ", "adipiscing ", "elit. ", "Morbi ", "lacinia ", "auctor ", "augue, ", "ac ", "tempus ");
               
    // StringBuilder
    var products = GetProducts();
    var stringBuilder = new StringBuilder();
    foreach (var product in products)
    {
        stringBuilder.Append(product.Name).AppendLine();
    }
    ```    

    * [5 ways to concatenate strings with C# .NET](https://dotnetcodr.com/2015/11/27/5-ways-to-concatenate-strings-with-c-net-2/)
    * [Adventures in Benchmarking - Memory Allocations](http://mattwarren.org/2016/02/17/adventures-in-benchmarking-memory-allocations/)
    * [String concatenation behind the scenes, part one](https://ericlippert.com/2013/06/17/string-concatenation-behind-the-scenes-part-one/), [part two](https://ericlippert.com/2013/06/24/string-concatenation-behind-the-scenes-part-two/)
    * [Most efficient way to concatenate strings?](http://stackoverflow.com/questions/21078/most-efficient-way-to-concatenate-strings)
    * [The Difference Between String and StringBuilder in C#](https://www.codeproject.com/Articles/1194964/The-Difference-Between-String-and-StringBuilder-in)

    &#x1F3F7; `string.Format` `String interpolation` `string.Concat` `StringBuilder`
1. Magiska strängar  
Undvik magiska strängar och tal eftersom det oftast är svårt att förstå dess innebörd. Använd `const`- och `readonly` medlemmar där det är möjligt. Ett tips är också att placera ofta använda konstanter i en egen konstantklass.

    &#x274C; UNDVIK:
    ```csharp
    if (currentOrderAmount > 10000)
    {
        return true;
    }
    ```
    &#x2705; GÖR SÅ HÄR:
    ```csharp 
    int const OrderAmountLimit = 10000;
    
    if (currentOrderAmount > OrderAmountLimit)
    {
        return true;
    }
    ```

    &#x274C; UNDVIK:
    ```csharp
    if (role == "Architect")
    {
        return ...
    }
    
    if (role == "Tester")
    {
        return ...
    }
    
    if (role == "Developer")
    {
        return ...
    }
    ```
    &#x2705; GÖR SÅ HÄR:
    ```csharp 
    public static class Role
    {
        public const string Architect = "Architect";
        public const string Tester = "Tester";
        public const string Developer = "Developer";
    }

    if (role == Role.Architect)
    {
        return ...
    }
    
    if (role == Role.Tester)
    {
        return ...
    }
    
    if (role == Role.Developer)
    {
        return ...
    }
    ```

    * [Magic Strings – No More!](https://blog.goyello.com/2014/12/30/magic-strings-no-more/)
    * [Eliminating Magic Strings in ASP.NET MVC](https://daveaglick.com/posts/eliminating-magic-strings)
    * [const (C# Reference)](https://msdn.microsoft.com/en-us/library/e6w8fe1b(v=vs.140).aspx)
    * [readonly (C# Reference)](https://msdn.microsoft.com/en-us/library/acdd6hb7(v=vs.100).aspx)
    * [C# CONSTANTS BEST PRACTICE](http://codebender.denniland.com/c-constants-best-practice/)
    * [Difference Between Const, ReadOnly and Static ReadOnly in C#](http://www.c-sharpcorner.com/UploadFile/c210df/difference-between-const-readonly-and-static-readonly-in-C-Sharp/)
    * [Some ways to tame magical strings in .NET and C#](https://danielwertheim.se/some-ways-to-tame-magical-strings-in-net-and-c/)

    &#x1F3F7; `magic strings` `readonly` `const`
 1. Använd as vid typekonvertering  
Att använda `as` ger bättre prestanda och kräver mindre kod än `try`/`catch`-metoden. Använd inte `is` och `as` i kombination eftersom det inte behövs.

    &#x274C; UNDVIK:
    ```csharp
    object a = 10;

    try
    {
        Class1 c1 = (Class1)a;
    }
    catch (InvalidCastException)
    {
        // Incorrect conversion
    }
    ```
    &#x2705; GÖR SÅ HÄR:
    ```csharp
    object a = 10;

    Class1 c1 = a as Class1;
    if (c1 == null)
    {
        // Incorrect conversion
    }
    ```  
    
    * [Using as vs casting in C#](http://theburningmonk.com/2010/04/net-tips-using-as-vs-casting-in-csharp/)
    * [Type conversion in C#](http://www.computerprogrammingtutorial.com/2016/03/type-conversion-in-c.html)
    * [CA1800: Do not cast unnecessarily](https://msdn.microsoft.com/en-us/library/ms182271.aspx)
    * [Casting and Type Conversions (C# Programming Guide)](https://msdn.microsoft.com/en-us/library/ms173105.aspx)
 
    &#x1F3F7; `as` `is` `Casting` `Type Conversions` 
1. Undvik boxing/unboxing  
Ibland är boxing nödvändigt, men du bör undvika det om möjligt eftersom det ger sämre prestanda och ökar minneskraven.  
    _(Typkonvertering är inte boxing eller unboxing, men det kan orsaka det ena eller det andra. En `int` är inte en `Class1`, det vill säga `int` ärver inte eller utökar inte `Class1`. Det betyder att du inte kan konvertera `int` till `Class1`. Typkonvertering orsakar konvertering bara om det är möjligt att göra det. Du kan gå från en `int` till en `double` och vice versa. Men du kan inte gå från en `int` till `Class1`.)_

    &#x274C; UNDVIK:
    ```csharp
    public class ClassA
    {
        public string Name {get; set;}
    }
    
    public class ClassB : ClassA
    {
    }

    private ClassA TransformClassBToClassA()
    {
        var classB = new ClassB {Name = "Name from classB"};
        
        var classA = (ClassA)classB;

        return classA;
    }
    ```  

    &#x2705; GÖR SÅ HÄR:
    ```csharp
    public class ClassA
    {
        public string Name {get; set;}
    }
    
    public class ClassB : ClassA
    {
    }

    private ClassA TransformClassBToClassA()
    {
        var classB = new ClassB {Name = "Name from classB"};
            
        var classA = classB as ClassA;

        return classA;
    }
    ```

    * [Understanding Boxing and Unboxing in C#](http://www.dotnettricks.com/learn/csharp/understanding-boxing-and-unboxing-in-csharp)
    * [Boxing and Unboxing (C# Programming Guide)](https://msdn.microsoft.com/en-us/library/yz2be5wk.aspx)
    * [Performance (C# and Visual Basic)](https://msdn.microsoft.com/en-us/library/ms173196.aspx)

    &#x1F3F7; `Boxing` `Unboxing` `Performance` 
1. Undvik out och ref  
Användning av `out`- eller `ref`-parametrar kräver erfarenhet av pekare, förståelse för hur värdetyper och referenstyper skiljer sig åt samt att man kan hantera metoder med flera returvärden. Dessutom är skillnaden mellan `out` och `ref` inte allmänt förstått. TryParse-metoder är ett undantag till regeln.
    
    &#x274C; UNDVIK:
    ```csharp
    public static void PassTheReference(ref string argument)
    {
        argument = argument + " ABCDE";
    }
    
    var argument = "12345";
    PassTheReference(ref argument);

    // argument = 12345 ABCDE
    ```  

    &#x2705; GÖR SÅ HÄR:
    ```csharp
    public static string BetterThanPassTheReference(string argument)
    {
        return argument + " ABCDE";
    }
    
    var argument = "12345";
    var newArgumentValue = BetterThanPassTheReference(argument);

    // newArgumentValue = 12345 ABCDE
    ```

    * [CA1021: Avoid out parameters](https://msdn.microsoft.com/en-us/library/ms182131.aspx)
    * [CA1045: Do not pass types by reference](https://msdn.microsoft.com/en-us/library/ms182146.aspx)
    * [Parameter Design -&gt; Parameter Passing](https://msdn.microsoft.com/en-us/library/ms229015(v=vs.110).aspx)

    &#x1F3F7; `out` `ref` `Performance` 
1. Any(), Count() > 0 eller Count > 0?  
Använd `Any()` för läsbarhetens skull, det är ett sätt att förklara sin intension. Om prestandan är superviktig rekommenderas det ofta att använda `Any()` framför `Count()` (extension metoden) men inte framför `Count` (egenskap). Förklaringen är att `Count` (egenskap) hämtar ett `int`-värde som sparats på heapen.

    &#x274C; UNDVIK:
    ```csharp
    var names = QueryForNames();
    if(names.Count() > 0) 
    {
       ...
    }
    ```
    &#x2705; GÖR SÅ HÄR:
    ```csharp
    var names = QueryForNames(); 
    if(names.Any()) 
    {
      ...
    }
    ```

    * [Enumerable.cs](https://referencesource.microsoft.com/#System.Core/System/Linq/Enumerable.cs,41ef9e39e54d0d0b,references)
    * [Which method performs better: .Any() vs .Count() > 0?](http://stackoverflow.com/questions/305092/which-method-performs-better-any-vs-count-0)
    * [ArrayList Count vs Any](http://stackoverflow.com/questions/23376225/arraylist-count-vs-any)
    * [What's the use of .Any() in a C# List<>?](http://softwareengineering.stackexchange.com/questions/296445/whats-the-use-of-any-in-a-c-list)
    * [Use Any() Instead of Count() To See if an IEnumerable Has Any Objects](http://firebreaksice.com/use-any-instead-of-count-to-see-if-an-ienumerable-has-any-objects/)
    * [List Any vs Count, which one is better for readability?](http://codereview.stackexchange.com/questions/27901/listt-any-vs-count-which-one-is-better-for-readability)
    * [List Any or Count?](http://stackoverflow.com/questions/5741617/listt-any-or-count)

    &#x1F3F7; `Any` `Count` `Enumerable` 
1. Välj rätt kollektionstyp  
Försök så långt det går att använda `IEnumerable` eller `IReadOnlyList` framför `IList<>`/`List<>` etc som returvärde från metoder. Är prestanda, storlek eller ordning viktig, undersök närmare vilken kollektionstyp som passar bäst tilländamålet.

    * [Guidelines for Collections](https://msdn.microsoft.com/en-us/library/dn169389%28v=vs.110%29.aspx?f=255&MSPPError=-2147217396)
    * [Selecting a Collection Class](https://msdn.microsoft.com/en-us/library/6tc79sx1(v=vs.110).aspx)
    * [Commonly Used Collection Types](https://msdn.microsoft.com/en-us/library/0ytkdh4s(v=vs.110).aspx)
    * [When To Use IEnumerable, ICollection, IList And List](http://www.claudiobernasconi.ch/2013/07/22/when-to-use-ienumerable-icollection-ilist-and-list/)
    * [C# Best Practices: Collections and Generics](https://app.pluralsight.com/library/courses/csharp-best-practices-collections-generics/table-of-contents)
    * [Difference Between IEnumerable, ICollection and IList Interface in C#](https://www.codeproject.com/Articles/1070991/Difference-Between-IEnumerable-ICollection-and-ILi)
    * [Best Practices Implementing IEnumerable Interface in C#](http://codinghelmet.com/?path=howto/best-practices-implementing-ienumerable-interface-in-cs)
    * [IEnumerable vs IReadOnlyList](http://enterprisecraftsmanship.com/2017/05/24/ienumerable-vs-ireadonlylist/)

1. Villkor (if-syntax)  
Sträva efter att spendera så lite tid som möjligt i en metod och placera den mest väntade processen först - det gör att det också blir mer lättläst.
    1. Undvik `else` genom att returnera värdet i samma ögonblick du vet vad det är.
    1. Försök undvika negationer i uttryck.
    1. Undvik nestlad kod med `if`-satser inuti `if`-satser (s.k. Arrow Anti Pattern).  

    &#x274C; UNDVIK:
    ```csharp
    private bool LoyaltyDiscountEligible(User user, short month, double currentOrderAmount)
    {
        bool returnValue = false;
 
        if (user != null)
        {
            if (month == 6 || month == 11)
            {
                if (user.UtilizedDiscountDuringLastwelveMonths)
                {
                    if (currentOrderAmount > 10000)
                    {
                        if (user.Credit)
                        {
                            if (user.LastTwelveMonthOrderSummary > 30000)
                            {
                                returnValue = true;
                            }
                        }
                    }
                }
            }
        }
 
        return returnValue;
    }
    ```
    &#x2705; GÖR SÅ HÄR:
    ```csharp
    private bool LoyaltyDiscountEligible(User user, short month, double currentOrderAmount)
    {
        var userIsLoggedIn = user != null;
        if (!userIsLoggedIn) return false;
 
        var inDiscountMoths = month == JuneAsNumber || month == NovemberAsNumber;
        if (!inDiscountMoths) return false;
 
        if (currentOrderAmount <= OrderAmountLimit) return false;
        if (!user.UtilizedDiscountDuringLastwelveMonths) return false;
        if (!user.Credit) return false;
        if (user.LastTwelveMonthOrderSummary < TwelveMonthOrderSummaryLimit) return false;
 
        return true;
    }
    ```

    * [Flattening Arrow Code](https://blog.codinghorror.com/flattening-arrow-code/)
    * [Observations on the ‘if’ statement](https://elegantcode.com/2009/08/14/observations-on-the-if-statement/)
    * [Anti-IF Campaign](http://cirillocompany.de/pages/anti-if-campaign)
    * [Best Practice on IF/ELSE Statement Order](http://stackoverflow.com/questions/1306158/best-practice-on-if-else-statement-order)
    * [Clean Code – Is my code always readable?](https://blog.goyello.com/2014/12/11/clean-code/)
    * [Don't use if-else statements instead of a simple (conditional) assignment](https://github.com/dennisdoomen/CSharpGuidelines/blob/master/Src/Guidelines/1500_MaintainabilityGuidelines.md#-dont-use-if-else-statements-instead-of-a-simple-conditional-assignment-av1545-)
    * [Branching Over A "Type Code" - A Code Smell](http://www.c-sharpcorner.com/article/branching-over-a-type-code-a-code-smell/)
    * [Clarification of “avoid if-else” advice [duplicate]](http://softwareengineering.stackexchange.com/questions/206816/clarification-of-avoid-if-else-advice)
    * [How to avoid multiple nested IFs](http://stackoverflow.com/questions/3666030/how-to-avoid-multiple-nested-ifs)
    * [Dude, are you still programming using if...then…else?](https://www.codeproject.com/Articles/12508/Dude-are-you-still-programming-using-if-then-else)
    * [How and Why to Avoid Excessive Nesting](https://www.codeproject.com/Articles/626403/How-and-Why-to-Avoid-Excessive-Nesting)
    * [Code Blocks and Nested Statements](https://www.devu.com/cs-asp/lesson-25-code-blocks-and-nested-statements/)
    * [Deep nesting of conditional Statements](https://books.google.se/books?id=xYgCAQAAQBAJ&pg=PA899&lpg=PA899&dq=c%23+if+else+nested+bad&source=bl&ots=FOclwKsY1g&sig=BOTlEEZwI7vNKSb5v8YVnHS4svc&hl=sv&sa=X&ved=0ahUKEwjyhN6-8cTRAhWBKCwKHYDnAD0Q6AEIYTAJ#v=onepage&q=c%23%20if%20else%20nested%20bad&f=false)

    &#x1F3F7; `if` `else` `nested` `Arrow Anti Pattern` 
1. Villkor och return på samma rad  
Om villkor och return-uttrycket tillsammans kan bli en kort rad och lätt kan läsas, placera dem på samma rad. Anledningen är att man på det sättet kan spara hela tre rader vilket gör att metoden blir mindre.
 
1. Villkor på en rad och retur-uttryck på nästa rad  
Retur-uttryck som inte är placerade på samma rad som `if`, måste inneslutas av måsvingar (`{…}`).

1. Linq, foreach eller for?  
Använd linq och metodsyntax (lambda) om det är möjligt. Det brukar innebära minst kod samtidigt som den också är läsbar. 

    &#x274C; UNDVIK:
    ```csharp
    private decimal GetTotalOrderSummary(IEnumerable<CustomerInfo> customers)
    {
        decimal totalOrderSummary = 0;
 
        foreach (var customer in customers)
        {
            foreach (var order in customer.Orders)
            {
                foreach (var orderRow in order.OrderRows)
                {
                    totalOrderSummary += orderRow.Amount;
                }
            }
        }
 
        return totalOrderSummary;
    }
    ```
    &#x2705; GÖR SÅ HÄR:
    ```csharp
    private decimal GetTotalOrderSummary(IEnumerable<CustomerInfo> customers)
    {
        var totalOrderSummary = customers
            .SelectMany(o => o.Orders)
            .SelectMany(r => r.OrderRows)
            .Sum(s => s.Amount);
 
        return totalOrderSummary;
    }
    ```
    * [=> Operator (C# Reference)](https://msdn.microsoft.com/en-us/library/bb311046.aspx)
    * [How to: Use Lambda Expressions in a Query (C# Programming Guide)](https://msdn.microsoft.com/en-us/library/bb397675.aspx)
    * [LINQ Query Expressions (C# Programming Guide)](https://msdn.microsoft.com/en-us/library/bb397676.aspx])
    * [LINQ Fundamentals with C# 6.0](https://www.pluralsight.com/courses/linq-fundamentals-csharp-6)
    * [Unleash the Power of LINQ, the .NET Way](https://www.edureka.co/blog/unleash-the-power-of-linq-the-net-way/)
    * [Why LINQ?](http://www.tutorialsteacher.com/linq/why-linq)
    * [The pitfalls of LINQ deferred execution](https://marcusclasson.com/2014/08/18/the-pitfalls-with-linq-deferred-execution/)
    * [Parallel LINQ (PLINQ)](http://www.csharpstar.com/csharp-parallel-linq/)
    * [LINQ Tips and Tricks](http://markheath.net/post/linq-tips-and-tricks)
    * [Optimising LINQ](http://mattwarren.org/2016/09/29/Optimising-LINQ/)

    &#x1F3F7; `foreach` `for` `LINQ` `Lambda Expressions` 
1. Undvik #if-direktiv för miljövariabler  
Undvik `#if`-direktiv för att ange miljöer som dev, stage, pre-production och production. Använd istället konfigurationer och transformeringar.

    * [#if DEBUG vs. Conditional(“DEBUG”)](http://stackoverflow.com/questions/3788605/if-debug-vs-conditionaldebug)
    * [C# Preprocessor Directives](https://msdn.microsoft.com/en-us/library/ed8yd1ha.aspx)

1. Kryptera känslig information  
Använd klasser som `SecureString` för att hålla hemlig information i minnet. Använd beprövad krypteringsalgoritmer för att spara personnummer och annat i databaser, filer etc.

    * [SecureString Class](https://msdn.microsoft.com/en-us/library/system.security.securestring(v=vs.110).aspx)
    * [System.Security.Cryptography Namespace](https://msdn.microsoft.com/en-us/library/system.security.cryptography(v=vs.110).aspx)

    &#x1F3F7; `SecureString` 
1. Begränsa tillgängligheten till typer  
Sätt typer (klasser, medlemmar, metoder etc) till `private` som standard, om de inte ska användas utanför din klass. Sätt typer till `internal` om de ska användas inom samma assembly osv.

    * [Access Modifiers (C# Programming Guide)](https://msdn.microsoft.com/en-us/library/ms173121.aspx)

    &#x1F3F7; `Access Modifiers` `public` `private` 
1. Använd string.Empty  
Använd `string.Empty` istället för två `""` (citationstecken), för att tilldela en sträng tomt värde eller jämföra strängar. 

    &#x274C; UNDVIK:
    ```csharp
    var text = "";
    ```
    &#x2705; GÖR SÅ HÄR:
    ```csharp
    var text = string.Empty;
    ```
    * [SA1122: UseStringEmptyForEmptyStrings](http://stylecop.soyuz5.com/SA1122.html)

    &#x1F3F7; `string.Empty` 
1. Använd inte .ToLower()  
Använd inte `.ToLower()` när du jämför strängar. Det skapas då ytterligare en temporär sträng i bakgrunden. Använd istället `string.Compare` som har inbyggt stöd för skiftkänslighet och kultur.

    &#x274C; UNDVIK:
    ```csharp
    var string1 = "Hello world!";
    var string2 = "Hello Sweden!";
    
    if(string1.ToLower() == string2.ToLower())
    {
        // The strings match.
    }
    else
    {
        // The strings do not match.
    }
    ```
    &#x2705; GÖR SÅ HÄR:
    ```csharp
    var string1 = "Hello world!";
    var string2 = "Hello Sweden!";
    
    var compareResult = string.Compare(string1, string2, StringComparison.OrdinalIgnoreCase);
    if(compareResult == 0)
    {
        // The strings match.
    }
    else
    {
        // The strings do not match.
    }
    ```
    * [String.Compare Method](https://msdn.microsoft.com/en-us/library/system.string.compare(v=vs.110).aspx)
    * [How to: Compare Strings (C# Programming Guide)](https://msdn.microsoft.com/en-us/library/cc165449.aspx)

    &#x1F3F7; `string.Compare` 
1. Objektinitialiserare  
Använd objektinitialiserare när nytt objekt initieras vars medlemmar kräver värden.

    Men använd ännu hellre konstruktorer från klassen som ska konsumera objekttypen. Och om du har en klass med många medlemmar, undersök om de hör ihop eller kan kapslas in i mindre klasser för att uppnå att typen bara har ett ansvarsområde.

    &#x274C; UNDVIK:
    ```csharp
    var person = new Person();
    person.Id = Guid.NewGuid(); 
    person.FirstName = "Stefan";
    person.LastName = "Johansson";
    person.Phone = "+46701234567";
    ```
    &#x2705; GÖR SÅ HÄR:
    ```csharp
    var person = new Person();
    {
        Id = Guid.NewGuid(); 
        FirstName = "Stefan";
        LastName = "Johansson";
        Phone = "+46701234567";
    }
    ```

    * [Object and Collection Initializers (C# Programming Guide)](https://msdn.microsoft.com/en-us/library/bb384062.aspx)

    &#x1F3F7; `Initializers` 
1. Instanisera objekt  
Sträva efter att instanisera objekt framför att konsumera statiska klasser. Anledningen är att man med ett instansiserat objekt kan använda Dependency Injection. DI i sin tur behövs för att kunna skriva bra enhetstester.

1. Skriv ut parameternamn  
Använd "named argument" för metoder där man inte har variabler/enums som man skickar in som parametrar.

    &#x274C; UNDVIK:
    ```csharp
    using (var streamWriter = new StreamWriter("test.txt", false))
    { 
        // ...
    }
    ```
    &#x2705; GÖR SÅ HÄR:
    ```csharp
    using (var streamWriter = new StreamWriter("test.txt", append: false))
    { 
        // ...
    }
    ```

    * [Specify optional parameter names even though not required?](http://softwareengineering.stackexchange.com/questions/307773/specify-optional-parameter-names-even-though-not-required)
    * [Named and Optional Arguments (C# Programming Guide)](https://msdn.microsoft.com/en-us/library/dd264739.aspx)
    * [Boolean parameters and code readability](https://www.codeproject.com/Articles/1182980/Boolean-parameters-and-code-readability)

    &#x1F3F7; `named argument` 
1. Använd Elvis-operatorn  
Använd `?.` för att hålla nere antal rader i metoder.

    &#x274C; UNDVIK:
    ```csharp
    Child child = null;

    var item = this.Parent;  
    if (item != null)  
    {  
        item = item.Child;  
        if (item != null)  
        {  
            item = item.Child;  
            if (item != null)  
            {  
                child = item.Child;  
            }  
        }  
    }

    if (child != null)
    {…}
    ```
    &#x2705; GÖR SÅ HÄR:
    ```csharp
    var child = parent?.child?.child?.child;  
    if (child != null)
    {...}
    ```

    * [Null-conditional Operators (C# and Visual Basic)](https://msdn.microsoft.com/en-us/library/dn986595.aspx?f=255&MSPPError=-2147217396)

    &#x1F3F7; `Null-conditional Operators` 
1. Komplicerade kod i return-uttryck  
Undvik att ha komplicerade uttryck i retursatser. Sträva efter att returnera en variabel som tidigare tilldelats. Syftet med det är att lättare kunna debugga/felsöka i framtiden. Genom att göra på det här sättet behöver man inte debugga klart metoden och få värdet först i den anropande metoden. En annan bonus är att man kan använda variabeln för att ytterligare uttrycka vad man har gjort (hämtat/beräknat). Du är helt enkelt snäll mot nästa utvecklare.

    &#x274C; UNDVIK:
    ```csharp
    public IEnumerable<SupportPage> Search(string searchTerm, int startPageId)
    {
        return SearchClient.Instance.Search<SupportPage>(Language.Swedish)
            .For(searchTerm)
            .AddWildCardQuery(searchTerm, x => x.Name)
            .AddWildCardQuery(searchTerm, x => x.Tags)
            .AddWildCardQuery(searchTerm, x => x.Keywords)
            .AddWildCardQuery(searchTerm, x => x.SearchText())
            .CommonFilter(startPageId)
            .BoostMatching(x => x.Tags.AnyWordBeginsWith(searchTerm), boost: 2)
            .Track()
            .GetContentResult();
    }
    ```
    &#x2705; GÖR SÅ HÄR:
    ```csharp
    public IEnumerable<SupportPage> Search(string searchTerm, int startPageId)
    {
        var contentResult = SearchClient.Instance.Search<SupportPage>(Language.Swedish)
            .For(searchTerm)
            .AddWildCardQuery(searchTerm, x => x.Name)
            .AddWildCardQuery(searchTerm, x => x.Tags)
            .AddWildCardQuery(searchTerm, x => x.Keywords)
            .AddWildCardQuery(searchTerm, x => x.SearchText())
            .CommonFilter(startPageId)
            .BoostMatching(x => x.Tags.AnyWordBeginsWith(searchTerm), boost: 2)
            .Track()
            .GetContentResult();
 
        return contentResult;
    }
    ```

1. Undvik att förändra parametervärden   
Undvik att förändra parametrar som skickas in i metoder. Och om det är oundvikligt, använd metodnamn som börjar på Populate, Set etc.

1. Använd var  
Använd `var` när typen är uppenbar eller vetskapen om vilken typ det är inte är viktig. Harmonisera till övriga variabeldeklarationer i aktuell metod (om alla typer är definierade, definiera den nya också). Lägg extra energi på namngivningen av variabeln, eftersom det är den man läser längre ner i koden. Ett annat skäl till att använda `var` är att distraktionen inte blir lika stor vid läsning framför en typ som är deklarerad som exempelvis `Dictionary<string, List<string>>`.

    &#x274C; UNDVIK:
    ```csharp
    XmlNodeList itemList = rssNode.SelectNodes("item”);
    ```
    &#x2705; GÖR SÅ HÄR:
    ```csharp
    var nodeListItems = rssNode.SelectNodes("item");
    ```

    * [Implicitly Typed Local Variables (C# Programming Guide)](https://msdn.microsoft.com/en-us/library/bb384061.aspx)

    &#x1F3F7; `var` 
1. Använd "ternary operator"  
Använd s.k. ternary operator för att minska antal kodrader.

    &#x274C; UNDVIK:
    ```csharp
    var greeting = "Good”;
    const string evening = "evening";
    const string day = "day”;
    const int eveningLimit = 17;
            
    var now = DateTime.UtcNow;
    if (now.Hour > eveningLimit)
    {   
        greeting += " " + evening + ".";
    }
    else
    {   
        greeting += " " + day + ".";
    }
    ```
    &#x2705; GÖR SÅ HÄR:
    ```csharp
    var greeting = "Good";
    const string evening = "evening";
    const string day = "day”;
    const int eveningLimit = 17;
            
    var now = DateTime.UtcNow;
    greeting = now.Hour > eveningLimit ? $"{greeting} {evening}." : $"{greeting} {day}.";
    ```

    * [Ternary operator](https://www.dotnetperls.com/ternary)

    &#x1F3F7; `Ternary operator` `?`
1. Egenskaper vs metoder  
Generellt sätt representerar metoder handlingar och egenskaper data. Egenskaper är avsedda att användas som fält, vilket betyder att de inte bör vara beräkningsmässigt komplexa eller skapa sidoeffekter. Använd egenskap när medlemmen är en logisk datamedlem, använd metoder i alla andra fall. Exempel på användningsområde kan vara att sätta ihop för- och efternamn för att bilda en ny egenskap. Man kan också tänka sig att trimma texter eller göra avrundningar, för att att visa i gränssnitt.

    * [Property Design](https://msdn.microsoft.com/en-us/library/ms229006(v=vs.110).aspx)
    * [C# Property vs. Method Guidelines](http://firebreaksice.com/csharp-property-vs-method-guidelines/)
    * [Properties vs. Methods](http://geekswithblogs.net/abhi/archive/2013/11/20/properties-vs.-methods.aspx)
    * [Properties vs Methods](https://stackoverflow.com/questions/601621/properties-vs-methods)
    * [Exposing Member Objects As Properties or Methods in .NET](https://stackoverflow.com/questions/601621/properties-vs-methods)
    * [When to use a property vs a method?](https://stackoverflow.com/questions/1854352/when-to-use-a-property-vs-a-method)
    * [Best practices: throwing exceptions from properties](https://stackoverflow.com/questions/1488472/best-practices-throwing-exceptions-from-properties)
    * [Using Properties (C# Programming Guide)](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/using-properties)


#### ASP.NET MVC
1. Undvik backendkod i vyer  
Undvik att placera backendlogik i vyer (cshtml). Det finns dock två undantag:
    1. Val av CSS-klasser utifrån objekt som kommer från backend.
    1. `switch`-satser för att välja partials att visa.

1. Metoder i Razor-vyer  
Om backendkoden blir lite längre enligt punkt ett ovan, använd functions och helpers för att kapsla in logik och rendering.

    &#x2139; EXEMPEL:
    ```html

    <div class="button-with-popup" style="text-align: @GetButtonAlign()">
    ...
    </div>

    @functions {
	
        public string GetButtonAlign()
        {
            var align = string.Empty;
            switch (Model.ButtonAlign)
            {
                case ButtonAlign.Left:
                    align = "left";
                    break;
                case ButtonAlign.Center:
		    align = "center";
                    break;
                case ButtonAlign.Right:
                    align = "right";
                    break;
            }

            return align;
        }
    }
    ```

1. Små kontrollermetoder  
Låt kontrollermetoderna vara små vilket gör att det blir enklare att testa logiken med att hämta modell i en separat metod. På det här sättet tydliggörs dessutom Model-View-Controller-konventionen.

    &#x274C; UNDVIK:
    ```csharp
    // Placeholder.
    ```
    &#x2705; GÖR SÅ HÄR:
    ```csharp
    // Placeholder.
    ```

1. Ingen logik i vymodller  
En vymodell bör aldrig vara ansvarig för att populera sig själv. Dvs, det ska aldrig finnas logik i dessa. Det kan göras undantag för exempelvis properties, för att exempelvis trimma en text eller liknande.
