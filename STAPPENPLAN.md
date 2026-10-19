# BuildCalc.apk maken, stap voor stap

Je doet dit één keer op je computer (Windows of Mac). Daarna komen nieuwe versies vanzelf via een live update.
Alles is gratis.

## Wat je nodig hebt (eenmalig installeren)

1. **Node.js** (LTS-versie): https://nodejs.org
2. **Android Studio**: https://developer.android.com/studio
   Open het één keer en laat het de Android SDK installeren (gewoon op Volgende klikken).
3. Je telefoon met een **USB-kabel**, of je zet de APK later via Drive of mail op je telefoon.

## A. De app bouwen

1. Pak `buildcalc-android-app.zip` uit, bijvoorbeeld in `Documenten\BuildCalc`.
   Je hebt dan de mappen `html` en `android-app` naast elkaar.
2. Open een opdrachtvenster in de map `android-app`
   (Windows: in Verkenner in de adresbalk `cmd` typen en op Enter drukken).
3. Typ:
   ```
   npm install
   npm run sync
   npm run open
   ```
   Android Studio opent nu het project. Wacht tot onderin "Gradle sync" klaar is.
4. **Eenmalig een eigen sleutel maken** (nodig om later te kunnen bijwerken zonder je gegevens te verliezen):
   menu **Build > Generate Signed App Bundle or APK... > APK > Create new...**
   Kies een bestandsnaam zoals `buildcalc.jks`, een wachtwoord, en vul je naam in.
   **Bewaar dit bestand en het wachtwoord goed** (bijvoorbeeld in je eigen Drive). Kwijt = nooit meer een update van de APK.
5. Kies **release** en klik **Create**. De APK staat daarna in
   `android-app/android/app/release/app-release.apk`. Hernoem hem naar `BuildCalc.apk`.
6. Zet hem op je telefoon (USB, Drive of mail) en tik erop. Sta "Installeren uit onbekende bron" toe.
7. Open BuildCalc. De eerste keer vraagt Android om toestemming voor **microfoon**, **camera** en **apparaten in de buurt** (Bluetooth). Kies telkens **Toestaan**.

## B. Live updates aanzetten (GitHub Pages)

1. Log in op https://github.com als **BuildCalc-Pro**.
2. Maak een nieuwe repository met de naam **`buildcalc`**, zet hem op **Public** (gratis Pages kan alleen bij openbare repositories).
3. Klik **Add file > Upload files** en sleep de **inhoud** van de map `android-app` erin
   (niet de map `node_modules`). Klik **Commit changes**.
4. Ga naar **Settings > Pages**. Bij "Branch" kies je **main** en de map **/docs**. Klik **Save**.
5. Na een minuutje staat de app op https://buildcalc-pro.github.io/buildcalc/
   - Daar staat ook de webversie: die kun je in Chrome openen en werkt beter dan het bestand uit Downloads.
   - De app kijkt bij elke start op `versie.json` of er een nieuwere versie is.

## C. Een nieuwe versie uitbrengen (zonder nieuwe APK)

1. Zet de nieuwe `buildcalc.html` in de map `html` (die krijg je van mij).
2. Typ in de map `android-app`:
   ```
   npm run update
   ```
   Dit vult de map `docs` met de nieuwe versie.
3. Upload de map `docs` opnieuw naar GitHub (Add file > Upload files) en klik **Commit changes**.
4. Bij de volgende start van de app verschijnt: "Nieuwe versie klaar. Nu herstarten?"

Je projecten, foto's, metingen en TopCalc-codes blijven daarbij staan: de update draait op hetzelfde
adres binnen de app, dus de opslag (localStorage en IndexedDB) wordt niet aangeraakt. Voor de zekerheid
maakt de app vlak voor het herstarten ook nog een back-up in het **BuildCalc-mapje in de app** (Instellingen, Terugzetten).

Alleen als ik iets aan de Android-kant verander (bijvoorbeeld een nieuw recht), is er een nieuwe APK
nodig. Bouw die dan met **dezelfde sleutel** uit stap A4 en installeer hem over de oude heen.
Verwijder de app nooit eerst: dan zijn je gegevens weg.

## Belangrijk

- Zet je **Gemini-sleutel nooit in de bestanden** die je naar GitHub uploadt (die zijn openbaar).
  Plak hem in de app bij Instellingen. `npm run update` stopt vanzelf als er toch een sleutel in staat.
- De versie zie je in de app onder Instellingen, met "(app)" erachter.
