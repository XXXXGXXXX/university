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

La ricostruzione è una copia di lavoro della trascrizione grezza, non un testo da redigere ex novo: duplica il file sorgente mantenendone testo, sequenza, paragrafi e marcatori, quindi applica direttamente alla copia solo correzioni locali giustificate. Non sostituire il grezzo e non ricreare la trascrizione a memoria, da appunti o da un riassunto. Confronta la copia con le altre fonti testuali disponibili e il contesto immediato. Correggi riconoscimento, segmentazione, punteggiatura o termini tecnici solo quando il testo sostiene la correzione; usa il contesto del corso per scegliere tra interpretazioni plausibili, mai per aggiungere contenuti.

Questa fase produce una trascrizione corretta, non un riassunto, appunti o una ricostruzione per argomenti. Resta vicina al verbatim: conserva nell'ordine tutto il parlato intelligibile, incluse ripetizioni, esitazioni, esempi, digressioni, interazioni, battute e richiami. Non potare, sintetizzare, accorpare frasi in formulazioni generiche, riordinare, parafrasare né rendere il discorso più formale. Sono ammesse solo correzioni palesi della trascrizione automatica, compresa una correzione grammaticale indispensabile a rendere leggibile il parlato senza cambiarne formulazione o senso. Non usare la plausibilità scientifica per trasformare parole incerte in affermazioni certe. Mantieni marcatori temporali e parlanti presenti, senza inventarne. Per dubbi irrisolti sostituisci solo la porzione non recuperabile con indicazioni uniformi come `[passaggio non comprensibile]` o `[termine incerto: …]`; non eliminare l'intera frase o il suo contesto, e aggiungi il tempo se disponibile.

Salva ogni parte come `.txt` con lo stesso identificativo completo della registrazione. Prima di usarla nel merge, verifica la corrispondenza tra registrazione, grezzo e ricostruzione. Procedi in sequenza sulla copia del grezzo: per ogni frase o unità di parlato, controlla che la ricostruzione contenga la stessa informazione e lo stesso ordine, mantenendo le parole recuperabili e marcando localmente quelle incerte. Non sostituire più frasi consecutive con un solo paragrafo tematico. Controlla le modifiche rispetto alla copia sorgente e annulla ogni riscrittura, omissione o riordino non motivato. Come controllo finale confronta anche lunghezza e numero di parole tra grezzo e ricostruzione: una riduzione superiore al 10% è un segnale obbligatorio per rifare il confronto dall'inizio; non è una soglia di accettazione né una giustificazione per tagliare. Ogni omissione residua deve essere identificabile come rumore non verbale, non parlato o duplicazione tecnica e non deve cancellare contenuto; in assenza di una motivazione verificabile, ripristina il segmento o rappresentalo con un marcatore d'incertezza. Il confronto sequenziale, non la somiglianza dei conteggi, è il criterio di completezza.

### 2. Unire le parti

Il merge è prima di tutto una trasformazione deterministica dei file, non una nuova generazione del testo. Individua le ricostruzioni della stessa data, verifica gli identificativi e ordinale per indice numerico (`_2` prima di `_10`). Non usare l'ordine alfabetico dei nomi, la data dei metadati o l'ordine restituito dal file system. Se identificativi, codifica o ordine sono ambigui, fermati su quella lezione e chiedi chiarimenti.

Costruisci il corpo iniziale del merge concatenando integralmente i file ricostruiti nell'ordine stabilito, con uno strumento di manipolazione dei file e senza passare il testo attraverso una riscrittura del modello. Conserva caratteri, paragrafi, punteggiatura e sequenza; non normalizzare o eliminare contenuto. Non aggiungere separatori testuali inventati tra le parti. Se un file non termina con un separatore di riga e la concatenazione unirebbe accidentalmente due segmenti, annota il confine e correggi solo la separazione minima nel file di merge; non alterare la ricostruzione sorgente. Inserisci le informazioni sulle parti incluse e mancanti in un'intestazione separata dal corpo, senza confonderle con il parlato.

Solo dopo aver prodotto questa concatenazione esamina i confini tra parti. Modifica il file di merge, non le ricostruzioni sorgenti, e limita gli interventi a duplicazioni effettive causate da sovrapposizioni documentabili oppure a raccordi le cui parole esatte siano recuperabili dalle ricostruzioni adiacenti. Registra nell'intestazione o in una nota di lavorazione identificativi del confine e testo rimosso o ricomposto, con la motivazione. Non formulare raccordi ex novo né parafrasarli: se manca un passaggio o la continuità non è certa, conserva il confine e segnala l'incertezza. Mantieni tutte le altre ripetizioni e i dettagli circostanziali.

Verifica il risultato in modo riproducibile: ricostruisci la concatenazione attesa dalle stesse fonti e confrontala con il corpo del merge, tenendo conto solo dell'intestazione e delle modifiche di confine esplicitamente registrate. Controlla che ogni segmento di ogni parte compaia nel merge nello stesso ordine, che nessun testo sia stato riscritto o omesso senza giustificazione e che nessuna parte sia duplicata o mancante. Se il confronto evidenzia differenze non spiegate, correggi il merge e ripeti la verifica. Non usare un riassunto, il conteggio delle parole o la sola somiglianza semantica come prova di correttezza e non modificare le ricostruzioni per parte per aggiornare il merge.

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

### Budget di token e dimensione dei blocchi

Prima di un passaggio lungo, stima la finestra di contesto effettivamente disponibile e considera insieme istruzioni, fonti, scheda di continuità, output atteso e margine per correzioni. Non saturare la finestra: come obiettivo iniziale usa al massimo il 55–60% per l'input, riserva almeno il 25% all'output e lascia il resto come margine. Sono quote di pianificazione, non soglie di correttezza: riduci il blocco se la risposta deve riprodurre quasi integralmente la fonte o se il conteggio è incerto. Non affidarti a una stima di token per dimostrare completezza.

Dimensiona il lavoro per fase:

- **Ricostruzione:** elabora una parte per volta e poi segmenti consecutivi abbastanza piccoli da poter confrontare ogni frase. Poiché l'output deve restare vicino al grezzo, limita di norma il testo sorgente a circa il 25–30% della finestra; includi solo istruzioni pertinenti e contesto adiacente minimo. Mantieni un breve margine sovrapposto tra blocchi per non perdere giunzioni, ma non duplicare il testo nel file finale.
- **Merge:** non reinserire in un unico prompt tutte le parti insieme al merge completo. Assembla le ricostruzioni in ordine usando gli strumenti testuali; usa il modello sui singoli confini e poi verifica per segmenti che il merge conservi contenuti e ordine. Il contesto di ogni controllo comprende le due giunzioni interessate, non l'intera lezione.
- **Piano editoriale:** lavora su segmenti del merge e registra le scelte in una struttura breve con riferimenti riconoscibili alla fonte. Riunisci i segmenti solo quando serve valutare la struttura complessiva; non copiare nel piano il merge né ripetere lunghi estratti.
- **Capitolo:** redigi una sezione o sottosezione per volta, passando il relativo estratto del merge e la parte corrispondente del piano. La scheda di continuità contiene solo terminologia e decisioni già verificate. Non chiedere in un singolo passaggio sia la stesura dell'intero capitolo sia la riproduzione o verifica integrale delle fonti.
- **Revisione:** confronta unità corrispondenti di merge, piano e capitolo, una sezione alla volta. La revisione deve poter vedere insieme fonte e testo da verificare; se non entrano con margine, riduci l'unità invece di sostituire il confronto con un riassunto. Restituisci discrepanze puntuali e riferimenti, non un generico giudizio di conformità.

### Uso dei subagents

Delega solo quando la quantità di materiale o il numero di unità indipendenti rende utile un contesto separato. Le parti distinte della stessa lezione e le lezioni indipendenti possono essere lavorate in parallelo; assegna a ciascun subagent identificativi e file di destinazione non sovrapposti. Non parallelizzare fasi dipendenti: merge dopo le ricostruzioni, piano dopo il merge, capitolo dopo il piano e la verifica finale dopo il capitolo.

Ogni incarico deve delimitare una sola unità, indicare le fonti autorizzate e vietate, le regole di trasformazione, il percorso di output e verifiche osservabili. Fornisci il contesto minimo necessario e i vincoli essenziali della fase, non l'intera cronologia, il corso o gli output di altre unità. Chiedi al subagent un artefatto completo oppure un rapporto breve con riferimenti verificabili, dubbi e controlli non eseguiti; evita relazioni narrative che duplicano la fonte e contaminano i passaggi successivi. Non trattare il risultato o la scheda di continuità come fonte primaria.

Usa, quando il volume lo giustifica, un controllo indipendente in contesto separato dalla generazione: il revisore riceve la fonte pertinente, l'artefatto e i criteri di accettazione, ma non le conclusioni del redattore. Chiedigli di segnalare omissioni, aggiunte, alterazioni d'ordine e incertezze con riferimenti puntuali; integra solo rilievi verificati sulla fonte. Il coordinatore mantiene la responsabilità di identificativi, ordine, coerenza tra fasi, integrazione dei risultati e verifiche finali. Un subagent non elimina i limiti di contesto: se il suo incarico supera il budget, va ulteriormente segmentato mantenendo confini e riferimenti, non alimentato con riassunti che sostituiscono la fonte.
