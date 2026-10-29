# A dékáni hivatal „működő” kapcsolati űrlapja – hibariport

Repó: https://github.com/istszabi/umfst-bh01-kapcsolati-urlap.git
Készítette: Istok Szabolcs

## 1. hiba
- **Hiba leírása és reprodukálása (lépések, böngésző, segédtechnológia):** Megnyitottam az oldalt Chrome-ban és elindítottam az NVDA képernyőolvasót. Az olvasó angol kiejtéssel próbálta felolvasni a magyar szöveget, ami emiatt teljesen érthetetlen volt.
- **Gyökérok (melyik sor, melyik szabály sérül):** `index.html` 2. sor. A `<html>` elemről hiányzott a `lang="hu"` attribútum (WCAG 3.1.1 - Language of Page).
- **Javítás (commit link, előtte/utána kódrészlet):**
  - Commit: https://github.com/istszabi/umfst-bh01-kapcsolati-urlap/commit/8b6161c
  - *Előtte:*
    ```html
    <html>
    ```
  - *Utána:*
    ```html
    <html lang="hu">
    ```
- **Hogyan tesztelted (W3C validátor, Lighthouse, Tab-bejárás, képernyőolvasó):** W3C validátor adott rá egy figyelmeztetést, a Lighthouse Accessibility audit jelezte a hiányát, és NVDA-val újra felolvastatva már magyar kiejtéssel szólalt meg.
- **Tanulság / érintett alapelv (pl. Szemantika előbb, stílus később; WCAG-kritérium):** A böngészőnek és a segédtechnológiának mindig pontosan meg kell adni a dokumentum nyelvét, különben helytelen nyelvi modult használnak.

## 2. hiba
- **Hiba leírása és reprodukálása (lépések, böngésző, segédtechnológia):** Képernyőolvasóval a fejlécben lévő képre lépve az olvasó csak annyit mondott ki, hogy „logo.png”, így a látássérült felhasználó nem tudja, mit ábrázol a kép.
- **Gyökérok (melyik sor, melyik szabály sérül):** `index.html` 11. sor. Az `<img>` elemhez nem volt megadva `alt` attribútum (WCAG 1.1.1 - Non-text Content).
- **Javítás (commit link, előtte/utána kódrészlet):**
  - Commit: https://github.com/istszabi/umfst-bh01-kapcsolati-urlap/commit/2ce80f1
  - *Előtte:*
    ```html
    <img src="logo.png" width="120" height="40">
    ```
  - *Utána:*
    ```html
    <img src="logo.png" alt="ÁOK Dékáni Hivatal logó" width="120" height="40">
    ```
- **Hogyan tesztelted (W3C validátor, Lighthouse, Tab-bejárás, képernyőolvasó):** W3C validátor hibát jelzett a hiányzó alt miatt, és Lighthouse-ban is piros jelzést kapott az elem.
- **Tanulság / érintett alapelv (pl. Szemantika előbb, stílus később; WCAG-kritérium):** Minden információt hordozó képre kell érdemi `alt` leírás, hogy a képernyőolvasó fel tudja olvasni a tartalmát.

## 3. hiba
- **Hiba leírása és reprodukálása (lépések, böngésző, segédtechnológia):** Az űrlap mezőibe kattintva vagy Tab-bal rájuk lépve gépeléskor eltűnt a felirat, a képernyőolvasó pedig csak annyit mondott, hogy „szerkesztés, üres”.
- **Gyökérok (melyik sor, melyik szabály sérül):** `index.html` 17–24. sorok. A mezőknek nem volt `<label>` elemük, csak `placeholder` volt megadva nekik (WCAG 1.3.1 - Info and Relationships, WCAG 3.3.2 - Labels or Instructions).
- **Javítás (commit link, előtte/utána kódrészlet):**
  - Commit: https://github.com/istszabi/umfst-bh01-kapcsolati-urlap/commit/1a9838a
  - *Előtte:*
    ```html
    <input type="text" name="nev" placeholder="Teljes név" required>
    <input type="text" name="email" placeholder="E-mail cím" required>
    ```
  - *Utána:*
    ```html
    <label for="nev">Teljes név:</label>
    <input type="text" id="nev" name="nev" placeholder="Teljes név" required>

    <label for="email">E-mail cím:</label>
    <input type="text" id="email" name="email" placeholder="E-mail cím" required>
    ```
- **Hogyan tesztelted (W3C validátor, Lighthouse, Tab-bejárás, képernyőolvasó):** Lighthouse audit során megjelent a „Form elements do not have associated labels” hiba, illetve képernyőolvasóval ellenőriztem, hogy felolvassa-e a mező nevét gépelés közben is.
- **Tanulság / érintett alapelv (pl. Szemantika előbb, stílus később; WCAG-kritérium):** A placeholder nem helyettesíti a labelt, mert kitöltéskor eltűnik, és a segédtechnológia sem tudja tartósan a mezőhöz kötni.

## 4. hiba
- **Hiba leírása és reprodukálása (lépések, böngésző, segédtechnológia):** Megnyitottam az oldalt böngészőben, és a főcím az előírt zöld szín helyett fekete maradt.
- **Gyökérok (melyik sor, melyik szabály sérül):** `style.css` 3. sor. A `.cim` osztályban elgépelt tulajdonságnév szerepelt: `colour: #0e7c66;` volt írva `color` helyett.
- **Javítás (commit link, előtte/utána kódrészlet):**
  - Commit: https://github.com/istszabi/umfst-bh01-kapcsolati-urlap/commit/7ac5069
  - *Előtte:*
    ```css
    .cim { colour: #0e7c66; font-size: 2rem; }
    ```
  - *Utána:*
    ```css
    .cim { color: #0e7c66; font-size: 2rem; }
    ```
- **Hogyan tesztelted (W3C validátor, Lighthouse, Tab-bejárás, képernyőolvasó):** Chrome DevTools (F12) Styles panelén látszott, hogy a `colour` tulajdonság alá van húzva mint érvénytelen/ismeretlen CSS szabály.
- **Tanulság / érintett alapelv (pl. Szemantika előbb, stílus később; WCAG-kritérium):** A böngésző csendben figyelmen kívül hagyja a hibásan leírt CSS tulajdonságokat, így a hibát a fejlesztői eszközökben kell megkeresni.

## 5. hiba
- **Hiba leírása és reprodukálása (lépések, böngésző, segédtechnológia):** Mobil nézetben az e-mail mezőre koppintva nem a speciális e-mail billentyűzet jelenik meg, ráadásul hiányos vagy hibás szöveget (pl. „alma”) is el lehet küldeni e-mail címként.
- **Gyökérok (melyik sor, melyik szabály sérül):** `index.html` 18. sor. Az e-mail mező típusa sima `type="text"` volt `type="email"` helyett (WCAG 1.3.5 - Identify Input Purpose).
- **Javítás (commit link, előtte/utána kódrészlet):**
  - Commit: https://github.com/istszabi/umfst-bh01-kapcsolati-urlap/commit/f912b77
  - *Előtte:*
    ```html
    <input type="text" name="email" placeholder="E-mail cím" required>
    ```
  - *Utána:*
    ```html
    <input type="email" id="email" name="email" placeholder="E-mail cím" required>
    ```
- **Hogyan tesztelted (W3C validátor, Lighthouse, Tab-bejárás, képernyőolvasó):** DevTools mobil emulációjával, valamint hibás formátumú e-mail cím beküldési kísérletével (a böngésző automatikusan hibaüzenetet ad).
- **Tanulság / érintett alapelv (pl. Szemantika előbb, stílus később; WCAG-kritérium):** A célhű HTML input típusok használata kényelmesebbé teszi a bevitelt mobilon, és beépített kliensoldali validációt nyújt.

## 6. hiba
- **Hiba leírása és reprodukálása (lépések, böngésző, segédtechnológia):** Tab billentyűvel végighaladva az oldalon nem lehetett látni, hogy éppen melyik beviteli mezőben vagy gombon áll a fókusz.
- **Gyökérok (melyik sor, melyik szabály sérül):** `style.css` 6. sor. Az `outline: none;` felülírta és teljesen eltüntette a fókuszkeretet (WCAG 2.4.7 - Focus Visible).
- **Javítás (commit link, előtte/utána kódrészlet):**
  - Commit: https://github.com/istszabi/umfst-bh01-kapcsolati-urlap/commit/b2748eb
  - *Előtte:*
    ```css
    input:focus, select:focus, textarea:focus, button:focus { outline: none; }
    ```
  - *Utána:*
    ```css
    input:focus, select:focus, textarea:focus, button:focus {
      outline: 2px solid #0e7c66;
      outline-offset: 2px;
    }
    ```
- **Hogyan tesztelted (W3C validátor, Lighthouse, Tab-bejárás, képernyőolvasó):** Billentyűzetes Tab-bejárással ellenőriztem a láthatóságot, és lefuttattam a Lighthouse Accessibility auditot.
- **Tanulság / érintett alapelv (pl. Szemantika előbb, stílus később; WCAG-kritérium):** Nem szabad kikapcsolni az alapértelmezett `outline`-t anélkül, hogy helyette saját, jól látható fókuszstílust biztosítanánk a billentyűzetet használók számára.

## 7. hiba
- **Hiba leírása és reprodukálása (lépések, böngésző, segédtechnológia):** Tab billentyűvel a gombra lépve kétszer kellett megnyomni a Tab-ot a továbblépéshez, és a W3C validátor is szerkezeti hibát jelzett az űrlap végén.
- **Gyökérok (melyik sor, melyik szabály sérül):** `index.html` 25. sor. A gomb egy hivatkozásba volt csomagolva (`<a href="#"><button>...`), ami érvénytelen HTML beágyazás (WCAG 4.1.1 - Parsing).
- **Javítás (commit link, előtte/utána kódrészlet):**
  - Commit: https://github.com/istszabi/umfst-bh01-kapcsolati-urlap/commit/7ba7368
  - *Előtte:*
    ```html
    <a href="#"><button>Küldés</button></a>
    ```
  - *Utána:*
    ```html
    <button type="submit">Küldés</button>
    ```
- **Hogyan tesztelted (W3C validátor, Lighthouse, Tab-bejárás, képernyőolvasó):** W3C Nu HTML Validator ellenőrzéssel (ami kimutatta a hibás beágyazást) és billentyűzetes fókuszteszttel.
- **Tanulság / érintett alapelv (pl. Szemantika előbb, stílus később; WCAG-kritérium):** Interaktív elemet nem ágyazunk másik interaktív elembe. Űrlap beküldésére kizárólag a `<button type="submit">` való.

## Összegzés
- **Mit tanultam:** Az akadálymentesítés nem egy utólagos extra feladat, hanem a helyes, szemantikus HTML kódolás alapja. Sok aprónak tűnő hiba (mint az `outline: none;` használata vagy a hiányzó `<label>` elemek) teljesen megakaszthatja a billentyűzettel vagy képernyőolvasóval navigáló felhasználókat.
- **Melyik alapelv sérült a leggyakrabban:** A helyes HTML szemantika és az akadálymentességi jelölések hiánya sérült a legtöbb helyen (leginkább az űrlapelemek feliratozása a WCAG 1.3.1 és a látható fókusz hiánya a WCAG 2.4.7 szerint).