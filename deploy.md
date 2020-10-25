# Deploy / publicering
[Tillbaka till huvudsidan](README.md)

## Publicering / deploy
**1.** Börja med att skapa ett nytt projekt på din dator. Skriv i terminalen:
```bash
npx vue create ditt-app-namn-gärna-med-gruppnamn-också
```

---
**2.** Skapa ett nytt repository på GitHub för hela projektet. När du skapat ett repo visar GitHub vad man ska skriva *i terminalen* för att koppla ihop ditt repo på GitHub med ditt lokala repo. Det bör se ut ungefär så här:
```bash
git remote add origin https://github.com/ditt-användarnamn/ditt-repo.git
git push -u origin master
```
Ladda om sidan på GitHub för att kontrollera att filerna har laddats upp.


---
**3.** Vi ska använda npm-paketet `gh-pages` för att publicera projektet.
```bash
# Installera paketet
npm i --save-dev gh-pages

# För att publicera en ny version:
npm run build
npx gh-pages -d dist/
```
-d talar om vilka filer som ska publiceras: alla i mappen `dist/`.

Först skapas gh-pages en ny branch som heter "gh-pages". Den innehåller bara de filer som ska publiceras. Sedan pushar gh-pages dem till GitHub och konfigurerar repot så att gh-pages branchen blir den som GitHub Pages använder.


Ännu bättre, lägg till det som ett kommando i package.json:
```json
"scripts": {
    "deploy": "npm run build & gh-pages -d dist/ "
}
```

---
**4.** Gå till repots inställningar på GitHub. Scrolla ner till avdelningen GitHub Pages och kopiera länken som finns där. Det är länken till den publicerade sidan.

Obs! GitHub Pages tar ibland 5-10 minuter på sig innan den uppdaterar filerna.
