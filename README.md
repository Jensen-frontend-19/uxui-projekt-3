# Interaktiv prototyp med CSS
Inlämningsuppgift 3 i fortsättningskursen UX/UI. Ni ska arbeta i grupper på 3-4 personer.

Tidigare i kursen har vi jobbat med designprocessens olika delar och hur en styleguide kan se ut. Nu ska vi ta **steget över från designskiss till kod**. Er uppgift är att tillverka en Vue-app som liknar en Figma-prototyp så mycket som möjligt.

Ta fram en **styleguide** och en **Figma-prototyp**. Det är tillåtet att återanvända material som ni tagit fram för tidigare inlämningsuppgifter. Men återvunnet material räknas inte med i bedömningen - det är alltså viktigare att ni gör en bra CSS-prototyp. Ni bör i vilket fall lägga minst halva tiden på CSS-prototypen.

Det är tillåtet att ändra i styleguide och prototyp under resans gång - det är så vi arbetar agilt med design!


### Appens funktion och innehåll
CSS-prototypen ni bygger ska uppfylla följande krav:
1. Vara responsiv - designen fungerar på smala skärmar
2. Minst 4 olika vyer
3. Realistisk, statisk data
4. Förbered en "snitslad bana" för användaren.
5. Animationer och hover-effekter (särskilt på desktop-versionen)

Oavsett om ni använder Figma-prototypen från första inlämningsuppgiften eller bygger en ny, så kan den behöva kompletteras så att den är **responsiv** och har **minst 4 olika vyer**.

Exempel på data: om ni bygger en prototyp för en webbshop, så ska ni hitta på en lagom mängd realistiska exempelprodukter. Produkterna kan vara *HTML i template*, eller en array i *komponentens data property*. Om ni bygger ett formulär där användaren förväntas fylla i data, så kan det vara förifyllt med realistisk exempeldata. **Lorem ipsum är absolut förbjudet!**

Med "*snitslad bana*" menas att användaren ska kunna klicka sig vidare genom appen, för att se alla olika vyer som ni har gjort. Men alla knappar behöver inte vara klickbara. Ni väljer själva vilken nivå ni vill lägga interaktiviteten på.


### Vue-projektet
+ Börja med att bestämma en mappstruktur. Vilka globala (delade) filer ska finnas? Var ska de ligga?
+ Skapa en view-komponent för varje route.
+ Utgå från Figma-prototypen och bygg en HTML-sida för en *view*. Ha med exempeldata direkt i HTML.
+ Lägg in HTML-koden i komponentens template.
+ Börja skriva CSS. Dela upp komponenten i flera komponenter efter behov
+ I komponenter där det behövs: flytta datan från template till komponentens data property
+ Koppla klickhändelser på element som man behöver kunna interagera med för att testa prototypen

Glöm inte att publicera appen online!


### Deploy
Appen ska publiceras online på GitHub, Heroku eller annan molntjänst. [Publicera Vue/React på Heroku](deploy.md)


### Så här ska ni arbeta
[Agil projektmetodik](agile.md)


### Inlämning
Alla filer som du committar till GitHub ska zippas och laddas upp på LearnPoint. Zip-arkivet ska ha filnamnet: `inlämning-prototyp-grupp-X.zip` där du byter ut "X" mot ditt gruppnummer eller gruppnamn.

Ändra i projektets `README.md` så att den innehåller
+ namn och klass för alla i gruppen
+ kortfattad beskrivning av app-idén
+ om ni utgått från resultatet av något tidigare projekt, berätta det
+ om ni gjort förbättringar jämfört med prototypen, berätta det
+ kortfattad beskrivning av hur ni delat upp arbetet
+ länk till Figma-prototypen som ni har utgått ifrån


### Bedömning
För **godkänt** ska ni skapa en funktionell CSS-prototyp efter en designskiss. Prototypen ska vara interaktiv.

För **väl godkänt** ska ni skapa en CSS-prototyp som följer en designskiss väl.
