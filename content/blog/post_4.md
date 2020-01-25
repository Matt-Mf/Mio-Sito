---
author: "Me"
date: 2020-01-25
title: OpenVPN Android Bug Installa-Certificato 
best: false
---

Utilizzando vpn commerciali per questioni, sia di privacy che in fase di test per accessi alla rete da posizioni differenti rispetto al mio client, mi sono imbattuto in questo fastidioso baco ogni qualvolta ci si connetta al tunnel.

Con l'ultima versione dell'app ufficiale disponibile sul play-store, al momento 3.1.0, in fase di connessione alla VPN viene richiesto tramite pop-up di selezionare o installare il certificato che il profilo non contiene.
Ovviamente si tratta di un baco, in quanto il profilo VPN precedentemente inserito tramite file .ovpn ha già un certificato interno.
Pur rendendo disponibile il certificato in formato .crt, non verrà installato ne rilevato.

Il tunnel VPN viene comunque creato e la connessione viene instaurata e mantenuta senza alcun problema. Basta selezionare "continua" e ignorare l'avviso del certificato mancante.

Rilevato il baco su Android OREO e Oxygen 5.1.8. Su versioni deprecate di Android come la 5.1 sembrerebbe non presentarsi.

## Come eliminare il noiosissimo baco che ad ogni avvio si ripresenta?

SOLUZIONE: Inserire all'interno del profilo .ovpn il seguente codice 

```
setenv CLIENT_CERT 0 
```

## Nota

Sulla stato delle segnalazioni e risoluzione del baco, un paio di discussioni sono già state aperte sul forum ufficiale OpenVPN, ma ancora niente risoluzione. 
Non escludo che potrebbero esserne già al corrente.

Discussione che ha ispirato questo piccolo promemoria:

```
forums.openvpn.net/viewtopic.php?t=26034
```
 


 
