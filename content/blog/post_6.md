---
author: "Me"
date: 2020-02-07
title: Windows 10 LTSC Optimize - My script
best: false
---
## Da Wikipedia per capire di che parliamo

Enterprise LTSC (Long-Term Servicing Channel) è una versione di supporto a lungo termine di Windows 10 Enterprise rilasciata ogni 2 o 3 anni. 
Ogni versione è supportata con aggiornamenti di sicurezza per 10 anni dopo il rilascio e non riceve intenzionalmente aggiornamenti di funzionalità. 
Alcune funzionalità, tra cui Microsoft Store e app in bundle, non sono incluse in questa edizione. 
Questa edizione fu in principio rilasciata come Windows 10 Enterprise LTSB (Long-Term Servicing Branch).
Ci sono attualmente 3 versioni di LTSC: una del 2015 (versione 1507), una del 2016 (versione 1607) e una del 2018 (versione 1809).


Dopo esserne venuto a conoscenza ed aver cucinato ad-hoc l'immagine iso attraverso vari tool, dopo un po' di test posso affermare concretamente che una versione così stabile, pulita ed ottimizzata non si vedeva da molto tempo da parte di Microsoft.
Perchè non renderla aperta al pubblico mainstream sottoforma di licenza acquistabile? Mistero. I professionisti ne sarebbero davvero felici. Eppure perseverano sulla strada secondo me sbagliata.

Ecco un'accesa e interessante discussione con un dipendente microsoft sul quando perchè e come (non) utilizzare LTSC: https://techcommunity.microsoft.com/t5/windows-it-pro-blog/ltsc-what-is-it-and-when-should-it-be-used/ba-p/293181

Una cosa è certa, con qualche piccolo ritocco lo ritengo il mio sistema operativo per desktop definitivo.

![image](/img/ltsc.png)


## Il mio script

https://github.com/Matt-Mf/My-LTSC-Optimize

Modifiche apportate: 

- Eliminazione della rimozione UAC che causava problemi ed instabilità di sistema.
- Eliminazione della rimozione di Defender.
- Piccoli fix vari.



