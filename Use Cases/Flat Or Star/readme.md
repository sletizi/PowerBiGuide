# 📊 FLAT TABLE VS STAR SCHEMA (SPOTISTATS)

## 📘 Introduzione: Flat Table e Star Schema nel Modello Dati

Nella modellazione dei dati su Power BI, una decisione chiave è **quanto normalizzare le informazioni**.

- Un **modello flat** (denormalizzato) contiene **tutte le informazioni** in un'unica tabella: ad ogni riga corrispondono tutte le proprietà associate, anche se ripetute.
- Un **modello a stella (star schema)** separa le **dimensioni** dalla **tabella dei fatti**: le informazioni ripetitive vengono isolate in tabelle piccole e collegate tramite ID.

Questo use case su **SpotiStats** dimostra **come la scelta tra flat e star** influisca su:
- Occupazione dello spazio nel modello
- Prestazioni di caricamento e refresh
- Complessità ed efficienza delle formule DAX

---

## 💡 Obiettivo dello Use Case

Nella versione attuale di SpotiStats, la tabella `streaming_history` contiene direttamente:
- `Track` (nome brano)
- `Album` (nome album)
- `Artist` (nome artista)

Ogni volta che una canzone viene ascoltata, queste informazioni **sono ripetute** su ogni riga.

Il nostro obiettivo è:
- Dimostrare che separando `Track`, `Album` e `Artist` in una dimensione autonoma (`Dim_Track`) e collegandola alla tabella dei fatti (`streaming_history`) attraverso un identificativo (`TrackID`), si ottengono **significativi benefici**.


---

## 👩‍💻 Cosa andremo a dimostrare

### ✅ 1. **Riduzione dello spazio occupato**
- In un modello flat, `Track`, `Album` e `Artist` occupano diversi MB nella fact table.
- In un modello star schema, questi campi esistono **una sola volta** nella dimensione e la fact contiene solo l'ID (integer, molto più leggero).

### ✅ 2. **Miglioramento delle performance DAX**
- I filtri applicati alle dimensioni sono più veloci.
- Le formule lavorano su ID numerici anziché su stringhe lunghe.
- Possiamo sfruttare funzioni DAX come `RELATED`, `TREATAS` e gerarchie `Artist > Album > Track` in modo più efficiente.

### ✅ 3. **Costruzione di formule più semplici e modulari**
- Con un modello a stella, il codice DAX è più pulito e riutilizzabile.
- Possiamo creare calcoli di ascolti per artista, album o brano usando semplici filtri sulle dimensioni.

### ✅ 4. **Migliore scalabilità del modello**
- Aggiungere nuove proprietà (es. genere musicale, durata, anno di pubblicazione) diventa più semplice.
- Il modello è più pronto per l'ottimizzazione VertiPaq.

---

## 🔧 Come realizzeremo il test

Implementeremo due versioni del modello:

- **Flat Model**: `streaming_history` contiene `Track`, `Album`, `Artist` come colonne testuali.
- **Star Schema Model**: `streaming_history` contiene solo `TrackID`, collegato alla tabella `Dim_Track` con le informazioni testuali.

Su ciascun modello misureremo:
- ⌛ Tempo di refresh
- 📊 Dimensione totale del file PBIX
- 📊 Dimensione tabella streaming_history
- 🔢 Complessità e performance di alcune formule DAX (es. ascolti per artista, album più ascoltati, etc.)

---

## 🔹 In sintesi

Questo use case fornirà **prove pratiche e misurabili** che:
- Il **modello a stella** è più performante,
- Permette di scrivere **DAX più efficiente**,
- È più **scalabile** e **manutenibile** rispetto a una tabella flat.

Il tutto contestualizzato in un progetto reale e concreto come **SpotiStats** 👁‍🔍.

