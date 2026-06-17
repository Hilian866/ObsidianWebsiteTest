

## 1. Architettura Meccanica e Concetti Chiave

Le connessioni seriali venivano utilizzate per i collegamenti WAN punto-punto geografici. A differenza delle porte Ethernet, i link seriali richiedono una netta separazione dei ruoli hardware per la sincronizzazione del segnale (Clocking):

- **DCE (Data Communications Equipment):** È il lato che fornisce il segnale di clock (il "metronomo" della velocità del link). Tipicamente rappresenta il provider (ISP). **Nei laboratori, un lato del cavo deve essere configurato come DCE e deve avere il comando `clock rate`.**
    
- **DTE (Data Terminal Equipment):** È il lato che riceve il clock. Tipicamente rappresenta il router del cliente (Customer Edge).
    
- **Encapsulation:** Le porte seriali Cisco utilizzano di default il protocollo **HDLC** (proprietario Cisco). L'alternativa standard industriale è il **PPP** (Point-to-Point Protocol), utilizzato per l'autenticazione (CHAP/PAP).
    

## 2. CLI di Configurazione Base (R1 - Lato DCE)

_Nota: In Packet Tracer, il lato DCE si riconosce dall'icona di un piccolo orologio sul cavo rosso._


>[!WARNING] ```Router# show controllers serial 0/1/0```

Plaintext

```
R1(config)# interface Serial 0/1/0
R1(config-if)# ip address 10.0.0.1 255.255.255.252
R1(config-if)# encapsulation ppp           ! Cambia da HDLC (default) a PPP (opzionale)

! --- COMANDO TASSATIVO SOLO SUL LATO DCE ---
R1(config-if)# clock rate 64000            ! Imposta la velocità di sincronizzazione (es. 64 Kbps)

R1(config-if)# no shutdown
```

## 3. CLI di Configurazione Base (R2 - Lato DTE)

Plaintext

```
R2(config)# interface Serial 0/1/0
R2(config-if)# ip address 10.0.0.2 255.255.255.252
R2(config-if)# encapsulation ppp           ! Deve corrispondere al lato opposto
R2(config-if)# no shutdown                 ! NON serve il clock rate sul lato DTE
```

## 4. Analisi Oggettiva e Troubleshooting (Comandi di Verifica)

### Verificare chi è DCE e chi è DTE

Se non vedi i componenti fisici o l'orologio in Packet Tracer, questo comando interroga l'hardware per capire chi deve gestire il clock:

_Se l'output dicesse `DTE V.35`, significa che l'inserimento del comando `clock rate` su quel router verrebbe ignorato dal sistema._

### Verifica dello Stato del Protocollo

#### ⚠️ Matrice degli Stati di Errore (Troubleshooting rapido)

- **Serial0/x is up, line protocol is up:** Tutto funzionante (Efficienza del monitoraggio OK).
    
- **Serial0/x is down, line protocol is down:** Problema fisico (Cavo scollegato, interfaccia spenta dall'altro lato o manca il `no shutdown`).
    
- **Serial0/x is up, line protocol is down:** Errore logico/incapsulamento. I due router hanno protocolli diversi (es. uno HDLC e uno PPP) oppure **ti sei dimenticato il comando `clock rate` sul lato DCE**.
    

# 🧠 Tag per Obsidian

`#networking` `#cisco-ios` `#wan` `#legacy` `#ccna-notes`