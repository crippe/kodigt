# Checklista för C# utvecklare - beta 0.5
![https://www.gizmodo.com.au/2016/01/this-woman-was-a-bored-button-pusher-before-jane-jetson-was-even-born/](https://github.com/crippe/kodigt/blob/master/wiki/images/RCA-computer-room-1959.jpg)
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
Hur ska man kunna hålla reda på alla designmönster, principer, riktlinjer, konventioner, akronymer och praxis när man kodar? För att inte tala om företagsstandarder, teamöverenskommelser och besynnerliga saker som externa beroenden försätter dig i?

Alla utvecklares dröm är att få börja på ett nytt blankt blad. Med nyvunnen erfarenhet från senaste projektet vill man den här gången göra rätt från början. I realiteten har man inte den möjligheten särskilt ofta. Jag skulle vilja påstå att det  finns massor med roliga saker att göra i en lösning som förvaltas. Refaktorera, skala bort, namnändra, prestandaförbättra och skriva fler tester gör dig till en hjälte/hjältinna. Det kommer bli ett nöje för andra att kodgranska. Ingen är emot förbättrad kodkvalité!

Så, hur är denna artikel tänkt att fungera och användas? Vad är den och vad är den inte? Punkterna utgår oftast från en typisk webblösning med Visual Studio, C#, ASP.NET och ReSharper. Artikeln tar upp ämnen som ofta diskuteras i team eller är typiska detaljer som missas i kod. Artikeln kan också fungera som underlag när man vill sätta upp kodpraxis i team. Tänker man samma? Mest av allt är det en kom-ihåg-lista att gå igenom innan man gör pull request/checka in/merga. Det är inte en komplett redogörelse för språket C#, SOLID, designmönster eller TDD. De finns andra mer djuplodade böcker och kurser för det. Den tar inte heller upp några riktlinjer för frontend-utveckling med JavaScript-ramverk, CSS etcetera. 
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

1. Namn på olika typer  
    Namnge typer enligt nedan.

    Language element&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|Casing&nbsp;&nbsp;&nbsp;&nbsp;|Example
    --------------------|----------|:-----------
    Class, Struct|Pascal|`AppDomain`
    Interface | Pascal | `IBusinessService`
    Enumeration type | Pascal | `ErrorLevel` |
    Enumeration values | Pascal | `FatalError` |
    Event | Pascal | `Click` |
    Private field | Camel | `listItem` |
    Protected field | Pascal | `MainPanel` |
    Constant field | Pascal | `MaximumItems` |
    Constant Local variable | Camel | `maximumItems` |
    Read-only static field | Pascal | `RedValue` |
    Local Variable | Camel | `listOfValues` |
    Method | Pascal | `ToString` |
    Namespace | Pascal | `System.Drawing` |
    Parameter | Camel | `typeName` |
    Type Parameter | Pascal | `TView` |
    Property | Pascal | `BackColor` |

    I ReSharper är det definierat på detta sätt som standard:  
    ![ReSharper Naming Style](https://github.com/crippe/kodigt/blob/master/wiki/images/resharper-naming-style.png?raw=true)

1. StyleCop-regler för namngivning  
Här är är de StyleCop-regler som finns för namngivning av medlemmar, typer och variabler:
    * [SA1301: ElementMustBeginWithLowerCaseLetter](http://stylecop.soyuz5.com/SA1301.html)
    * [SA1302: InterfaceNamesMustBeginWithI](http://stylecop.soyuz5.com/SA1302.html)
    * [SA1303: ConstFieldNamesMustBeginWithUpperCaseLetter](http://stylecop.soyuz5.com/SA1303.html)
    * [SA1304: NonPrivateReadonlyFieldsMustBeginWithUpperCaseLetter](http://stylecop.soyuz5.com/SA1304.html)
    * [SA1305: FieldNamesMustNotUseHungarianNotation](http://stylecop.soyuz5.com/SA1305.html)
    * [SA1306: FieldNamesMustBeginWithLowerCaseLetter](http://stylecop.soyuz5.com/SA1306.html)
    * [SA1307: AccessibleFieldsMustBeginWithUpperCaseLetter](http://stylecop.soyuz5.com/SA1307.html)
    * [SA1308: VariableNamesMustNotBePrefixed](http://stylecop.soyuz5.com/SA1308.html)
    * [SA1309: FieldNamesMustNotBeginWithUnderscore](http://stylecop.soyuz5.com/SA1309.html)
    * [SA1310: FieldNamesMustNotContainUnderscore](http://stylecop.soyuz5.com/SA1310.html)

Referenser:
* [Naming Guidelines](http://www.dofactory.com/reference/csharp-coding-standards)
* [C# Coding Standards and Naming Conventions](http://www.dofactory.com/reference/csharp-coding-standards)
* [StyleCop - Wikipedia](https://en.wikipedia.org/wiki/StyleCop)
***
### Layoutkonventioner

1. Ordning i fil  
Sträva efter att ordna medlemmar i en fil enligt StyleCop regel [SA1201: ElementsMustAppearInTheCorrectOrder](http://stylecop.soyuz5.com/SA1201.html).  
    
    | StyleCop                                                                                                                                                                                                                                                                                                                        	| ReSharper 	|
    |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|---------------------	|
    | På rotnivån ser det ut så här:<ul><li>Extern Alias Directives</li><li>Using Directives</li><li>Namespaces</li><li>Delegates</li><li>Enums</li><li>Interfaces</li><li>Structs</li><li>Classes</li></ul>  <br>Inuti en class, struct eller interface ordnas det enligt följande:<ul><li>Inuti en class, struct eller interface ordnas det enligt följande:</li><li>Fields</li><li>Constructors</li><li>Finalizers (Destructors)</li><li>Delegates</li><li>Events</li><li>Enums</li><li>Interfaces</li><li>Properties</li><li>Indexers</li><li>Methods</li><li>Structs</li><li>Classes</li></ul>   	| ![File layout - ReSharper - StyleCop](https://github.com/crippe/kodigt/blob/master/wiki/images/file-layout-resharper-stylecop.png?raw=true) 	|

    Två saker kan man fokusera på:
    1. Sortera metoder i bokstavsordning och placera alla publika först.
    1. Sortera medlemmar i klasser i bokstavsordning.

1. Klasser läggs i separata filer  
Se vidare i: [SA1402: FileMayOnlyContainASingleClass](http://stylecop.soyuz5.com/SA1402.html)

1. Indrag  
Använd fyra (4) mellanslag istället för tabb i filer.  
    Se vidare i: [SA1027: TabsMustNotBeUsed](http://stylecop.soyuz5.com/SA1027.html)

1. Tomrader mellan element  
Ha alltid en tomrad mellan element. Det gäller såväl mellan metoder som kodblock. Ett block kan vara ett **if**-uttryck eller **foreach** osv.  
    Se vidare i: [SA1516: ElementsMustBeSeparatedByBlankLine](http://stylecop.soyuz5.com/SA1516.html)

1. Flera tomrader  
Undvik flera tomrader på rad.  
    Se vidare i: [SA1507: CodeMustNotContainMultipleBlankLinesInARow](http://stylecop.soyuz5.com/SA1507.html)
 
1. Regioner  
Undvik att använda regioner.  
    Se vidare i: [SA1124: DoNotUseRegions](http://stylecop.soyuz5.com/SA1124.html)
    * [C# regions is a design smell](http://enterprisecraftsmanship.com/2015/12/08/c-regions-is-a-design-smell/) 

1. Beräkning och kontroll  
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
***
### Kommentarkonventioner

I möjligaste mån, undvik att skriva kommentarer. Lägg istället energi på att beskriva din intention i namn på metoder,  variabler och dela upp kod på ett förståeligt sätt. Det finns några undantag till rekommendationen:
1. Märkning av kod som behöver förändras med "TODO".  
TODO-kommentarer skrivs enligt mönstret:  
    **[//][mellanslag][TODO:][mellanslag][Text som börjar med stor bokstav och slutar med punkt.]** 

    &#x2139; EXEMPEL:
    ```csharp
    // TODO: En kommentar.
    ```
1. Beskrivning av skeenden, flöden etc som ligger utanför lösningens kontroll och som inte på ett bra och enkelt sätt kan beskrivas i kod.

1. Vid skapande av API  
Om du skapar ett ASP.NET Web API är dokumentation en del av lösningen.

    * [Creating Help Pages for ASP.NET Web API](https://docs.microsoft.com/en-us/aspnet/web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages) 
    * [Swashbuckle - Swagger for WebApi 5.5.3](https://github.com/domaindrivendev/Swashbuckle)
    * [RESTful Web API Help Documentation using Swagger UI and Swashbuckle](https://www.codeproject.com/Articles/1078249/RESTful-Web-API-Help-Documentation-using-Swagger-U)

Referenser:  
* [SA1005: SingleLineCommentsMustBeginWithSingleSpace](http://stylecop.soyuz5.com/SA1005.html)
* [Comments in Clean Code? Think Documentation](http://www.daedtech.com/comments-clean-code-think-documentation/)
* [Don’t document your code. Code your documentation.](https://dev.to/raddikx/dont-document-your-code-code-your-documentation)
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
    &#x2705; GÖR SÅ HÄR:
    ```csharp
    // Placeholder.
    ```

1. Onårbar kod  
Kontrollera om det finns kod som inte kan nås och ta bort den om så skulle vara fallet. ReSharper markerar sådan kod som nedtonad grå.

1. Varningar vid byggen  
Kontrollera och åtgärda varningar som visas när projekten byggs. Tillse att "Enable Code Analysis on Build" är ikryssat på respektive projekt.

1. using direktiv  
Sortera och ta bort **using**-direktiv som inte längre används.
    ```csharp
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;

1. Returnera inte null  
Returnera instansierade objekt framför null i metoder. Var noga att kontrollera objekt som ändå kan vara null.
    * [How to Avoid Returning Null from a Method](http://www.codinghelmet.com/?path=howto/avoid-returning-null)
    * [Tactical Design Patterns in .NET: Control Flow -&gt; Motivation to Avoid Null Reference](https://app.pluralsight.com/player?course=tactical-design-patterns-dot-net-control-flow&author=zoran-horvat&name=tactical-design-patterns-dot-net-control-flow-m2&clip=0&mode=live)
    * [My takeaways from “Clean Code” -> Don’t Pass Null](https://medium.com/@webprolific/my-takeaways-from-clean-code-a70ca8382884)
    * [Is it Really Better to 'Return an Empty List Instead of null'? / Part 1](https://www.codeproject.com/Articles/794448/Is-it-Really-Better-to-Return-an-Empty-List-Instea), [Part 2](https://www.codeproject.com/Articles/797453/Is-it-Really-Better-to-Return-an-Empty-List-Inst), [Part 3](https://www.codeproject.com/Articles/820066/Is-it-Really-Better-to-Return-an-Empty-List-Inst), [Part 4](https://www.codeproject.com/Articles/834677/Is-it-Really-Better-to-Return-an-Empty-List-Inst)

1. Konsekvent kod  
Deklarera typer på samma sätt genom hela lösningen. Använd inte både **Int32** och **int** eller **String** och **string**.
    
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
1. Använd using-block  
Använd using-block för **IDisposable** objekt.

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
    * [ using Statement (C# Reference)](https://msdn.microsoft.com/en-us/library/yh598w02.aspx)

1. Exceptions  
Använd **try**-**catch** och **finally** där du vet att det finns risk att undantag uppstår och du vet att du kan göra något åt det. Undvik det annars.

    Ett exception är inte detsamma som ett fel. Om ett exception uppstår har något oväntat hänt. Ta en metod som under normala omständigheter alltid fungerar. Men om minnet tar slut kommer **OutOfMemoryException** att kastas vilket är ett exempel på något oväntat.

    Undvik att använda den generella **Exception**-klassen, skapa istället en egen som ärver från ApplicationException. Avsluta alltid egna klasser med ordet Exception (**public UserNotFoundException: Exception {}**).

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
 
1. Lägga ihop strängar  
Det finns flera sätt att sätta ihop strängar. Här är några tumregler:
    1. Sex eller färre strängar: använd "**+**", string interpolation eller **string.Format**.
    1. Över sex strängar men där man på förhand vet antal element: använd **string.Concat**.
    1. Över sex strängar och okänt antal: använd **StringBuilder**.  
    
    * [5 ways to concatenate strings with C# .NET](https://dotnetcodr.com/2015/11/27/5-ways-to-concatenate-strings-with-c-net-2/)
    * [Adventures in Benchmarking - Memory Allocations](http://mattwarren.org/2016/02/17/adventures-in-benchmarking-memory-allocations/)
    * [String concatenation behind the scenes, part one](https://ericlippert.com/2013/06/17/string-concatenation-behind-the-scenes-part-one/)
    * [Most efficient way to concatenate strings?](http://stackoverflow.com/questions/21078/most-efficient-way-to-concatenate-strings)

1. Magiska strängar  
Undvik magiska strängar och tal eftersom det oftast är svårt att förstå dess innebörd. Använd const- och readonly medlemmar där det är möjligt. Ett tips är också att placera ofta använda konstanter i en egen konstantklass.

    * [const (C# Reference)](https://msdn.microsoft.com/en-us/library/e6w8fe1b(v=vs.140).aspx)
    * [readonly (C# Reference)](https://msdn.microsoft.com/en-us/library/acdd6hb7(v=vs.100).aspx)
    * [C# CONSTANTS BEST PRACTICE](http://codebender.denniland.com/c-constants-best-practice/)
    * [Difference Between Const, ReadOnly and Static ReadOnly in C#](http://www.c-sharpcorner.com/UploadFile/c210df/difference-between-const-readonly-and-static-readonly-in-C-Sharp/)

 1. Använd as vid typekonvertering  
Att använda **as** ger bättre prestanda och kräver mindre kod än **try**/**catch**-metoden. Använd inte **is** och **as** i kombination eftersom det inte behövs.

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
 
1. Undvik boxing/unboxing  
Ibland är boxing nödvändigt, men du bör undvika det om möjligt eftersom det ger sämre prestanda och ökar minneskraven.  
    _(Typkonvertering är inte boxing eller unboxing, men det kan orsaka det ena eller det andra. En **int** är inte en **Class1**, det vill säga **int** ärver inte eller utökar inte **Class1**. Det betyder att du inte kan konvertera **int** till **Class1**. Typkonvertering orsakar konvertering bara om det är möjligt att göra det. Du kan gå från en **int** till en **double** och vice versa. Men du kan inte gå från en **int** till **Class1**.)_


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

1. Undvik out och ref  
Användning av **out**- eller **ref**-parametrar kräver erfarenhet av pekare, förståelse för hur värdetyper och referenstyper skiljer sig åt samt att man kan hantera metoder med flera returvärden. Dessutom är skillnaden mellan **out** och **ref** inte allmänt förstått. TryParse-metoder är ett undantag till regeln.
    

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

1. Any(), Count() > 0 eller Count > 0?  
Använd **Any()** för läsbarhetens skull, det är ett sätt att förklara sin intension. Om prestandan är superviktig rekommenderas det ofta att använda **Any()** framför **Count()** (extension metoden) men inte framför **Count** (property). Förklaringen är att **Count** (property) hämtar ett **int**-värde som sparats på heapen.

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

1. Välj rätt kollektionstyp  
Försök så långt det går att använda **IEnumerable** framför **IList<>**/**List<>** etc som returvärde från metoder. Är prestanda, storlek eller ordning viktig, undersök närmare vilken kollektionstyp som passar bäst tilländamålet.

    * [Guidelines for Collections](https://msdn.microsoft.com/en-us/library/dn169389%28v=vs.110%29.aspx?f=255&MSPPError=-2147217396)
    * [Selecting a Collection Class](https://msdn.microsoft.com/en-us/library/6tc79sx1(v=vs.110).aspx)
    * [Commonly Used Collection Types](https://msdn.microsoft.com/en-us/library/0ytkdh4s(v=vs.110).aspx)
    * [When To Use IEnumerable, ICollection, IList And List](http://www.claudiobernasconi.ch/2013/07/22/when-to-use-ienumerable-icollection-ilist-and-list/)
    * [C# Best Practices: Collections and Generics](https://app.pluralsight.com/library/courses/csharp-best-practices-collections-generics/table-of-contents)
    * [Difference Between IEnumerable, ICollection and IList Interface in C#](https://www.codeproject.com/Articles/1070991/Difference-Between-IEnumerable-ICollection-and-ILi)
    * [Best Practices Implementing IEnumerable Interface in C#](http://codinghelmet.com/?path=howto/best-practices-implementing-ienumerable-interface-in-cs)

1. Villkor (if-syntax)  
Sträva efter att spendera så lite tid som möjligt i en metod och placera den mest väntade processen först - det gör att det också blir mer lättläst.
    1. Undvik **else** genom att returnera värdet i samma ögonblick du vet vad det är.
    1. Försök undvika negationer i uttryck.
    1. Undvik nestlad kod med **if**-satser inuti **if**-satser (s.k. Arrow Anti Pattern).  

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

1. Villkor och return på samma rad  
Om villkor och return-uttrycket tillsammans kan bli en kort rad och lätt kan läsas, placera dem på samma rad. Anledningen är att man på det sättet kan spara hela tre rader vilket gör att metoden blir mindre.
 
1. Villkor på en rad och retur-uttryck på nästa rad  
Retur-uttryck som inte är placerade på samma rad som villkor (if), måste inneslutas av måsvingar (**{…}**).

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

1. Undvik #if-direktiv för miljövariabler  
Undvik #if-direktiv för att ange miljöer som dev, stage, pre-production och production. Använd istället konfigurationer och transformeringar.

    * [#if DEBUG vs. Conditional(“DEBUG”)](http://stackoverflow.com/questions/3788605/if-debug-vs-conditionaldebug)
    * [C# Preprocessor Directives](https://msdn.microsoft.com/en-us/library/ed8yd1ha.aspx)

1. Kryptera känslig information  
Använd klasser som SecureString för att hålla hemlig information i minnet. Använd beprövad krypteringsalgoritmer för att spara personnummer och annat i databaser, filer etc.

    * [SecureString Class](https://msdn.microsoft.com/en-us/library/system.security.securestring(v=vs.110).aspx)
    * [System.Security.Cryptography Namespace](https://msdn.microsoft.com/en-us/library/system.security.cryptography(v=vs.110).aspx)

1. Begränsa tillgängligheten till typer  
Sätt typer (klasser, medlemmar, metoder etc) till **private** som standard, om de inte ska användas utanför din klass. Sätt typer till **internal** om de ska användas inom samma assembly osv.

    * [Access Modifiers (C# Programming Guide)](https://msdn.microsoft.com/en-us/library/ms173121.aspx)

1. Använd string.Empty  
Använd **string.Empty** istället för två "" (citationstecken), för att tilldela en sträng tomt värde eller jämföra strängar. 
Se vidare i [SA1122: UseStringEmptyForEmptyStrings](http://stylecop.soyuz5.com/SA1122.html)

1. Använd inte .ToLower()  
Använd inte **.ToLower()** när du jämför strängar. Det skapas då ytterligare en temporär sträng i bakgrunden. Använd istället **string.Compare** som har inbyggt stöd för skiftkänslighet och kultur.

    * [String.Compare Method](https://msdn.microsoft.com/en-us/library/system.string.compare(v=vs.110).aspx)
    * [How to: Compare Strings (C# Programming Guide)](https://msdn.microsoft.com/en-us/library/cc165449.aspx)

1. Objektinitialiserare  
Använd objektinitialiserare när nytt objekt initieras vars medlemmar kräver värden.

    En rekommendation är att hellre konstruktorer från klassen som ska konsumera objekttypen. Om du har en klass med många medlemmar, undersök om de hör ihop eller kan kapslas in i mindre klasser för att uppnå att typen bara har ett ansvarsområde.

    * [Object and Collection Initializers (C# Programming Guide)](https://msdn.microsoft.com/en-us/library/bb384062.aspx)

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

1. Metoder och många parametrar  
Antal parametrar i metodsignaturer bör vara runt fyra (4). Om det blir fler, skapa en s.k. "wrapper"-klass istället som används som parameter. Använd konstruktorn i wrapper-klassen framför att objektinitialisera den.

    * [How many parameters are too many?](http://stackoverflow.com/questions/174968/how-many-parameters-are-too-many)
    * [How many parameters in C# method are acceptable?](http://stackoverflow.com/questions/12431932/how-many-parameters-in-c-sharp-method-are-acceptable)
 
1. Använd Elvis-operatorn  
Använd **?.** för att hålla nere antal rader i metoder.

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

1. Undvik långa metoder  
Undvik metoder som är längre än 15-20 rader. Men, det är bara ett riktmärke. Det kan finnas skäl till att en metod är längre än så.
Se vidare här: [How long should a single method be?](http://enterprisecraftsmanship.com/2017/01/19/how-long-should-a-single-method-be/)

1. Refaktorera klasser  
Dela upp klasser när de bryter mot SRP (Single Responsibility Principle). En klass ska ha ett ansvar och syfte.

1. Undvik att förändra parametervärden   
Undvik att förändra parametrar som skickas in i metoder. Och om det är oundvikligt, använd metodnamn som börjar på Populate, Set etc.

1. Använd var  
Använd **var** när typen är uppenbar eller vetskapen om vilken typ det är inte är viktig. Harmonisera till övriga variabeldeklarationer i aktuell metod (om alla typer är definierade, definiera den nya också). Lägg extra energi på namngivningen av variabeln, eftersom det är den man läser längre ner i koden. Ett annat skäl till att använda **var** är att distraktionen inte blir lika stor vid läsning framför en typ som är deklarerad som exempelvis **Dictionary<string, List<string>>**.

    &#x274C; UNDVIK:
    ```csharp
    XmlNodeList itemList = rssNode.SelectNodes("item”);
    ```
    &#x2705; GÖR SÅ HÄR:
    ```csharp
    var nodeListItems = rssNode.SelectNodes("item");
    ```

    * [Implicitly Typed Local Variables (C# Programming Guide)](https://msdn.microsoft.com/en-us/library/bb384061.aspx)

#### ASP.NET MVC
1. Undvik backendkod i vyer  
Undvik att placera backendlogik i vyer (cshtml). Det finns dock två undantag:
    1. Val av CSS-klasser utifrån objekt som kommer från backend.
    1. **switch**-satser för att välja partials att visa.

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
