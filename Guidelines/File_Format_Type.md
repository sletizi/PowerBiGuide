# Formati Power BI: PBIX, PBIT, PBIP

## PBIX (Power BI Desktop File)

**Descrizione:**
Il formato `.pbix` è il file principale di Power BI Desktop. Contiene tutto il necessario per creare e visualizzare un report.

**Contiene:**
- Modello dati (importato o in DirectQuery)
- Power Query (ETL)
- Visualizzazioni e layout del report
- Misure, colonne calcolate e relazioni (DAX)

**Scenari d'uso:**
- Sviluppo locale del report
- Analisi interattiva
- Condivisione con altri utenti Power BI Desktop

---

## PBIT (Power BI Template File)

**Descrizione:**
Il file `.pbit` è un template di report. Non contiene i dati ma conserva la struttura del report e le query.

**Contiene:**
- Tutti gli elementi del `.pbix`, **esclusi i dati**
- Query Power Query con parametri
- Modello dati e misure DAX
- Layout del report

**Scenari d'uso:**
- Riutilizzo di un report con diverse fonti dati
- Distribuzione standardizzata di report all'interno dell'organizzazione

---

## PBIP (Power BI Project)

**Descrizione:**
Introdotto più recentemente, il formato `.pbip` è progettato per supportare scenari di **versionamento del codice**, **lavoro collaborativo** e integrazione con **sistemi di controllo versione** (es. Git).

**Come funziona:**
- Salva il progetto Power BI come una **struttura di file e cartelle** (anziché un singolo file binario come il PBIX)
- Ogni componente è salvato come file leggibile/modificabile (per lo più in JSON)

**Struttura tipica di un progetto PBIP:**
```
Project/
├── AdventureWorks.Report/
├── AdventureWorks.SemanticModel/
├── .gitignore
└── AdventureWorks.pbip
```

più dettagli al link:
https://learn.microsoft.com/it-it/power-bi/developer/projects/projects-overview

**Vantaggi:**
- Ogni componente è versionabile in modo indipendente
- Puoi collaborare su file diversi (es. uno lavora sul modello, un altro sul report)
- Integrazione nativa con Git e pipeline DevOps
- Comparazione facilitata tra versioni (i file sono leggibili/testuali)

**Scenari d'uso:**
- Progetti in team
- Gestione versioni (Git, Azure DevOps)
- Automazione e CI/CD di report Power BI

**Nota importante:**
> I file `.pbip` possono essere riaperti in Power BI Desktop. Da lì puoi riconvertirli in `.pbix` o gestirli direttamente come progetto.

---

## Confronto sintetico
| Formato | Contenuto | Dati inclusi | Scenari d'uso principali |
|---------|-----------|--------------|---------------------------|
| PBIX    | Report completo | ✅ Sì | Sviluppo locale, distribuzione |
| PBIT    | Template report | ❌ No | Riutilizzo, standardizzazione |
| PBIP    | Struttura progetto leggibile | ✅ Sì | Versionamento, DevOps, Git |

