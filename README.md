# Serverside programmering
## Individuellt projekt

### Uppgift
Du ska bygga en webbserver med **Node.js**, **Express** och **MongoDB**.

### Kravspec
Göteborgaren Berra behöver uppgradera sin båtaffär. Han vill ha en webbshop där man kan söka på och köpa båtar. Men innan man kan bygga en frontend vill han ha ett API. Din uppgift är att registrera båtarna i en databas och bygga ett API för det.

För att Berra ska kunna kontrollera att API:et fungerar som det ska behöver det finnas en databas. För att man inte ska behöva lägga in all data manuellt varje gång man byter server, ska du göra skript som lägger in data i databasen.

---

#### Databas
Databasen ska använda MongoDB. Den ska innehålla minst 10 båt-dokument med olika värden.

---
#### Datamodell
En båt har följande egenskaper:
* id - skapas av databasen!
* modellnamn - sträng med upp till 64 tecken
* tillverkningsår - heltal
* pris - flyttal (tal med decimaler)
* segelbåt - kan vara ja/nej
* motor - kan vara ja/nej
* bild URL - *level up*

---

#### API spec
API:et ska ha följande *endpoints*:

|Resurs    |Metod   |Förväntat svar|
|----------|--------|---|
|/         | GET    |Servar frontend (senare)|

Denna endpoint serverar en minimal index.html.
```
http://localhost:3000/
http://localhost:3000/index.html
```
<br>

|Resurs    |Metod   |Förväntat svar|
|----------|--------|---|
|/assets/  | GET    |Servar bilder (statiska resurser, *level up*)|

En *level up* som ska kunna strömma bilder till klienten.
```
http://localhost:3000/assets/boat001.jpg
```
<br>

|Resurs    |Metod   |Förväntat svar|
|----------|--------|---|
|/boats/   | GET    |Returnerar en array med alla båtar|

Använd denna för att kontrollera vad som finns i databasen. När databasen växer är det ineffektivt att hämta *alla* dokument, men det är okej i den här uppgiften eftersom vi inte har så många dokument.
```
http://localhost:3000/boats/
[
    { id: '001', model: 'Nimbus C9', ... },
    { id: '002', model: 'Candela Seven', ''' },
    ...
]
```
<br>

|Resurs    |Metod   |Förväntat svar|
|----------|--------|---|
|/boat/:id | GET    |Returnerar en båt med efterfrågat id|
|/boat/    | POST   |Sparar ett båt-objekt i databasen|
|/boat/:id | DELETE |Tar bort en båt från databasen|
|/boat/    | PUT    |Uppdaterar en befintlig båt - *level up*|

CRUD-operationer på datan. Man ska kunna lägga till, hämta eller ta bort ett båt-dokument ur databasen med hjälp av dessa endpoints. <br><br>
Enstaka värden kan skickas med *querystring*, men POST och PUT kommer att skicka hela båt-objekt. Använd *request body* i stället för querystring.
```
http://localhost:3000/boat/001 (GET)
http://localhost:3000/boat/    (POST har data i request body)
http://localhost:3000/boat/001 (DELETE)
http://localhost:3000/boat/    (PUT har data i request body)
```
<br>

|Resurs    |Metod   |Förväntat svar|
|----------|--------|---|
|/search/  | GET    |Returnerar upp till fem sökträffar|

```
Alla querystring-parametrar är valfria.
http://localhost:3000/search/?word=nimbus
http://localhost:3000/search/?word=nimbus&maxprice=30000&is_sail=yes&has_motor=yes
http://localhost:3000/search/?has_motor=yes&order=lowprice
```

##### Sökning
Man ska använda querystring för att tala om vad man söker efter. API:et ska hantera följande parametrar:
* **word** - en sträng med ett ord som måste finnas i modellnamnet
* **maxprice** - högsta tillåtna priset
* **is_sail** - yes/no, om det är en segelbåt *[level up]*
* **has_motor** - yes/no, om den har motor *[level up]*
* **madebefore** - måste vara tillverkad före detta år *[level up]*
* **madeafter** - måste vara tillverkad efter detta år *[level up]*
* **order** - vilken sorteringsnyckel som ska användas *[level up]*

Exempel: en sökning på `word=ara` matchar både `BaRa` och `Skaraborg`.

Sökresultatet ska sorteras med hjälp av sorteringsnyckeln:
* `lowprice` - lägst pris först
* `name_asc` - modellnamn, stigande i bokstavsordning
* `name_desc` - modellnamn, fallande i bokstavsordning
* `oldest` - äldst båt först, dvs fallande efter ålder
* `newest` - yngst båt först

Exempel: `order=lowprice` ska sortera resultatet så den billigaste båten visas först.

---

#### Level ups
1. Minst 20 dokument i databasen
1. Node-skript som återställer databasen (tar bort allt och lägger in alla dokument igen)
1. Enkel Vanilla JavaScript-app som demonstrerar API-funktioner
1. Ändra ett båt-dokument i databasen med ett PUT request
1. Varje båtobjekt i databasen har en URL till en bild
1. Bilderna finns i databasen
1. Fler alternativ på sökning
1. Publicera uppgiften på nätet, till exempel med hjälp av Netlify eller Heroku

### Bedömning
Utdrag ur kursplanen:
> För betyget Godkänd ska den studerande
> * Visa grundläggande förståelse för server side programmering

> För betyget Väl Godkänd ska den studerande:
> * Uppnått kraven för betyget godkänt
> * Visa god förståelse för server side programmering

För godkänt på uppgiften ska du göra ett projekt som följer kravspecifikationen.

För väl godkänt ska du dessutom visa att du har en *god förståelse*. Detta gör du genom att implementera tillräckligt många *Level ups*. Både kvalitet (hur bra) och kvantitet (hur många) kommer att tas med i bedömningen.

### Inlämning
Lämna in uppgiften genom att skicka ett meddelande till läraren via slack. Tala om vilka level ups du har gjort. Om du har publicerat uppgiften så ska du skicka länk till den också. Exempel:

> Här är min inlämning i kursen Serverside programmering. <br>
> **Länk till repot på GitHub** (OBS! Kontrollera att repot inte är privat) <br>
> Jag har implementerat följande level ups: **1, 2, 4**. <br>
> Webbservern är publicerad här: **(URL)**
