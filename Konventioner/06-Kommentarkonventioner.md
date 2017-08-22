## 6. Kommentarkonventioner

1. Undvik kommentarer   
I möjligaste mån, undvik att skriva kommentarer. Lägg istället energi på att beskriva din intention i namn på metoder,  variabler och dela upp kod på ett förståeligt sätt. 

    * <a href="https://visualstudiomagazine.com/articles/2013/06/01/roc-rocks.aspx" target="_blank">Why You Shouldn't Comment (or Document) Code</a>
    * [Comments in Clean Code? Think Documentation](http://www.daedtech.com/comments-clean-code-think-documentation/)
    * [Don’t document your code. Code your documentation.](https://dev.to/raddikx/dont-document-your-code-code-your-documentation)
    * [Fighting Evil in Your Code: Comments on Comments](https://www.simple-talk.com/opinion/opinion-pieces/fighting-evil-code-comments-comments/)

    **Undantag till denna rekommendation:**
1. Märkning av kod som behöver förändras med "TODO".  
TODO-kommentarer skrivs enligt mönstret:  
    `[//][mellanslag][TODO:][mellanslag][Text som börjar med stor bokstav och slutar med punkt.]`

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
    * <a href="Show off your API with a little Swagger..." target="_blank">Show off your API with a little Swagger...</a>
   
    
***
<span style="float:left">&#x25C0; <a href="05-Layoutkonventioner.md">Layoutkonventioner</a></span>  |  <span style="float:right"><a href="07-CSharp-konventioner_och_checklista.md">C#-konventioner och checklista</a> &#x25B6;</span>
