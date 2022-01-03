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

<img src="/slide/m2.png" width="450" height="300" />

Quello che vorremmo capire è quanto è capace il modello di riconoscere il guasto a seguito di "leggere" modifiche del dataset. Ricordiamo infatti che ogni dataset ha una propria impronta e che lo stesso guasto presenta dataset diversi a seguito ad esempio dei tempi di arrivo degli allarmi che non potranno mai essere tutti esattamente dello stesso valore.
Tuttavia anche due guasti differenti hanno dataset differenti per cui in questo caso il modello non dovrà confondersi assegnando ai due eventi codici di guasto diversi.

Prima di iniziare la simulazione si fa notare al lettore che stiamo addestrando il modello attraverso un solo dataset noto per il guasto 1, il guasto 2 ed il guasto 3. In realtà sappiamo bene che per ottenere dei buoni risultati con sistemi di apprendimento artificiale (e non solo) abbiamo bisogno di molti dataset. Questo non è sempre possibile, almento per impronte di guasto di macchine industriali complesse.
Da qui l'idea di realizzare un sistema che potesse essere addestrato anche successivamente dal manutentore in modo da costruire dei database dei pesi nel tempo migliorando le predizioni del sistema.

