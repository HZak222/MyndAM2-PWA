[README.md](https://github.com/user-attachments/files/28577283/README.md)
# 📷 MYNDA — Leiðbeiningar

Þetta er PWA (Progressive Web App) sem tekur myndir og sendir þær beint á Google Drive,
**án þess að vista þær í símann**.

---

## Hvað þarft þú?

- GitHub reikning (til að hýsa appið)
- Google reikning (Google Drive + Apps Script)

---

## Skref 1 — Setja upp Google Drive möppu

1. Opnaðu [drive.google.com](https://drive.google.com)
2. Búðu til nýja möppu, t.d. **„Mynda Upload"**
3. Opnaðu möppuna og skoðaðu URL-inn í vafranum.
   Hann lítur svona út:
   ```
   https://drive.google.com/drive/folders/1aBcDeFgHiJkLmNoPqRsTuVwXyZ
   ```
4. **Afritaðu þennan langa kóða** — þetta er `FOLDER_ID` sem þú þarft seinna.

---

## Skref 2 — Búa til Google Apps Script

1. Farðu á [script.google.com](https://script.google.com)
2. Smelltu á **„Nýtt verkefni"** (New project)
3. Eyddu öllu sem er þegar í `Code.gs`
4. **Límdu inn** allan kóðann úr skránni `apps-script.gs`
5. Finndu þessa línu efst:
   ```javascript
   var FOLDER_ID = 'SETTU_FOLDER_ID_HER';
   ```
   Skiptu `SETTU_FOLDER_ID_HER` út fyrir kóðann sem þú afritaðir í Skref 1.
   Dæmi:
   ```javascript
   var FOLDER_ID = '1aBcDeFgHiJkLmNoPqRsTuVwXyZ';
   ```
6. Vistaðu (`Ctrl+S` eða disklingur-takkinn) og gefðu verkefninu nafn, t.d. **„Mynda"**

---

## Skref 3 — Prófa tenginguna

1. Í Apps Script, veldu fallið **`testSetup`** í fellivalmyndinni (þar sem stendur „doPost")
2. Smelltu á ▶ **Run**
3. Ef þú sérð `✅ Tókst!` í log-inum — allt í lagi!
4. Ef villa kemur upp — athugaðu FOLDER_ID og að þú sért innskráður á réttan Google reikning

---

## Skref 4 — Birta Apps Script sem vefþjónustu

1. Smelltu á **„Deploy"** → **„New deployment"**
2. Smelltu á ⚙️ táknið við hliðina á „Type" og veldu **„Web app"**
3. Fylltu út svona:
   - **Description:** Mynda v1
   - **Execute as:** Me (þinn Google reikningur)
   - **Who has access:** Anyone *(þarf að vera "Anyone" til að símaappið geti sent)*
4. Smelltu á **„Deploy"**
5. **Afritaðu Web app URL-inn** — hann lítur svona út:
   ```
   https://script.google.com/macros/s/AKfycb.../exec
   ```
   ⚠️ Geymdu þennan URL vel — þú þarft hann í síðasta skrefi!

---

## Skref 5 — Setja upp á GitHub Pages

1. Búðu til nýtt **public** repository á [github.com](https://github.com), t.d. `mynda-pwa`
2. Uploadaðu þessar skrár í repo-ið:
   - `index.html`
   - `manifest.json`
   - `sw.js`
3. Farðu í **Settings** → **Pages**
4. Undir „Source", veldu **Deploy from a branch** → branch: `main`, folder: `/ (root)`
5. Smelltu á **Save**
6. Eftir 1-2 mínútur er appið aðgengilegt á:
   ```
   https://[github-notendanafn].github.io/mynda-pwa/
   ```

---

## Skref 6 — Tengja appið við Apps Script

1. Opnaðu GitHub Pages URL-inn í síma eða tölvu
2. Appið biður þig um **Apps Script URL**
3. Límdu inn URL-inn sem þú fékst í Skref 4
4. Smelltu á **„Vista og halda áfram"**

---

## Nota appið

1. Sláðu inn **bílnúmer eða annað auðkenni** (t.d. `ABC123`)
2. Smelltu á **„Hefja Session"**
3. Leyfðu aðgang að myndavél þegar spurt er
4. **Taktu myndir** — þær fara beint á Google Drive, **engar myndir vistar í síma**
5. Í Google Drive verður til mappa með nafni auðkennisins, t.d. `ABC123/`
6. Smelltu á **„Ljúka"** þegar þú ert búinn

---

## Bæta appinu á heimaskjá (valfrjálst en þægilegt)

**iPhone/iPad (Safari):**
1. Opnaðu appið í Safari
2. Smelltu á deilitáknið (ferhyrningur með ör)
3. Veldu „Add to Home Screen"

**Android (Chrome):**
1. Opnaðu appið í Chrome
2. Chrome spyr sjálfkrafa um uppsetningu — eða farðu í valmynd → „Add to Home Screen"

---

## Tölvan þín flokkar myndir

Þar sem myndir fara á Google Drive í möppur með auðkenni (t.d. `ABC123/`),
getur tölvan þín notað Google Drive Desktop app og sett upp sjálfvirkt flokkunarforrit
(Python, AutoHotkey o.s.frv.) til að færa myndir á netdrif.

---

## Vandamál?

| Vandamál | Lausn |
|---|---|
| „Myndavél leyfð ekki" | Leyfðu camera í stillingum vafrans |
| „Upload mistókst" | Athugaðu Apps Script URL og nettengingu |
| Myndir fara ekki á Drive | Keyrðu `testSetup` í Apps Script og athugaðu FOLDER_ID |
| Apps Script biður um leyfi | Samþykktu leyfisbeiðnina í Google |
