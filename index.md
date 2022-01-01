# Olimpiadi Automazione Siemens 2022
Progetto Looking For Troubles "L4T"
Realizzato in collaborazione tra:
- <b> [Fermi-Giorgi Lucca](https://www.polofermigiorgi.edu.it/) </b>
- <b> [Galilei-Artiglio Viareggio](http://www.iisgalileiartiglio.edu.it/) </b>
- <b> [Koerber Tissue Lucca](https://www.koerber-tissue.com/it/) </b>


## Finalità
Il presente lavoro ha come finalità l’individuazione rapida di guasti di una macchina complessa e di fornire al manutentore dei video-tutorials lanciati direttamente dal PLC S7 1500 allo smartphone o ad altri device in dotazione al fine di semplificare l’attività manutentiva.
Operativamente la localizzazione degli stati di guasto avviene sul piano attraverso coordinate polari che descrivono una particolare spirale logaritmica. Tale traiettoria opportunamente supportata da informazioni provenienti da sensori specifici, potrebbe descrivere lo stato di funzionamento della macchina utile per la manutenzione predittiva.
Piu’ semplicemente la spirale logaritmica si adatta allo scopo anche con pochi od unici dataset iniziali per tipologia di guasto, situazioni frequenti in ambito industriale.

## Descrizione generale del modello
Il modello si basa sull’idea che gli stati di guasto di una macchina complessa possano essere associati ad un percorso descritto da una funzione come ad esempio la spirale aurea. Tale scelta, di notevole valenza didattica per le diverse implicazioni matematiche e storico-filosofiche ovvero con ricadute multidisciplinari, si è rilevata efficace anche da un punto di vista pratico stimolando al contempo la curiosità degli studenti.

## Impronta dell’evento guasto
Quando un evento riconducibile ad un guasto produce un allarme rappresentato da una serie di segnali booleani e/o analogici in cascata che aumenta con l’aumentare della complessità del sistema, può essere utile studiare “l’impronta” che connota tale evento per aiutare il manutentore ad intervenire e risolvere il problema nel piu’ breve tempo possibile.
Ora se l'impronta lasciata da questo evento (per impronta si intende la sequenza di bit, l'istante di tempo in cui commutano, la loro durata, eventuali altri segnali analogici ecc.) sono sempre ed esattamente tutti uguali per ogni evento indifferentemente dalla causa che lo genera, allora è sufficiente un calcolo combinatorio (es. mappa Karnaugh) per stabilire con certezza l’origine del guasto.
Se invece l’impronta dell’evento cambia leggermente di volta in volta pur essendo la causa scatenante la stessa, allora l’impiego di una rete neurale installata direttamente sul PLC può essere una valida alternativa per l’individuazione del guasto.
Possiamo pensare di rappresentare questo ragionamento con una serie di immagini composte da matrici luminose dove ogni luce rappresenta la sequenza e la durata dei bit che intervengono a seguito del guasto.

![fig1](/slide/fig1.png)

A prima vista le tre impronte sembrano uguali ma osservando attentamente si possono notare leggere differenze. In questo caso il riconoscimento dell’immagine può essere affidato ad un sistema esperto, previo addestramento, come ad esempio una funzione retro-azionata che aggiorna i pesi proprio come fa una rete neurale. Chiameremo tali “matrici luminose”, matrici dataset. Per spiegare meglio l’idea è possibile fare ricorso alla seguente rappresentazione grafica 

![fig2](/slide/fig2.png)

Durante la fase di addestramento sono determinati i pesi della funzione per ogni dataset di guasto.
Durante la fase di riconoscimento è valutata sul piano la posizione del nuovo dataset ed associato al punto di guasto piu’ vicino. 

![fig3](/slide/fig3.png)

Nel caso di figura il modello propone al manutentore il video-tutorial relativo alla riparazione del guasto 3. Se la previsione non è confermata, il sistema propone il video-tutorial del guasto 2. In questo caso è possibile correggere i pesi addestrando il modello tenendo conto del nuovo scenario.
Di seguito è discussa una possibile applicazione di una spirale aurea da installare su un PLC S7 1500 per l’individuazione dell’impronta dell’origine del guasto da comunicare al manutentore.

## Video di presentazione del progetto
**under construction**

<html lang="it"> 
<body>
    <div class="container">
         <!-- finestra popup 3 -->
        <a href="#x" class="overlay" id="win3"></a>
        <div class="popup">
            <div class="video">
         <!-- il link you tube deve essere selezionato dal link di rete lasciando la cartella embed -->
		    <iframe width="640" height="320" src="https://youtube.com/embed/jat2C_UBPgM" ></iframe>
            </div>
            <a class="close" title="Chiudere" href="modal.html" onclick = "modal.html(); return false;"></a>
        </div>
    </div>
</body>
</html>

## Chatterbot con Telegram
Per poter interagire con la chat del manutentore occorre cercare su Telegram @incercadiguai_bot
Digitando i numeri da 1 a 7, che semplicemente rappresentano i codici di guasto riconosciuti in fase di addestramento del PLC, è possibile ricevere le informazioni circa il ripristino del guasto. Naturalmente i video caricati hanno valenza didattica. In uno scenario industriale tali video dovrebbero essere disponibili già in fase di progettazione direttamente dal software Digital Twin come ad esempio NX di Siemens. Infatti la manutenzione non è un mero atto finale, una attività svincolata dal processo progettuale ma anzi orienta le scelte costruttive al fine di migliorare i costi e la durata di vita del prodotto 

# Abbecedario matematico
Di seguito si riassumono alcuni concetti fondamentali utilizzati nella definizione del modello matematico caricato nel PLC S71500 Siemens
La descrizione degli oggetti utilizzati segue lo schema di figura partendo dagli ingressi o matrice di dataset, passando per la funzione logaritmica fino alla retroazione di aggiornamento dei pesi

![fig4](/slide/fig4.png)

## Spirale Logaritmica
Prima di affrontare l'aspetto matematico di seguito si ribadisce l'opportunità della scelta della spirale logaritmica. Se prendiamo la funzione e la studiamo nel piano cartesiano si osserva che per ogni angolo esiste un modulo associato. Nella figura seguente la sezione in colore azzurro rappresenta il campo di esistenza compreso tra 0 e multipli di due volte pigreco 

![f10](/slide/f10.png)

Nella figura seguente sono indicati due stati distinti che differiscono di circa un angolo giro

![f11](/slide/f11.png)

Se I due punti P1 e P2 rappresentano due stati distinti di guasto, è possibile ricondurre ciascuno agli stato di guasto noti afferenti alle curve g1 e f1

![f12](/slide/f12.png)


## Matrice dei dataset
La matrice dei dataset ha dimensione nx3.
- La prima colonna della matrice rappresenta lo stato degli allarmi in termini booleani 
- La seconda colonna rappresenta i tempi di arrivo degli allarmi che prima di essere caricati nel DB subiscono una normalizzazione
- La terza colonna rappresenta l’ordine di arrivo della sequenza degli allarmi

![fig5](/slide/fig5.png)

## Matrice dei pesi
La matrice dei pesi è aggiornata dal feedback durante l’addestramento della rete di apprendimento automatico ed ha dimensione nx3.
- La prima colonna della matrice rappresenta i pesi degli allarmi
- La seconda colonna rappresenta i pesi del tempo di arrivo della sequenza degli allarmi
- La terza colonna rappresenta i pesi dell’ordine di arrivo della sequenza degli allarmi

![fig6](/slide/fig6.png)

## Funzione “z” o ∅(z)
Un tipo di guasto riconducibile alla matrice dei dataset e dei pesi è individuabile attraverso la seguente relazione

![fig7](/slide/fig7.png)

Operativamente la matrice dei dataset x (nx3) è proiettata attraverso la trasposta matrice dei pesi W (3×n) secondo la relazione W^T∙x=Z  in uno spazio 3x3. 

Della matrice risultante Z è calcolata la somma della diagonale principale che costituisce l’input di rete

![fig8](/slide/fig8.png)

La matrice x di dataset è anch’essa proiettata in uno spazio 3x3 attraverso il prodotto con la sua trasposta. Il calcolo del valore assoluto del determinante della nuova matrice associa il volume di guasto nello spazio 3x3 della matrice stessa

![fig9](/slide/fig9.png)

## Aggiornamento dei pesi
La spirale logaritmica 

![fig10](/slide/fig10.png) 

è utilizzata nel feedback per la stima dei pesi, mentre la funzione di costo da minimizzare è

![fig11](/slide/fig11.png)

dove Y rappresenta il termine noto per l’addestramento ed è, in questo contesto, il modulo relativo al tipo di guasto che giace sulla traiettoria della spirale logaritmica

Posto 

![fig12](/slide/fig12.png) 

la variazione dei pesi (derivata parziale) della spirale logaritmica sarà

![fig13](/slide/fig13.png) 

Applicando il metodo della discesa del gradiente sulla funzione di costo per la ricerca dei pesi si ha

![fig14](/slide/fig14.png)

Il cambiamento del peso è definito come il gradiente negativo moltiplicato il tasso di apprendimento 

![fig15](/slide/fig15.png)

Sostituendo si ha

![fig16](/slide/fig16.png)

![fig17](/slide/fig17.png)

![fig18](/slide/fig18.png)

che costituiscono gli aggiornamenti dei pesi a seguito del feedback

## Caso Studio
.. in progress


