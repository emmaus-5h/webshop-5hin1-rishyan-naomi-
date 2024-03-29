# antekeningen

1. Aanpassen APi
    Zie video 5
Mapje api/index.js
rgeele: app.get('/api/products') geet aan waar de web de vraag aaan de api vraagt en getproduct geeft de code die de vraag beantwoord. In getProducts staat de sql query voor de database
regel  const sqlOpdracht = db.prepare('SELECT products.id AS id, products.name AS name, products.description AS description, products.code AS code,products.amount AS amount, products.price AS price FROM products ORDER BY id ASC')
pas de query aan, zodat de extra velden door uit de database worden opgevraagd. Gebruik altijd 'AS' bij 1:n moet je join gebruiken  


3. Aanpassen web
    Zie video 6

  web/index.html
  onder de regel  <!-- template for product info--> staat het template voor een product het teplate wordt voor elke product gekopieerd.
  als je een veld toevoegd aan de template dan moet je de waarde erin laten zetten.
  Dat doe je 



























Deze repo is onderdeel van het vak informatica op het Emmauscollege Rotterdam.

[Meer info over deze opdracht](https://informatica.emmauscollege.nl/)

# Basis uitleg hoe de webshop werkt
The basic idea is that a webpage of the shop is loaded by the browser and information on the articles in the shop are added to that depending on what the user selects.

1. You open a browser and navigate to the webshop. 
2. The browser downloads the html and css files from the server. It also downloads a piece of javascript code.
3. The javascript code is being executed by the browser. The javascript code connects to a link on the server that is connected to the api. This is called a REST-interface. Through the REST interface, the javascript code in the browser request information on the articles it needs to display.
4. The api is a programm on the server which connects to the database. It requests information from the database and sends it back to the browser. The result is sent in json-format.
5. The javascript programm in the browser looks at the json-file and adds elements containing articels in the shop to the DOM. The DOM is the model of the html files that the browser keeps in it memory and shows to the user. These elements added are displayed by the browser.

An alternative approach would be to have the server build complete web-pages including all information on articles. This is the idea behind the php programming language. The REST-interface is gaining popularity. An advantage of REST above php is that REST allows for more responsive (interfactive) websites.

# Uitleg hoe je de webshop kunt aanpassen 

## Server opnieuw starten
__Codespaces__ <br>
Gebruik het terminal window te zien zijn.<br>
Stop de server door typen van [CRTL]+[C].<br>
Start de server met het volgene commando.<br>
```
bash start.sh
```
Om de server te (her)starten kun je ook de start knop gebruiken die je ziet als je op het "run en debug" icoon in de iconenbalk links op het scherm drukt.

__Replit__<br>
druk op de groene "Run"-knop<br>

__Gitpod__<br>
Gebruik het terminal window waar de server-berichten te zien zijn.
Stop de server door typen van [CRTL]+[C].<br>
Start de server met het volgene commando
```
bash start.sh
```
## Wijzigingen aanbrengen in de database
Wijzig de sql-commando's in het bestand db/create.sql<br>
Start de server opnieuw (zie elders hoe dat moet) nadat de sql-commando's gewijzigd zijn. Zo zorg je ervoor dat de database opnieuw gemaakt wordt door de nieuwe sql-commando's uit te voeren.

## Fouten zoeken in de database
Open de database in de terminal met het volgende commando
```
sqlite3 db/my.db
```
Je kunt met SQL commanda's zien wat er in de database staat.<br>
Bijvoorbeeld het commando: `SELECT * from Products;` (vergeet de ; aan het einde niet)

Meer handige commando's:<br>
- Een lijstje met tabellen `.tables`
- De namen van de kolommen in de tabel products: `.schema products`
- De eerste 3 rijen van de tabel products: `SELECT * FROM products LIMIT 3;`
- sqlite3 afsluiten: `.quit`

## Fouten zoeken in de api
Je kunt het antwoord van de api testen door achter de link naar je webshop /api/products te typen, bijvoorbeeld:<br>
`https://....-8080.app.github.dev/api/products` (voor codespaces, pas aan voor jouw webshop-adres)<br>
`https://....repl.co/api/products` (voor replit, pas aan voor jouw webshop-adres)<br>
`https://....gitpod.io/api/products` (voor gitpod, pas aan voor jouw webshop-adres)

Bekijk de terminal (codespaces en gitpod) of console (replit) van de server, daar kun je foutmeldingen zien.
Je kunt in de code in de map api opdrachten toevoegen die inhoud van variabelen afdrukken. Bijvoorbeeld:
```
console.log("Waarde van i is ", i);
```
Start de server opnieuw (zie elders hoe dat moet) nadat de code gewijzigd is.

## Fouten zoeken in de webpages
Bekijk de console in de browser, daar kun je foutmeldingen zien.<br>
In Chrome open je de console in het menu -> Weergave -> Ontwikkelaar -> JavaScript-console. <br>
Je kunt in de code op strategische plaatsen de volgende opdracht toevoegen:
```
debugger
```
Als de console open staat dan stopt de browser met het uitvoeren van code als hij het debugger commando tegenkomt. Je kunt dan via de console opdrachten geven. Je kunt de inhoud van variabelen bekijken met de opdracht:
```
console.log("Waarde van i is ", i);
```

## Mail configureren in Replit
__er zijn afgelopen jaar dingen in replit veranderd, waardoor je je webshop op dit moment geen mail kunt laten sturen__
De shop mailt elke order die geplaatst is.
Mailen werkt niet in gitpod, omdat verkeer over de smtp-port geblokkeerd wordt.
Mailen door de shop in replit werkt als volgt.
Zet de environment variabelen (slotje links in replit menu)
```
GMAIL_EMAIL=<email account>
GMAIL_PASSWORD=<email wachtwoord>
ORDER_MAIL_TO=<jouw email waar je orders ontvangt>
```

Als je gmail gebruikt zonder tweestapsverificatie:<br>
Zet in gmail (account->beveiliging) gebruik van minder veilige apps aan

Als je gmail gebruikt met tweestapsverificatie:<br>
Maak een app-wachtwoord (account->beveiliging) en zet dat in GMAIL_PASSWORD

Test je emailconfiguratie:<br>
Doe een bestelling en kijk naar de console in replit of gitpod. 
De api meldt op de console als mail succesvol is verzonden en geeft een foutmelding als het niet is gelukt.

# Uitleg over bestanden en mappen

## db folder
Database with information on the arcticles in the shop. The commands in the db.sql file build te database. The database is build everytime start.sh is executed. 

## web folder
Static (non changing) html, css en js files.

## api folder
js files which are being executed on the server when the api is called

## start.sh
Dit bestand bevat de commando's om de webshop (opnieuw) te starten. Je voert dit bestand uit in de terminal met het commando
```
bash start.sh
```

## .devcontainer en .vscode folder
Mappen met de configuratie voor Codespaces

## .replit en replit.nix
Bestanden met de configuratie voor replit<br>
We use a bash-repl (language="bash" in .replit file), because bash has sqlite3 and nodejs installed. Downside of bash-repl: The nodejs-repl installs packages automatically by scanning your code. In the bash-repl we have to maintain dependencies in a packages file manually. 

## .gitpod.yml
Bestand met de configuratie voor replit<br>

# Uitleg van code
De code is voorzien van commentaar op punten waar de werking misschien niet eenvoudig te volgen is.
We gaan er vanuit dat je basiskennis hebt over html, css en Javascript. Dit heb je geleerd in de vierde klas. 
In deze webshop worden een aantal technieken gebruikt die je niet in de vierde hebt gehad. Die lichten we kort toe.

## functies als parameters
Bij de aanroep van een functie kun je variabelen meegeven als parameter. 
Dit ken je van de vierde klas.
Je kunt ook functies meegeven als parameter. 
In Javascript wordt dit veelvuldig gebruikt.

## asynchrone functies
In de meeste programmeertalen wordt code van boven naar beneden uitgevoerd. 
In Javascript wordt soms met de volgende opdracht doorgegaan voordat de vorige klaar is. 
Als de vorige klaar is dan wordt er een functie aangeroepen die als parameter is meegegeven aan de vorige opdracht.
Deze functie wordt een callback genoemd.
Het gebruik van callbacks is een krachtige functionaliteit van Javascript maar voor beginnende programmeurs lastig te doorgronden. 
Een callback wordt bijvoorbeeld gebruikt bij het versturen van mail.

## html templates
Je kunt Javascript gebruiken om extra elementen aan je webpagina toe te voegen nadat deze geladen is. 
Een veelgebruikte manier daarvoor is het opnemen van een stukje template in het html bestand (html tussen <template> en </template>)
Het template wordt niet door de browser getoond, maar het stuk html in het template kan in Javascript worden gekopieerd (gecloned) en aangepast.
Dit wordt bijvoorbeeld gebruikt bij het tonen van artikelen in de shop.

# Vraag en antwoord

## port forwarden met Codespaces
Op school zit er een fout in het netwerk, gebruik daar dit trucje om de port naar de server te openen:

- Knip de link van je Codespace boven in je browser naar een nieuw tabblad (de link lijkt op https://xxxxxx-xxxxxx-xxxxxx.github.dev)
- Verander de link in https://xxxxxx-xxxxxx-xxxxxx-8080.app.github.dev (dus voeg -8080.app toe)
- Je ziet nu de webpagina die je in je codespace gemaakt hebt. Vergeet niet de server te starten.
    
## Letop als je replit gebruikt!
1. Als je de repo importeert in replit, dan moet je de taal "bash" kiezen.
Dit kies je nadat je de link naar de repo hebt opgeven en voordat je op de import knop drukt.
2. Het voorbeeld van je webshop in Webview toont geen artikelen.
Open het voorbeeld in een apart tab (klik in Webview op icoontje met vierkant en pijl).

# Documentatie 

* tutorial building a REST-api with postgressDB + jsnode + jsexpress<br>
https://blog.logrocket.com/setting-up-a-restful-api-with-node-js-and-postgresql-d96d6fc892d8/
* serving static files with jsexpress<br>
https://expressjs.com/en/starter/static-files.html
* basic html & css & javascript reference<br>
https://www.w3schools.com
* basic sql course<br>
https://www.khanacademy.org/computing/computer-programming/sql
* sqlite3 gebruiken op in Shell<br>
https://www.sqlite.org/cli.html
* better-sqlite library gebruiken in nodejs (javascript)<br>
https://github.com/JoshuaWise/better-sqlite3/blob/HEAD/docs/api.md
* shoppping basket lokaal opslaan<br>
google op local storage javascript basket
* bestelling mailen<br>
video met gebruik van nodemailer (module in javascript) vind je hier: https://youtu.be/Va9UKGs1bwI
* replit online editor en hosting ontwikkelomgeving<br>
https://docs.replit.com/
* gitpod online editor en hosting ontwikkelomgeving<br>
https://www.gitpod.io/docs/
* introduction to docker (kennis alleen nodig als je de repo heftig wilt aanpassen)<br>
https://docker-curriculum.com
* yarn (kennis alleen nodig als je de repo heftig wilt aanpassen)<br>
https://yarnpkg.com/getting-started

# Credits
- avs123a<br>
for a "Simple inventory list example with crud using : NodeJS, express framework, pug template, sqlite database and bootstrap". See https://github.com/avs123a/NodeJS-simple-example
- Robert Bakker [Notalifeform](https://www.gihub.com/Notalifeform)<br>
for help almost 24x7 with many questions and problems and providing basic shop called gitpodnode to be further developed by students on gitpod and deplyed freely on heroku. See https://gitpod.io/#https://github.com/Notalifeform/gitpodnode




