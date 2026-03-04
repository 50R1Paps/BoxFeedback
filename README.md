# WOD Feedback Box 🏋️

> Sistema di feedback anonimo per box CrossFit — hostato su GitHub Pages, dati salvati su Google Sheets.

---

## Come funziona

Gli atleti aprono `index.html` dal loro telefono, votano il WOD del giorno (👍/👎) e valutano la settimana su 5 dimensioni con uno slider 1–10. I dati arrivano anonimi su un Google Sheet. I coach accedono alla dashboard protetta da password per vedere trend, medie e storico settimane.

```
Atleta → index.html → Google Apps Script → Google Sheets → dashboard.html → Coach
```

---

## Stack

| Componente | Tecnologia                    |
| ---------- | ----------------------------- |
| Frontend   | HTML + CSS + JS vanilla       |
| Hosting    | GitHub Pages (gratuito)       |
| Backend    | Google Apps Script (gratuito) |
| Database   | Google Sheets                 |
| Grafici    | Chart.js                      |

---

## File

```
├── index.html          # Pagina pubblica per gli atleti
├── dashboard-[id].html # Dashboard privata per i coach
├── Code.gs             # Google Apps Script (backend)
└── README.md
```

---

## Setup

### 1. Google Sheet

1. Crea un nuovo foglio su [sheets.google.com](https://sheets.google.com)
2. Copia l'ID dall'URL:
   ```
   https://docs.google.com/spreadsheets/d/[QUESTO_E_L_ID]/edit
   ```

### 2. Google Apps Script

1. Vai su [script.google.com](https://script.google.com) → **Nuovo progetto**
2. Incolla il contenuto di `Code.gs`
3. Sostituisci `IL_TUO_SPREADSHEET_ID_QUI` con l'ID copiato sopra
4. Salva → seleziona `testSave` dal menu a tendina → clicca ▶ **Esegui**
5. Verifica che nel Sheet sia apparso il foglio `Feedback` con una riga di test
6. **Distribuisci → Nuova distribuzione → App Web**
   - Esegui come: `Me`
   - Chi ha accesso: `Chiunque`
7. Copia l'URL della web app

### 3. Collega le pagine allo script

In `index.html` sostituisci:

```javascript
const APPS_SCRIPT_URL = "YOUR_APPS_SCRIPT_URL_HERE";
// con:
const APPS_SCRIPT_URL = "https://script.google.com/macros/s/TUO_ID/exec";
```

Fai lo stesso in `dashboard-[id].html`.

### 4. Configura la dashboard

In `dashboard-[id].html` cambia anche la password e il link di ritorno all'index:

```javascript
const DASHBOARD_PASSWORD = "crossfit2025"; // ← cambia con la tua
```

### 5. Pubblica su GitHub Pages

1. Carica i file nella repository
2. **Settings → Pages → Source: main branch**
3. Il sito è live su `https://[username].github.io/[repo]/`

---

## Dati raccolti

Il foglio `Feedback` viene creato automaticamente con queste colonne:

| Timestamp | Data | Settimana | Date Settimana | N° Settimana | Voto WOD | Atmosfera | Programmazione | Varietà | Intensità | Coaching |

Nessun dato personale viene salvato. I feedback sono completamente anonimi.

---

## Aggiornare lo script

Ogni volta che modifichi `Code.gs` devi creare una **nuova versione** della distribuzione:

**Distribuisci → Gestisci distribuzioni → ✏️ → Nuova versione → Distribuisci**

L'URL rimane invariato.

---

## Accessi

| Pagina                | Chi              | Come                    |
| --------------------- | ---------------- | ----------------------- |
| `index.html`          | Tutti gli atleti | Link diretto            |
| `dashboard-[id].html` | Solo i coach     | Link privato + password |
