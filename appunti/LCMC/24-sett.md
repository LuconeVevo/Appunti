Dato un automa $A = (Q, \Sigma, \delta, q_0, F)$, come definisco il linguaggio di $A$ (le stringhe $W$ che il linguaggio accetta)?

$$ L(A) = \{w:\hat{\delta}(q_0,w)\in F\}$$
dove $\hat{\delta}(q_0,w)$ e' lo stato finale raggiunto dall'automa consumando la stringa $w$ partendo dallo stato $q_0$.

Per definire $\hat{\delta}$ usiamo l'induzione:
**Base**: $$\hat{\delta}(q,\epsilon) = q$$
**Induzione**: $$ \hat{\delta}(q,xa) = \delta(\hat{\delta}(q,x),a) $$
I linguaggi sono divisi in classi, la classe dei linguaggi definiti dai FA sono chiamati **linguaggi regolari**.

# Automi a stati finiti non deterministici (NFA)

Un NFA accetta una stringa se, tra i tanti possibili, esiste un cammino che conduce ad uno stato finale. 
Ad esempio un automa che accetta tutte e solo le stringhe che finiscono in `01`:
![](NFA01.png)

Un NFA e' una quintupla $A = (Q, \Sigma, \delta, q_0, F)$
dove $\delta$ e' una funzione di transizione da $Q \times \Sigma$ all'insieme dei sottoinsiemi di $Q$, cioe': $(q,a) \mapsto Q'$ con $Q' \subseteq Q$ (a differenza di DFA il risultato e' un sottoinsieme di Q)

Funzione estesa $\hat{\delta}(q,\epsilon)$, per induzione:
**Base**: 
$$ \hat{\delta}(q,\epsilon) = {q} $$
**Induzione**:
$$\hat{\delta}(q,xa) = \bigcup_{p\in\hat{\delta}(q,x)}\delta(p,a)$$
^^ unione tra tutti gli stati ottenuti con $\delta(p,a)$ per ogni $p$ preso dall'insieme degli stati raggiungibili consumando la stringa $x$.

Gli NFA sono di solito piu' facili da "programmare" dei DFA e **per ogni NFA $N$ esiste un DFA $D$, tale che $L(D) = L(N)$ e viceversa.**
Ogni stato del DFA e' un insieme degli stati del NFA.
Dato un NFA $N$:
$$ N = (Q_N, \Sigma, \delta_N, q_0, F_N) $$
possiamo costruire un DFA:
$$ D = (Q_D, \Sigma, \delta_D, \{q_0\}, F_D) $$
tale che $L(D) = L(N)$
Il passaggio da NFA a DFA ha complessita' esponenziale nel caso peggiore ($2^{|Q_N|}$), per evitare la crescita esponenziale degli stati possiamo costruire la tabella di transizione per $D$ solo per stati accessibili $S$ come segue:
**Base**: $S = \{q_0\}$ e' accessibile in $D$
**Induzione**: Se lo stato $S$ e' accessibile, lo sono anche gli stati $\delta_D(S,a)$ per ogni $a\in\Sigma$.

**Teorema 2.11**: Sia $D$ il DFA ottenuto da un NFA $N$ con la costruzione a sottoinsiemi. Allora $L(D) = L(N)$.
**Teorema 2.12**: Un linguaggio $L$ e' accettato da un DFA se e solo se $L$ e' accettato da un NFA.

## Transizioni epsilon
Una transizione epsilon non consuma alcun simbolo della stringa in input.
Permettono di creare versioni piu' semplici dei NFA ($\epsilon$-NFA).

Un $\epsilon$-NFA e' una quintupla $(Q,\Sigma,\delta,q_0,F)$ dove $\delta$ e' una funzione da $Q \times (\Sigma\cup\{\epsilon\})$ all'insieme dei sottoinsiemi di $Q$.
### Epsilon-chiusura

Chiudiamo uno stato aggiungendo tutti gli stati raggiungibili da lui tramite una sequenza $\epsilon\epsilon\dots\epsilon$.
Definizione induttiva di $\epsilon\text{CLOSE}(q)$:
**Base**: $q\in\epsilon\text{CLOSE}(q)$
**Induzione**:
$$ p \in \epsilon\text{CLOSE}(q)\ \text{and}\ r \in \delta(p,\epsilon) \Rightarrow r \in \epsilon\text{CLOSE}(q) $$

Definiamo induttivamente $\hat{\delta}$ per automi $\epsilon$-NFA
**Base**:
$$ \hat{\delta}(q,\epsilon) = \epsilon\text{CLOSE}(q) $$
**Induzione**:
$$ \hat{\delta}(q,xa) = \bigcup_{p\in\hat{\delta}(q,x)}(\bigcup_{t\in\delta(p,a)}\epsilon\text{CLOSE}(t)) $$

Il linguaggio accettato e': $\{w:\hat{\delta}(q_0,w)\cap F \neq \emptyset\}$


