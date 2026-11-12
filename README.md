# Boekenchecker

Nederlandse boekenlijst met barcodescanner, statistieken en accounts.

## Bestanden
Zet deze allemaal in de hoofdmap van je GitHub-repo:
`index.html`, `firebase-config.js`, `manifest.json`, `icon.svg`, `icon-192.png`, `icon-512.png`

## 1. GitHub Pages
1. Maak een nieuwe repo en upload de bestanden.
2. Settings → Pages → Branch: `main`, map `/ (root)` → Save.
3. Je site staat op `https://JOUWNAAM.github.io/REPONAAM/`.

## 2. Firebase (accounts + opslag)
1. Firebase console → nieuw project (of je bestaande project).
2. **Authentication → Sign-in method**: zet *E-mail/wachtwoord* aan (en *Google* als je die knop wilt gebruiken).
3. **Authentication → Settings → Authorized domains**: voeg `JOUWNAAM.github.io` toe.
4. **Firestore Database** → database maken (productiemodus) → tabblad **Rules** → plak dit en klik Publish:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{uid}/books/{book} {
      allow read, write: if request.auth != null && request.auth.uid == uid;
    }
  }
}
```

5. **Projectinstellingen → Je apps → Web-app (</>)** → kopieer de config en plak die in `firebase-config.js`.

Iedereen ziet daarna alleen zijn eigen boeken. Zolang `firebase-config.js` niet is ingevuld,
werkt de app in lokale modus (boeken staan dan alleen op dat ene apparaat).

## Goed om te weten
- De scanner heeft de camera nodig en werkt alleen via https (GitHub Pages is https).
- Boekgegevens komen van Google Books en Open Library. Niet elk Nederlands boek staat erin;
  dan vul je titel en schrijver zelf in.
- Meerdere schrijvers bij één boek: scheid ze met `&`, dan tellen ze allebei mee.
