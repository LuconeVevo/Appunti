Linguaggi naturali / di programmazione:
- Lessico (le parole valide)
- Sintassi (le frasi)

Generazione automatica del codice del parser / compilatore per un nuovo linguaggio tramite un approccio dichiarativo.

Algoritmo: procedura che prima o poi termina.
Problema decidibile: si puo' risolvere con un computer.

I programmi scrivibili in un qualsiasi linguaggio sono enumerabili, ma i problemi non lo sono.


L'aspetto fondamentale e' dare un significato agli stati

# Automi a stati finiti

Modello per descrivere situazioni di calcolo in cui si **consumano informazioni una alla volta**, e durante la consumazione si devono memorizzare **quantita' finite di informazioni**.

**Tesi di Turing-Church**: ogni problema calcolabile da un algoritmo (piu' in generale tramite una procedura) puo' essere risolto da una Machina di Turing.

Alcuni problemi sono **non calcolabili** (non risolvibili algoritmicamente), come la raggiungibilita' di una certa istruzione in un qualsiasi programma dato.

Le ==logiche temporali== permettono di esprimere **propieta'** del tipo:
- non e' possibile raggiungere uno stato in cui il negozio ha spedito e non e' possibile raggiungere il trasferimento del denaro

**Model checker**: strumenti che verificano se *propieta' espresse tramite logiche temporali valgono oppure no*. Nel caso di fallimento forniscono controesempi (computazioni che non soddisfano la propieta').

# Linguaggi

**Alfabeto**: Insieme **finito** e non vuoto di simboli
Esempi: 
- $\Sigma = \{0,1\}$ (alfabeto binario)
- $\Sigma = \{a,b,c,\dots,z\}$ (inseme di tutte le lettere minuscole)
**Stringa**: Sequenza finita di simboli da un alfabeto $\Sigma$, es `0011001` e' una stringa su alfabeto $\{0,1\}$
**Stringa vuota**: La stringa con zero occorrenze di simboli da $\Sigma$, denotata con $\epsilon$
**Lunghezza di una stringa**: numero di posizioni per i simboli nella stringa, $|w|$ denota la lunghezza di $w$.

**Potenze di un alfabeto**: $\Sigma^k$ insieme delle stringhe di lunghezza $k$ con simboli da $\Sigma$.

L'insieme di tutte le stringhe su $\Sigma$ e' denotato da $\Sigma^*$, quindi:
$$ \Sigma^* = \Sigma^0 \cup \Sigma^1 \cup \Sigma^2 \cup \dots $$
La chiusura positiva di $\Sigma$, denotata con $\Sigma^+$, e':
$$ \Sigma^+ = \Sigma^1 \cup \Sigma^2 \cup \Sigma^3 \cup \dots $$
$$ \Sigma^* = \Sigma^+ \cup \{\epsilon\} $$

**Concatenazione**: Se $x$ e $y$ sono stringhe, allora $xy$ e' la stringa ottenuta collocando una copia di $y$ subito dopo una copia di $x$.
Per ogni stringa $x$, si ha $x\epsilon = \epsilon x = x$

**Linguaggi**:
Se $\Sigma$ e' un alfabeto, e $L \subseteq \Sigma^*$, allora $L$ e' un linguaggio, ad esempio:
- Insieme delle parole italiane legali
- Insieme dei programmi C legali
- Il linguaggio vuoto $\emptyset$
- Il linguaggio $\{\epsilon\}$ consiste della stringa vuota

## Automi a stati finiti deterministici

**Automa deterministico** $\rightarrow$ ogni stato ha una e una sola transizione uscente etichettata per ogni simbolo dell'alfabeto.

Un DFA e' una quintupla
$$ A = (Q, \Sigma, \delta, q_0, F) $$
- $Q$ e' un insieme finito di stati
- $\Sigma$ e' un alfabeto finito (simboli in input)
- $\delta$ e' una funzione di transizione da $Q \times \Sigma$ a $Q$, cioe': $(q, a) \mapsto p$
- $q_0 \in Q$ e' lo stato iniziale
- $F \subseteq Q$ e' un insieme di stati finali
![](dfa.png)

Un automa a stati finiti (FA) *accetta* una stringa $w = a_1 a_2 \dots a_n$ se esiste un cammino nel diagramma di transizione che:
1. Inizia nello stato iniziale
2. Finisce in uno stato finale (di accettazione)
3. Ha una sequenza di etichette $a_1 a_2 \dots a_n$

Ad esempio l'automa sopra accetta la stringa `01101`