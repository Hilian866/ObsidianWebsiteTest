### 🧠 Core Logic
Implementazione di una **pipeline di blogging automatizzata** che trasforma le note di **Obsidian** in un sito web statico professionale. Il sistema si basa sulla fase di **"Express"** del framework **CODE** di Tiago Forte, eliminando ogni attrito tra la generazione dell'idea e la sua pubblicazione online. [00:18](https://www.youtube.com/watch?v=dnE7c0ELEH8&t=18s)

---

### 🛠️ Lo Stack Tecnologico (The "Insane" Pipeline)
Il workflow automatizzato utilizza una combinazione di strumenti locali e cloud per garantire velocità e controllo totale del codice.

| Componente | Strumento | Scopo Tecnico |
| :--- | :--- | :--- |
| **Editor / PKM** | **Obsidian** | Scrittura in Markdown e gestione conoscenza. |
| **Generator** | **Hugo** | Framework per la creazione di siti statici (SSG). |
| **Automation** | **Python** | Script per la gestione degli asset (immagini) di Obsidian. |
| **Repository** | **GitHub** | Versioning e trigger per il deployment. |
| **Hosting** | **Hostinger** | Hosting performante con supporto Webhook. |

> [!INFO] Il Framework CODE
> Basato sul libro *"Building a Second Brain"*, il processo segue quattro fasi: **Capture** (Cattura), **Organize** (Organizza), **Distill** (Distilla) ed **Express** (Esprimi). Quest'ultima fase è il fulcro del video: condividere per validare la propria competenza. [00:52](https://www.youtube.com/watch?v=dnE7c0ELEH8&t=52s)

---

### 🏗️ Configurazione Tecnica di Base

#### 1. Setup di Obsidian e Hugo
Il blog vive in una sottocartella specifica del vault di Obsidian chiamata `posts`. [05:10](https://www.youtube.com/watch?v=dnE7c0ELEH8&t=310s)
Per far funzionare **Hugo**, è necessario installare preventivamente:
- **Git**: Per il controllo di versione.
- **Go (Golang)**: Linguaggio su cui è costruito Hugo. [06:16](https://www.youtube.com/watch?v=dnE7c0ELEH8&t=376s)

#### 2. Sincronizzazione dei file
Per spostare i file Markdown dal Vault di Obsidian alla cartella `content` di Hugo, si utilizzano comandi di sistema:
- **Windows**: `robocopy`
- **Mac/Linux**: `rsync` [13:18](https://www.youtube.com/watch?v=dnE7c0ELEH8&t=798s)

---

### 🐍 Il Problema delle Immagini (Python Script)
Obsidian gestisce gli allegati in una cartella centralizzata, mentre Hugo richiede che le immagini siano in una cartella `static`. Il video propone uno **script Python** per:
1. Analizzare i file Markdown alla ricerca di link a immagini.
2. Copiare fisicamente i file dalla cartella `Attachments` di Obsidian alla cartella `static/images` di Hugo.
3. Riformattare il link nel Markdown per renderlo compatibile con il web. [16:20](https://www.youtube.com/watch?v=dnE7c0ELEH8&t=980s)

```python
# Esempio logica script:
# Step 1: Cerca link immagini tipo ![[immagine.png]]
# Step 2: Copia file in Hugo static_images_dir
# Step 3: Sostituisce link con formato standard Markdown ![](images/immagine.png)
```

---

### 🚀 Deployment e Automazione Webhook

#### Autenticazione e Git
È fondamentale configurare le **SSH Keys** per permettere allo script di comunicare con GitHub senza richiedere password manualmente ad ogni commit. [20:41](https://www.youtube.com/watch?v=dnE7c0ELEH8&t=1241s)

#### Deployment Strategico
Anziché caricare tutto il progetto, si utilizza il comando `git subtree split` per estrarre solo la cartella `public` (il sito compilato) e inviarla a un branch specifico (es. `hostinger-deploy`). [21:13](https://www.youtube.com/watch?v=dnE7c0ELEH8&t=1273s)

> [!ABSTRACT] Auto-Deployment tramite Webhook
> Configurando un **Webhook** su GitHub e puntandolo all'URL fornito da **Hostinger**, il server riceve un segnale ogni volta che il codice viene aggiornato e scarica automaticamente la nuova versione del blog. [23:35](https://www.youtube.com/watch?v=dnE7c0ELEH8&t=1415s)

---

### ⚡ Il "Mega Script" Finale
Per rendere il processo realmente **frictionless**, tutti i passaggi sopra descritti vengono condensati in un unico script Bash o PowerShell. [25:24](https://www.youtube.com/watch?v=dnE7c0ELEH8&t=1524s)

> [!CAUTION] Attenzione ai Metadati
> Ogni nota di Obsidian destinata al blog deve contenere il **Frontmatter** (YAML) corretto (titolo, data, tags, draft), altrimenti Hugo non sarà in grado di processare il post correttamente. [14:33](https://www.youtube.com/watch?v=dnE7c0ELEH8&t=873s)

---
*Nota generata per il Personal Knowledge Management su Obsidian.*