Ecco una nota strutturata per **Obsidian** sull'argomento **IPS/IDS**, progettata per la tua preparazione al **CCNA**.

---


> [!ABSTRACT]
> 
> **Core Logic:** Analizzare la differenza tra monitoraggio passivo (IDS) e prevenzione attiva (IPS) per proteggere la rete da minacce che i firewall tradizionali non possono rilevare tramite la Deep Packet Inspection (DPI).

### 🔍 Definizioni Fondamentali

> [!INFO] **Intrusion Detection System (IDS)**
> 
> Un dispositivo o software che monitora il traffico di rete alla ricerca di attività sospette o violazioni delle policy. Opera in modalità **promiscua** (copia del traffico) e genera solo **alert**.

> [!INFO] **Intrusion Prevention System (IPS)**
> 
> Un'evoluzione dell'IDS che siede direttamente nel percorso del traffico (**In-line**). Ha la capacità di analizzare il pacchetto e **bloccare** la minaccia in tempo reale prima che raggiunga la destinazione.

---

### ⚔️ Confronto Tecnico: IDS vs IPS

|**Caratteristica**|**IDS (Intrusion Detection)**|**IPS (Intrusion Prevention)**|
|---|---|---|
|**Posizionamento**|**Out-of-band** (Porta SPAN/Mirror)|**In-line** (Il traffico lo attraversa)|
|**Azione**|Genera Log e Alert|Scarta pacchetti e chiude sessioni|
|**Impatto Rete**|Nessun ritardo (lavora su copie)|Può introdurre **Latenza** (ispezione live)|
|**Obiettivo**|Visibilità e Analisi post-evento|Protezione proattiva e Mitigazione|

---

### 🛠️ Metodi di Rilevamento

Per identificare il "male", questi sistemi utilizzano due driver principali:

### 📑 1. Signature-based (Basato su Firme)

- **Logica:** Confronta il traffico con un database di "impronte digitali" di attacchi noti.
    
- **Pro:** Estremamente accurato per minacce conosciute.
    
- **Contro:** Inefficace contro gli attacchi **Zero-Day** (minacce nuove non ancora catalogate).
    

### 📈 2. Anomaly-based (Basato su Anomalie)

- **Logica:** Crea una "baseline" del traffico normale e interviene quando vede deviazioni statistiche (es. un picco di traffico ICMP mai visto prima).
    
- **Pro:** Può rilevare attacchi sconosciuti.
    
- **Contro:** Alto rischio di **Falsi Positivi**.
    

---

### ⚠️ Limitazioni e Rischi

> [!CAUTION] **Asimmetria Operativa e Latenza**
> 
> L'adozione di un **IPS** introduce un **Single Point of Failure**: se l'IPS fallisce o è sovraccarico, il traffico legittimo potrebbe essere bloccato o rallentato significativamente. Inoltre, l'ispezione del traffico criptato (HTTPS) richiede risorse massive per la decrittazione e ricrittazione (SSL Inspection).

---

### 💡 Integrazione nel Modello Cisco

Nel programma **CCNA**, l'IPS non è quasi mai un'entità isolata, ma è integrato nei seguenti nodi:

- **Next-Generation Firewalls (NGFW):** Dispositivi come i Cisco **Firepower** che uniscono Firewall, IPS e AMP (Advanced Malware Protection).
    
- **Cloud Security:** Servizi come **Cisco Umbrella** che spostano la prevenzione a livello di risoluzione DNS.
    
- **NBAR (Layer 7):** Mentre l'IPS cerca minacce, **NBAR** identifica le applicazioni per ottimizzare il traffico tramite **QoS**, lavorando entrambi con la **Deep Packet Inspection (DPI)**.
    

---

### 📋 Checklist per l'Esame

- [ ] Ricordare che l'IPS è **In-line**.
    
- [ ] Sapere che l'IDS non blocca il traffico, invia solo **notifiche**.
    
- [ ] Distinguere tra **Signature** (noto) e **Anomaly** (comportamento).
    
- [ ] Associare l'IPS al concetto di **Deep Packet Inspection**.