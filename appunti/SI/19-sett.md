# Portafoglio applicativo aziendale
Si differenzia in base alla tipologia di azienda

## CIM / Smart manufacturing
Computer integrated manufacturing, e' una architettura multilivello finalizzata all'ottimizzazione dei processi e alla gestione delle risorse.
SCADA e' un componente del sistema CIM, permette di prendere tutte le informazione che stanno sulle singole macchine e centralizzare per motivi di controllo il funzionamento della singola macchina.
IoT e' un sistema distribuito, ogni agente ha reasoning on board, SCADA e' centralizzato
![](SCADA_arch.png)
I sistemi SCADA sono nella fase stabile dell'hype cycle, si sono evoluti per scalabilita' e capacita' di analisi dei dati raccolti e attualmente si punta sulla sicurezza.
## MES
MES (livello superiore a SCADA) implementano ottimizzazioni di tutta la fabbrica
Ricevono ordini dall'ERP, raccolgono dati dallo SCADA e forniscono informazioni aggiornate all'ERP.

## ERP
Suite di moduli applicativi che supportano l'intera gamma dei processi aziendali.
Un unico sistema e una unica base di dati (unicita' dell'informazione), con processi implementati sopra attraverso una interfaccia unica.
L'obiettivo finale e' la circolarita' delle informazioni.
![](ERP_arch.png)
Sono prescrittivi, cioe' implementano a priori i processi aziendali; questo implica un cambiamento dei processi a causa dei vincoli imposti dal ERP (business process reengineering), esiste pero' un margine ottenuto tramite la parametrizzazione.
A questi moduli possono essere aggiunti:
- PLM (Product Lifecycle Mangement)
- SCM (Supply Chain Management)
- CRM(Customer Relationship Management)
- E-Procurement

### Unicita' dell'informazione
Tutte le elaborazioni condividono uno e un solo valore per ogni informazione, questo aspetto e' ottenuto utilizzando un'unica base di dati condivisa che offre i seguenti vantaggi:
- ==Sincronizzazione dei dati== 
- ==Assenza di ridondanza==
- ==Tracciabilita' degli aggiornamenti==
- ==Affidabilita' dell'informazione aziendale==

### Estensione e modularita'
L'ampiezza della copertura dei sistemi ERP fa si che questi possano essere utilizzati come unica soluzione per il SI.
La modularita' del sistema permette all'azienda di scegliere solo i moduli di interesse. Le strategie adottabili sono:
- Incrementale: si acquistano progressivamente i moduli che nella precedente configurazione del SI mancavano
- One stop shopping: si predilige la linearita' acquistando i moduli di un solo vendor
- Best of breed: vengono utilizzati i moduli di diversi vendor che meglio si prestano alle esigenze dell'azienda o che sono considerati i migliori

Tipicamente per aziende con funzioni core di nicchia si adotta un approccio best of breed per le funzioni core e one stop shop per le rimanenti.
Per aziende con funzioni core generiche si adotta un unico fornitore che copra tutte le funzionalita' possibili, mentre si adotta un approccio best of breed per le funzioni non coperte.

### Prescrittivita'
I sistemi ERP incorporano la logica del processo gestionale, e' quindi necessario far aderire i processi aziendali a quelli definiti nell'ERP. Questo puo' avere un elevato impatto organizzativo. Esistono grandi margini di personalizzazione necessari a gestire il gap tra il modulo standard e le specificita' delle aziende.

### Architettura
I sistemi ERP nascono su architetture client-server e si evolvono verso schemi thin-client web enabled per supportare la logica di rete.