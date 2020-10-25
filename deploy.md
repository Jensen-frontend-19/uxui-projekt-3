# Deploy / publicering
[Tillbaka till huvudsidan](README.md)

## Publicering / deploy
*Den här guiden förutsätter att du har laddat upp databasen i molnet och kan anropa den från Express-servern. Då behöver du inte göra något för att databasen ska fungera. Guiden utgår också från Heroku, men du kan förutsätta att andra plattformar som Netlify fungerar på liknande sätt.*

**1.** Börja med att skapa ett nytt projekt. Vi använder frontend-projektet som bas eftersom create-react-app automatiskt skapar ett nytt repository med bra inställningar.
```bash
npx create-react-app ditt-app-namn
```
---
**2.** Skapa en mapp med namnet `server/`. Där ska du lägga alla backend-filer. Observera att hela projektet bara ska ha *en* package.json-fil.
Så här kan din mappstruktur se ut:
```text
|- .git/
|- .gitignore
|- package.json
|- Procfile              <-- skapa den här, se steg 6
|- src/                  <-- här hamnar koden React-appen
|- build/                <-- skapas när du bygger frontend-appen med "npm run build"
|- server/               <-- skapa den här!
    |- server.js
    |- ...
```

Resten av guiden förutsätter att filen som du startar servern med heter `server.js`.

---
**3a.** Heroku bestämmer vilken port som Express ska använda. Uppdatera `server.js` så att den använder rätt port.
```javascript
// Använd en variabel till portnumret
const port = 1337;   // FEL
const port = process.env.PORT || 1337;   // RÄTT

// Använd static middleware för att serva de statiska frontend-filerna (se steg 2)
server.use(express.static(__dirname + '/../build'));

// Glöm inte att starta servern med rätt portnummer
// Man kan se allt som skrivs ut med console.log från Herokus portal
server.listen(port, () => console.log('Server is listening on port ' + serverPort));

```
---
**3b.** Tips! Om du använder routing i frontend, se till att alla routes för API:et börjar med `/api`. Då undviker man konflikter mellan frontend och backend. Exempel:
```text
GET  /api/boats
POST /api/boat
osv.
```

---
**4.** Lägg till och committa backend-filerna till ditt lokala repo.

---
**5.** Skapa ett nytt repository på GitHub för hela projektet. När du skapat ett repo visar GitHub vad man ska skriva *i terminalen* för att koppla ihop ditt repo på GitHub med ditt lokala repo. Det bör se ut ungefär så här:
```bash
git remote add origin https://github.com/ditt-användarnamn/ditt-repo.git
git push -u origin master
```
Ladda om sidan på GitHub för att kontrollera att filerna har laddats upp.

---
**6.** Nu ska vi förbereda repot så att Heroku vet hur det ska göra för att bygga och publicera appen. (*build och deploy*) Skapa en fil med namnet `Procfile` (stort P, ingen filändelse, inte ens .txt) i projektets root med följande innehåll:
```text
release: npm run build
web: node server/server.js
```

Detta betyder att när Heroku ska publicera en ny **release** av appen, så ska den börja med att bygga frontend-appen. (Heroku kör `npm install` automatiskt innan den börjar.) När Heroku kör `npm run build` skapas filer i mappen `/build`.

När releasen är byggd kommer Heroku att starta **webbservern** genom att köra filen `server/server.js`.

---
**7.** Skapa ett konto på [Heroku](https://heroku.com/). Klicka på `New -> Create new app`.

---
**8.** Koppla ihop Heroku med GitHub. Skriv in namnet på ditt GitHub-repo. Slå på *Automatic deploy from master*. Från och med nu, varje gång du pushar en ny version till GitHub, så kommer Heroku att *bygga och publicera* den. Avsluta med att klicka på *Deploy branch* för att publicera direkt. (Det kan ta någon minut.)

Klicka på `Open app` för att testköra. Håll tummarna!

---
**9.** Express-servern servar både frontend och backend. När du skickar GET/POST request med AJAX så är det till samma webbserver som servar frontend. Problemet är att det är olika när man utvecklar och när man har publicerat online.

Din lokala Express webbserver använder ett portnummer som du hittar på, t.ex port==1337.

När du utvecklar startar React en *utvecklingsserver* som vanligtvis har port==3000. Den är användbar när vi bygger frontend.

När du gör AJAX från frontend med en URL, till exempel `/api/boat?id=5`, då används samma server och portnummer som servat frontend-filerna. Om det står `http://localhost:3000/` i webbläsarens adressfält, så kommer ditt request att skickas till `http://localhost:3000/` i stället för `http://localhost:1337/`! Detta är bara ett problem när man kör sin app från utvecklingsservern. Reacts lösning är att man lägger till en rad med ordet **proxy** i sin package.json, efter avdelningen `scripts`:
```json
"scripts": {
  "start": "react-scripts start",
  "build": "react-scripts build",
  "test": "react-scripts test",
  "eject": "react-scripts eject"
},
"proxy": "http://localhost:1337",   <- lägg till den här! Använd ditt Express portnummer!
```

Alternativ lösning: create-react-app skapar en variabel, vars värde beror på om vi använt `npm run start` (utvecklingsversionen) eller `npm run build` (production). (Du kan bli tvungen att lägga till stöd för CORS i servern.)
```javascript
let baseUrl;
if( process.env.NODE_ENV === 'production' ) {
	// AJAX stannar kvar på samma server när vi kör production, använd relativ URL
	baseUrl = '/api';
}
else {  // NODE_ENV === 'development'
	// Använd absolut URL med portnumret från din serverfil, steg 3a
	baseUrl = 'http://localhost:1337/api';
}
const response = await fetch(baseUrl + '/boats', { method: 'GET' });
const allTheBoats = await response.json();
```

**9b.** Vue använder också en proxy-inställning, men man gör det med en annan fil. Skapa filen `vue.config.js` i samma mapp som package.json:
```javascript
module.exports = {
  devServer: {
    proxy: "http://localhost:1337"   // använd ditt Express portnummer!
  }
}
```
