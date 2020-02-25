---
author: "Me"
date: 2020-02-07
title: Windows 10 LTSC Optimize - My forked script
best: false
---

Enterprise LTSC (Long-Term Servicing Channel) è una versione a supporto esteso di Windows 10 Enterprise rilasciata ogni 2 o 3 anni. 

Ogni versione è supportata con aggiornamenti di sicurezza per 10 anni dopo il rilascio e non riceve intenzionalmente aggiornamenti di funzionalità. 

Alcune funzionalità, tra cui Microsoft Store e app in bundle, non sono incluse in questa edizione. 

Questa edizione fu in principio rilasciata come Windows 10 Enterprise LTSB (Long-Term Servicing Branch).

Ci sono attualmente 3 versioni di LTSC: una del 2015 (versione 1507), una del 2016 (versione 1607) e una del 2018 (versione 1809).

------------------------------------------------------------------------------------------------------------------------

Dopo esserne venuto a conoscenza ed aver cucinato ad-hoc l'immagine .iso attraverso vari tool e un po' di test, posso affermare concretamente che una versione così stabile, pulita ed ottimizzata non si vedeva da molto tempo da parte di Microsoft. Ricordate il lontano XP Sp 3 o il più recente 7 ultimate? A voi la scelta sul più stabile.

Perchè non rendere LTSC aperta al pubblico consumer sottoforma di licenza acquistabile? Mistero. I professionisti in particolare sarebbero davvero felici di non dover risolvere problemi su problemi dopo ogni aggiornamento che porta funzionalità inutilizzate. Inoltre un'installazione pulita è tutto ciò di cui si ha bisogno.
Che me ne faccio di Candy Crash o dell'integrazione Xbox su delle macchine da ufficio? Questo, a parer mio, è uno dei tanti ambiti in qui una distribuzione Windows ridondante è solo un intralcio che potrebbe portare anche ad una estensione delle superifici di possibile attacco relativamente alla sicurezza. 

Eppure perseverano su di una strada secondo me sbagliata. Quello che viene a meno sono la stabilità e la sicurezza a scapito di nuove funzionalità e sincronizzazioni su cloud ridondanti, perchè oggi è la moda del dato/app centralizzato è forte, ma non per questo soluzione ottima e vincente per tutti gli ambiti.
Per non parlare del beta testing a cui sono sottoposti inconsapevolmente tutti gli utilizzatori a meno di opt-out anche complessi (telemetria, account microsoft forzato ecc.).

Ecco un'accesa e interessante discussione con un dipendente microsoft sul loro blog; quando perchè e come (non) utilizzare LTSC secondo loro: 

```
https://techcommunity.microsoft.com/t5/windows-it-pro-blog/ltsc-what-is-it-and-when-should-it-be-used/ba-p/293181
```

Una cosa è certa, con qualche piccolo ritocco lo ritengo il mio sistema operativo per desktop definitivo.

![image](/img/ltsc.png)


## Script -->

```
https://github.com/Matt-Mf/My-LTSC-Optimize
```
Modifiche apportate: 

- Eliminazione della rimozione UAC che causava problemi ed instabilità di sistema.
- Eliminazione della rimozione di Defender.
- Piccoli fix vari.

## Guida LTSC Crafting -->

```
https://rentry.co/ltsc_optimize
```
