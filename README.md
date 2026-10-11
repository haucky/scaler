# Bewusstseinskarte

Sprich aus, was dich beschäftigt – die App ordnet es auf der *Map of Consciousness* von David R. Hawkins ein und zeigt für jede der 17 Stufen, wie du auf dieser Stufe über dein Thema denken würdest. Passende Sätze von dir werden wörtlich zitiert.

## Deployen auf GitHub Pages

1. Neues Repository anlegen, z. B. `bewusstseinskarte`.
2. Alle Dateien aus diesem Ordner hochladen (`index.html`, `manifest.webmanifest`, `sw.js`, Ordner `icons/`).
3. Repository → **Settings → Pages** → Source: *Deploy from a branch*, Branch `main`, Ordner `/ (root)`.
4. Nach ca. 1 Minute läuft die App unter `https://<dein-name>.github.io/bewusstseinskarte/`.
5. Auf dem Handy öffnen → „Zum Home-Bildschirm“ (iOS: Teilen-Menü, Android: Menü → App installieren).

Beim ersten Start fragt die App nach deinem Gemini API-Key ([aistudio.google.com/apikey](https://aistudio.google.com/apikey)).

## Technik

- **Modell:** `gemini-3.8-flash` (stabil, nimmt Audio direkt an). Transkription und Auswertung passieren in **einem** Aufruf, die Antwort kommt als JSON nach festem Schema. Modell und Denktiefe sind in den Einstellungen änderbar.
- **Audio:** Die Aufnahme wird im Browser in 16-kHz-Mono-WAV umgewandelt (funktioniert auf iOS und Android gleich) und direkt an Google geschickt. Gespeichert wird kein Audio. Maximal 5 Minuten pro Aufnahme.
- **Verlauf:** lokal auf dem Gerät, exportierbar und importierbar als JSON.
- **Offline:** Der Service Worker cached nur die App-Dateien. API-Anfragen laufen nie über den Cache.

## Zum API-Key

Der Key liegt im `localStorage` der Website. Der Browser trennt diesen Speicher strikt nach Herkunft (Origin), andere Websites und Apps kommen nicht heran.

**Wichtig bei GitHub Pages:** Alle Projekte unter `https://<dein-name>.github.io/...` teilen sich denselben Origin. Ein anderes Projekt, das du dort veröffentlichst, könnte den Key also lesen. Wenn du dort nur eigenen Code hostest, ist das kein Problem. Sonst: eine eigene Domain für dieses Repo verwenden.

Zusätzlich empfehlenswert (in der [Google Cloud Console → APIs & Dienste → Anmeldedaten](https://console.cloud.google.com/apis/credentials)):

- Key auf die **Generative Language API** beschränken.
- Unter *Anwendungseinschränkungen* → **HTTP-Verweis-URLs**: `https://<dein-name>.github.io/*` eintragen.
- Ein **Budget-Limit** bzw. eine Benachrichtigung in der Abrechnung setzen.

## Updates

Wenn du `index.html` änderst, in `sw.js` die Zeile `const CACHE = 'bewusstseinskarte-v1'` hochzählen (v2, v3 …), damit installierte Apps die neue Version laden.

---

Skala nach David R. Hawkins, *Power vs. Force*. Keine Diagnose, nur ein Spiegel.
