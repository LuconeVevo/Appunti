# Fondamenti

I dati sono un ingrediente fondamentale del machine learning, dove il comportamento dei modelli non e' pre-programmato ma e' appreso dai dati stessi.
Generalmente un campione nel dominio di interesse e' definito ==Data-point==. (un esempio del dominio). Un suo sinonimo e' ==pattern==.

## Tipi di pattern

- ==Numerici==: valori associati a caratteristiche misurabili o conteggi. Tipicamente continui, soggetti a ordinamento. Rappresentabili come vettori numerici nello spazio multidimensionale.
- ==Categorici==: valori associati a caratteristiche qualitative e alla presenta/assenza di una caratteristica. Talvolta soggetti a ordinamento. E' possibile mapparli su numeri attraverso tecniche di encoding o embedding.
- ==Sequenze==: pattern sequenziali con relazioni spaziali o temporali. Es stream audio, una frase, un video. Spesso a lunghezza variabile. La posizione nella sequenza e le relazioni con predecessori e successori sono importanti. E' necessario l'aspetto della "memoria".
- ==Altri dati strutturati==: output organizzati in strutture complesse quali alberi e grafi.

## Dati tabulari (eterogenei)

In molte applicazioni aziendali, i dati sono organizzati in una tabella, nelle cui colonne troviamo gli attributi (features) e nelle righe i record (data point).
- Le colonne possono avere formato numerico o categorico
- Le colonne sono eterogenee
- I dati possono essere incompleti e fortemente sbilanciati
- Non e' semplice definire una metrica di similarita' tra record

## Encoding

Dato il campo materiale con 5 valori possibili: {Acciaio, Cemento, Ghisa, Polietilene, PVC} come codificarlo in formato numerico?

==One-hot encoding==: si rimuove il campo e al suo posto si aggiungono tanti campi (o colonne) quanti sono i valori distinti. Ciascun campo e' associato a un materiale diverso e puo' assumere solo valore 0 o 1.

==Ordinal encoding==: si trasforma il campo originale in campo numerico associando ai materiali dei valori ordinali.

## Classificazione

==Classificazione==: assegnare una **classe** a un pattern.
- Necessario apprendere una funzione capace di eseguire il mapping dallo spazio dei pattern allo spazio delle classi.
- Si una spesso anche il termine **riconoscimento**.
- Nel caso di 2 classi si usa il termine **binary classification**, con piu' di due classi **multi-class classification**.

==Classe==: insieme di pattern aventi proprieta' comuni, e' un concetto semantico e dipende strettamente dall'applicazione.

Esempi:
- Spam detection
- Face recognition
- Credit card fraud detection
- Pedestrian classification
- Medical diagnosis
- Stock trading

## Regressione

==Regressione== assegnare un **valore continuo** a un pattern.
- Utile per la predizione di valori continui.
- Risolvere un problema di regressione corrisponde ad apprendere una funzione approssimante delle coppie `<input, output>` date.

Esempi:
- Stima prezzi di vendita appartamenti nel mercato immobiliare
- Stima del rischio per compagnie assicurative
- Predizione energia prodotta da impianto fotovoltaico
- Modelli sanitari di predizione dei costi
- Object detection

## Clustering

Individuare gruppi (cluster) di pattern con caratteristiche simili.
Le classi del problema non sono note e i pattern non etichettati $\rightarrow$ la natura non supervisionata del problema lo rende piu' complesso della classificazione. Spesso nemmeno il numero di cluster e' noto a priori. I cluster individuati nell'apprendimento possono essere poi utilizzati come classi.

Esempi:
- Marketing: definizione di gruppi di utenti in base ai consumi
- Genetica: raggruppamento individui sulla base di analogie DNA
- Bioinformatica: partizionamento geni in gruppi con caratteristiche simili
- Visione: segmentazione non supervisionata

## Riduzione di dimensionalita'

==Riduzione di dimensionalita'==: ridurre il numero di dimensioni dei pattern in input.
Consiste nell'apprendimento di un mapping da $R^d$ a $R^k$ con $k \lt d$.
Questo tipo di compressione puo' essere utile per eliminare informazioni non utili.
Puo' essere usato per visualizzare dati con dimensioni elevate.

## Representation Learning

Il successo di molte applicazioni di machine learning dipende dall'efficacia di rappresentazione dei pattern in termini di features.
Definiamo features ad-hoc (hand-crafted) per le diverse applicazioni, questa operazione prende il nome di ==feature engineering==.
Per il riconoscimento di oggetti esistono numerosi descrittori di forma, colore e tessitura che possiamo utilizzare.
E' anche possibile apprendere automaticamente le features.

## Modelli discriminativi

I modelli discriminativi hanno l'obiettivo di assegnare un nuovo data point a una classe. La cosa importante e' appendere il decision boundary che separa le classi.

## Modelli generativi
Appendono la distribuzione probabilistica degli esempi usati per il loro addestramento. Dopo l'addestramento possono:
- Generare nuovi dati sintetici a partire da numeri random
- Modificare o trasformare l'input
- Classificare l'input comparando le probabilita' che sia generato dalle diverse classi

## Apprendimento

==Supervisionato==: almeno nel training set i dati sono etichettati (per classificazione conosciamo le classi), situazione tipica nella classificazione, regressione e in alcune tecniche di riduzione di dimensionalita'.
==Non supervisionato==: il training set non e' etichettato, situazione tipica del clustering e nella maggior parte di tecniche di riduzione di dimensionalita'
==Semi-Suprvisionato==: il training set e' etichettato parzialmente