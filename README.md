# REA Projekt

En enkel webbsida där du skriver in en app, produkt eller tjänst som du vill "research engineera" med [REA](https://github.com/morluto/rea), och där du ser alla dina tidigare projekt.

- Sidan är en enda fil (`index.html`) och kan ligga på GitHub Pages.
- Varje projekt sparas som en **issue** i ett eget repo, så listan finns på alla dina enheter.
- Sidan skapar en färdig **prompt** som du kopierar in i din agent (Claude Code, Codex, Cursor m.fl.) där REA är installerat. Själva analysen körs alltså hos dig, inte på sidan.
- Resultatet klistrar du in som kommentar på projektets issue. Status (Planerad, Pågår, Klar) ändrar du direkt på sidan.

## Installation

### 1. Två repon (rekommenderat)

| Repo | Innehåll | Synlighet |
|---|---|---|
| `rea-tracker` | Den här sidan (`index.html`) | Publikt (krävs för gratis GitHub Pages) |
| `rea-projects` | Dina projekt som issues | **Privat** |

Sidan är publik men innehåller ingen data. Projekten ligger i det privata repot och kan bara läsas med din token.

(Vill du förenkla kan du använda ett enda publikt repo, men då kan alla läsa dina projekt.)

### 2. Publicera sidan

1. Skapa repot `rea-tracker` och lägg `index.html` i roten.
2. Gå till **Settings → Pages**, välj **Deploy from a branch**, branch `main` och mapp `/ (root)`.
3. Efter någon minut finns sidan på `https://DITTNAMN.github.io/rea-tracker/`.

### 3. Skapa en token

1. Skapa det privata repot `rea-projects` (tomt räcker, och Issues måste vara aktiverat).
2. Gå till **GitHub → Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token**.
3. Under **Repository access** väljer du *Only select repositories* och bara `rea-projects`.
4. Under **Permissions → Repository permissions** sätter du **Issues** till *Read and write*.
5. Kopiera token (`github_pat_...`).

### 4. Anslut sidan

Öppna sidan, klicka **Inställningar**, skriv `DITTNAMN/rea-projects` och klistra in token, och klicka **Spara och testa**. Etiketterna (`rea-project`, `rea:planned`, `rea:in-progress`, `rea:done`) skapas automatiskt första gången du skapar ett projekt.

## Så använder du den

1. Skriv in målet (t.ex. "Notes"), välj typ och beskriv vad du vill förstå.
2. Klicka **Skapa projekt**. Ett issue skapas.
3. Klicka **Kopiera prompt** på projektet och klistra in den i din agent med REA installerat (`npx rea-agents setup`).
4. Klistra in resultatet som kommentar på issuen och markera projektet som **Klar**.

## Säkerhet och begränsningar

- Token sparas i webbläsarens localStorage på den enhet du använder och skickas bara till `api.github.com`. Använd en token som är begränsad till ett repo och ta bort den under Inställningar → Rensa på delade datorer.
- Listan visar upp till 100 projekt (senaste först).
- REA ska bara användas på programvara du äger eller har tillstånd att undersöka, se [REA:s ansvarsfriskrivning](https://github.com/morluto/rea/blob/main/DISCLAIMER.md).

## Nästa steg (valfritt)

Ett litet script på din dator kan hämta projekt med etiketten `rea:planned`, köra REA via din agent och lägga resultatet som kommentar, så att du kan starta analyser direkt från webben.
