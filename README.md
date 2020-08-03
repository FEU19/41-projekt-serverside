# Serverside programmering
## Individuellt projekt

### Uppgift
Du ska bygga en webbserver med **Node.js**, **Express** och **MongoDB**.

### Kravspec
Ur-göteborgaren Berra behöver uppgradera sin båtaffär. Han vill ha en webbshop där man kan söka på och köpa båtar. Men innan man kan bygga en frontend vill han ha ett API. Din uppgift är att registrera båtarna i en databas och bygga ett API för det.


#### API spec
|Resurs    |Metod   |Förväntat svar|
|----------|--------|---|
|/         | GET    |Servar frontend (senare)|

```
http://localhost:3000/
http://localhost:3000/index.html
```

|Resurs    |Metod   |Förväntat svar|
|----------|--------|---|
|/assets/  | GET    |Servar bilder (statiska resurser, *level up*)|

```
http://localhost:3000/assets/boat001.jpg
```

|Resurs    |Metod   |Förväntat svar|
|----------|--------|---|
|/boats/   | GET    |Returnerar en array med alla båtar|

```
http://localhost:3000/boats/
[
    { id: '001', model: 'Nimbus C9', ... },
    { id: '002', model: 'Candela Seven', ''' },
    ...
]
```

|Resurs    |Metod   |Förväntat svar|
|----------|--------|---|
|/boat/:id | GET    |Returnerar en båt med efterfrågat id|
|/boat/    | POST   |Sparar ett båt-objekt i databasen|
|/boat/:id | DELETE |Tar bort en båt från databasen|

```
http://localhost:3000/boat/001 (GET)
http://localhost:3000/boat/    (POST har data i request body)
http://localhost:3000/boat/001 (DELETE)
```

|Resurs    |Metod   |Förväntat svar|
|----------|--------|---|
|/search/  | GET    |Returnerar upp till fem sökträffar|

```
Alla querystring-parametrar är valfria.
http://localhost:3000/search/?word=nimbus&maxprice=30000&is_sail=yes&has_motor=yes
```
##### Sökning
Man ska använda querystring för att tala om vad man söker efter. API:et ska hantera följande parametrar:
* **word** - en sträng med ett ord som måste finnas i modellnamnet
* **maxprice** - högsta tillåtna priset
* **is_sail** - yes/no, om det är en segelbåt
* **has_motor** - yes/no, om den har motor
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

#### Datamodell
En båt har följande egenskaper:
* id - skapas av databasen!
* modellnamn - sträng med upp till 64 tecken
* tillverkningsår - heltal
* pris - flyttal (tal med decimaler)
* segelbåt - kan vara ja/nej
* motor - kan vara ja/nej
* bild URL - *level up*

#### Level ups
1. ?
1. URL till bild för varje båtobjekt
1. publicera uppgiften på nätet, till exempel med hjälp av Heroku

### Betygskriterier
Från kursplanen:
> För betyget Godkänd ska den studerande
> * Visa grundläggande förståelse för server side programmering
> * Med viss handledning utveckla databasdrivna applikationer

> För betyget Väl Godkänd ska den studerande:
> * Uppnått kraven för betyget godkänt
> * Visa god förståelse för server side programmering

För godkänt på uppgiften ska du göra ett projekt som följer godkänt-nivån i kravspecifikationen.

För väl godkänt ska du visa att du har en *god förståelse*. Detta gör du genom att implementera tillräckligt många *Level ups*. Både kvalitet (hur bra) och kvantitet (hur många) kommer att tas med i bedömningen.

### Inlämning
Lämna in uppgiften genom att skicka en länk till ditt GitHub-repo till läraren via slack. Om du har publicerat uppgiften så skicka länk till den också.
