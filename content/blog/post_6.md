---
author: "Me"
date: 2020-02-07
title: Windows 10 LTSC - Cucinando l'.ISO perfetta
best: false
---

Enterprise LTSC (Long-Term Servicing Channel) è una versione a supporto esteso di Windows 10 Enterprise rilasciata ogni 2 o 3 anni. 

Ogni versione è supportata con aggiornamenti di sicurezza per 10 anni dopo il rilascio e non riceve intenzionalmente aggiornamenti di funzionalità. 

Alcune funzionalità, tra cui Microsoft Store e app in bundle, non sono incluse in questa edizione. Quindi niente giochi fuffa preinstallati, niente integrazioni superflue (xbox ecc.)e niente nuove funzionalità non richieste distribuite mensilmente. Insomma, niente fronzoli.

Questa edizione fu in principio rilasciata come Windows 10 Enterprise LTSB (Long-Term Servicing Branch).

Ci sono attualmente (Oggi 2020) 3 versioni di LTSC: una del 2015 (versione 1507), una del 2016 (versione 1607) e una del 2019 (versione 1809).

----------------

Dopo esserne venuto a conoscenza, ed aver cucinato ad-hoc l'immagine .iso attraverso vari tool e un po' di test (**Link alla guida che ho scovato in fondo alla pagina**), posso affermare concretamente che una versione così stabile, pulita ed ottimizzata non si vedeva da molto tempo da parte di Microsoft. Ricordate il lontano XP Sp 3 o il più recente 7 ultimate? A voi la scelta sul più stabile.

* Perchè la scelta da parte di Microsoft di **non** rendere LTSC disponibile al pubblico consumer sottoforma di licenza acquistabile? 
* Perchè Windows 10 LTSC deve essere un prodotto riservato solo al ramo business più stretto? 
* Perchè Windows 10 LTSC non è semplicemente Windows 10 stesso senza gli inutili fronzoli e circostanze che dovrebbero esistere solo in una ipotetica versione beta?

I professionisti IT, a quanto vedo, sarebbero davvero felici di non dover risolvere problemi su problemi dopo ogni aggiornamento che porta funzionalità inutilizzate e non richieste che nel milgiore dei casi portano ad un inutile consumo di risorse. Un sistema operativo pulito e longevo in termini di aggiornamenti di sicurezza, di un prodotto stabilmente testato, è tutto ciò di cui si ha bisogno in ambito professionale.
L'utilità di Candy Crash o dell'integrazione Xbox su delle macchine da lavoro?
La sicurezza di un integrazione con un smartphone sconosciuto in ambito aziendale?

La soluzione "mitigante" in questo caso è passare le giornate nel registro delle policy a configurare ogni minimo cavillo su cui Microsoft ha ben pensato di divertirsi.

Quello che viene a meno sono la stabilità e la sicurezza a scapito di nuove funzionalità e sincronizzazioni su cloud ridondanti, perchè oggi è la moda del dato/app/servizio centralizzato a farla da padrone, ma non per questo soluzione ottima e vincente per tutti gli ambiti. Il paradigma del Software as-a-service non è sempre un'alternativa valida.
Per non parlare del beta testing a cui sono sottoposti inconsapevolmente tutti gli utilizzatori del sistema operativo più diffuso al mondo, a meno di opt-out contorti e fuori dalla portata di tutti (telemetria varia, account microsoft, sincronizzazioni ecc.).

Ecco che ho trovato un'accesa e interessante discussione con un dipendente microsoft su un loro blog post.
Quando perchè e come (non) utilizzare LTSC secondo la stessa Microsoft: 

```
https://techcommunity.microsoft.com/t5/windows-it-pro-blog/ltsc-what-is-it-and-when-should-it-be-used/ba-p/293181
```

Qui invece sono descritte le peripezie di un coraggioso utente Reddit che ha cercato di approfondire in che modo un utente "comune" possa ottenere una licenza per LTSC:

```
https://www.reddit.com/r/sysadmin/comments/bbof9s/windows_10_enterprise_ltsc_what_are_the_purchase/
```

Una cosa è certa, con qualche piccolo ritocco lo ritengo oggi il sistema operativo per desktop definitivo. 

![image](/img/ltsc.png)


## Script -->

```
https://github.com/Matt-Mf/My-LTSC-Optimize
```
Modifiche apportate: 

- Eliminazione della rimozione UAC che causava problemi ed instabilità di sistema.
- Eliminazione della rimozione di Defender.

## Guida LTSC .iso Crafting -->

```
https://rentry.co/ltsc_optimize
```

<br>

-------

Aggiornamento: Forse una modalità per l'acquisto di una licenza per LTSC (a partire da una installazione di windows 10 OEM pulita) esiste. Di certo c'è solo la complessità della procedura da seguire.

```
https://community.spiceworks.com/topic/2167558-explicit-instructions-for-purchasing-a-windows-10-ltsc-license
```

