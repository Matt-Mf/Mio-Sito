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

Niente di troppo complesso se non la perdita di tempo nel dover scannerizzare tutti i documenti necessari. Basterebbe istituire un database pubblico del titolo occupazionale e l'integrazione con SPID, ma sarebbe troppo semplice. Comunque mai meno di cinque fotocopie cartacee per qualsiasi procedura. Gli alberi tagliati e le pensioni degli sportellisti ringraziano.

Bene torniamo a noi; appena si apre la homepage vengo subito accolto dal banner GDPR per i cookie posizionato all'estremo superiore della pagina, in modo da offuscare qualsiasi riferimento. Inusuale.

Capisco che magari in questo modo si voglia ottenere l'attenzione dell'utente bloccandogli l'accesso alla navbar, ma una soluzione meno invasiva, che magari non pregiudichi l'estetica e lasci un minimo di punti di riferimento per l'utente, sarebbe gradita. 

Penso che esista una regola non scritta nel web-design, in riferimento al fatto di non coprire mai navbar e logo principale visto che sono i punti di riferimento principali per un utente durante la consultazione di un portale. (oltre alla URL ovviamente)

![image](/img/ebi1.JPG)

Queste dopotutto sono piccolezze, almeno il banner è presente quindi un minimo di fiducia sul rispetto GPDR da parte del portale, possiamo anche riporla.

Ecco che subito dopo noto che il tutto è interamente servito in chiaro.

Di primo impatto penso ad un certificato SSL temporaneamente scaduto e/o in manutenzione, oppure all'utilizzo di un sistema di caching obsoleto/malconfigurato che magari serve solo determinate sezioni in chiaro.

Facendomi un giro, noto invece che tutti i form come qualsiasi altra sezione, sono serviti in chiaro. Nient HTTPS/SSL.
Ovviamente ad eccezione di qualche font servito da Google. Altro che mixed-content... qua è tutto in chiaro e sembrerebbe esserlo da parecchio tempo.

Per un portale di questo tipo che tratta **dati personali** in un momento dove l'utilizzo del mezzo digitale è d'obbligo, è già di per se grave.

Visti comunque i trascorsi del famoso "click day" INPS, non c'è da stupirsi.

-------
I FORM in http
---
-------
Veniamo alla compilazione dei vari moduli per la richiesta dei contributi.

Il punto dolente sono la compilazione di questi form con dati personali sensibili quali indirizzi, cf, identificativi vari che poi verranno restituiti in chiaro al server attraverso una POST che se siamo fortunati verrà validata. 

Magari un'analisi più approfondita per verificare la validazione degli input e testare un paio di attacchi (XSS, SQL Injection ecc.) si potrebbe fare, ma il mio tempo è limitato e non vorrei mai rubare il lavoro ai LulzSecITA o qualche team di hacker pakistani. Mi limiterò ad una veloce analisi superficiale, anche se sono abbastanza sicuro che non ne uscirebbero bene.

Compilando i campi e dopo una conferma inviata via email (che probabilmente può essere intercettata in uscita dallo stesso server vista la presenza del mail-server sullo stesso), viene generata l'apertura di un secondo form dove inserire i documenti scannerizzati (carta di identità ecc.) sempre poi restituiti in chiaro al server in POST e su chissà poi che altro backend interno.

(da verifica successiva sulle porte in ascolto, sullo stesso server girano infatti webserver, email-server con smtp e pop3 e altri servizi pericolosamente exploitabili...)

La goccia che ha fatto traboccare il vaso e che mi ha spinto ad investigare questa immondizia software è relativa al fatto che il secondo form non accettava in alcun modo i miei allegati.

I formati "accettati" erano PDF, JPEG, JPG, PNG sotto i 4mb. 
Provando con file JPEG, PNG, JPG sotto e sopra i 4mb, ogni inserimento risultava non valido. Quindi è ovvio che in questo modo non si poteva procedere e abbiamo desistito scegliendo di inoltrare la richiesta via raccomandata.

Convertire tutti i file in documenti pdf, anche per fare solo un tentativo, era fuori questione a quel punto.

Un bug? Vittima di un attacco man-in-the-middle?

Una post mal interpretata? Il server si sarà spaventato vista la rarità di user_agent: Chromium-Linux? 

Il tutto è semplicemente fatto con i piedi e quindi non funziona?

-------
Investighiamo...
---
-------

![image](/img/ebi2.JPG)

Stiamo solo entrando nella tana del coniglio, perchè vado a curiosare web-server e lo stato di SSL su cui gira il portale. 

Una versione di IIS abbastanza antiquata... La 8.5 che risale ai tempi di Windows 8.1 e probabilmente implementata su un vecchio Windows server 2012 circa dello stesso periodo, ma mai dire mai. 

Una veloce panoramica delle vulnerabilità su cui si potrebbe fare leva ne riporta un bel reportorio. D'altronde è probabile che le patch non siano state applicate quindi il divertimento è assicurato.

![image](/img/ebi3.JPG)

-------
X-AspNet-Version
---
-------

Ecco che anche i response header sono divulgati in chiaro e ci mostrano la versione del ASP.net framework direi non del tutto recente. (Siamo alla 4.8)
Un aiutino ad eventuali hacker, servito su un piatto d'argento.

![image](/img/ebi4.JPG)


Le vulnerabilità note di .NET Framework 4 da sfruttare non mancano, per non parlare di quelle zero-day che potrebbero esistere.

![image](/img/ebi5.JPG)

-------
CMS
---
-------

Come CMS a quanto pare è utilizzato DotNetNuke che non escludo non venga aggiornato da parecchio tempo. Un'analisi più raffinata a ricerca della versione utilizzata potrebbe facilmente confermare la mia ipotesi e quindi portare a galla numeri imbarazzanti di vulnerabilità sfruttabili.

![image](/img/ebi6.JPG)

-------
Porte esposte
---
-------

Situazione di porte e servizi esposti: pessima!

Per riservatezza non entrerò nel dettaglio dello scan, ma oltre alle porta 80 (http) sono aperte altre 4 porte relative a servizi altamente vulnerabili.
Della 443 (HTTPS) non c'è traccia.

Il server ha accettato la connessione via telnet mentre tentavo di raggiungere uno dei servizi su porta aperta.
Non bene.

![image](/img/ebi12.JPG)

-------
Dominio e responsabilità
---
-------

Il server fa capo ad Aruba, quindi visionando il loro catalogo è plausibile che l'offerta sia per un server dedicato Windows 2012 e IIS 8.5, relativo all'offerta Hosting Windows.
Tralasciando il fatto che ad oggi la versione stabile è Windows server 2019, il server sembrerebbe localizzato in una delle farm di Arezzo, quindi è loro.

Nelle informazioni sul dominio (e quindi gestione) invece fa capolino questa buffa società di "consulenza" dell'anteguerra.

![image](/img/ebi7.JPG)

Alicom sembrerebbe una società che in tempi passati rivendeva servizi per Aruba, ora confluita.

>Aruba Business Partner è il programma rivenditori di Aruba attraverso cui aziende e professionisti IT possono gestire o rivendere tutti i dei prodotti Aruba.

Ricercando sul web altre informazioni ci si imbatte in omonimi o reindirizzamenti verso Aruba.
Una pagina preistorica, degna di fare parte di una vetrina di archeologia informatica, compare.
Da una veloce lettura sembrerebbe una pagina che guida l'utente alla configurazione per l'accesso ai loro servizi web dei tempi passati.
Parliamo di Windows95, Netscape e lire per intenderci.

```
http://www.alicom.com/servizi_frame.htm
```
-------
Record DNS
---
-------

![image](/img/ebi8.JPG)

I record mi reindirizzano verso un grovoglio di vecchie e nuove società di hosting dentro una cortina di fumo.

Tramite traceroute è visibile come endpoint la società EQUINIX che fa anche da ASN definendo le policy di routing. Partner di Aruba?...

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

Lavorare su sistemi legacy (ma soprattutto aggiornarli dopo secoli di immutabilità) è una delle sfide più toste da affrontare per un admin IT, ma non resta che rimboccarsi le maniche perchè la sicurezza informatica è una disciplina trascendete e in determinati ambiti si scontra profondamente con la vita delle persone, le quali si affidano ai vari sistemi che incontrano, dietro garanzie di abili ed etici professionisti che "dovrebbero" protegger-ci.

Il data-breach in questo caso è dietro l'angolo, e la mia persona come la mia vita è indissolubilmente legata anche ai miei dati. 

Due pesi e due misure non possono più esistere nel 2020. 

Tuteliamo-ci, please.

