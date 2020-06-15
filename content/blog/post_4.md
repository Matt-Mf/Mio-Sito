---
author: "Me"
date: 2020-01-25
title: OpenVPN Android Bug Installa-Certificato 
best: false
---

Utilizzando vpn per questioni sia di privacy personale che di web-test extra-geografici rispetto al mio client, mi sono imbattuto in questo fastidioso bug ogni qualvolta ci si connetta al tunnel vpn su Android.

Con l'ultima versione dell'app ufficiale disponibile sul play-store, al momento 3.1.0, in fase di connessione alla VPN viene richiesto sempre tramite pop-up di selezionare o installare il certificato che il profilo pare non contenga.

**Ovviamente si tratta di un bug, in quanto il profilo VPN precedentemente inserito tramite file .ovpn ha già un certificato interno.**

Pur inserendo il certificato in formato .crt, non verrà comunque installato correttamente ne rilevato.

Il tunnel VPN viene comunque creato e la connessione viene instaurata e mantenuta senza alcun problema. Basta selezionare "continua" e ignorare l'avviso del certificato mancante.

**Il bug è presente su Android OREO e Oxygen 5.1.8. Su versioni ormai deprecate di Android come la 5.1 sembrerebbe non presentarsi. Con Android 10 non ho personalmente testato**


## Quindi come eliminare il noiosissimo e inutile avviso che ad ogni avvio si ripresenta?
-----------

Soluzione: Inserire all'interno del profilo .ovpn la seguente riga di codice 

```
setenv CLIENT_CERT 0 
```

<br>


## Nota
-----------
Una soluzione alternativa potrebbe anche essere utilizzare il più recente Wireguard.

Sulla stato della segnalazione e risoluzione del bug, un paio di discussioni sono già state aperte sul forum ufficiale OpenVPN.
Non escludo che potrebbero esserne comunque già al corrente.

La discussione sul forum ufficiale che ha ispirato questo piccolo promemoria:

```
forums.openvpn.net/viewtopic.php?t=26034
```
 


 
