# Progetto di una base di dati per la gestione di una palestra

**Elaborato per il corso di Basi di dati**  
**A.A 2018/2019**

**Cavalieri Giacomo**  
giacomo.cavalieri2@studio.unibo.it  
0000830738

## Indice

1. [Analisi dei requisiti](#analisi-dei-requisiti)
   - Intervista
   - Estrazione dei concetti principali
2. [Progettazione concettuale](#progettazione-concettuale)
   - Schema Scheletro
   - Schema finale
3. [Progettazione logica](#progettazione-logica)
   - Stima del volume dei dati
   - Descrizione delle operazioni principali e stima della loro frequenza
   - Schemi di navigazione e tabelle degli accessi
   - Raffinamento dello schema
   - Analisi delle ridondanze
   - Traduzione di entità e associazioni in relazioni
   - Schema relazionale finale
   - Traduzione delle operazioni in query SQL
4. [Progettazione dell'applicazione](#progettazione-dellapplicazione)
   - Descrizione dell'architettura dell'applicazione realizzata

---

## Analisi dei requisiti

Si vuole realizzare un database a supporto dell'automatizzazione della gestione di una palestra. Pertanto, la base di dati dovrà immagazzinare informazioni relative ai clienti, alle loro rispettive schede di allenamento nonché agli ingressi effettuati.

Gli allenatori della palestra potranno dunque consultare tutte le schede degli iscritti, aggiungere nuovi esercizi, compilare nuove schede etc.

### Intervista

Un primo testo ottenuto dall'intervista è il seguente:

Si vuole tenere traccia degli iscritti alla palestra memorizzandone nome, cognome, codice fiscale ed eventualmente un numero di telefono e una mail. Al momento dell'iscrizione di un nuovo cliente si crea una tessera che riporta la data di rilascio e un codice identificativo, usata per poter entrare in palestra.

Un cliente può entrare solo nel caso in cui disponga di un abbonamento valido, ogni ingresso viene memorizzato con relativa data e ora.

Gli abbonamenti, comprati da un listino di cui è mantenuto uno storico, sono caratterizzati da una durata e un prezzo, inoltre al momento dell'acquisto può essere applicato anche uno sconto al cliente. Qualora il cliente lo richiedesse, l'abbonamento può essere sospeso, una sola volta nel periodo di validità dell'abbonamento, per un determinato periodo (durante il quale non si potrà entrare in palestra) per poi essere riattivato successivamente (e.g. per periodi prolungati di malattia che impedirebbero di frequentare la palestra, vacanze, etc.).

Ogni cliente dispone di una e una sola scheda di allenamento realizzata da uno degli istruttori; inoltre si mantiene uno storico di tutte le schede possedute dal cliente così da poter dare consigli personalizzati su allenamenti futuri.

Una scheda, pur avendo una durata indicata in settimane, può essere utilizzata dal cliente fino a quando lo desidera (seppur non consigliato) e perderà di validità solo qualora gliene venisse assegnata una nuova.

Una scheda si compone di un numero variabile di tabelle, ciascuna delle quali contiene una routine di esercizi. Per ogni settimana della durata della scheda, un esercizio è caratterizzato da un numero di serie da effettuare, ciascuna con un numero di ripetizioni, e una pausa da effettuare fra una serie e l'altra; infine, ogni esercizio può avere anche un peso associato da usare.

Tutte le schede, così come i singoli esercizi posseggono uno o più obiettivi (e.g. dimagrimento, tonificazione, riabilitazione ginocchio etc.).

Il compito dello staff della palestra è assegnare nuove schede ai clienti, creare nuovi esercizi e assistere i clienti che prenotino un allenamento personalizzato (un allenatore può assistere al massimo un cliente al giorno e un cliente può prenotare al massimo un allenamento al giorno).

### Esempio di scheda di allenamento

Esempio di scheda di allenamento con 2 tabelle della durata di 3 settimane. Ogni colonna riporta il numero di serie e il numero di ripetizioni per serie oltre al recupero da effettuare fra una serie e l'altra.

| Esercizio | 1ª SETTIMANA | 2ª SETTIMANA | 3ª SETTIMANA |
|-----------|--------------|--------------|--------------|
| PANCA PIANA | 4 x 10 - rec. 1'30'' | 4 x 8 - rec. 2' | 4 x 6 - rec. 2'15'' |
| CHEST PRESS | 3 x 10 - rec. 1'30'' | 3 x 8 - rec. 1'45'' | 3 x 6 - rec. 2' |
| ALZATE LATERALI | 3 x 10 - rec. 1'30'' | 3 x 10 - rec. 1'30'' | 3 x 8 - rec. 1'45'' |
| SQUAT | 4 x 10 con 5 kg - rec. 1' | 4 x 8 con 8 kg - rec. 2' | 4 x 6 con 12 kg - rec. 2' |
| LEG CURL STESO | 5 x 8 - rec. 2' | 5 x 10 - rec. 2'15'' | 5 x 10 - rec. 2'15'' |
| STACCO | 4 x 10 - rec. 1'30'' | 4 x 8 - rec. 2' | 4 x 6 - rec. 2'15'' |
| TRICIPITI AL CAVO | 3 x 10 - rec. 1'30'' | 3 x 10 - rec. 1'30'' | 3 x 8 - rec. 1'45'' |
| ALZATE LATERALI | 3 x 10 - rec. 1'30'' | 3 x 10 - rec. 1'30'' | 3 x 8 - rec. 1'45'' |

### Terminologia

| Termine | Breve descrizione | Eventuali sinonimi |
|---------|-------------------|-------------------|
| Cliente | Colui che frequenta la palestra ed effettua allenamenti in base a quanto riportato sulla propria scheda | Iscritto |
| Istruttore | Colui che deve assistere i clienti durante i propri allenamenti e si occupa di assegnare nuove schede | Membro dello staff |
| Scheda | Oggetto che riporta gli esercizi da effettuare durante un allenamento organizzandoli in tabelle | Scheda di allenamento |
| Tabella | Componente fondamentale nella quale si dividono le schede | Routine di esercizi |
| Serie | Ripetizione in sequenza di uno stesso esercizio un determinato numero di volte | |
| Recupero | Tempo indicato in minuti e secondi di pausa fra una serie di esercizi e la successiva | Pausa |

### Estrazione dei concetti principali

A seguito della lettura e comprensione dei requisiti, si procede redigendo un testo che ne riassuma tutti i concetti e in particolare ne estragga quelli principali eliminando le ambiguità sopra rilevate:

Per ogni cliente della palestra vengono memorizzati nome, cognome, codice fiscale ed eventualmente un numero di telefono e una mail. Ogni cliente possiede un codice univoco fornitogli al momento dell'iscrizione. Un cliente può entrare in palestra solo nel caso in cui disponga di un abbonamento valido, ogni ingresso viene memorizzato con relativa data e ora.

Ogni abbonamento ha una durata e un prezzo e al momento dell'acquisto si può effettuare uno sconto per il cliente. I prezzi degli abbonamenti sono memorizzati in un listino di cui si mantiene uno storico delle versioni. L'abbonamento può essere sospeso una sola volta per un determinato periodo per posticiparne la scadenza.

Di ogni cliente si memorizzano le vecchie schede e la scheda attuale che perde di validità nel momento in cui ne viene assegnata una nuova.

Una scheda si compone di almeno una tabella. Per ogni settimana della durata della scheda, gli esercizi riportati nelle tabelle sono caratterizzati da un numero di serie da effettuare, ciascuna con un numero di ripetizioni, un recupero e un eventuale peso da usare. Schede e esercizi posseggono obiettivi.

Gli istruttori devono assegnare nuove schede ai clienti, compilarne di nuove e creare esercizi. Infine devono assistere quei clienti i quali richiedano sessioni di allenamento private (un istruttore può assistere al massimo un cliente al giorno e un cliente può prenotare al massimo un allenamento al giorno).

### Operazioni principali richieste

1. Iscrivere un nuovo cliente
2. Aggiungere un nuovo istruttore
3. Registrare l'ingresso di un cliente
4. Registrare l'acquisto di un abbonamento da parte di un cliente
5. Cambiare il listino prezzi per l'anno corrente
6. Sospendere l'abbonamento di un cliente
7. Assegnare una scheda già esistente ad un cliente
8. Compilare una nuova scheda
9. Leggere tutte le tabelle della scheda attuale di un cliente
10. Data la tabella di una scheda visualizzare tutti i suoi esercizi
11. Visualizzare gli esercizi in base a particolari filtri (e.g. con uno specifico obiettivo o che riguardano uno specifico muscolo etc.)
12. Registrare la prenotazione di una sessione di allenamento individuale
13. Mostrare il prossimo allenamento di un cliente o un istruttore

---

## Progettazione concettuale

### Schema Scheletro

Le entità di istruttore e cliente sono la generalizzazione di una entità persona, identificata tramite un codice univoco (non si utilizza il codice fiscale per evitare problemi di omocodia).

Dall'analisi del dominio si evince come un cliente non possa prenotare più di un allenamento in una giornata così come un istruttore non possa seguire più di un allenamento in una giornata. Perciò si utilizzano come identificatori della entità allenamento sia la combinazione di istruttore e giorno che cliente e giorno tramite le associazioni assiste e prenotazione.

Un cliente possiede più abbonamenti nel tempo, dunque non è sufficiente una associazione fra cliente e tipo abbonamento con un attributo "data di acquisto" perché non permetterebbe a un cliente di possedere più volte una stessa tipologia di abbonamento. Per risolvere tale problema si ricorre alla reificazione dell'acquisto dell'abbonamento identificando tale entità tramite il codice del cliente e la data di acquisto.

Rimane il vincolo inespresso che un cliente non può acquistare un abbonamento fino alla scadenza del precedente acquisito.

Poiché il listino degli abbonamenti può cambiare al più fra un anno e il successivo viene identificato tramite l'anno nel quale è stato composto. Le tipologie di abbonamento di cui si compone devono avere tutte durata differente, questo viene modellato utilizzando come identificatore di tipologia abbonamento la sua durata e l'anno del listino nel quale compare.

Una stessa scheda può essere assegnata a più clienti (e.g. scheda per principianti, scheda tonificazione…), dunque ho optato per utilizzare una seconda entità, scheda posseduta, per rappresentare il possedimento di un particolare tipo di scheda. Ogni scheda posseduta è posseduta da un solo cliente il quale dispone di una sola scheda attuale, tale possedimento è rappresentato dalla associazione possedimento attuale. Ho scelto di utilizzare tale distinzione nelle associazioni in quanto un cliente può possedere molteplici schede ma sempre una sola scheda attuale che verrà visualizzata con alta frequenza, risulta quindi necessario poterla trovare velocemente.

Ogni scheda presenta una suddivisione in tabelle (identificate tramite la loro posizione nella scheda) a loro volta divise in sequenze di esercizi la cui posizione all'interno della tabella viene utilizzata per identificarli in maniera univoca. Così facendo viene rispettato il vincolo per cui, data una scheda, una sua tabella e un posizione in quest'ultima è univocamente determinato l'esercizio che vi compare.

Per modellare il concetto di ripetizione settimanale è stata creata una entità settimana che, in associazione con l'esercizio in scheda permette di memorizzare le ripetizioni per tale settimana. Rimane il vincolo inespresso per cui il numero di settimane associate a una scheda deve essere pari alla durata della scheda e ogni esercizio in scheda deve essere associato a tutte le settimane della scheda di cui fa parte.

---

## Progettazione logica

### Stima del volume dei dati

| Concetto | Costrutto | Volume |
|----------|-----------|---------|
| Cliente | E | 10.000 |
| Ingresso | E | 1.000.000 |
| Effettuazione | R | 1.000.000 |
| Abbonamento | E | 30.000 |
| Acquisizione | R | 30.000 |
| Tipo Abbonamento | E | 40 |
| Tipologia | R | 30.000 |
| Listino | E | 10 |
| Composizione | R | 40 |
| Istruttore | E | 10 |
| Allenamento | E | 15.000 |
| Assiste | R | 15.000 |
| Prenotazione | R | 15.000 |
| Scheda Posseduta | E | 100.000 |
| Possedimento attuale | R | 10.000 |
| Possedimento | R | 100.000 |
| Scheda | E | 50.000 |
| Compilazione | R | 50.000 |
| Produce | R | 100.000 |
| Tabella | E | 100.000 |
| Composizione scheda | R | 100.000 |
| Esercizio in tabella | E | 800.000 |
| Tipologia Esercizio | R | 800.000 |
| Composizione tabella | R | 800.000 |
| Ripetizione | R | 24.000.000 |
| Settimana | E | 300.000 |
| Suddivisione | R | 300.000 |
| Esercizio | E | 500 |
| Muscolo | E | 20 |
| Riguarda | R | 200 |
| Obiettivo | E | 30 |
| Obiettivo Scheda | R | 25.000 |
| Obiettivo Esercizio | R | 1.000 |

### Descrizione delle operazioni principali e stima della loro frequenza

| Codice | Operazione | Frequenza |
|---------|------------|-----------|
| 1 | Iscrivere un nuovo cliente | 2 al giorno |
| 2 | Aggiungere un nuovo istruttore | 1 all'anno |
| 3 | Registrare l'ingresso di un cliente, controllando la validità dell'abbonamento | 100 al giorno |
| 4 | Registrare l'acquisto di un abbonamento da parte di un cliente | 5 al giorno |
| 5 | Cambiare il listino prezzi per l'anno corrente | 1 all'anno |
| 6 | Sospendere l'abbonamento di un cliente | 5 al mese |
| 7 | Assegnare una scheda già esistente ad un cliente | 10 al giorno |
| 8 | Compilare una nuova scheda | 1 al mese |
| 9 | Leggere tutte le tabelle della scheda attuale di un cliente | 100 al giorno |
| 10 | Data la tabella di una scheda visualizzare tutti i suoi esercizi e ripetizioni | 200 al giorno |
| 11 | Visualizzare gli esercizi in base a particolari filtri | 1 al mese |
| 12 | Registrare la prenotazione di una sessione di allenamento individuale | 2 al giorno |
| 13 | Mostrare il prossimo allenamento di un cliente o un istruttore | 40 al giorno |

### Schemi di navigazione e tabelle degli accessi

#### OP 1 - Iscrivere un nuovo cliente

| Concetto | Costrutto | Accessi | Tipo |
|----------|-----------|---------|------|
| Cliente | E | 1 | S |
| **Totale** | | **1S** | **→ 2 al giorno** |

#### OP 2 - Aggiungere un nuovo istruttore

| Concetto | Costrutto | Accessi | Tipo |
|----------|-----------|---------|------|
| Istruttore | E | 1 | S |
| **Totale** | | **1S** | **→ 2 all'anno** |

#### OP 3 - Registrare l'ingresso di un cliente

Prima di permettere l'ingresso di un cliente bisogna verificare che questo disponga di un abbonamento valido, questo comporterà dover leggere gli abbonamenti del cliente che, in media, sono 3.

| Concetto | Costrutto | Accessi | Tipo |
|----------|-----------|---------|------|
| Effettuazione | R | 1 | S |
| Ingresso | E | 1 | S |
| Acquisizione | R | 3 | L |
| Abbonamento | E | 3 | L |
| **Totale** | | **2S + 6L** | **→ 1000 al giorno** |

#### OP 4 - Registrare l'acquisto di un abbonamento da parte di un cliente

Per poter portare a termine tale operazione, è necessario prima verificare che il cliente che sta acquisendo l'abbonamento non disponga di uno non ancora scaduto. Questo comporta ulteriori letture degli abbonamenti di un cliente.

| Concetto | Costrutto | Accessi | Tipo |
|----------|-----------|---------|------|
| Acquisizione | R | 3 | L |
| Abbonamento | E | 3 | L |
| Acquisizione | R | 1 | S |
| Abbonamento | E | 1 | S |
| Tipologia | R | 1 | S |
| **Totale** | | **3S + 6L** | **→ 60 al giorno** |

#### OP 5 - Cambiare il listino prezzi per l'anno corrente

Si considera che, al momento della aggiunta del nuovo listino, vengano aggiunte anche le tipologie di abbonamento di cui si compone che, in media, sono 4 per listino.

| Concetto | Costrutto | Accessi | Tipo |
|----------|-----------|---------|------|
| Listino | E | 1 | S |
| Composizione | R | 4 | S |
| Tipo abbonamento | E | 4 | S |
| **Totale** | | **9S** | **→ 18 all'anno** |

#### OP 6 - Sospendere l'abbonamento di un cliente

Per sospendere l'abbonamento di un cliente è necessario verificare che ve ne sia uno valido che possa essere sospeso, questo comporta la lettura degli abbonamenti del cliente.

| Concetto | Costrutto | Accessi | Tipo |
|----------|-----------|---------|------|
| Acquisizione | R | 3 | L |
| Abbonamento | E | 3 | L |
| Abbonamento | E | 1 | S |
| **Totale** | | **1S + 6L** | **→ 40 al mese** |

#### OP 7 - Assegnare una scheda già esistente ad un cliente

Si assume di conoscere già il codice della scheda da assegnare e il codice del cliente a cui assegnarla. Nel momento in cui viene assegnata una scheda, si scrive sia nella relazione possedimento che in possedimento attuale (andando a sostituire una eventuale scheda presente in precedenza). Inoltre quando si inserisce una scheda, bisogna leggere quella che si sta andando a sostituire per scrivere il corretto valore nel campo ordinale della nuova scheda.

| Concetto | Costrutto | Accessi | Tipo |
|----------|-----------|---------|------|
| PossedimentoAttuale | R | 1 | L |
| Scheda posseduta | E | 1 | L |
| Scheda posseduta | E | 1 | S |
| Possedimento | R | 1 | S |
| Possedimento Attuale | R | 1 | S |
| **Totale** | | **3S + 2L** | **→ 800 al giorno** |

#### OP 8 - Compilare una nuova scheda

Compilare una nuova scheda è un processo che si compone di diverse fasi: bisogna innanzitutto creare una scheda e tante entità settimana a essa associate pari alla sua durata; dopodiché è necessario creare le tabelle della scheda (in media sono 2 per scheda) e per ognuna inserirvi degli esercizi (in media 8 per tabella). Aggiunti gli esercizi, per ciascuno bisogna indicare una ripetizione per ogni settimana della tabella.

| Concetto | Costrutto | Accessi | Tipo |
|----------|-----------|---------|------|
| Scheda | E | 1 | S |
| Suddivisione | R | 6 | S |
| Settimana | E | 6 | S |
| Composizione scheda | R | 2 | S |
| Tabella | E | 2 | S |
| Composizione tabella | R | 16 | S |
| Esercizio in tabella | E | 16 | S |
| Tipologia | R | 16 | S |
| Ripetizione | R | 96 | S |
| Obbiettivo scheda | R | 1 | S |
| **Totale** | | **162S** | **→ 324 al mese** |

#### OP 9 - Leggere tutte le tabelle della scheda attuale di un cliente

Innanzitutto è necessario reperire la scheda attuale di un cliente, questo richiederà una lettura in Possedimento Attuale, dopodiché si dovranno leggere le tabelle di tale scheda.

| Concetto | Costrutto | Accessi | Tipo |
|----------|-----------|---------|------|
| Possedimento Attuale | R | 1 | L |
| Scheda Posseduta | E | 1 | L |
| Produce | R | 1 | L |
| Scheda | E | 1 | L |
| Composizione scheda | R | 2 | L |
| Tabella | E | 2 | L |
| **Totale** | | **8L** | **→ 800 al giorno** |

#### OP 10 - Data la tabella di una scheda visualizzare tutti i suoi esercizi

| Concetto | Costrutto | Accessi | Tipo |
|----------|-----------|---------|------|
| Composizione tabella | R | 8 | L |
| Esercizio in tabella | E | 8 | L |
| Ripetizione | E | 48 | L |
| **Totale** | | **64L** | **→ 12.800 al giorno** |

#### OP 11 - Visualizzare gli esercizi in base a particolari filtri

Considero il caso generico di un filtro sul muscolo e uno sull'obiettivo.

| Concetto | Costrutto | Accessi | Tipo |
|----------|-----------|---------|------|
| Riguarda | R | 10 | L |
| Esercizio | E | 10 | L |
| Obiettivo Esercizio | E | 2 | L |
| Esercizio | R | 2 | L |
| **Totale** | | **24L** | **→ 24 al mese** |

#### OP 12 - Registrare la prenotazione di una sessione di allenamento individuale

Supponendo di conoscere il codice del cliente e dell'istruttore da inserire nella tabella sarà sufficiente una scrittura dell'entità Allenamento.

| Concetto | Costrutto | Accessi | Tipo |
|----------|-----------|---------|------|
| Allenamento | E | 1 | S |
| Assiste | R | 1 | S |
| Prenotazione | R | 1 | S |
| **Totale** | | **3S** | **→ 12 al giorno** |

#### OP 13 - Mostrare il prossimo allenamento di un cliente o un istruttore

Si analizza il costo per una sola delle due query che risultano perfettamente simmetriche.

| Concetto | Costrutto | Accessi | Tipo |
|----------|-----------|---------|------|
| Allenamento | E | 1.5 | L |
| Assiste | R | 1 | L |
| Istruttore | E | 1 | L |
| **Totale** | | **3.5L** | **→ 140 al giorno** |

### Raffinamento dello schema

#### Eliminazione delle gerarchie

Per l'eliminazione della gerarchia persona si è scelto di adottare l'approccio del collasso verso il basso, replicando così gli attributi in istruttore e cliente. Si è adottata questa strategia in quanto si deve interagire con i clienti molto più spesso che con gli istruttori, e non si ha la necessità che l'identificatore per tali entità sia globalmente univoco.

#### Eliminazione degli attributi compositi

Nello schema è presente un attributo composito nell'entità abbonamento che è stato diviso nelle sue sotto-componenti. Sarà poi necessario accertarsi, a livello di applicazione, che tali attributi siano sempre entrambi impostati a un valore coerente o entrambi null.

#### Scelta delle chiavi primarie

Nello schema sono già evidenziate senza ambiguità tutte le chiavi primarie per la maggior parte delle entità; per quanto riguarda l'entità scheda, si sceglie di usare come chiave primaria il codice mentre per l'allenamento la chiave primaria sarà data dal giorno e l'associazione con cliente.

#### Eliminazione degli identificatori esterni

Nello schema E/R sono eliminate le seguenti relazioni:

- Prenotazione, importando codiceCliente in Allenamento
- Assiste, importando codiceIstruttore in Allenamento
- Effettuazione, importando codiceCliente in Ingresso
- Acquisizione, importando codiceCliente in Abbonamento
- ComposizioneListino, importando anno in TipoAbbonamento
- Tipologia, importando durata e anno in Abbonamento
- Produce, importando codiceScheda in SchedaPosseduta
- PossedimentoAttuale, importando codiceScheda e ordinale in Cliente
- Possedimento, importando codiceCliente in SchedaPosseduta
- Compilazione, importando codiceIstruttore e l'attributo data in Scheda
- Suddivisione, importando codiceScheda in Settimana
- ComposizioneScheda importando codiceScheda in Tabella
- ComposizioneTabella, importando posizioneTabella e codiceScheda in EsercizioInTabella
- Ripetizione, reificata importando codiceScheda, ordinaleSettimana da Settimane e posizioneTabella, posizioneEsercizio da EsercizioInTabella
- Tipologia, importando nomeEsercizio in EsercizioInTabella
- ObiettivoEsercizio, reificata importando nomeEsercizio da Esercizio e codiceObiettivo da Obiettivo
- ObiettivoScheda, reificata importando codiceScheda da Scheda e codiceObiettivo da Obiettivo
- Riguarda, reificata importando nomeEsercizio da Esercizio e nomeMuscolo da Muscolo

# Analisi delle ridondanze

È stata inserita una ridondanza tramite l'uso dell'associazione Possedimento Attuale, in quanto sarebbe sufficiente l'associazione Possedimento per risalire alla scheda attuale di un cliente, effettuando un ordinamento delle schede possedute per ordinale.

È riportata la valutazione del risparmio in termini di accessi dato dall'uso di questo approccio:

## OP 7 - Assegnare una scheda già esistente ad un cliente

L'avere una ridondanza in questo caso aiuta nell'inserimento: infatti, poiché la scheda attuale dispone di un ordinale, inserire il successivo nella nuova scheda può essere fatto tramite una lettura.

Senza ridondanza sarebbe invece necessario leggere tutte le schede possedute dal cliente e individuare quella con ordinale maggiore per stabilire il prossimo numero da inserire:

### Con ridondanza:
| Concetto | Costrutto | Accessi | Tipo |
|----------|-----------|---------|------|
| Possedimento Attuale | R | 1 | L |
| Scheda posseduta | E | 1 | L |
| Scheda posseduta | E | 1 | S |
| Possedimento | R | 1 | S |
| Possedimento Attuale | R | 1 | S |

**Totale: 3S + 2L → 800 al giorno**

### Senza ridondanza:
| Concetto | Costrutto | Accessi | Tipo |
|----------|-----------|---------|------|
| Possedimento | R | 10 | L |
| Scheda posseduta | E | 10 | L |
| Scheda posseduta | E | 1 | S |
| Possedimento | R | 1 | S |
| Possedimento Attuale | R | 1 | S |
| Scheda attuale | E | 1 | S |

**Totale: 4S + 20L → 2800 al giorno**

## OP 9 - Leggere tutte le tabelle della scheda attuale di un cliente

L'associazione ridondante Possedimento Attuale permette di ottenere con due sole letture il codice della scheda attuale del cliente. Senza ridondanza (seconda tabella) sarebbe necessario leggere tutte le schede del cliente per stabilire quale sia quella con ordinale maggiore.

### Con ridondanza:
| Concetto | Costrutto | Accessi | Tipo |
|----------|-----------|---------|------|
| Possedimento Attuale | R | 1 | L |
| Scheda Posseduta | E | 1 | L |
| Produce | R | 1 | L |
| Scheda | E | 1 | L |
| Composizione scheda | R | 2 | L |
| Tabella | E | 2 | L |

**Totale: 8L → 800 al giorno**

### Senza ridondanza:
| Concetto | Costrutto | Accessi | Tipo |
|----------|-----------|---------|------|
| Possedimento Attuale | R | 10 | L |
| Scheda Posseduta | E | 10 | L |
| Produce | R | 1 | L |
| Scheda | E | 1 | L |
| Composizione scheda | R | 2 | L |
| Tabella | E | 2 | L |

**Totale: 26L → 2600 al giorno**

Si può vedere come in entrambi i casi la ridondanza garantisca un notevole vantaggio in termini di accessi risparmiati, per questo verrà mantenuta.

# Traduzione di entità e associazioni in relazioni

```
abbonamenti(codiceCliente, dataAcquisto, sconto, dataSospensione, dataRiattivazione, annoListino, durata)

allenamenti(codiceCliente: clienti, giorno, codiceIstruttore: istruttori, oraInizio, oraFine)
UNIQUE(codiceIstruttore, giorno)

clienti(codice, nome, cognome, CF, dataNascita, genere, ordinaleSchedaAttuale*: schede_possedute.ordinale, codiceSchedaAttuale*: schede_possedute.codice, telefono*, mail*)

esercizi(nome, descrizione*)

esercizi_in_tabella((codiceScheda, posizioneTabella): tabelle, posizioneEsercizio, nomeEsercizio: esercizi)

ingressi(codiceCliente: clienti, dataOra)

istruttori(codice, nome, cognome, CF, dataNascita, genere)

listini(anno)

muscoli(nome)

obiettivi(codiceObiettivo, descrizione)

obiettivi_esercizi(nomeEsercizio: esercizi, codiceObiettivo: obiettivi)

obiettivi_schede(codiceScheda: schede, codiceObiettivo: obiettivi)

riguarda(nomeEsercizio: esercizi, nomeMuscolo: muscoli)

ripetizioni((posizioneTabella, posizioneEsercizio, codiceScheda): esercizi_in_tabella, ordinale_settimana: settimane, serie, ripetizione, peso*, recupero)

schede(codiceScheda, nome, durata, genere, dataCompilazione, codiceIstruttore: istruttori)
UNIQUE(nome)

schede_possedute(codiceCliente: clienti, ordinale, codiceScheda: schede)

settimane(codiceScheda: schede, ordinale)

tabelle(codiceScheda: schede, posizioneTabella)

tipi_abbonamento(annoListino: listini, durata, prezzo)
```

# Traduzione delle operazioni in query SQL

## OP 1 - Iscrivere un nuovo cliente

```sql
INSERT INTO clienti (nome, cognome, CF, dataNascita, genere, telefono, mail)
VALUES (?, ?, ?, ?, ?, ?, ?)
```

## OP 2 - Aggiungere un nuovo istruttore

```sql
INSERT INTO istruttori (nome, cognome, CF, dataNascita, genere)
VALUES (?, ?, ?, ?, ?)
```

## OP 3 - Registrare l'ingresso di un cliente

Per verificare se il cliente dispone di un abbonamento valido la seguente query deve restituire un record, questo sarà l'unico abbonamento valido (si ha la certezza che ci sia un solo abbonamento valido per come viene gestita l'aggiunta di nuovi abbonamenti acquisiti).

```sql
SELECT *
FROM abbonamenti
WHERE codiceCliente = ?
AND DATEDIFF(NOW(), dataAcquisto) - IF(dataSospensione IS NOT NULL, DATEDIFF(dataRiattivazione, dataSospensione), 0) < durata
AND IF(dataSospensione IS NOT NULL, (NOW() < dataSospensione OR NOW() >= dataRiattivazione), true)
```

Se tale condizione risulta soddisfatta, si può aggiungere il nuovo ingresso col codice del cliente che potrà entrare in palestra.

```sql
INSERT INTO ingressi (codiceCliente)
VALUES (?)
```

## OP 4 - Registrare l'acquisto di un abbonamento da parte di un cliente

Si può registrare un abbonamento solo se il cliente non dispone già di abbonamenti validi, ovvero se la seguente query non ritorna alcun record:

```sql
SELECT *
FROM abbonamenti
WHERE codiceCliente = ?
AND DATEDIFF(NOW(), dataAcquisto) - IF(dataSospensione IS NOT NULL, DATEDIFF(dataRiattivazione, dataSospensione), 0) < DATEDIFF(DATE_ADD(dataAcquisto, INTERVAL durata MONTH), dataAcquisto)
```

Appurata la possibilità di comprare un nuovo abbonamento si potrà aggiungere.

```sql
INSERT INTO abbonamenti (codiceCliente, sconto, durata, annoListino)
VALUES (?, ?, ?, SELECT anno
         FROM listini
         ORDER BY anno DESC
         LIMIT 1)
```

Così facendo si forza l'acquisto di tipologie di abbonamento che sono presenti solo nel listino in uso, ovvero quello più recente.

## OP 5 - Cambiare il listino prezzi per l'anno corrente

L'operazione per aggiungere un listino è la seguente:

```sql
INSERT INTO listini (anno)
VALUES (YEAR(NOW()))
```

Per aggiungere tipologie di abbonamento a un listino:

```sql
INSERT INTO tipiAbbonamento
VALUES (YEAR(NOW()), ?, ?)
```

Si presuppone che tutti gli abbonamenti vengano aggiunti al momento della creazione del listino (o al più nel medesimo anno) e che, ovviamente, un listino si riferisca all'anno corrente nel quale viene creato.

## OP 6 - Sospendere l'abbonamento di un cliente

Il cliente deve disporre di un abbonamento valido che non sia già stato sospeso una volta (in quanto proibito sospenderlo per più di una volta), dunque sarà necessario eseguire la seguente query che dovrà restituire un solo risultato, ovvero il record relativo all'abbonamento da modificare:

```sql
SELECT *
FROM abbonamenti
WHERE codiceCliente = ?
AND DATEDIFF(NOW(), dataAcquisto) < DATEDIFF(DATE_ADD(dataAcquisto, INTERVAL durata MONTH), dataAcquisto)
AND dataSospensione IS NULL
```

```sql
UPDATE abbonamenti
SET dataSospensione = ?,
    dataRiattivazione = ?
WHERE codiceCliente = ?
AND dataAcquisto = ?
```

## OP 7 - Assegnare una scheda già esistente ad un cliente

Le query per eseguire l'assegnazione sono le seguenti e devono essere eseguite nell'ordine riportato affinché i numeri ordinali delle schede risultino corretti.

```sql
UPDATE clienti
SET ordinaleSchedaAttuale = ordinaleSchedaAttuale + 1
WHERE codiceCliente = ?
```

```sql
INSERT INTO schedePossedute (codiceCliente, codiceScheda, ordinale)
VALUES (?, ?, SELECT ordinaleSchedaAttuale
         FROM clienti
         WHERE codiceCliente = ?)
```

```sql
UPDATE clienti
SET codiceSchedaAttuale = ?
WHERE codiceCliente = ?
```

## OP 8 - Compilare una nuova scheda

```sql
INSERT INTO schede (nome, durata, genere, codiceIstruttore)
VALUES(?, ?, ?, ?)
```

Dopodiché, vanno inserite tante settimane per quanto indicato dalla durata, quindi bisognerà eseguire a livello applicativo la seguente query più volte, incrementando di volta in volta l'ordinale della settimana:

```sql
INSERT INTO settimane
VALUES (LAST_INSERT_ID(), ?)
```

Infine si aggiungerà alla scheda tante tabelle quanto desiderato come segue:

```sql
INSERT INTO tabelle
VALUES (LAST_INSERT_ID(), ?)
```

E a ogni tabella si aggiungerà quanti esercizi si vuole aggiungendo anche una ripetizione per ogni settimana.

```sql
INSERT INTO esercizi_in_tabella
VALUES (LAST_INSERT_ID(), ?, ?, ?)
```

```sql
INSERT INTO ripetizioni
VALUES (?, ?, LAST_INSERT_ID(), ?, ?, ?, ?)
```

## OP 9 - Leggere tutte le tabelle della scheda attuale di un cliente

```sql
SELECT *
FROM tabelle
WHERE codiceScheda = ?
```

## OP 10 - Data la tabella di una scheda visualizzare tutti i suoi esercizi

```sql
SELECT posizioneEsercizio, nomeEsercizio
FROM esercizi_in_tabella
WHERE codiceScheda = ?
AND posizioneTabella = ?
ORDER BY posizioneEsercizio ASC
```

## OP 11 - Visualizzare gli esercizi in base a particolari filtri

In generale è richiesta la possibilità di filtrare gli esercizi in base ai loro obiettivi o ai muscoli che riguardano, dunque una generica query di filtraggio potrebbe essere:

```sql
SELECT E.nome, E.descrizione
FROM esercizi E, riguarda R, obiettivi_esercizi O
WHERE R.nomeEsercizio = E.nome
AND O.nomeEsercizio = E.nome
AND R.nomeMuscolo = ?
OR codiceObiettivo = ?
```

## OP 12 - Registrare la prenotazione di una sessione di allenamento individuale

```sql
INSERT INTO allenamenti
VALUES (?, ?, ?, ?, ?)
```

## OP 13 - Mostrare il prossimo allenamento di un cliente o un istruttore

Query per gli istruttori che permette di visualizzare il nome del cliente:

```sql
SELECT C.nome, C.cognome, A.*
FROM allenamenti A, clienti C
WHERE C.codiceCliente = A.codiceCliente
AND codiceIstruttore = ?
AND giorno > NOW()
ORDER BY giorno
LIMIT 1
```

Query per i clienti che permette di visualizzare il nome dell'istruttore:

```sql
SELECT I.nome, I.cognome, A.*
FROM allenamenti A, istruttori I
WHERE I.codiceIstruttore = A.codiceIstruttore
AND codiceCliente = ?
AND giorno > NOW()
ORDER BY giorno
LIMIT 1
```

# Progettazione dell'applicazione

## Descrizione dell'architettura dell'applicazione realizzata

L'applicazione per interfacciarsi al database è stata realizzata in Java, sfruttando lo strumento di ORM Hibernate; il database risiede in locale e il DBMS usato è mySQL. L'applicazione è una semplice JavaFX application che fa uso di file FXML (uno per ogni finestra indipendente) associati a un proprio controller il quale ha il compito di portare a termine le query appoggiandosi alla classe DatabaseConnection.

Per la maggior parte delle query, la correttezza dei dati inseriti viene verificata dal DBMS sfruttando opportuni check, così facendo si è cercato di ridurre al minimo i controlli che l'applicazione deve effettuare.

Nella scheda relativa ai clienti è stato inserito, per completezza, un form per poter registrare nuovi ingressi da parte dei clienti; tuttavia questa operazione dovrebbe essere effettuata automaticamente tramite la connessione a un dispositivo di lettura di codici a barre (nelle schede dei clienti).

L'inserimento di una scheda è un processo complesso diviso in più passaggi, per questo si ricorre all'uso di una seconda finestra pop-up (con un proprio controller distinto) grazie alla quale è possibile effettuare il rollback delle query di inserimento qualora, in un qualunque passaggio, si dovesse verificare un errore. Inoltre impedisce all'utente di creare schede mal formate dove per esempio una tabella non possiede esercizi.

L'applicazione fornisce nel complesso le funzionalità richieste evidenziate nella fase di progettazione, includendo ulteriormente alcune banali operazioni non elencate come la cancellazione di un cliente o di un istruttore.