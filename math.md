# Rappresentazione grafica del modello e PLC S7 1500
In questa sezione sono raccolti gli argomenti principali del modello spiegati per immagini con lo scopo di chiarire meglio gli aspetti matematici trattati nell'[abbecedario](/index.md)
## Dal dataset alla matrice dei pesi
Supponiamo di simulare il modello manualmente attraverso l'uso di un HMI. In altre parole supponiamo di essere il manutentore che a seguito di un guasto rilevato addestra il modello al fine di permetterne il riconoscimento in automatico a seguito di un evento successivo

<img src="/slide/m1.png" width="420" height="300" />

I campi bianchi sono accessibili dal manutentore che può caricare con numeri reali che rappresentano in ordine da sinistyra verso destra:
- il dataset o l'impronta del guasto
- il modulo del vettore sulla spirale logaritmica associato a quel guasto

I campi azzurri non sono accessibili al manutentore e rappresentano:
- i pesi calcolati dal modello
- la diagonale della matrice quadrata
- il modulo del vettore che incontra il punto sulla spirale logaritmica associato a quel guasto ricalcolato dal modello
- l'angolo del mudulo del vettore 

I pulsanti giallo-oro rappresentano i database nei quali sono memorizzati i pesi addestrati. La memorizzazione avviene alla pressione touch del rispettivo pulsante. Trattandosi di un esempio grafico descrittivo sono stati presi a riferimento tre soli guasti ovvero tre database inducati con i numeri 1A, 2B e 3C

