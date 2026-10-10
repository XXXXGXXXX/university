# Guida per lavorare sulle lezioni

## Obiettivo e priorità

Per ogni corso, trasforma le trascrizioni automatiche in una trascrizione ricostruita per parte, un merge per lezione, un piano editoriale e appunti universitari completi in LaTeX. Includi il capitolo nel documento del corso, compila il PDF e registra una breve revisione finale.

La fedeltà alle fonti viene prima della brevità: il capitolo è materiale di studio completo, non un riassunto. La libertà editoriale aumenta per fasi: correzioni limitate nella ricostruzione, soli raccordi nel merge, tagli espliciti e motivati nel piano, riformulazione fedele nel capitolo. Non colmare lacune né aggiungere conoscenze non sostenute dalle fonti.

## Fonti, identificativi e destinazioni

- Ogni cartella di primo livello dedicata a un corso è un'unità indipendente. Individua in essa le registrazioni, le trascrizioni grezze e le convenzioni già in uso; la cartella delle trascrizioni può chiamarsi `trascarizioni` e non va rinominata senza richiesta.
- Le registrazioni audio sono risorse dell'utente: non aprirle, riprodurle o usarle per verifiche, e non chiedere accesso. È consentito controllarne nomi e identificativi per abbinare le parti; le sole fonti consultabili per i contenuti sono i testi disponibili.
- Non modificare le fonti grezze. Mantieni separati i materiali sorgente, gli intermedi e i capitoli:
  - `elaborati-assistente/trascrizioni-ricostruite/YYYY-MM-DD_N.txt`: ricostruzione di ciascuna parte e `YYYY-MM-DD.txt`: merge della lezione;
  - `elaborati-assistente/appunti/YYYY-MM-DD.md`: piano editoriale;
  - `elaborati-assistente/revisioni/YYYY-MM-DD.md`: revisione finale;
  - `lezioni/YYYY-MM-DD.tex`: capitolo completo della lezione.
- L'identificativo canonico della fonte è `YYYY-MM-DD_N` (data della lezione e indice della parte). Abbina registrazione, trascrizione grezza e ricostruzione per identificativo completo, non per vicinanza o data dei file; ordina per data e indice numerico. Non dedurre la data dai metadati dei file né correggere nomi discordanti per supposizione. In caso di discrepanza, segnala il problema e chiedi indicazioni.
- Prima di creare file o cartelle, controlla la struttura effettiva, `main.tex` e le impostazioni del corso; riusa le convenzioni compatibili. La configurazione in `.vscode/settings.json` definisce la ricetta di compilazione e i PDF vanno in `.build/`.

## Avvio e selezione del lavoro

- La richiesta `lezione` avvia il flusso completo per le nuove trascrizioni già fornite. Trattala come equivalente a `aggiorna appunti` o `elabora le nuove trascrizioni`; non chiedere quale lezione elaborare se le fonti la identificano. Se l'utente specifica corso o lezione, limita lì la scansione.
- All'avvio esamina le cartelle dei corsi e le sorgenti grezze, senza confonderle con gli output. Confronta le parti con le ricostruzioni, poi verifica per data merge, piano, capitolo e relativo `\input` in `main.tex` per individuare il lavoro mancante.
- Completa le fasi mancanti senza rigenerare o sovrascrivere risultati esistenti. Se una fonte grezza è cambiata dopo l'elaborazione, segnala la differenza e chiedi prima di sostituire gli output. Se non c'è lavoro, non modificare né ricompilare nulla. Se un'ambiguità blocca una lezione, esplicitala e prosegui con le lezioni indipendenti.
- Lavora solo sui materiali necessari alla lezione; non caricare o riassumere un intero corso per dare contesto. Non accorpare date diverse. Riunisci in un solo capitolo tutte le parti disponibili della stessa data, in ordine numerico. Se una parte manca, non inventarla: indica nel merge e nel capitolo le parti assenti e i limiti che ne derivano.

## Flusso di lavoro

### 1. Ricostruire ciascuna parte

Confronta la trascrizione grezza con le altre fonti testuali disponibili e il contesto immediato. Correggi riconoscimento, segmentazione, punteggiatura o termini tecnici solo quando il testo sostiene la correzione; usa il contesto del corso per scegliere tra interpretazioni plausibili, mai per aggiungere contenuti.

Questa fase resta vicina al verbatim: conserva nell'ordine tutto il parlato intelligibile, incluse ripetizioni, esitazioni, esempi, digressioni, interazioni e richiami. Non potare, sintetizzare, riordinare, parafrasare né rendere il discorso più formale. Sono ammesse solo correzioni palesi della trascrizione automatica, compresa una correzione grammaticale necessaria a rendere leggibile il parlato senza cambiarne formulazione o senso. Mantieni marcatori temporali e parlanti presenti, senza inventarne. Per dubbi irrisolti usa indicazioni uniformi come `[passaggio non comprensibile]` o `[termine incerto: …]`, aggiungendo il tempo se disponibile.

Salva ogni parte come `.txt` con lo stesso identificativo completo della registrazione. Prima di usarla nel merge, verifica la corrispondenza tra registrazione, grezzo e ricostruzione. Controlla in sequenza che ogni segmento intelligibile sia rappresentato e che non siano scomparse frasi o informazioni per brevità o rilevanza presunta.

### 2. Unire le parti

Crea `elaborati-assistente/trascrizioni-ricostruite/YYYY-MM-DD.txt` usando esclusivamente le ricostruzioni della stessa lezione, in ordine numerico. Esamina la giunzione di ogni coppia: rimuovi solo duplicazioni dovute a sovrapposizioni documentabili e completa un raccordo solo se le parole sono recuperabili con certezza dai testi e dal contesto immediato. Non riscrivere, riassumere, riordinare o potare.

Mantieni ripetizioni e dettagli circostanziali. Se il raccordo è incerto, conserva una separazione o segnala il passaggio mancante, senza creare continuità artificiale. Riporta all'inizio le parti incluse e quelle attese ma mancanti; rendi riconoscibili confini e interruzioni quando necessario. Verifica il merge in sequenza contro tutte le parti: a parte duplicazioni di confine documentate e raccordi certi, deve conservarne tutto il testo e l'ordine. Non modificare le ricostruzioni per parte per aggiornare il merge.

### 3. Preparare il piano editoriale

Crea un solo `elaborati-assistente/appunti/YYYY-MM-DD.md`, basato sul merge; consulta le ricostruzioni per chiarire dubbi. Non usare fonti esterne o audio. Il piano è uno strumento operativo, non una trascrizione, un capitolo o un sorgente LaTeX.

Indica contenuti e concetti presenti, struttura e sequenza proposte, raccordi e riformulazioni utili a una prosa universitaria chiara e rigorosa, senza cambiare significato o ridurre informazioni. Evidenzia definizioni, esempi, cautele, eccezioni, nessi logici, termini incerti e lacune da preservare.

La selezione editoriale avviene qui: specifica ogni omissione proposta con riferimento o contenuto riconoscibile e motivazione, spiegando perché non fa perdere contenuto o contesto utile. Limitala a rumore, duplicazioni, interruzioni tecniche o digressioni senza valore didattico. Non scartare esempi, ripetizioni esplicative, precisazioni, eccezioni, domande d'esame o digressioni che aggiungono contesto; nel dubbio, conserva. Non presentare come certo ciò che la fonte lascia incerto. Se non ci sono omissioni giustificate, non proporne.

### 4. Redigere il capitolo

Crea `lezioni/YYYY-MM-DD.tex` usando insieme piano e merge: il piano guida struttura e tagli, il merge resta il riferimento per la fedeltà. Scrivi appunti completi, organici e formali, non un riassunto. Conserva tutti i contenuti sostanziali intelligibili: definizioni, ragionamenti, esempi, analogie, precisazioni, eccezioni, ripetizioni utili e richiami. Puoi riorganizzare e correggere la forma, ma non comprimere più idee in formulazioni generiche né omettere contenuti perché colloquiali, secondari o apparentemente ridondanti. Applica solo omissioni esplicitamente motivate nel piano; escludi al più rumore, interruzioni tecniche, scambi non didattici e passaggi incomprensibili. Non colmare limiti della fonte per supposizione.

Prima di intervenire, controlla il preambolo, la lingua, la struttura, `main.tex` e i capitoli esistenti. Il capitolo deve essere un sorgente incluso nel documento del corso, non un documento autonomo né un rinvio agli intermedi: non dichiarare un secondo `\documentclass` e normalmente non usare `\input` al suo interno. Aggiungi in commenti iniziali le fonti effettivamente consultate (merge e percorsi relativi/nominativi delle trascrizioni grezze e ricostruite per ogni parte usata); puoi elencare i nomi dei file audio solo per identificare le risorse, specificando che non sono state consultate. Indica parti mancanti e passaggi testuali incerti. Usa file LaTeX ausiliari solo se necessari e documentane la ragione.

Organizza il capitolo con sezioni e sottosezioni adatte allo studio; usa formule, tabelle, elenchi o immagini solo se chiariscono contenuti sostenuti dalle fonti. Rispetta stile e convenzioni del corso, proteggi i caratteri speciali e controlla ambienti, parentesi, riferimenti e percorsi. Inserisci in `main.tex` un `\input{lezioni/YYYY-MM-DD}` senza sostituire il documento principale. Compila con la ricetta in `.vscode/settings.json`, risolvi gli errori introdotti e verifica che il PDF aggiornato sia in `.build/`.

### 5. Revisionare e consegnare

Dopo la compilazione, rileggi ogni sezione e sottosezione confrontandola in sequenza con il merge e con le scelte del piano. Verifica fedeltà, copertura, esempi, precisazioni, terminologia, omissioni autorizzate e assenza di aggiunte non supportate; non basarti sulla sola fluidità né sulle verifiche già svolte durante la stesura. La revisione riguarda le fonti testuali disponibili: non richiedere né rimandare a controlli audio.

Crea o aggiorna `elaborati-assistente/revisioni/YYYY-MM-DD.md` con esito, problemi concreti (o indicazione esplicita che non ne sono emersi), testi confrontati e limiti/incertezze residui. Se trovi errori o omissioni sostanziali, correggi il capitolo, ricompila e ripeti il controllo delle sezioni interessate; documenta solo l'esito della versione finale. Non dichiarare verifiche non eseguite o criticità non risolte.

Prima della consegna accertati che le fonti grezze siano intatte; gli identificativi e l'ordine delle parti siano corretti; ricostruzioni, merge, piano e capitolo rispettino le regole delle rispettive fasi; il merge e il capitolo segnalino parti mancanti e dubbi; il capitolo sia incluso in `main.tex`, compilato e presente nel PDF in `.build/`; la revisione finale sia documentata. Nel riepilogo indica file creati o aggiornati, verifiche effettivamente svolte e punti ancora incerti o bloccati.

## Uso del contesto

Gestisci una lezione alla volta e mantieni distinti grezzo, ricostruzione, merge, piano e capitolo. Per ogni blocco passa solo il segmento necessario e il minimo contesto adiacente. Tra blocchi conserva una breve scheda di continuità con termini e grafie verificati, nomi o abbreviazioni, decisioni editoriali e dubbi aperti; non trattarla come fonte e verifica ogni affermazione sui testi ricostruiti. Non trasferire automaticamente terminologia o conclusioni tra corsi, lezioni o versioni delle fonti. A ogni fase confronta l'output con la sua fonte.
