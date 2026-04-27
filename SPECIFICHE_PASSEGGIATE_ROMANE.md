# 🎼 PASSEGGIATE ROMANE - SISTEMA ITINERARI TEMATICI
## Virtual Travel Assistant - Estensione con Percorsi Cronologici e Culturali

---

## 📋 PANORAMICA DEL SISTEMA

### Concetto Base
Il sistema evolve da una collezione statica di POI a un'esperienza narrativa strutturata attraverso **itinerari tematici** che:
- Seguono una sequenza cronologica (alba → tramonto)
- Sono associati a un **personaggio ispiratore** (artista, compositore, scrittore)
- Offrono **esperienze multisensoriali** (musica, letteratura, arte)
- Hanno una durata massima di **1 giorno**
- Creano un **filo narrativo coerente** tra i POI

---

## 🎯 CASO PILOTA: "Le Fontane di Roma di Respighi"

### Personaggio Ispiratore
**Ottorino Respighi (1879-1936)**
- Compositore italiano del periodo tardo-romantico
- Celebre per il poema sinfonico "Fontane di Roma" (1916)
- Opera in 4 movimenti, ciascuno dedicato a una fontana in un momento specifico della giornata

### Struttura dell'Itinerario

| Tappa | Fontana | Orario | Movimento Respighi | Durata Visita |
|-------|---------|--------|-------------------|---------------|
| 1 | Fontana di Villa Giulia | Alba (6:00) | I. La fontana di Valle Giulia all'alba | 45 min |
| 2 | Fontana del Tritone | Mattino (10:00) | II. La fontana del Tritone al mattino | 30 min |
| 3 | Fontana di Trevi | Mezzogiorno (12:30) | III. La fontana di Trevi al meriggio | 60 min |
| 4 | Fontana di Villa Medici | Tramonto (18:00) | IV. La fontana di Villa Medici al tramonto | 45 min |

**Durata totale:** ~8 ore (inclusi spostamenti e pause)

---

## 🏗️ ARCHITETTURA DATI

### Struttura JSON Estesa

```json
{
  "itinerari": [
    {
      "id": "respighi_fontane",
      "nome": "Le Fontane di Roma di Respighi",
      "personaggio": {
        "nome": "Ottorino Respighi",
        "biografia_breve": "Compositore...",
        "immagine": "assets/respighi.jpg",
        "opere_correlate": ["Fontane di Roma (1916)", "Pini di Roma (1924)"]
      },
      "tema": "Musica Classica - Poema Sinfonico",
      "durata_totale": "8 ore",
      "difficolta": "facile",
      "distanza_km": 6.5,
      "tappe": [
        {
          "numero": 1,
          "poi_id": "villa_giulia_fontana",
          "orario_consigliato": "06:00",
          "momento_giornata": "alba",
          "durata_visita_min": 45,
          "esperienza_culturale": {
            "musica": {
              "brano": "Fontane di Roma - I. La fontana di Valle Giulia all'alba",
              "spotify_url": "https://open.spotify.com/...",
              "descrizione_musicale": "Note pastorali evocano il canto degli uccelli..."
            },
            "letteratura": {
              "citazione": "L'alba su Roma è un dipinto che si rinnova...",
              "autore": "Gabriele D'Annunzio"
            },
            "atmosfera": "Quiete mattutina, luce dorata, canto degli uccelli"
          }
        },
        // ... altre tappe
      ],
      "note_logistiche": "Iniziare presto per godere dell'alba. Portare acqua.",
      "accessibilita": "Tutte le tappe sono accessibili con mezzi pubblici"
    }
  ],
  "poi": [
    // POI individuali con dati estesi
  ]
}
```

---

## 🎨 FUNZIONALITÀ DELL'INTERFACCIA

### 1. Vista Principale: Selezione Itinerario
- **Card degli itinerari** con:
  - Immagine del personaggio
  - Nome della passeggiata
  - Durata e difficoltà
  - Preview tappe (timeline visuale)
  - Bottone "Inizia Passeggiata"

### 2. Vista Itinerario Attivo
- **Timeline cronologica** laterale con:
  - Orari consigliati
  - Icone dei momenti della giornata (🌅🌞🌆🌃)
  - Indicatore tappa corrente
  - Progress bar (es. "Tappa 2/4 - 50% completato")

### 3. Vista Tappa Singola
- **Informazioni POI** standard (storia, curiosità)
- **Sezione "Esperienza Culturale"**:
  - 🎵 Player audio integrato (brano Respighi)
  - 📖 Citazione letteraria correlata
  - 🎨 Galleria immagini artistiche
  - 🌤️ Descrizione atmosfera (ora del giorno)

### 4. Navigazione Itinerario
- Bottoni "Tappa Precedente" / "Tappa Successiva"
- Mappa con percorso tracciato (linea colorata tra POI)
- Indicazioni di spostamento (tempo stimato, distanza)

---

## 🎼 ESPERIENZA CULTURALE MULTIMEDIALE

### Componente Musicale
```javascript
esperienza_culturale: {
  musica: {
    brano: "Fontane di Roma - I. La fontana di Valle Giulia all'alba",
    compositore: "Ottorino Respighi",
    esecutore: "Orchestra di Santa Cecilia, Antonio Pappano",
    durata_sec: 280,
    spotify_url: "https://...",
    youtube_url: "https://...",
    descrizione_musicale: "Il movimento si apre con dolci accordi d'archi 
                          che evocano il canto degli uccelli all'alba. 
                          Flauti e clarinetti imitano i trilli..."
  }
}
```

### Componente Letteraria
```javascript
letteratura: {
  citazione: "L'alba su Roma è un dipinto che si rinnova ogni mattino, 
             quando la luce dorata accarezza i marmi antichi...",
  autore: "Gabriele D'Annunzio",
  opera: "Il Piacere (1889)",
  contesto: "Descrizione del risveglio di Roma vista da Villa Medici"
}
```

### Componente Atmosferica
```javascript
atmosfera: {
  momento: "alba",
  luce: "dorata e radente",
  suoni: ["canto degli uccelli", "scroscio d'acqua", "silenzio urbano"],
  temperatura: "fresca (~15°C)",
  affollamento: "minimo",
  consiglio_fotografico: "Luce ideale per foto controluce della fontana"
}
```

---

## 🗺️ VISUALIZZAZIONE CARTOGRAFICA

### Mappa con Percorso Tracciato
```javascript
// Polyline che collega le tappe in sequenza
const routeCoordinates = [
  [41.9167, 12.4792], // Villa Giulia
  [41.9035, 12.4894], // Tritone
  [41.9009, 12.4833], // Trevi
  [41.9077, 12.4823]  // Villa Medici
];

const route = L.polyline(routeCoordinates, {
  color: '#e74c3c',
  weight: 4,
  opacity: 0.7,
  dashArray: '10, 10',
  lineJoin: 'round'
}).addTo(map);
```

### Marker Personalizzati per Tappa
- **Tappa 1 (Alba):** Marker arancione con icona 🌅
- **Tappa 2 (Mattino):** Marker giallo con icona ☀️
- **Tappa 3 (Mezzogiorno):** Marker rosso con icona 🌞
- **Tappa 4 (Tramonto):** Marker viola con icona 🌆

---

## 📱 INTERFACCIA UTENTE

### Homepage: Selezione Itinerario

```
┌─────────────────────────────────────────────┐
│  🏛️ PASSEGGIATE ROMANE                      │
│  Itinerari tematici attraverso la storia    │
└─────────────────────────────────────────────┘

┌─────────────────────────────────────────────┐
│ [Foto Respighi]                             │
│                                             │
│ 🎼 Le Fontane di Roma                       │
│    di Ottorino Respighi                     │
│                                             │
│ ⏱️ 8 ore  📍 4 tappe  🚶 6.5 km             │
│                                             │
│ Alba → Mattino → Mezzogiorno → Tramonto     │
│                                             │
│ [Inizia Passeggiata] [Dettagli]             │
└─────────────────────────────────────────────┘

┌─────────────────────────────────────────────┐
│ [Foto Caravaggio]                           │
│                                             │
│ 🎨 Sulle Tracce di Caravaggio               │
│    (Coming Soon)                            │
└─────────────────────────────────────────────┘
```

### Vista Itinerario Attivo

```
┌──────────────┬───────────────────────────────┐
│ TIMELINE     │ MAPPA + DETTAGLI              │
│              │                               │
│ 🌅 06:00     │ [MAPPA CON PERCORSO]          │
│ ● Villa      │                               │
│   Giulia     │ ━━━━━━━━━━━━━━━━━━━━━━━━━━━━ │
│              │                               │
│ ☀️ 10:00     │ 📍 TAPPA 2/4: Tritone         │
│ ◉ Tritone    │                               │
│ (ATTUALE)    │ [Foto Fontana Tritone]        │
│              │                               │
│ 🌞 12:30     │ 🎵 Ora ascolta:               │
│ ○ Trevi      │ ♫ Fontana del Tritone         │
│              │   (Respighi) [▶️ Play]        │
│ 🌆 18:00     │                               │
│ ○ Villa      │ 📖 Citazione:                 │
│   Medici     │ "Il Tritone sembra danzare..." │
│              │                               │
│ [← Indietro] │ [Prossima Tappa →]            │
└──────────────┴───────────────────────────────┘
```

---

## 🧩 COMPONENTI AGGIUNTIVI

### 1. Progress Tracker
```javascript
{
  tappe_completate: 1,
  tappe_totali: 4,
  percentuale: 25,
  tempo_trascorso: "1h 30min",
  tempo_stimato_rimanente: "6h 30min"
}
```

### 2. Audio Player Integrato
```html
<div class="music-player">
  <h4>🎵 Ascolta il brano dedicato:</h4>
  <audio controls>
    <source src="audio/respighi_tritone.mp3" type="audio/mpeg">
  </audio>
  <p class="music-description">
    Orchestra di Santa Cecilia - Antonio Pappano<br>
    <em>"Il Tritone emerge possente dalle acque..."</em>
  </p>
</div>
```

### 3. Indicazioni di Spostamento
```javascript
{
  da: "Fontana del Tritone",
  a: "Fontana di Trevi",
  distanza_m: 850,
  tempo_a_piedi: "12 min",
  indicazioni: "Scendi per Via del Tritone, prosegui fino a Via delle Muratte"
}
```

---

## 📊 SCHEMA DATI COMPLETO

### Tabella Relazioni

```
ITINERARI (1) ─────── ha ─────── (N) TAPPE
                                   │
                                   │ riferisce
                                   ↓
                                  POI (1)
                                   │
                                   │ contiene
                                   ↓
                        ESPERIENZA_CULTURALE (1)
```

### Campi Richiesti

**ITINERARIO:**
- id, nome, personaggio, tema, durata_totale, difficoltà, distanza_km
- tappe[], note_logistiche, accessibilità

**TAPPA:**
- numero, poi_id, orario_consigliato, momento_giornata, durata_visita_min
- esperienza_culturale{}, indicazioni_spostamento{}

**POI:**
- id, nome, coordinate, descrizione, storia, curiosità, metadata{}

**ESPERIENZA_CULTURALE:**
- musica{}, letteratura{}, atmosfera{}, galleria_immagini[]

---

## 🎓 VALORE DIDATTICO

### Per gli Studenti
- **Interdisciplinarità:** Collega musica, letteratura, storia dell'arte
- **Pensiero cronologico:** Sequenza temporale degli eventi
- **Gestione del tempo:** Pianificazione itinerario reale

### Per i Turisti
- **Esperienza immersiva:** Non solo vedere, ma ascoltare e sentire
- **Narrativa coerente:** Filo rosso che lega i luoghi
- **Ottimizzazione visita:** Percorso già pianificato

### Per le Istituzioni
- **Destagionalizzazione:** Passeggiate all'alba/tramonto
- **Valorizzazione asset minori:** Villa Giulia meno nota di Trevi
- **Engagement culturale:** Musica classica come attrattore

---

## 🔮 ITINERARI FUTURI

### 2. "Sulle Tracce di Caravaggio"
- **Personaggio:** Michelangelo Merisi da Caravaggio
- **Tema:** Arte Barocca e vita dissoluta
- **Tappe:** 
  1. Vicolo del Divino Amore (casa) - Mattino
  2. San Luigi dei Francesi - Mezzogiorno
  3. Santa Maria del Popolo - Pomeriggio
  4. Campo de' Fiori (scena del delitto) - Sera
- **Esperienza:** Lettura brani processuali, analisi opere

### 3. "La Roma di Goethe - Il Viaggio in Italia"
- **Personaggio:** Johann Wolfgang von Goethe
- **Tema:** Grand Tour letterario
- **Tappe:** Caffè Greco, Colosseo, Villa Borghese, Campidoglio
- **Esperienza:** Letture da "Viaggio in Italia", stampe d'epoca

### 4. "I Giardini Segreti del Rinascimento"
- **Personaggio:** Papa Giulio II
- **Tema:** Architettura dei giardini
- **Tappe:** Villa Farnesina, Orto Botanico, Villa Doria Pamphilj, Giardino degli Aranci
- **Esperienza:** Botanica rinascimentale, simbologia vegetale

---

## 🛠️ IMPLEMENTAZIONE TECNICA

### File Structure
```
vta-passeggiate/
├── index.html
├── itinerari.json          ← Nuovo file dati itinerari
├── poi.json                ← POI individuali (espanso)
├── assets/
│   ├── personaggi/
│   │   ├── respighi.jpg
│   │   └── caravaggio.jpg
│   ├── audio/
│   │   ├── respighi_villa_giulia.mp3
│   │   ├── respighi_tritone.mp3
│   │   └── ...
│   └── citazioni/
│       └── dannunzio_alba.txt
└── styles/
    └── itinerari.css
```

### API Endpoints (Futuro)
```
GET /api/itinerari              → Lista tutti gli itinerari
GET /api/itinerari/{id}         → Dettaglio itinerario
GET /api/itinerari/{id}/tappe   → Tappe dell'itinerario
POST /api/progresso             → Salva progresso utente
GET /api/meteo/{data}           → Consigli meteo per itinerario
```

---

## 📈 METRICHE DI SUCCESSO

### KPI da Monitorare
1. **Completion Rate:** % utenti che completano l'itinerario
2. **Time on Site:** Durata media sessione (target: >45 min)
3. **Audio Play Rate:** % utenti che ascoltano i brani musicali
4. **Share Rate:** Condivisioni social dell'itinerario
5. **Return Rate:** Utenti che fanno >1 passeggiata

### A/B Testing
- Con vs senza musica → Engagement
- Timeline visuale vs testuale → Usabilità
- Orari fissi vs flessibili → Completion rate

---

## ✅ CHECKLIST SVILUPPO

**Fase 1: MVP (Minimum Viable Product)**
- [ ] Struttura dati itinerari.json
- [ ] UI selezione itinerario (card)
- [ ] Mappa con percorso tracciato
- [ ] Timeline laterale
- [ ] Navigazione tappe (prev/next)

**Fase 2: Esperienza Culturale**
- [ ] Audio player integrato
- [ ] Citazioni letterarie
- [ ] Descrizioni atmosfera
- [ ] Galleria immagini

**Fase 3: Features Avanzate**
- [ ] Progress tracking (localStorage)
- [ ] Indicazioni spostamento (Google Maps API)
- [ ] Notifiche orario ottimale
- [ ] Modalità offline (PWA)

**Fase 4: Scalabilità**
- [ ] Almeno 3 itinerari completi
- [ ] CMS per gestione contenuti
- [ ] Analytics integrato
- [ ] Multilingua (EN, IT)

---

**Versione Documento:** 1.0  
**Data:** 2025-02-03  
**Autore:** Virtual Travel Assistant - Passeggiate Romane Extended
