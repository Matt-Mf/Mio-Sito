---
author: "Me"
date: 2020-02-07
title: Windows 10 LTSC - Ottimizzazione ISO
best: false
---

Enterprise LTSC (Long-Term Servicing Channel) è una versione a supporto esteso di Windows 10 Enterprise rilasciata ogni 2 o 3 anni. 

Ogni versione è supportata con aggiornamenti di sicurezza per 10 anni dopo il rilascio e non riceve intenzionalmente aggiornamenti di funzionalità. 

Alcune funzionalità, tra cui Microsoft Store e app in bundle, non sono incluse in questa edizione. Quindi niente giochi preinstallati, niente integrazioni superflue (xbox ecc.) e niente nuove funzionalità non richieste distribuite mensilmente.

Questa edizione fu in principio rilasciata come Windows 10 Enterprise LTSB (Long-Term Servicing Branch).

Ci sono attualmente (2020) 3 versioni di LTSC: una del 2015 (versione 1507), una del 2016 (versione 1607) e una del 2018 (versione 1809).

------------------------------------------------------------------------------------------------------------------------

Dopo esserne venuto a conoscenza ed aver cucinato ad-hoc l'immagine .iso attraverso vari tool e un po' di test, posso affermare concretamente che una versione così stabile, pulita ed ottimizzata non si vedeva da molto tempo da parte di Microsoft. Ricordate il lontano XP Sp 3 o il più recente 7 ultimate? A voi la scelta sul più stabile.

Allora perchè la scelta da parte di Microsoft di non rendere LTSC disponibile al pubblico consumer sottoforma di licenza acquistabile? 
Perchè Windows 10 LTSC deve essere un prodotto difficilmente acquistabile e riservato solo al ramo business? 
Perchè Windows 10 LTSC non è Windows 10 stesso senza gli inutili fronzoli che dovrebbero esistere solo in una versione beta?

I professionisti in particolare sarebbero davvero felici di non dover risolvere problemi su problemi dopo ogni aggiornamento che porta funzionalità inutilizzate e non richieste. Un'installazione pulita e longeva di un prodotto stabilmente testato è tutto ciò di cui si ha bisogno in ambito professionale.
Che me ne faccio di Candy Crash o dell'integrazione Xbox su delle macchine da lavoro?

Quello che viene a meno sono la stabilità e la sicurezza a scapito di nuove funzionalità e sincronizzazioni su cloud ridondanti, perchè oggi è la moda del dato/app centralizzato a farla da padrone, ma non per questo soluzione ottima e vincente per tutti gli ambiti. Il paradigma del Software as a service non è sempre un'alternativa valida.
Per non parlare del beta testing a cui sono sottoposti inconsapevolmente tutti gli utilizzatori del sistema operativo più diffuso al mondo, a meno di opt-out contorti (telemetria, account microsoft, sincronizzazioni ecc.).

Ecco un'accesa e interessante discussione con un dipendente microsoft sul loro blog; quando perchè e come (non) utilizzare LTSC secondo la stessa Microsoft: 

```
https://techcommunity.microsoft.com/t5/windows-it-pro-blog/ltsc-what-is-it-and-when-should-it-be-used/ba-p/293181
```

Qui sono descritte le peripezie di un coraggioso utente Reddit che ha cercato di approfondire in che modo un utente "comune" possa ottenere una licenza per LTSC:

```
https://www.reddit.com/r/sysadmin/comments/bbof9s/windows_10_enterprise_ltsc_what_are_the_purchase/
```

Una cosa è certa, con qualche piccolo ritocco lo ritengo oggi il sistema operativo per desktop definitivo, ma che per qualche motivo a noi sconosciuto, Microsoft custodisce gelosamente per sé e per pochi eletti. 

![image](/img/ltsc.png)


## Script -->

```
https://github.com/Matt-Mf/My-LTSC-Optimize
```
Modifiche apportate: 

- Eliminazione della rimozione UAC che causava problemi ed instabilità di sistema.
- Eliminazione della rimozione di Defender.

## Guida LTSC Crafting -->

```
https://rentry.co/ltsc_optimize
```
