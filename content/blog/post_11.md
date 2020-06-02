---
author: "Me"
date: 2020-06-02
title: "Ebiter Milano e portale web - Malasicurezza IT all'italiana"
best: false
---

È iniziato tutto un fresco due giugno.
A volte capita che assista i miei genitori in qualche compilazione di moduli online non del tutto chiari, o nel seguire procedure a dir poco oscure, ai limiti delle possibilità burocratiche umane.

In questo caso è la procedura per la riscossione di un semplice contributo alla genitorialità da EBiTer Milano.

>Ente Bilaterale per lo sviluppo dell'occupazione, della professionalità e della tutela sociale nel settore Terziario.

Niente di troppo complesso se non la perdita di tempo nel dover scannerizzare tutti i documenti necessari. Basterebbe un database pubblico del titolo occupazionale (che non sono un dato strettamente riservato, tranne eccezioni di sicurezza) e l'integrazione con SPID, ma sarebbe troppo semplice. Mai meno di cinque fotocopie cartacee per qualsiasi procedura. Gli alberi e gli sportellisti ringraziano.

Bene torniamo a noi; appena si apre la homepage vengo subito accolto dal banner GDPR per i cookie posizionato all'estremo superiore della pagina. Inusuale.

Capisco che magari in questo modo si voglia ottenere l'attenzione dell'utente bloccandogli l'accesso alla navbar, ma una soluzione meno invasiva, che magari non pregiudichi l'estetica e mi permetterebbe di capire almeno dove sono finito senza dovermi riferire alla sola url, sarebbe gradita. 

Penso che esista una regola non scritta in riferimento al fatto di non coprire mai navbar e logo visto che sono i punti di riferimento per un utente durante la consultazione di un portale. 

![image](/img/ebi1.JPG)

Queste dopotutto sono piccolezze, almeno il banner è presente quindi un minimo di fiducia sul rispetto della GPDR da parte del portale, possiamo anche riporla.

Ecco che subito dopo noto che il portale è interamente servito in chiaro senza HTTPS.

Di primo impatto penso ad un certificato SSL temporaneamente scaduto e in manutenzione, ma per un portale di questo tipo che tratta **anche dati personali** in un momento dove l'utilizzo del mezzo digitale è d'obbligo, è già di per se grave.
Oppure ad un malfunzionamento del servizio in stile INPS click day.

Facendomi un giro, noto che tutti i servizi presenti sul portale come tutti i form, sono serviti solo in HTTP ad eccezione di qualche font servito da Google. Altro che mixed-content... qua è tutto in chiaro e lo è da sempre.

-------
I FORM in http
---
-------
Veniamo alla compilazione dei vari moduli per la richiesta dei contributi.

Il punto dolente sono la compilazione di questi form con dati personali sensibili quali indirizzi, cf, identificativi vari che poi verranno restituiti in chiaro al server attraverso una semplice POST che se siamo fortunati verrà validata. Magari se farò mai un'analisi più approfondita una verifica per XSS potrei anche farla...

Compilando i campi e dopo una conferma via email, viene generata l'apertura di un secondo form dove inserire i documenti scannerizzati (carta di identità ecc.) sempre poi restituiti in chiaro al server e su chissà che altro backend interno.

La goccia che ha fatto traboccare il vaso e che mi ha spinto ad investigare questa immondizia software è relativa al fatto che il secondo form non accettava in alcun modo i miei allegati.

I formati "accettati" erano PDF, JPEG, JPG, PNG sotto i 4mb. 
Provando con file JPEG, PNG, JPG sotto e sopra i 4mb, ogni inserimento risultava non valido. Quindi è ovvio che in questo modo non si poteva procedere e abbiamo desistito scegliendo di inoltrare la richiesta via raccomandata.

Convertire tutti i file in documenti pdf, anche per fare solo un tentativo, era fuori questione a quel punto.

Un bug? 

Il server si sarà spaventato vista la rarità di user_agent: Chromium-Linux? 

Il tutto è semplicemente fatto con i piedi e quindi non funziona?

-------

Investighiamo...
---
-------

![image](/img/ebi2.JPG)

Stiamo solo entrando nella tana del coniglio, perchè vado a curiosare il webserver e lo stato di ssl su cui gira il portale. 

Una versione di IIS abbastanza antiquata... La 8.5 che risale ai tempi di Windows 8.1 e probabilmente implementata su un vecchio Windows server 2012 circa dello stesso periodo, ma mai dire mai.

Una veloce panoramica delle vulnerabilità su cui si potrebbe fare leva ne riporta un bel reportorio. D'altronde è probabile che le patch non siano state applicate quindi il divertimento è assicurato.

![image](/img/ebi3.JPG)

-------
X-AspNet-Version
---
-------

Ecco che anche i response header sono divulgati in chiaro e ci mostrano la versione del ASP.net framework direi non del tutto recente. (Siamo alla 4.8)

![image](/img/ebi4.JPG)


Le vulnerabilità note di .NET Framework 4 da sfruttare non mancano, per non parlare di quelle zero-day che potrebbero esistere.

![image](/img/ebi5.JPG)

-------
CMS
---
-------

Come CMS a quanto pare è utilizzato DotNetNuke che non escludo non venga aggiornato da parecchio tempo. Un'analisi più raffinata a ricerca della versione utilizzata potrebbe facilmente confermare la mia ipotesi.

![image](/img/ebi6.JPG)

-------
Porte esposte
---
-------

Situazione di porte e servizi esposti: pessima!

Per riservatezza non entrerò nel dettaglio dello scan, ma oltre alle porta 80 (http) sono aperte altre 4 porte relativamente a servizi altamente vulnerabili.
Della 443 non c'è traccia.

Il server ha accettato la connessione via telnet mentre tentavo di raggiungere uno dei servizi su porta aperta.
Non bene.

![image](/img/ebi12.JPG)

-------
Dominio e responsabilità
---
-------

Il server fa capo ad Aruba, quindi visionando il loro catalogo è plausibile che l'offerta sia per un server dedicato Windows 2012 e IIS 8.5, relativo all'offerta Hosting Windows.
Tralasciando il fatto che ad oggi la versione ultima è Windows server 2019, il server sembrerebbe localizzato in una delle farm di Arezzo, quindi è loro.

Nelle informazioni sul dominio invece fa capolino questa buffa società di "consulenza" dell'anteguerra.

![image](/img/ebi7.JPG)

Alicom sembrerebbe una società che in tempi passati rivendeva servizi per Aruba, ora confluita.

>Aruba Business Partner è il programma rivenditori di Aruba attraverso cui aziende e professionisti IT possono gestire o rivendere tutti i dei prodotti Aruba.

Ricercando sul web altre informazioni ci si imbatte in omonimi o reindirizzamenti verso Aruba.
Una pagina preistorica, degna di fare parte di una vetrina di archeologia informatica, compare.
Da una veloce lettura sembrerebbe una pagina che guida l'utente alla configurazione per l'accesso ai loro servizi web dei tempi passati.
Parliamo di  Windows95, Netscape e lire per intenderci.

```
http://www.alicom.com/servizi_frame.htm
```
-------
Record DNS
---
-------

![image](/img/ebi8.JPG)

I record mi reindirizzano verso un grovoglio di vecchie e nuove società di hosting dentro una cortina di fumo.

Tramite traceroute è visibile come endpoint la società EQUINIX che fa anche da ASN definendo le policy di routing.

I nomi dominio dei nameservers sono rispettivamente:

```
dns.consultingweb.it
dns2.consultingweb.it
```

Ricercando qualche informazione si trovano thread su forum vecchi di decine di anni che avvertono di stare alla larga da questa ex-società, ormai probabilmente confluita, per pratiche scorrette.

Per esempio:

```
Occhio a Consultingweb!! - Forum discussion
https://www.hostingtalk.it/forum/topic/3590-occhio-a-consultingweb/
```

Facendo Reverse IP Lookup scopriamo invece che sotto lo stesso ip confluiscono più domini uno dei quali non restituisce nulla mentre l'altro la pagina di pre-configurazione di IIS.

![image](/img/ebi9.JPG)

-------

Forse abbandonato, o in manutenzione?...

![image](/img/ebi10.JPG)

-------
Due parole conclusive
---
-------

In una sezione un po' nascosta del sito si puà trovare il seguente annuncio inserito da chissà quanto tempo:

![image](/img/ebi11.JPG)

Non resta che augurarsi che la situazione venga presa in mano da qualcuno di leggermente più competente e all'avanguardia.

Lavorare su sistemi legacy (ma soprattutto aggiornarli dopo secoli di immutabilità) è una delle sfide più toste da affrontare per una figura in campo IT, ma non resta che rimboccarsi le maniche perchè la sicurezza informatica è una disciplina trascendete e in determinati ambiti si scontra profondamente con la vita delle persone, le quali si affidano ai vari sistemi che incontrano, dietro garanzie di abili ed etici professionisti.

La mia persona è indissolubilmente anche i miei dati. 

Due pesi e due misure non possono più esistere nel 2020. 

Tuteliamo-ci.

