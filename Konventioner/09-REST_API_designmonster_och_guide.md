## 09. REST API designmönster och guide  

### Inledning

Denna artikel beskriver en målbild för hur man vill att api:er ska se ut och fungera. I grund och botten bör man följa det som är norm inom API-design, men det finns också utrymme för vissa anpassningar. Denna guide är inte en komplett redogörelse för hur REST eller REST API:er fungerar. Här lyfts istället det som man i team ofta diskuterar samt vad som är extra aktuellt och viktigt.

### Terminilogi

Ett REST API är en samling av individuellt adresserbara resurser. Resurser refereras med sina resursnamn och manipuleras genom en uppsättning metoder (även känt som verb eller operationer). 

Resource/resurs = en del av data exempelvis en "order".  
Collection/kollektion = en grupp av resurser såsom "orders".  
URL = identifierar platsen för en resurs eller kollektion.

### Praxis

1. Använd substantiv för resursnamn.  
1. Undvik verb i resurs-url:er, använd motsvarande HTTP metod istället.
1. Använd gemener genomgående i url:er.
1. Använd s.k. "kebab-case"/"spinal-case" med "-" för att separera ord i url:er.
1. Använd s.k. "camelCase” för att definiera parametrar. Exempel: /orders/{orderId}
1. Använd versionsnummer. Exempel: /v1/orders/{orderId}
1. Använd header-data för inloggningsinformation (<a href="https://en.wikipedia.org/wiki/JSON_Web_Token" target="_blank">jwt</a>), applikationsversioner, format (json) etc.
1. Använd plural för att peka ut kollektioner. Exempelvis: /orders
1. Använd s.k. query-string för att hämta delmängder av ett större resultat eller för att sortera.
1. Använd "/" för att navigeria i hirakier, men avsluta utan "/".
1. Undvik specialtecken i url:er.

Mönsterexempel:

<table>
<thead>
	<tr>
		<th>HTTP metod</th>
		<th>API DNS-namn</th>
		<th>Version</th>
		<th>Kollektionsid</th>
		<th>Resursid</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>GET</td>
		<td>http://rest-api.azurewebsites.net</td>
		<td>/v1</td>
		<td>/orders</td>
		<td>/{orderId}</td>
	</tr>
</tbody>
</table>

<table>
<thead>
	<tr>
		<th>HTTP metod</th>
		<th>API DNS-namn</th>
		<th>Version</th>
		<th>Kollektionsid</th>
		<th>Resursid</th>
		<th>Operation</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>POST</td>
		<td>http://rest-api.azurewebsites.net</td>
		<td>/v1</td>
		<td>/orders</td>
		<td>/{orderId}</td>
	    <td>/accept</td>
	</tr>
</tbody>
</table>

### Svarsmeddelanden och felkoder
Använd <a href="https://www.iana.org/assignments/http-status-codes/http-status-codes.xhtml" target="_blank">HTTP-statuskoder</a> vid alla svar på anrop, och returnera dem som header-info. Returnera data i bodyn, i json-format.

### Swagger  
Använd <a href="https://swagger.io/blog/api-strategy/difference-between-swagger-and-openapi/" target="_blank">Swagger/Open API</a> för att, så långt det är möjligt, automatiskt dokumentera API:er. 

### Version  
Använd <a href="https://en.wikipedia.org/wiki/Software_versioning#Semantic_versioning" target="_blank">semantisk versionering</a> (major, minor, patch) som grund för att versionera api:er. En ändring i ett api handlar oftast om att man bryter kontrakt och vill stödja flera klientversioner. Använd därför formatet vX i url:er, vilket motsvarar version X.0.0 (en major-ändring).

### Referenser

* <a href="https://github.com/microsoft/api-guidelines/blob/vNext/Guidelines.md" target="_blank">Microsoft REST API Guidelines</a> 
* <a href="https://stackoverflow.blog/2020/03/02/best-practices-for-rest-api-design/" target="_blank"> Best practices for REST API design</a>
* <a href="https://slack.engineering/how-we-design-our-apis-at-slack/" target="_blank">How We Design Our APIs at Slack</a>
* <a href="https://cloud.google.com/apis/design" target="_blank">API design guide  |  Cloud APIs  |  Google Cloud</a>
* <a href="https://swagger.io/resources/articles/best-practices-in-api-design/" target="_blank">Best Practices in API Design</a>