# Guida per lavorare sulle lezioni

## Obiettivo

Per ogni corso, trasformare le registrazioni e le trascrizioni automatiche in:

1. trascrizioni ricostruite, il più possibile fedeli parola per parola a ciò che è stato detto;
2. una trascrizione ricostruita unica per lezione, ottenuta raccordando le parti disponibili;
3. un piano editoriale degli appunti della lezione;
4. un capitolo LaTeX completo, incluso nel documento del corso e compilato in PDF.

La fedeltà alle fonti viene prima della completezza apparente o dello stile. Non colmare lacune con nozioni plausibili ma non supportate.

## Struttura e convenzioni

- Ogni cartella di primo livello dedicata a un corso è un'unità di lavoro indipendente.
- In ciascun corso, individua la cartella delle registrazioni e quella delle trascrizioni grezze. Nei materiali esistenti la cartella delle trascrizioni può chiamarsi `trascarizioni`: trattala come cartella sorgente e non rinominarla senza richiesta.
- Non modificare né sovrascrivere registrazioni e trascrizioni grezze.
- Salva i risultati in cartelle distinte; usa l'identificativo completo per i file relativi a una singola parte e la sola data per gli elaborati dell'intera lezione:
  - `elaborati-assistente/trascrizioni-ricostruite/`: una trascrizione `.txt` per ogni registrazione/parte (`YYYY-MM-DD_N.txt`) e la trascrizione unificata della lezione (`YYYY-MM-DD.txt`);
  - `elaborati-assistente/appunti/`: un piano editoriale in Markdown per lezione (`YYYY-MM-DD.md`), non un testo LaTeX e non il capitolo definitivo;
  - `lezioni/`: un capitolo LaTeX completo e autonomo per lezione (`YYYY-MM-DD.tex`), importato dal `main.tex` del corso.
- Usa come identificativo canonico della fonte la parte del nome nel formato `YYYY-MM-DD_N` (per esempio `2026-10-01_1`): la data è quella della lezione e `N` identifica la parte. Mantieni esattamente lo stesso identificativo, inclusi separatori e indice, nella registrazione, nella trascrizione grezza e nella trascrizione ricostruita; cambia solo l'estensione e la cartella. Non usare la data di creazione o modifica dei file al posto della data della lezione.
- Prima di elaborare una fonte, verifica la corrispondenza dell'identificativo completo tra registrazione, trascrizione grezza e trascrizione ricostruita. Abbina le parti per identificativo, non solo per vicinanza delle date; ordinale per data e poi per indice numerico. Se date o indici non corrispondono, non correggere o accorpare i nomi per supposizione: segnala la discrepanza e chiedi indicazioni.
- Tutti gli elaborati intermedi dell'assistente devono restare sotto `elaborati-assistente/`, separati dai materiali dell'utente. Le trascrizioni ricostruite per parte sono testo semplice `.txt` con identificativo `YYYY-MM-DD_N`; il merge della lezione è un distinto file `.txt` denominato `YYYY-MM-DD.txt`. Gli appunti sono un piano editoriale Markdown denominato `YYYY-MM-DD.md`. Il capitolo finale `lezioni/YYYY-MM-DD.tex` contiene direttamente il capitolo LaTeX completo: in generale non deve includere con `\input` altri file di appunti o frammenti.
- Prima di creare o rinominare cartelle o file, controlla la struttura effettiva e i riferimenti in `main.tex`. Riutilizza le convenzioni già presenti quando non sono in conflitto con queste indicazioni.
- Usa `.vscode/settings.json` come fonte per la ricetta di compilazione e la cartella dei PDF. La configurazione corrente produce i PDF in `.build/` all'interno della cartella del corso, separandoli dalle cartelle operative.

## Flusso di lavoro

### Avvio rapido

- Il comando `lezione` avvia il flusso completo per le nuove trascrizioni grezze già fornite dall'utente nelle cartelle dei corsi. Avvialo senza chiedere quale lezione elaborare quando le fonti permettono di identificarla.
- Sono equivalenti richieste brevi come `aggiorna appunti` o `elabora le nuove trascrizioni`; se l'utente indica un corso o una lezione specifici, limita la scansione a quelli.
- All'avvio, passa in rassegna le cartelle di primo livello dei corsi e individua le cartelle sorgente delle trascrizioni, incluse quelle chiamate `trascarizioni`. Non trattare cartelle di output o file già elaborati come fonti grezze.
- Confronta gli identificativi dei file grezzi con le ricostruzioni per parte; verifica poi, per data, la trascrizione unificata, il piano editoriale, `lezioni/` e i relativi `\input` in `main.tex` per individuare fasi mancanti. Elabora le nuove fonti e riprendi le fasi mancanti senza rigenerare né sovrascrivere risultati esistenti. Se una fonte grezza è cambiata dopo l'elaborazione, non sostituire automaticamente i risultati: segnala la differenza e chiedi indicazioni.
- Raggruppa in un solo capitolo tutte le parti della stessa lezione: il file sotto `lezioni/` si chiama `YYYY-MM-DD.tex`, mentre le fonti e le ricostruzioni per parte mantengono l'indice (`YYYY-MM-DD_N`). Il capitolo deve essere un sorgente LaTeX completo per quella lezione, non un indice di `\input` verso gli appunti intermedi. In generale non inserire `\input` dentro il capitolo; ammettilo solo quando una necessità concreta lo giustifica. Prima di intervenire, controlla i capitoli e gli `\input` esistenti per evitare duplicati.
- Usa la data dell'identificativo canonico come data della lezione. Il capitolo deve integrare le parti disponibili della stessa data in ordine numerico; non accorpare fonti con date diverse. Se manca una trascrizione o una parte, non inventarne il contenuto: segnala chiaramente che il capitolo è incompleto e quali fonti mancano.
- Per ogni lezione nuova o incompleta, esegui nell'ordine: ricostruisci ciascuna parte, unisci le parti ricostruite in un'unica trascrizione della lezione, scrivi il piano editoriale, redigi da quel piano e dalla trascrizione un capitolo LaTeX completo. Infine assicurati che `main.tex` importi il capitolo con `\input{lezioni/YYYY-MM-DD}` e compila il PDF nella cartella `.build/` del corso. Segui tutte le verifiche e le cautele descritte nelle sezioni successive.
- Se l'audio corrispondente è disponibile, usalo per verificare la trascrizione secondo le regole sotto; se manca o non è accessibile, lavora solo sul testo grezzo, senza dichiarare una verifica audio e indicando chiaramente il limite. Non inventare parti mancanti.
- Se non ci sono nuove fonti né fasi da completare, non modificare o ricompilare nulla e riferisci che non è stato trovato lavoro. Se un problema o un'ambiguità blocca una lezione, non indovinare: segnala cosa manca e prosegui con le altre lezioni indipendenti.

### 1. Delimitare il lavoro

- Identifica corso, lezione, data, registrazioni e corrispondenti trascrizioni grezze.
- Verifica l'ordine delle parti e se una lezione è distribuita su più registrazioni.
- Lavora solo sui materiali necessari alla lezione richiesta; non caricare o riassumere interi corsi per fornire contesto.
- Annota in modo sintetico eventuali fonti mancanti, parti non corrispondenti o problemi di qualità audio.

### 2. Ricostruire la trascrizione

- Confronta la trascrizione grezza con l'audio, ascoltando il passaggio dubbio e un margine sufficiente prima e dopo. L'audio è la fonte primaria; la trascrizione e il contesto servono a localizzare e interpretare le parole, non a sostituire l'ascolto.
- Se l'audio non è accessibile o intelligibile, non dichiarare di averlo verificato. Correggi solo gli errori sostenuti dal testo e dal contesto immediato; segnala i passaggi irrisolti.
- Correggi errori di riconoscimento, segmentazione, punteggiatura e termini tecnici solo quando la correzione è sostenuta dalla fonte. Usa il contesto del corso per scegliere tra interpretazioni plausibili, non per aggiungere contenuti.
- Conserva ordine, significato, esempi, ripetizioni rilevanti, esitazioni che cambiano il senso e formulazioni effettivamente pronunciate. Non riscrivere il parlato come appunti in questa fase.
- Non inventare parole, definizioni, nessi causali, nomi o citazioni. Se un passaggio non è ricostruibile, usa una notazione esplicita e uniforme, ad esempio `[passaggio non comprensibile]` o `[termine incerto: …]`; aggiungi un riferimento temporale quando disponibile.
- Mantieni eventuali marcatori temporali o riferimenti ai parlanti già presenti, senza crearne di non verificati.
- Salva il risultato come testo semplice `.txt` in `elaborati-assistente/trascrizioni-ricostruite/`, con lo stesso identificativo completo della registrazione. Non inserire comandi o marcatura LaTeX. Mantieni distinguibili le parti della lezione.
- Prima di includere una trascrizione ricostruita per parte nel merge, verifica che il suo identificativo coincida con quello della trascrizione grezza e della registrazione corrispondenti.

### 3. Unire le trascrizioni ricostruite

- Dopo aver ricostruito le singole parti, uniscile in ordine numerico in `elaborati-assistente/trascrizioni-ricostruite/YYYY-MM-DD.txt`. Usa come base solo le trascrizioni ricostruite delle parti della stessa lezione, non le trascrizioni grezze direttamente.
- Esamina con attenzione la fine e l'inizio di ogni coppia di parti consecutive. Quando il discorso prosegue e il raccordo è sostenuto dal contesto immediato, collega le frasi senza ripetizioni e correggi soltanto eventuali parole chiaramente recuperabili. Non colmare lacune con ipotesi.
- Se il raccordo non è certo, mantieni una separazione esplicita tra le parti o un'indicazione di passaggio mancante/incerto, invece di creare una continuità artificiale. Conserva nel merge le informazioni circostanziali e le ripetizioni ancora presenti nella ricostruzione: la selezione editoriale avviene nel piano e nel capitolo, non alterando la trascrizione.
- Rendi riconoscibili i confini o le interruzioni quando servono a non confondere un cambio di registrazione con una pausa del docente. Riporta all'inizio del file le parti incluse e segnala quelle attese ma mancanti; non inventarne il contenuto.
- Verifica il merge rileggendo in sequenza le giunzioni e confrontandolo con tutte le trascrizioni ricostruite incluse. Non sovrascrivere una trascrizione per parte per aggiornare il merge.

### 4. Preparare il piano editoriale

- Parti dalla trascrizione unificata `YYYY-MM-DD.txt`. Consulta le trascrizioni ricostruite per parte e l'audio solo per verificare dubbi o riferimenti; non introdurre materiale esterno alla lezione.
- Crea un solo file Markdown `elaborati-assistente/appunti/YYYY-MM-DD.md`. È un piano di lavoro per redigere il capitolo, non una seconda trascrizione, non il capitolo già scritto e non un sorgente LaTeX.
- Indica gli argomenti e i concetti effettivamente presenti, proponi una sequenza e una struttura ragionata del capitolo, e descrivi come collegare i passaggi tra argomenti.
- Annota quali passaggi del parlato sono circostanziali, ripetitivi o fuori tema e possono essere omessi; motiva le omissioni rilevanti per evitare di eliminare contenuti didattici. Indica inoltre come rendere più chiari, rigorosi e formali i concetti in prosa da manuale universitario, senza cambiarne il significato.
- Evidenzia definizioni, esempi, cautele, nessi logici, termini incerti e lacune da preservare o verificare. Se una parola o un nesso non è recuperabile con sufficiente certezza, non presentarlo nel piano come fatto accertato né colmarlo con conoscenze esterne.
- Mantieni il piano sintetico ma operativo: ogni indicazione deve poter essere applicata al capitolo e ricondotta alla trascrizione unificata. Il piano non sostituisce né modifica la trascrizione.

### 5. Redigere il capitolo della lezione

- Genera `lezioni/YYYY-MM-DD.tex` usando insieme il piano editoriale Markdown e la trascrizione unificata della stessa lezione. Il piano guida struttura e scelte editoriali; la trascrizione è il riferimento per verificare che i contenuti siano fedeli alla lezione.
- Scrivi direttamente nel capitolo una trattazione organica, ben strutturata e formale, come un testo universitario. Riordina il discorso secondo il piano, costruisci transizioni chiare ed elimina gli elementi circostanziali indicati, conservando definizioni, relazioni, esempi e precisazioni didatticamente rilevanti.
- Non copiare gli appunti in LaTeX dentro il capitolo e non usare appunti o trascrizioni per parte come file inclusi. Il capitolo deve poter essere letto come un unico documento sorgente; usa `\input` al suo interno solo per un'esigenza specifica e motivata.
- Non aggiungere nozioni, definizioni o collegamenti causali assenti dalla lezione. Se un'integrazione esterna viene richiesta, distinguila chiaramente e cita la fonte. Mantieni esplicite le incertezze e le parti mancanti che incidono sulla comprensione.
- Aggiungi commenti iniziali con le fonti effettivamente usate: trascrizione unificata e identificativi di tutte le parti incluse, oltre ai percorsi di trascrizioni grezze e registrazioni disponibili. Indica chiaramente le parti mancanti o non verificate.
- Controlla `main.tex`: deve contenere un `\input{lezioni/YYYY-MM-DD}` per ogni capitolo previsto, senza includere direttamente gli appunti intermedi. Mantieni preambolo, lingua, struttura e formattazione coerenti con il corso; il capitolo usa le strutture previste dal documento principale, per esempio `\chapter`, senza dichiarare un secondo `\documentclass`.
- In casi eccezionali in cui il capitolo abbia bisogno di file LaTeX ausiliari, documenta la ragione e verifica che i percorsi funzionino sia nel documento principale sia nella compilazione prevista.

## Uso del contesto e prevenzione della contaminazione

- Gestisci una sola lezione alla volta e mantieni distinti i passaggi: ricostruzione, merge, piano editoriale e capitolo LaTeX. Non mescolare testo grezzo e testo rielaborato nello stesso risultato.
- Per ogni blocco, passa al modello solo il segmento necessario, il minimo contesto adiacente e le istruzioni pertinenti. Evita di inserire tutte le registrazioni, trascrizioni o lezioni del corso in un unico prompt.
- Tra blocchi, non riutilizzare l'intero testo generato in precedenza come fonte. Porta avanti solo una breve scheda di continuità con: termini verificati e grafia scelta, nomi/abbreviazioni, decisioni editoriali e punti ancora incerti.
- Considera la scheda di continuità un aiuto alla coerenza, non una fonte fattuale: verifica ogni affermazione sulla trascrizione ricostruita o sull'audio.
- Tieni separati corso, lezione e versione delle fonti. Non trasferire automaticamente terminologia o conclusioni da un'altra lezione.
- Alla fine di ogni fase, confronta l'output con la relativa fonte; non dedurre la correttezza dalla sola fluidità del testo.

## Capitolo LaTeX e PDF

- Segui preambolo, lingua, impaginazione, stile e struttura già adottati dal corso; controlla `main.tex` prima di creare o modificare capitoli.
- Crea o aggiorna la trascrizione unificata e il piano editoriale, quindi il capitolo completo sotto `lezioni/`. Il capitolo finale deriva dal piano e dalla trascrizione unificata, non da elaborati LaTeX intermedi. Inserisci nel `main.tex` del corso un `\input{lezioni/YYYY-MM-DD}` per ogni capitolo, senza sostituire il documento principale con un capitolo isolato.
- Nomina il capitolo `YYYY-MM-DD.tex` e integra tutte le parti della stessa lezione in ordine numerico. Aggiungi all'inizio del sorgente LaTeX un commento con le fonti effettivamente usate, indicando i percorsi relativi e i nomi completi dei file (registrazioni, trascrizioni grezze e ricostruite) con i rispettivi identificativi. Riporta tutte le parti incluse; segnala le parti mancanti senza inventarne il contenuto.
- Se una parte non è disponibile, non crearne una ricostruzione; indica nel merge e nel capitolo finale quali parti non sono state incluse e perché.
- Organizza il capitolo con sezioni e sottosezioni utili allo studio. Il file del capitolo contiene direttamente la trattazione e normalmente non contiene `\input`; usa elenchi, formule, tabelle e immagini solo quando chiariscono la lezione e sono sostenuti dalle fonti.
- Mantieni invariato il contenuto scientifico sostenuto dalla trascrizione durante la redazione e l'impaginazione. Proteggi correttamente i caratteri speciali LaTeX e verifica parentesi, ambienti, riferimenti e inclusioni.
- Compila usando la ricetta configurata in `.vscode/settings.json` e risolvi gli errori introdotti dal capitolo. Controlla che il PDF aggiornato sia presente in `.build/` nella cartella del corso; non considerare sufficiente il solo salvataggio dei sorgenti.

## Verifica e consegna

Prima di concludere, verifica che:

- le fonti grezze siano rimaste inalterate;
- le trascrizioni ricostruite siano testo semplice e gli identificativi data/parte corrispondano tra registrazioni e trascrizioni;
- le ricostruzioni per parte siano state unite nel file `YYYY-MM-DD.txt`, con i raccordi incerti e le parti mancanti indicati chiaramente;
- il piano editoriale `YYYY-MM-DD.md` specifichi struttura, raccordi, riformulazioni e omissioni previste senza sostituirsi al testo finale;
- il capitolo LaTeX sia una trattazione completa derivata dal piano e verificata sulla trascrizione unificata, senza inclusioni degli appunti intermedi;
- il capitolo LaTeX abbia nome `YYYY-MM-DD.tex`, raccolga le parti della lezione e indichi fonti incluse e parti mancanti;
- ogni trascrizione ricostruita corrisponda alla registrazione/parte corretta e renda espliciti i dubbi irrisolti;
- il piano editoriale e il capitolo coprano i contenuti previsti senza duplicazioni o aggiunte non supportate;
- il capitolo sia incluso in `main.tex` e rispetti le convenzioni del corso;
- la compilazione sia riuscita e il PDF si trovi in `.build/`.

Nel riepilogo finale indica i file creati o aggiornati, le verifiche svolte e gli eventuali passaggi che restano incerti o bloccati. Non dichiarare completata una verifica che non è stata eseguita.