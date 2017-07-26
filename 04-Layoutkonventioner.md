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
