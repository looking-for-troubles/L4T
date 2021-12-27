# Olimpiadi Automazione Siemens 2022
Progetto Looking For Troubles "L4T"
Realizzato in collaborazione tra:
- [E.Fermi-G.Giorgi Lucca](https://www.polofermigiorgi.edu.it/)
- [Galilei-Artiglio Viareggio](http://www.iisgalileiartiglio.edu.it/)
- [Koerber Tissue](https://www.koerber-tissue.com/it/)


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
[fig1](/slide/fig1.png)



## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/looking-for-troubles/L4T/edit/gh-pages/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [Basic writing and formatting syntax](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/looking-for-troubles/L4T/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
