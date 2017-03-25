

Hur ska man kunna hålla reda på alla designmönster, principer, riktlinjer, konventioner, akronymer och praxis när man kodar? För att inte tala om företagsstandarder, teamöverenskommelser och besynnerliga saker som externa beroenden försätter dig i?

Alla utvecklares dröm är att få börja på ett nytt blankt blad. Med nyvunnen erfarenhet från senaste projektet vill man den här gången göra rätt från början. I realiteten har man inte möjlighet till nystart särskilt ofta, men det finns massor med roliga saker att göra i en lösning som förvaltas. Jag lovar!
Jag är en varm anhängare av att skriva läsbar kod, konsekvent formatering samt att aldrig sluta refaktorera. Jag har också lärt mig på senare tid att kodgranskning, och de diskussioner det brukar resultera i, höjer kvalitén mer än man först anar.


Så, hur är denna artikel tänkt att fungera? Vad är den och vad är den inte? Punkterna utgår från en webblösning med Visual Studio, C#, ASP.NET, epi och ReSharper. De tar upp saker som ofta diskuteras i team eller är typiska som missas i kod. Det är inte en komplett redogörelse för SOLID eller designmönster. De finns andra med djuplodade artiklar för det. Den tar inte heller upp några riktlinjer för frontend-utveckling med JavaScript, CSS etcetera

***
### Mindset

_"Always code as if the guy who ends up maintaining your code will be a violent psychopath who knows where you live."_ / John F. Woods, 1991-09-25

_"Any fool can write code that a computer can understand. Good programmers write code that humans understand."_ / Martin Fowler. Refactoring: Improving the design of existing code.

***
### Namnkonventioner

Om inget annat sägs eller andra teamöverenskommelser finns, följ Microsofts namngivning, dokumentation och guider. Harmonisera med .NET ramverket.

* [Naming Guidelines](http://www.dofactory.com/reference/csharp-coding-standards)
* C# Coding Standards and Naming Conventions

***
### Språkkonventioner och checklista - generellt

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
    // Platshållare
    ```

1. Onårbar kod  
Kontrollera om det finns kod som inte kan nås och ta bort den om så skulle vara fallet. ReSharper markerar sådan kod som nedtonad grå.

1. Varningar vid byggen  
Kontrollera och åtgärda varningar som visas när projekten byggs. Tillse att "Enable Code Analysis on Build" är ikryssat på respektive projekt.

1. using direktiv  
Ta bort och sortera using-direktiv som inte längre används.
    ```csharp
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;

1. 
