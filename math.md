# Rappresentazione grafica del modello e PLC S7 1500
In questa sezione sono raccolti gli argomenti principali del modello spiegati per immagini con lo scopo di chiarire meglio gli aspetti matematici trattati nell'[abbecedario](/index.md)
## Dal dataset alla matrice dei pesi
Supponiamo di simulare il modello manualmente attraverso l'uso di un HMI. In altre parole supponiamo di essere il manutentore che a seguito di un guasto rilevato addestra il modello al fine di permetterne il riconoscimento in automatico per un evento successivo

<img src="/slide/m1.png" width="450" height="300" />

I campi bianchi sono accessibili dal manutentore che può caricare con numeri reali che rappresentano in ordine da sinistra verso destra:
- il dataset o l'impronta del guasto
- il modulo del vettore sulla spirale logaritmica associato a quel guasto

I campi azzurri non sono accessibili al manutentore e rappresentano:
- i pesi calcolati dal modello
- la diagonale della matrice quadrata
- il modulo del vettore che incontra il punto sulla spirale logaritmica associato a quel guasto ricalcolato dal modello
- l'angolo del mudulo del vettore 

I pulsanti giallo-oro rappresentano i database nei quali sono memorizzati i pesi addestrati. La memorizzazione avviene alla pressione touch del rispettivo pulsante. Trattandosi di un esempio grafico descrittivo sono stati presi a riferimento tre soli guasti ovvero tre database indicati con i numeri:
- 1A
- 2B
- 3C

I tre stati di guasto appartengono alla spirale logaritmica e sono individuati nell'immagine seguente con i punti U, W e H. Per questi punti sono individuati i moduli dei vettori ed i rispettivi angoli sul piano polare. I moduli saranno utilizzati per l'addestramento del modello. 

<img src="/slide/m2.png" width="450" height="250" />

Quello che vorremmo capire è quanto è capace il modello di riconoscere il guasto a seguito di "leggere" modifiche del dataset. Ricordiamo infatti che ogni dataset ha una propria impronta e che lo stesso guasto presenta dataset diversi a seguito ad esempio dei tempi di arrivo degli allarmi che non potranno mai essere tutti esattamente dello stesso valore.
Tuttavia anche due guasti differenti hanno dataset differenti per cui in questo caso il modello non dovrà confondersi assegnando ai due eventi codici di guasto diversi.

Prima di iniziare la simulazione si fa notare al lettore che stiamo addestrando il modello attraverso un solo dataset noto per il guasto 1, il guasto 2 ed il guasto 3. In realtà sappiamo bene che per ottenere dei buoni risultati con sistemi di apprendimento artificiale (e non solo) abbiamo bisogno di molti dataset. Questo non è sempre possibile, almento per impronte di guasto di macchine industriali complesse.
Da qui l'idea di realizzare un sistema che potesse essere addestrato anche successivamente dal manutentore in modo da costruire dei database dei pesi nel tempo migliorando le predizioni del sistema.

## Addestramento Guasti
Supponiamo di avere un dataset di 12 elementi e di dover addestrare altrettanti pesi. Prendiamo a riferimento il seguente dataset per il guasto 1A, intendendo che il numero zero si riferisce ad uno stato d'allarme (sensore, reè ecc) non commutato e dunque il relativo tempo di arrivo sarà anch'esso mancante

<img src="/slide/m3.png" width="100" height="300" />

Dopo aver inizializzato i pesi in modo random con numeri "piccoli" ed aver inserito il valore del modulo pari a 1.32 relativo al giasto 1A, il modello fornisce la risposta di figura che viene salvata nel rispettivo database

<img src="/slide/m4.png" width="450" height="300" />

Nello stesso modo carichiamo i guasti 2B e 3C modificando i rispettivi dataset e moduli relativi ai punti W ed H.

Supponiamo che per il guasto 2B sia 

<img src="/slide/m5.png" width="450" height="300" />

E per il guasto 3C 

<img src="/slide/m6.png" width="450" height="300" />

## Riconoscimento Guasti
Addestrati i pesi si passa adesso al riconoscimento delle impronte di guasto. Per semplicità e per riprova del caricamento corretto dei pesi nei rispettivi database, inizialmente sottoponiamo al modello i dataset di addestramento

<img src="/slide/m7.png" width="450" height="300" />

risposta corretta per il guasto 1A

<img src="/slide/m8.png" width="450" height="300" />

risposta corretta per il guasto 2B

<img src="/slide/m9.png" width="450" height="300" />

risposta corretta per il guasto 3C

Proviamo adesso a "muovere" i valori del dataset del guasto 3C, supponendo di modificare i tempi degli allarmi mantenendo inalterata la sequenza di arrivo

<img src="/slide/m10.png" width="450" height="300" />

L'impronta del guasto 3C seppure leggermente differente è riconosciuta dal modello per l'angolo ma non per il modulo. La differenza consiste in un lieve aumento di alcuni valori dei segnali di allarme

Cerchiamo di capire meglio cosa è successo. Calcoliamo mediante [Scilab](https://www.scilab.org/) l'angolo generato dal prodotto tra la nuova matrice dataset e la matrice di addestramento dei pesi

Inseriamo quindi la matrice dataset e la matrice dei pesi e calcoliamo la trasposta

<img src="/slide/m11.png" width="450" height="300" />

Calcoliamo infine il prodotto tra matrici ed estraiamo l'angolo dalla diagonale principale

<img src="/slide/m12.png" width="350" height="200" />

Si ricorda che questa operazione non è altro che l'input di rete fornito al modello secondo il seguente schema

<img src="/slide/fig4.png" width="250" height="150" />

Riportiamo il risultato dell'operazione sul piano polare ed osserviamo che il vettore k è prossimo al vettore h e quindi il modello associa il nuovo dataset al guasto 3C

<img src="/slide/m13.png" width="450" height="200" />

Ripetiamo i conti con Scilab anche per i pesi relativi ai guasti 1A e 2B

- Guasto 2B

<img src="/slide/m14.png" width="442" height="424" />

- Guasto 1A

<img src="/slide/m15.png" width="442" height="424" />

Completiamo adesso il diagramma polare con gli ultimi risultati ottenuti

<img src="/slide/m16.png" width="922" height="398" />

Siamo prossimi ad una situazione limite con verso di rotazione antioraria che corrisponde ad un aumento dei tempi di arrivo degli allarmi. L'angolo beta infatti è prossimo all'angolo alfa. L'angolo alfa rimane tuttavia il minore ed il modello è in grado di associare il codice guasto corretto

<img src="/slide/m17.png" width="873" height="375" />

Proviamo adesso a cercare la situazione limite contraria riducendo il tempo di arrivo degli allarmi

<img src="/slide/m18.png" width="873" height="375" />

Come nel caso precedente utilizziamo Scilab per posizionare i vettori nel piano

- Guasto 3C

<img src="/slide/m19.png" width="441" height="422" />

- Guasto 2B

<img src="/slide/m20.png" width="441" height="422" />

- Guasto 1A

<img src="/slide/m21.png" width="441" height="422" />

Riportiamo i risultati sul piano polare

<img src="/slide/m22.png" width="754" height="371" />

Quello che si osserva è che per ogni addestramento di un *unico* dataset si ha a disposizione un settore all'interno del quale il modello effettua una predizione corretta. Il settore a cui fa riferimento il codice guasto può essere ampliato a seguito di un nuovo addestramento di un nuovo dataset. Questa attività può essere svolta all'occorrenza dal manutentore durante il ciclo di vita della macchina ed entrare a far parte di un database unico a disposizione dell'azienda
