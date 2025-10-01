Ottimizzare il modello rispetto a come si comportera' su dati futuri
Modello $M$ e' regolato da un set di ==parametri== $\Theta$. Questa dipendenza e' resa esplicita indicando il modello come $M(\Theta)$ 
L'apprendimento consiste nell'individuare il valore ottimo $\Theta^*$
$$ \Theta^* = argmax_\Theta f(Train,M(\Theta)) $$
Oppure minimizzando l'errore (==loss-function==):
$$ \Theta^* = argmin_\Theta f(Train,M(\Theta)) $$

$f$ puo' essere ottimizzata:
- Esplicitamente, con metodi che operano a partire dalla sua definizione matematica.
- Implicitamente, utilizzando metodi euristici

Stabilito il modello, prima dell'apprendimento deve essere definito il valore degli ==iperparametri== $H$, che definiscono i dettagli architetturali del modello.

L'addestramento avviene tramite un approccio a due livelli. Nel livello esterno si fissano gli iperparametri $H$; a livello interno si esegue l'apprendimento e si valutano le prestazioni, al termine della procedura si scelgono gli iperparametri $H^*$ che hanno fornito prestazioni migliori.

```
for H in Hyperparameter values:
	Theta* = argmin_theta f(Train, M(H, Theta))
	Evaluate M(Valid, H, Theta*)
Select best hyperparameters(H*)
```

- Il **Training** set e' l'insieme di pattern su cui addestrare il modello per ottenere il valore ottimo dei parametri $\Theta$
- Il **Validation** set e' l'insieme di pattern su cui tarare gli iperparametri $H$
- Il **Test** set e' l'insieme di pattern su cui valutare le prestazioni finali

## Suddivisione dei pattern

### Set disgiunti

Se i dati sono sufficientemente numerosi per la complessita' del problema e del modello scelto (non producono overfitting), si possono usare ==Set Disgiunti==.
Aumentare la partizione di Train consente di addestrare meglio il modello, ma Validation e Test set troppo piccoli non permettono di misurare con sufficiente confidenza  le prestazioni e la generalizzazione.

> La dimensione del validation/test set dipende anche dall'entita' dell'errore atteso. Se l'errore di classificazione del sistema e' del 10%, con un test set di 2500 esempi avremo 250 casi di errore. Se l'errore e' di 0.2% avremo solo 5 errori con conseguente scarsa affidabilita' statistica.

La divisione puo' essere random (==shuffling==) oppure ==mirato==. Ad esempio per mantenere separati periodi temporali di train e test. Nel caso di serie temporali, dove il sistema e' addestrato su un periodo storico per produrre previsioni per un periodo successivo, uno split random non e' corretto (causa sovrastima) in quanto il training set include data point temporalmente vicini a quelli di test.

### K-fold Cross-Validation

Una scelta piu' robusta degli iperparametri (necessaria per dataset di piccole dimensioni) si ottiene con la procedura di *k-fold Cross-Validation*.

Nell'ipotesi di $15000$ pattern totali e $k = 5$:
- $5000$ pattern sono ==scorporati a priori== per il Test set
- i $10000$ pattern rimanenti (dopo il mescolamento) sono suddivisi in $5$ gruppi (*fold*) da $2000$ pattern ciascuno
![](k-fold.png)
- Per ogni ==combinazione di iperparametri $H_i$== che si vuole valutare:
	- Si esegue $5$ volte il training scegliendo uno dei fold come Valid set e i $4$ rimanenti come Train
	- Si calcola l'accuratezza $\text{avg\_acc}_i$ come media/mediana delle $5$ accuratezze sui rispettivi Valid
- Si sceglie la combinazione di iperparametri con migliore $\text{avg\_acc}$
- Scelti gli iperparametri ottimali si riaddestra il modello su tutto il training set ($5$ fold) e, solo a questo punto si verificano le prestazioni sul test set.

==Leave one out==: caso estremo di cross-validation dove i fold hanno dimensione $1$. Si utilizza solo quando i pattern sono $\lt 100$.

## Cherry picking

Avviene quando viene scelto il modello migliore "validando" sul test set. Produce ==overfitting== del test set. Non usare il test set per orientare le scelte durante lo sviluppo di un sistema.

## Selezione automatica di iperparametri

Quando possibile e' utile ricercare i valori ottimali degli iperparametri in modo automatico:

- ==Grid search==: per ogni iperparametro si definisce un insieme di valori da provare. Il sistema e' valutato su tutte le combinazioni di valori di tutti gli iperparametri. Puo' essere molto costoso.
- ==Random search==: sorteggia casualmente valori di iperparametri dai range/distribuzioni specificati/e, eseguendo un numero prefissato di iterazioni.

## Metriche di prestazioni

E' possibile utilizzare direttamente la funzione obiettivo per quantificare le prestazioni, ma si preferisce una misura legata alla semantica del problema.

In un problema di ==classificazione==, l'**accuratezza** di classificazione $[0\dots100\%]$ e' la percentuale di pattern correttamente classificati. L'errore di classificazione e' il suo complemento.
$$ \text{acc} = \frac{\#\text{pattern correttamente classificati}}{\#\text{pattern classificati}} $$
$$ \text{Err} = 100\%-\text{acc} $$
Nei problemi di ==regressione== si valuta in genere l'==RMSE== (Root Mean Squared Error) ovvero la radice della media dei quadrati degli scostamenti tra valore vero e valore predetto.
$$ \text{RMSE} = \sqrt{\frac{1}{N}\sum_{i=1\dots N}(\text{pred}_i -\text{true}_i)^2} $$
## Matrice di Confusione

La ==confusion matrix== e' utile nei problemi di classificazione per capire come sono distribuiti gli errori. Per esempio, in un problema di classificazione digit ($10$ classi):
- Assumiamo che sulle righe ci siano le classi **True** (o Real o Actual) e sulle colonne le classi **Predicted**
- Una cella $(r,c)$ riporta il numero di casi in cui il sistema ha predetto di classe $c$ un pattern di classe vera $r$
- Idealmente la matrice dovrebbe essere diagonale, dato che valori fuori dalla diagonale indicano casi di errore
![](confusion_matrix.png)

La matrice puo' essere normalizzata per classi True, per passare dal numero di errori alla percentuale di errore.

### Classificazione Binaria

Dato un classificatore binario e $T = P + N$ pattern da classificare ($P$ positivi e $N$ negativi), il risultato di ciascuno dei tentativi di classificazione puo essere:
- ==True Positive== (**TP**): un pattern positivo e' stato correttamente assegnato ai positivi
- ==True Negative== (**TN**): un pattern negativo e' stato correttamente assegnato ai negativi
- ==False Positive== (**FP**): un pattern negativo e' stato erroneamente assegnato ai positivi. Detto errore di **Tipo I** o **False**
- ==False Negative== (**FN**): un pattern positivo e' stato erroneamente assegnato ai negativi. Detto errore di **Tipo II** o **Miss**

Passando da errori a frequenze/probabilita' (corrisponde alla normalizzazione per righe della confusion matrix)
$$ \text{TPR(True Positive Rate)} = \frac{TP}{P} $$
$$ \text{TNR(True Negative Rate)} = \frac{TN}{N} $$
$$ \text{FPR(False Positive Rate)} = \frac{FP}{N} $$
$$ \text{FNR(False Negative Rate)} = \frac{FN}{P} $$
Con queste notazioni possiamo scrivere l'accuratezza di classificazione come:
$$ \text{acc} = \frac{TP + TN}{T} $$
con $T = P+N$.

I $4$ casi sono facilmente collocabili sulle $4$ celle della matrice di confusione $(2\times2)$, le relative frequenze occupano le stesse posizioni sulla matrice di confusione normalizzata:
![](confusion_binary.png)

## DET e ROC

L'output di un classificatore e' spesso ==probabilistico== (valore continuo in $[0\dots1]$). In un problema di ==classificazione binaria== i pattern possono essere predetti come positivi confrontando l'output con una soglia $t$. Soglie restrittive (elevate) riducono i false positive a discapito dei false negative; viceversa soglie tolleranti (basse) riducono i false negative a discapito dei false positive.
![](FNR_FPR_graph.png)
Le due curve possono essere "condensate" in una curva ==DET== (**Detection Error Tradeoff**) che nasconde la soglia $t$. La rappresentazione ==ROC== (**Receiver Operating Characteristic**) riporta in ordinata TPR invece che FNR (e' ribaltata verticalmente rispetto a DET).
![](DET_ROC.png)

### Area Under Curve

Conoscendo la curva ROC di due sistemi come riconosciamo quello migliore?
Il sistema migliore e' quello la cui curva e' piu' "alta", nel caso in cui le curve si intersecano l'ottimalita' dipende dal punto di lavoro desiderato.

Un confronto puo' essere effettuato "mediando" sui diversi punti di lavoro del sistema.
L'**area sotto la curva ROC** (==AUC==) e' uno scalare in $[0\dots1]$ che caratterizza la prestazione media (maggiore e' meglio e').
Puo' essere calcolata come **integrale numerico** attraverso il metodo dei trapezi.

## Precision - Recall

Notazione usata in classificazione con classi sbilanciate.
Definiti a partire da $TN,TP,FP,FN$ (classificazione binaria).
- ==Precision== indica quanto e' accurato il sistema (dato da il rapporto tra il numero di TP e il numero di elementi totali classificati positive)
$$ \text{Precision} = \frac{TP}{TP + FP} $$
- ==Recall== indica quanto il sistema e' selettivo (equivale a $TPR$ (numero di TP su numero di P))
$$ \text{Recall} = \frac{TP}{TP + FN} = \frac{TP}{P} = TPR $$

Nella classificazione multi-classe precision e recall si possono calcolare **per ciascuna classe** (considerando la classe come positive e gli esempi di tutte le altre come negative).
![](precision-recall.png)

## Indicatori compatti

Indicatori a singolo valore utili per comparare l'accuratezza di modelli diversi.
- ==F1-score== (valori continui in $0\dots1$) e' calcolato come **media armonica** di Precision e Recall:
$$ \text{F1-score} = 2\times\frac{\text{Precision}\times\text{Recall}}{\text{Precision}+\text{Recall}} $$
	- Corrisponde alla media aritmetica se $\text{Precision} =\text{Recall}$
- ==Average Precision (AP)==: e' una sorta di **AUC** sul grafico Recall/Precision:
$$ AP = \sum_n(R_n-R_{n-1})Pn $$
Dove $P_n$ e $R_n$ sono i valori di precision e recall alla soglia $n$.

- ==Sensitivity== corrisponde a Recall e $TPR$, usato in diagnostica medica. Ad esempio: tra tutti i sottoposti al test quanti infetti sono correttamente identificati come tali?
- ==Specificity== corrisponde a $TNR$, usato in diagnostica medica, indica quanto e' accurato il sistema. Ad esempio: che percentuale di non infetti sottoposti a test sono stati dichiarati sani? (Corrisponde alla Recall della classe negativa)

### In Object detection

Possibili diversi tipi di errore, tra cui: oggetto non trovato, classe errata, bounding box sbagliata o imprecisa.
- ==Average Precision== (AP): calcolata per oggetti di una singola classe su tutto il database.
- ==mean Average Precision== (mAP): la media di AP su tutte le classi.
- Per calcolare $TP$ e $FP$ si considera una prediction corretta quando la classe e' giusta e la Intersection over Union (==IoU==) delle bounding box e' maggiore di un valore dato.

### Problemi Closed e Open set

Nel caso piu' semplice e piu' comune si assume che il pattern da classificare appartenga a una delle classi note (==closed set==).
In altri casi i pattern da classificare possono appartenere a una delle classi note o a nessuna di queste (==open set==).
Due soluzioni:
- Aggiunta di una classe fittizia "il resto del mondo" e si aggiungono al training set gli "esempi negativi".
- Si consente al sistema di non assegnare il pattern. A tal fine si definisce una *soglia* e si assegna il pattern alla classe piu' probabile solo quando la probabilita' e' superiore alla soglia.

## Convergenza

E' il primo obiettivo da perseguire durante l'addestramento sul Train set.
Per un classificatore il cui addestramento prevede un processo ==iterativo== si ha convergenza quando:
- La **loss** ha andamento *decrescente*
- L'**accuratezza** ha andamento *crescente*

## Generalizzazione e Overfitting

L'obiettivo e' massimizzare l'accuratezza su Test. Nell'ipotesi che Valid sia rappresentativo di Test, ci poniamo l'obiettivo di massimizzare l'accuratezza su Valid.
- Per ==generalizzazione== si intende la capacita' di **trasferire** l'elevata accuratezza raggiunta su Train e Valid.
- Se i gradi di liberta' del classificatore sono eccessivi, si raggiunge elevata accuratezza su Train, ma non su Valid (abbiamo scarsa generalizzazione). In questo caso si parla di ==overfitting== di Train. Questa situazione si verifica molto facilmente quando Train e' di piccole dimensioni
![](overfitting.png)
Nei processi di addestramento iterativo, tipicamente dopo un certo numero di iterazioni l'accuratezza su Valid non aumenta piu' (o inizia a decrescere) a causa dell'overfitting.
Questo comportamento puo' essere evitato arrestando l'addestramento nel punto ideale (==early stopping==).

### Controllare l'Ovefitting (massimizzare generalizzazione)

- I gradi di liberta' del classificatore non devono essere eccessivi, ma adeguati rispetto alla complessita' del problema.
	- Buona norma partire con **pochi gradi di liberta'** (controllati attraverso iperparametri) e via via aumentarli monitorando l'accuratezza su Train e Valid.
- I gradi di liberta' influenzano la ==regolarita'== della soluzione appresa.
	- La regolarita' della soluzione puo' essere talvolta controllata aggiungendo un **fattore regolarizzante** alla loss-function che penalizza soluzioni irregolari.

