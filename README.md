# IncluDO — Frontend

**IncluDO** è un chatbot AI di orientamento formativo dedicato ai corsi artigianali tradizionali.  
Questo repository contiene il **frontend** React, che permette agli utenti di conversare con **Indo**, l'assistente virtuale del progetto.

---

##  Stack Tecnologico

| Tecnologia | Versione | Ruolo |
|---|---|---|
| [React](https://react.dev/) | ^19 | UI Framework |
| [Vite](https://vitejs.dev/) | ^8 | Build tool & dev server |
| Vanilla CSS | — | Styling (design "Ethereal Dark") |
| [Railway](https://railway.app/) | — | Hosting del frontend |

---

##  Struttura del Progetto

```
includo-frontend/
├── public/
│   └── logo_favicon.png       # Favicon del progetto
├── src/
│   ├── components/
│   │   ├── Chat.jsx           # Componente principale: gestisce sessione, stato e API calls
│   │   ├── MessageList.jsx    # Lista messaggi con supporto streaming
│   │   ├── MessageBubble.jsx  # Singola bolla messaggio (utente / assistente)
│   │   └── InputBox.jsx       # Input testuale con pulsante di invio
│   ├── App.jsx                # Root component
│   ├── App.css                # Design system "Ethereal Dark" (glassmorphism)
│   └── main.jsx               # Entry point React
├── index.html                 # Template HTML con meta SEO (lang: it)
├── vite.config.js             # Configurazione Vite
├── railway.json               # Configurazione deploy Railway
└── .env                       # Variabili d'ambiente (non committare)
```

---

##  Installazione e Avvio Locale

### Prerequisiti
- Node.js >= 18
- npm >= 9

### Setup

```bash
# 1. Clona il repository
git clone https://github.com/<tuo-utente>/includo-frontend.git
cd includo-frontend

# 2. Installa le dipendenze
npm install

# 3. Configura le variabili d'ambiente
cp .env.example .env
# Modifica VITE_API_URL con l'URL del tuo backend

# 4. Avvia il server di sviluppo
npm run dev
```

L'app sarà disponibile su `http://localhost:5173`.

---

##  Variabili d'Ambiente

Crea un file `.env` nella root del progetto:

```env
VITE_API_URL=https://tuo-backend.up.railway.app
```

>  **Non committare mai il file `.env`** — è già incluso nel `.gitignore`.

| Variabile | Descrizione |
|---|---|
| `VITE_API_URL` | URL base del backend Laravel (senza slash finale) |

---

##  Script Disponibili

```bash
npm run dev      # Avvia il dev server con HMR
npm run build    # Crea la build di produzione in /dist
npm run preview  # Anteprima locale della build di produzione
npm run lint     # Analisi statica del codice con ESLint
```

---

##  Deploy

Il frontend è configurato per il deploy su **Railway** tramite `railway.json`.  
Il comando di avvio in produzione è:

```bash
npx serve -s build -l $PORT
```

### Variabili d'ambiente in produzione (Railway)
Aggiungi `VITE_API_URL` nelle impostazioni del servizio Railway, puntando all'URL pubblico del backend.

---

##  Architettura

```
Utente
  │
  ▼
InputBox.jsx  ──────────────────────────────────────────┐
                                                        │
Chat.jsx  (gestisce sessione UUID + chiamata /api/chat) │
  │  ◄─── localStorage (includo_session) ───────────────┘
  │
  ▼  POST { session_id, message }
Backend Laravel  (includo-backend.up.railway.app)
  │
  ▼  JSON reply  |  Streaming text
MessageList.jsx + MessageBubble.jsx
```

- La **sessione** è persistita in `localStorage` tramite `crypto.randomUUID()`, garantendo continuità della conversazione anche tra refresh di pagina.
- La risposta del backend viene gestita in **doppia modalità**: JSON standard oppure **streaming** (Server-Sent Events / chunked response).

---

##  Design

Il tema visivo è **"Ethereal Dark"**, basato su:
- Glassmorphism con `backdrop-filter: blur`
- Palette scura con accenti viola/indigo
- Animazioni e micro-interazioni CSS
- Layout completamente responsive (mobile-first)

---

##  Repository Correlati

| Repository | Descrizione |
|---|---|
| `includo-backend` | Backend Laravel con AI, RAG e database MySQL |

---

## Autore

Nicolò

📧 Email: nicomelzi05@gmail.com

🌐 GitHub: https://github.com/nico25m

💼 LinkedIn: https://linkedin.com/in/nicolò-melzi

🌐 Link al Progetto: https://nico25m.github.io/includo-frontend/

🌐 Link al Progetto webhosted: https://includo-frontend.vercel.app/
