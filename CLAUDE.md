# CLAUDE.md – Documenti di progetto SAP

## Obiettivo
Redigere documenti di progetto SAP partendo dai template forniti. **Al momento si produce solo l'Analisi Funzionale** (Functional Technical Specification). BDP, BPML e RTM verranno in seguito, con i loro template.

Progetto attuale: **Programma calcolo IFRS 16**, un **documento unico** che copre due pillar:
1. **Pillar 1 – Interface/Estrazione**: un programma con transazione estrae da S4 le registrazioni contabili IFRS 16 (tabella `VIRADOCITEM`) e le salva su file, in locale o su cartella di rete. Il file viene poi caricato su ECC, a mano oppure con un job che usa un programma già esistente (TBD).
2. **Pillar 2 – Report**: un report parte dai contratti Real Estate IFRS 16 presenti su S4 e produce uno schema di voci. Gli utenti riportano poi queste voci a mano sul sistema del bilancio consolidato.

## Cartelle (`Programma calcolo IFRS16/`)
| Cartella | Contenuto | Uso |
|---|---|---|
| `TEMPLATE/` | `CHN-402-…_V3.docx` | Modello di struttura e stile. **Non modificarlo**: lavora sempre su una copia. |
| `NOTE/` | Appunti dell'utente | Fonte principale dei requisiti. |
| `EXAMPLE/` | `BACHINPUT BASE.xlsx`, CSV di output di esempio | Specifiche del Pillar 1: tracciato e mapping, parametri di selezione, tabelle custom (`ZGUID`, `ZCONTI_IFRS16`), controlli. |
| `TABLES/` | Estratti di tabelle SAP (es. `VIRADOCITEM`) | Per nomi dei campi e dati di esempio. |
| `MAIL/` | Thread di mail con il cliente (`.msg`, leggibili con `olefile`) | Decisioni concordate: logica delta, centri di costo, schema contabile, regole del batch input, voci del consolidato. Prevalgono su appunti ed Excel se più recenti. |
| `OUTPUT/` | Documenti prodotti | Qui si salvano i documenti finiti. |

Nota: gli appunti numerano i fogli Excel in modo diverso dall'ordine reale. Fai riferimento al **nome del foglio**, non al numero.

## Come redigere il documento
1. Leggi tutti i file di `NOTE/`, `EXAMPLE/`, `TABLES/` e `MAIL/` prima di scrivere.
2. Parti da una copia del template: mantieni gli stili Word (`Heading 1/2`, `Body copy`), le tabelle e l'indice, e sostituisci il contenuto del CHN-402. Per i file `.docx` usa python-docx.
3. **Frontespizio e dati del documento:**
   - Object ID e titolo: segnaposto `CHN-XXX – Programma calcolo IFRS 16`
   - Progetto / Cliente: `AMS SAP` / `E80`
   - Autore: **Giuseppe Simone**
   - Revisore: **Filippo Boriello – SDM Deloitte**
   - Object Type: Report + Interface
   - Process Area: Finance
4. **Lingua:** titoli delle sezioni in inglese, come nel template. Testo in italiano.
5. **Livello tecnico:** lo stesso del CHN-402.
   - Cita esplicitamente tabelle e campi SAP (es. `VIRADOCITEM-BUKRS`).
   - Numera gli step di elaborazione.
   - Descrivi parametri di selezione e output (ALV o file).
6. Riporta il **mapping del tracciato del Pillar 1** (foglio "Struttura file e mapping", riga 2) come **griglia** con queste colonne: campo di output, fonte o regola, note.
7. Per le **informazioni mancanti** (es. step del Pillar 2 successivi al 2, "file Excel Y", programma ECC, report standard "RF S XXX"):
   - scrivi comunque il documento;
   - segna il punto come **TBD** nel testo;
   - aggiungilo alla tabella **Open Items**.

   Non fermarti a chiedere.

## Salvataggio e versioni
- Percorso: `Programma calcolo IFRS16/OUTPUT/CHN-XXX-AnalisiFunzionale_IFRS16_V<n>.docx`
- A ogni revisione salva un nuovo file con la versione successiva (V2, V3…) e aggiungi una riga alla tabella **Document Edit History**: versione, data, modifiche, autore.
