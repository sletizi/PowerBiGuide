
# Linee guida per l’ottimizzazione e la gestione dei report Power BI  

## 1. Sposta le logiche sui Database ed evita operazioni pesanti in Power BI  
Per ottenere report più performanti:  
- **Sposta il più possibile le logiche sui Database**. Per report complessi, crea viste materializzate che puoi richiamare in modo più leggero.  
- **Evita le SELECT * (ed equivalenti)**. Seleziona solo i campi necessari e, se possibile, commenta quelli non utilizzati per poterli riprendere successivamente.  
- **Crea i campi calcolati alla fonte**, ovvero nel database o nel modello dati, anziché in Power BI. I calcoli fatti all’origine sono più efficienti rispetto a quelli eseguiti in tempo reale.  
- Limita l’uso di **Power Query per trasformare i dati**: cambia i tipi di dati e applica le trasformazioni alla fonte per ridurre il carico su Power BI.  

---

## 2. Usa l'architettura a stella  
Adotta sempre un'**architettura a stella** per la costruzione del modello dati:  
- Minimizza le tabelle di dimensione ridondanti, come le **dim_calendario**.  
- Mantieni relazioni chiare e pulite tra tabelle di fatto e tabelle di dimensione per semplificare la manutenzione.  

---

## 3. Filtro dinamico sulle date  
Evita di filtrare utilizzando date fisse. Utilizza **filtri dinamici** per assicurarti che il report rimanga sempre aggiornato, ad esempio filtrando gli ultimi 30 giorni o il mese corrente.  

---

## 4. Ottimizza il codice DAX  
Scrivere codice DAX efficiente può fare una grande differenza sulle prestazioni del report.  
Ecco alcuni consigli:  
- **Preferisci `DIVIDE` al simbolo `/`**, per evitare errori di divisione per zero e migliorare le performance.  
- Usa le **variabili (`VAR`)** per evitare calcoli ridondanti e migliorare la leggibilità del codice.  
- **Evita funzioni pesanti come `RELATED` e `LOOKUPVALUE`**: quando possibile, crea colonne calcolate nel modello dati o nel database.  
- **`SUMMARIZECOLUMNS`** è generalmente più performante rispetto a `SUMMARIZE`.  
- Evita calcoli in righe singole (`ROW CONTEXT`) quando puoi sostituirli con calcoli basati su contesto di filtro (`FILTER CONTEXT`).  

---

## 5. Evita di caricare milioni di record  
Progetta regole di aggregazione chiare insieme agli utilizzatori del report:  
- **Crea diversi report a seconda delle scale temporali** (giornaliera, mensile, annuale).  
- Riutilizza i dati esistenti per più report e ambiti, evitando duplicazioni inutili.  
- Pianifica attentamente il livello di dettaglio necessario e carica solo i record realmente utili per l’analisi.  

---

## 6. Pianifica gli aggiornamenti  
Organizza il calendario degli aggiornamenti in modo da evitare che troppe basi dati vengano aggiornate contemporaneamente. Questo riduce i rischi di sovraccarico e migliora la disponibilità del report per gli utenti finali.  

---

## 7. Usa i parametri per personalizzare i report  
I parametri in Power BI sono estremamente utili per offrire flessibilità agli utenti finali:  
- **Selezione dinamica di KPI**: consenti all’utente di scegliere quale KPI visualizzare su uno stesso grafico (ad esempio, fatturato, margine o costi).  
- **Filtri configurabili**: puoi creare delle **simil-Pivot** che permettono all’utente di aggregare i dati a piacimento.  
- **Confronti temporali dinamici**: usa i parametri per modificare il periodo di riferimento (ad esempio, anno corrente vs anno precedente).  

---

## 8. Limita il numero di visualizzazioni per pagina  
Non sovraccaricare una singola pagina del report con troppe visualizzazioni:  
- **Mantieni un design pulito** e facilmente leggibile, concentrandoti su 4-6 visualizzazioni per pagina.  
- **Blocca la visualizzazione di troppi record contemporaneamente** utilizzando filtri predefiniti, come la selezione di un singolo mese o trimestre per volta.  

---

## 9. Analizza le performance del report  
Se il report è lento, utilizza strumenti come **DAX Studio** e **Measure Killer** per individuare le misure o le query che stanno rallentando l’elaborazione.  
- **DAX Studio** ti permette di analizzare i tempi di esecuzione delle misure e ottimizzarle.  
- **Measure Killer** aiuta a identificare quali misure stanno pesando di più sul report.  

---

## 10. Utilizza un sistema di Version Control (Git) per il versioning dei report  
Versionare i report Power BI con Git consente di:  
- **Tracciare tutte le modifiche apportate** nel tempo.  
- **Collaborare in team** evitando conflitti.  
- **Ripristinare versioni precedenti** in caso di errori o regressioni.  

### 📌 Come utilizzare Git per Power BI  
- **Salva i report `.pbix` nel repository Git**, organizzando la struttura del progetto in cartelle (report, script SQL, documentazione).  
- Se vuoi un controllo più granulare, **estrai il contenuto del file `.pbix` in formato `.pbit`** (template) e traccia i singoli file JSON e XML.  
- Automatizza i commit con **script PowerShell** o integra una pipeline CI/CD per garantire che le versioni siano sempre aggiornate.
