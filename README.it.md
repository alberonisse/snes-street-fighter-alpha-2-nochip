# LETTERA APERTA A GUSTAVO FRANCO
[Português](README.md) / [English](README.en.md) / [Español](README.es.md) / [Italiano](README.it.md) / [Deutsch](README.de.md) / [简体中文](README.zh-CN.md) / [日本語](README.ja.md) / [繁體中文（香港）](README.zh-HK.md)

Richiesta di chiarimenti, correzione dell'attribuzione e ritrattazione

11 novembre 2026

Gustavo,

Ho creato questo fork dopo che hai archiviato il repository perché è stato l'unico modo rapido e diretto che ho trovato per cercare di farti arrivare questa lettera il prima possibile.

Scrivo per contestare l'attribuzione pubblicata nel tuo repository, che identifica le cartucce menzionate nella pagina come una commercializzazione della tua implementazione di Street Fighter Alpha 2 senza S-DD1.

La mia dichiarazione sull'origine dell'edizione è esplicita: non ho utilizzato materiale del tuo progetto nell'edizione USA da 8 MiB con Shin Akuma e caricamento accelerato che ho fornito tramite la mia decompressione e le patch preparate per la memoria 29LV640. Dichiaro che le cartucce a cui mi riferisco utilizzano questa edizione. Contesto l'attribuzione di queste cartucce al tuo progetto senza un'identificazione tecnica del contenuto effettivamente utilizzato.

Il mio obiettivo con questa lettera è chiarire l'origine dell'edizione in questione, spiegare il percorso del mio lavoro e chiedere che l'attribuzione pubblica sia sostenuta da prove verificabili.

## 1. IL PERCORSO DEL MIO PROGETTO

Il mio lavoro non è iniziato con la messa a disposizione delle patch da 8 MiB. C'è stato un precedente processo di studio dell'S-DD1, sviluppo di strumenti, analisi della mappatura, assemblaggio di schede, correzioni e test su una console SNES reale.

Il piano originale prevedeva una PCB con CPLD, destinata a controllare l'accesso ai dati e preservare i dettagli dell'implementazione. Non intendevo rendere apertamente disponibile tutta questa struttura di decompressione, organizzazione dei dati e ricostruzione.

Quando ho saputo della pubblicazione del tuo progetto, mi sono sentito profondamente demotivato. Ho iniziato a considerare compromesso l'elemento distintivo del lavoro in cui stavo investendo tempo e impegno. Questa era la mia percezione del futuro del mio progetto.

È in questo contesto che ho deciso di cambiare direzione e rendere disponibili privatamente la decompressione e le patch dell'edizione da 8 MiB, per dare continuità al lavoro già svolto. Questa decisione non autorizza a identificare automaticamente l'edizione che ho fornito come una versione del tuo repository.

## 2. COME FUNZIONA IL MIO APPROCCIO ALLA DECOMPRESSIONE

Nel nucleo originale di sdd1_unpacker, ho studiato e isolato l'implementazione dell'S-DD1 presente in bsnes. I crediti del codice sono stati mantenuti: Andreas Naive per l'algoritmo/implementazione originale e byuu per il port di bsnes. Non rivendico l'invenzione dell'algoritmo S-DD1.

Questo codice è stato adattato in uno strumento C++ indipendente dall'interfaccia grafica e dal funzionamento completo dell'emulatore, con lettura validata dei dati della ROM e gestione dei banchi di memoria dell'S-DD1.

Il gioco non tratta l'intera ROM come un unico file compresso. Richiede flussi specifici, normalmente durante i trasferimenti DMA. Per questo, il lavoro ha comportato l'analisi di descrittori e tabelle della ROM originale, la registrazione delle richieste effettuate durante l'esecuzione e il consolidamento di origine, dimensione e configurazione dei banchi di memoria.

Il trace canonico della ricostruzione storica contiene 3.155 identità di request in 3.160 righe. Le cinque righe aggiuntive registrano evidenze di altri punti di chiamata per richieste già catalogate. Le request osservate e le voci inferite staticamente sono classificate separatamente; questo conteggio non significa 3.155 flussi compressi distinti né dimostra, di per sé, la copertura di tutte le situazioni del gioco.

La catena del nucleo originale è stata strutturata così: ROM originale USA, analisi e trace, catalogo delle request, decompressione dei dati, organizzazione in un nuovo layout, patch DMA e verifiche della ricostruzione senza S-DD1.

Questa ricostruzione ha richiesto di distinguere l'indirizzo della CPU dall'offset nel file, rispettare le regioni ROM dello SNES e reindirizzare le routine trattate verso dati già decompressi. Non si riduce ad aumentare la dimensione del file o a cambiarne l'intestazione.

## 3. L'ADATTAMENTO DA 8 MiB E LA SCHEDA SEMPLICE

La linea da 8 MiB va distinta dal precedente nucleo di ricostruzione da 16 MiB. Ha seguito un altro processo di organizzazione e allocazione, utilizzando un inventario estratto dalla base da 16mb con cui ho eseguito i test e che ho pubblicato su YouTube, oltre a correzioni e verifiche successive. Non la presento come un semplice ritaglio del file da 16 MiB.

L'edizione è stata preparata per una scheda semplice, con i collegamenti adeguati e un'unica memoria Flash TSOP48 da 8 MiB, la 29LV640 in modalità x8. Questa edizione non richiede S-DD1 o CPLD per funzionare in questa configurazione ed è stata testata su una console SNES reale. È stata preparata anche la variante per una scheda LoROM modificata.

Esiste una differenza oggettiva rispetto alla conversione storica da 12 MiB documentata nel tuo progetto. Questa immagine da 12 MiB non può essere semplicemente scritta sulla 29LV640 da 8 MiB e utilizzata nella configurazione che ho mostrato. Il tuo stesso resoconto tecnico descrive una mappatura specifica, inclusa una finestra nei banchi C0-FF:

https://github.com/snes9xgit/snes9x/issues/1081

Non sto affermando che la tua implementazione non possa mai essere adattata a una cartuccia fisica, né negando i test su hardware che hai documentato. Sto distinguendo un'immagine da 12 MiB e la sua mappatura dall'edizione da 8 MiB preparata per la mia configurazione di scheda.

Se la proposta è ampliare l'accesso al gioco, ritengo importante riconoscere anche questa strada: permettere alle persone di utilizzare una scheda semplice e componenti accessibili, senza dover acquistare una flashcart specifica. Avevo già documentato una scheda di test utilizzata in questo lavoro; il video figura nell'elenco alla fine di questa lettera.

## 4. CREDITI E PRECISIONE

La presente contestazione si riferisce specificamente all'edizione USA da 8 MiB utilizzata nelle cartucce menzionate. L'origine di questa edizione va esaminata a partire dai file effettivamente utilizzati, dalle loro patch e dalla loro provenienza. Non va presunta sulla base di inventari di un'altra regione o di revisioni di ricerca separate, né della semplice somiglianza tra le funzionalità annunciate.

Non rivendico la paternità esclusiva dell'algoritmo pubblico, di routine di terzi o dei dati del gioco originale. Rivendico il corretto riconoscimento del lavoro di integrazione, adattamento, correzione e validazione svolto nell'edizione che ho fornito.

## 5. REGISTRAZIONI PUBBLICHE PER VERIFICARE LA CRONOLOGIA

Presento le registrazioni seguenti affinché i contenuti e le date di pubblicazione possano essere confrontati con la cronologia delle versioni. Documentano il percorso che sto raccontando; non sostituiscono il confronto dei file effettivamente utilizzati nella cartuccia.

Scheda semplice di test:
https://www.youtube.com/shorts/EVQoQB8mD1A

Registrazione complementare 1:
https://www.youtube.com/shorts/uhzHfQFPbVw

Registrazione complementare 2:
https://www.youtube.com/shorts/23gS_IEGDqc

Trasmissione relativa al progetto:
https://www.youtube.com/live/zakojPNeGc0

Registrazione complementare 3:
https://www.youtube.com/shorts/PXVAKPfAO1E

Registrazione complementare 4:
https://www.youtube.com/shorts/y8PAzIzPz1I

Registrazione complementare 5:
https://www.youtube.com/shorts/bStb8AW_QzQ

Registrazione complementare 6:
https://www.youtube.com/shorts/if26BECUllI

Fase con PCB e CPLD:
https://www.youtube.com/shorts/X-Hby6Vw-m4

Video che ho pubblicato prima della preparazione e della condivisione privata delle patch da 8 MiB:
https://www.youtube.com/shorts/YZbpycbEW0w

Dimostrazione successiva del gioco su una scheda semplice con la 29LV640:
https://www.youtube.com/shorts/GKl1eOMFks0

Il mio chiarimento rivolto a te:
https://youtu.be/8X8jRSXFb5I

## 6. CHE COSA CHIEDO

La pubblicazione a cui mi riferisco si trova qui:
https://github.com/gufranco/snes-street-fighter-alpha-2-nochip

Chiedo che tu chiarisca quale file è stato esaminato, quale sia il suo hash, da quale cartuccia sia stato ottenuto e quali elementi tecnici abbiano sostenuto l'attribuzione alla tua implementazione.

Chiedo inoltre che il confronto consideri la mappatura fisica, le routine, le patch e la revisione concreta, anziché prendere come prova soltanto la descrizione commerciale o la presenza di funzionalità come Shin Akuma e caricamento accelerato.

Finché questa identificazione resterà contestata e non sarà stata presentata una dimostrazione tecnica, chiedo che la pubblicazione renda esplicita questa condizione e ritiri l'attribuzione categorica. Qualora l'errore venga confermato, chiedo la correzione delle pubblicazioni e una ritrattazione con una visibilità equivalente a quella dell'esposizione originale.

Rispetto il tuo lavoro e ti chiedo di rispettare anche il mio. Non intendo promuovere attacchi personali o sminuire la tua dedizione.

La questione che pongo è oggettiva: l'origine di un'implementazione deve essere dimostrata. Un risultato simile, un nome in un annuncio o una confezione non sostituiscono l'analisi del contenuto effettivamente utilizzato.

Cordiali saluti,

Responsabile del progetto ALBER MULTI HOUSE
