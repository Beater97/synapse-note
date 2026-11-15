# Informativa sulla privacy

**Synapse note** · Ultimo aggiornamento: 15 novembre 2026

[🇬🇧 English](PRIVACY.md) · [🇮🇹 Italiano](PRIVACY.it.md)

---

## In breve

**Synapse non raccoglie niente.** Nessun account, nessuna registrazione, nessuna telemetria, nessuna statistica d'uso, nessuna segnalazione automatica degli errori. Le tue note, i tuoi allegati e le tue impostazioni stanno in una cartella sul tuo computer.

Dietro l'applicazione non c'è nessun server di Synapse. Lo sviluppatore non ha modo di sapere che l'hai installata, cosa ci scrivi, o se la usi.

Alcune funzioni mandano dati a terzi **solo quando le usi**: un motore AI in rete, un link pubblico, note e cartelle condivise con altri PC. Qui sotto trovi ognuna, con cosa viene mandato e dove.

---

## Quali dati tiene l'app, e dove

Tutto quel che Synapse salva sta sul tuo computer, di partenza in:

```
C:\Users\<tu>\.synapse
```

Puoi spostare la cartella dove vuoi da Impostazioni → *Dati e backup*.

| Cosa | Dove |
| --- | --- |
| Note, cartelle, impostazioni | `notes.db`, un normale file SQLite |
| Allegati, immagini, video | `documenti\` |
| Immagini di sfondo | `sfondi\` |
| Archivi di password | `notes.db`, cifrati (vedi sotto) |
| Chiavi API dei motori AI in rete | Gestione credenziali di Windows, non il database |
| Log degli errori | `errori.log`, testo semplice, solo in locale |

Niente di tutto questo viene salvato o raccolto dallo sviluppatore. Se cancelli la cartella i dati non ci sono più, a meno che tu non abbia fatto un backup o condiviso una nota con qualcuno.

## Archivi di password

Il contenuto degli archivi è cifrato con **AES-256-GCM**, con una chiave derivata dalla password principale tramite **Argon2id** (64 MB di memoria, 3 passate, sale diverso per archivio). A ogni scrittura si usa un nonce nuovo.

**La password principale non viene mai salvata**, né su disco né altrove. Esiste in memoria solo mentre un archivio è aperto. Vuol dire che nessuno, nemmeno lo sviluppatore, può recuperare i tuoi segreti se la dimentichi, ed è proprio questo il punto.

Gli archivi di password non si pubblicano, non si condividono con altri PC, non vengono mandati a nessun motore AI e non entrano nella ricerca.

## Quando l'app usa la rete

Synapse funziona completamente offline. Le connessioni di rete avvengono **solo** in questi casi, tutti avviati da te:

| Cosa fai | Dove va la richiesta | Cosa viene mandato |
| --- | --- | --- |
| Usi l'assistente con **Ollama** | `127.0.0.1:11434`, Ollama sul tuo computer | la tua richiesta e le note che l'assistente legge. Con un modello scaricato in locale non esce mai dal computer; con un modello **cloud** di Ollama, è Ollama a inoltrarla ai suoi server (vedi sotto) |
| Usi l'assistente con **Claude** | `api.anthropic.com` (Anthropic) | la tua richiesta, la nota aperta e le note che l'assistente legge per rispondere, con la tua chiave API |
| Usi l'assistente con **GPT** | `api.openai.com` (OpenAI) | le stesse cose, con la tua chiave API |
| Usi un motore **compatibile OpenAI** | l'indirizzo che hai scritto | le stesse cose, con la tua chiave API se l'hai impostata |
| Chiedi all'assistente di cercare sul web | `html.duckduckgo.com` | solo le parole della ricerca |
| Chiedi all'assistente di leggere una pagina, o carichi una specifica API da un indirizzo | l'indirizzo indicato da te o dall'assistente | solo la richiesta. Gli indirizzi del tuo computer o della tua rete locale vengono rifiutati |
| Apri una pagina web dentro un blocco della tela | il sito che apri | quel che manda un normale browser: quel sito ti vede, come qualunque sito |
| Crei un **link pubblico** | Cloudflare (`*.trycloudflare.com`) | la pagina della nota che hai condiviso, servita dal tuo computer (vedi sotto) |
| Condividi note o cartelle **con altri PC** | gli altri PC, attraverso la rete iroh (vedi sotto) | le note condivise e i loro allegati, cifrati end-to-end |
| Scarichi il programma dei link dalla configurazione o alla prima condivisione | `github.com` (le versioni di `cloudflared` di Cloudflare) | solo la richiesta di download |
| Installi Ollama, Python o un modello AI dalla schermata di benvenuto | `ollama.com`, `python.org`, l'archivio dei modelli di Ollama | solo la richiesta di download |

Nient'altro. Nessuna statistica d'uso, nessuna «telefonata a casa», nessun controllo degli aggiornamenti che porti con sé un identificativo. Puoi verificarlo con un firewall: blocca l'app del tutto, e tutto tranne i casi qui sopra continua a funzionare.

**In nessuno di questi casi Synapse raccoglie qualcosa.** Quel che un terzo fa con una richiesta che hai chiesto tu (un fornitore AI con il tuo testo, DuckDuckGo con le parole cercate, Cloudflare con una pagina condivisa, un sito che hai aperto) è regolato dall'informativa di quel terzo.

## L'assistente AI

Il motore lo scegli tu in Impostazioni → *Intelligenza artificiale*.

**Ollama (di partenza).** Synapse parla con `127.0.0.1:11434`, il servizio di Ollama sul tuo computer. Con un modello scaricato che gira in locale, le note si leggono in locale, la risposta nasce in locale, e niente esce dal computer.

> ### ⚠️ I modelli cloud di Ollama
>
> Ollama può servire anche **modelli cloud**, che girano sui server di Ollama. Se accedi a Ollama e scegli uno di quelli, il servizio locale inoltra la richiesta, e con lei **il testo che hai mandato: la tua domanda e le note che l'assistente ha letto**.
>
> Quella connessione la fa Ollama, non Synapse, e ricade sotto l'[informativa di Ollama](https://ollama.com/privacy). I modelli cloud si riconoscono dal suffisso `-cloud` nel nome. Se vuoi la garanzia che niente esca dal computer, usa un modello scaricato in locale (`ollama pull`).

**Claude, GPT o un server compatibile OpenAI.** Con uno di questi motori, le tue richieste, la nota aperta e le note che l'assistente legge per rispondere vengono mandate a quel fornitore, con la tua chiave API. Il fornitore le tratta secondo le sue condizioni ([Anthropic](https://www.anthropic.com/legal/privacy), [OpenAI](https://openai.com/policies/privacy-policy)), e l'uso si paga sul tuo conto presso di lui. Con un server compatibile OpenAI i dati vanno a chi gestisce quel server: se gira sul tuo computer, non escono da lì.

Le chiavi API stanno in Gestione credenziali di Windows, mai nel database, nei backup o nei file condivisi. Gli archivi di password non vengono mai inviati, con nessun motore.

## Link pubblici

Il mappamondo in una nota pubblica una fotografia di quella nota come pagina web. La pagina è servita **dal tuo computer** finché Synapse è aperto, e arriva in rete attraverso un tunnel gratuito di Cloudflare (`cloudflared`, senza account). Questo vuol dire che:

- chi ha il link può leggere quella pagina, e Cloudflare trasporta il traffico fra lui e il tuo computer;
- il link vale **10 minuti** da quando è stato creato, poi smette di funzionare; chiudendo Synapse si ferma subito;
- vedi ogni link aperto, e lo chiudi, da *Condivisioni* nella barra in alto.

## Note e cartelle condivise con altri PC

Quando inviti qualcuno in una nota o in una cartella, le due copie di Synapse si collegano direttamente fra loro, con [iroh](https://iroh.computer). Il canale è **cifrato end-to-end** con chiavi che appartengono alle due installazioni.

- Non c'è nessun server di Synapse. Quando le due reti non permettono un collegamento diretto, il traffico passa da un relay pubblico di iroh, che inoltra byte cifrati che non può leggere né cambiare.
- Perché i PC si trovino, mentre la condivisione è attiva la chiave di rete di ogni installazione e i suoi indirizzi di rete del momento vengono pubblicati nel servizio di ricerca di iroh.
- Viaggia solo quel che hai condiviso: le note, i loro allegati (fino a 100 MB l'uno) e i nomi scelti da te e dagli altri membri. Gli archivi di password non viaggiano mai.
- Prima che qualcuno entri vedi il suo nome e decidi tu. Da *Condivisioni* cambi i permessi o togli i membri.

Gli altri membri ricevono una copia completa di quel che hai condiviso, sul loro computer, e Synapse non può riprendersela.

## Minori

Synapse è uno strumento d'uso generale e non è rivolto ai minori. Non raccoglie dati da nessuno, di nessuna età.

## Terze parti

Synapse è fatta con librerie open source; l'elenco completo, con le licenze, è nell'app in Impostazioni → Informazioni → *Crediti*. Quelle librerie girano in locale e nessuna manda dati da nessuna parte, salvo per le funzioni descritte sopra.

Se installi Ollama, Python o `cloudflared`, o usi un fornitore AI in rete, quei programmi e servizi sono regolati dalle loro condizioni. Non fanno parte di Synapse, e Synapse non manda loro niente oltre a quel che le chiedi.

## Distribuzione

Se hai installato Synapse dal **Microsoft Store**, il download lo gestisce Microsoft e a quella transazione si applica la sua informativa. Se l'hai scaricata da **GitHub**, vale lo stesso per GitHub. Nessuno dei due passa allo sviluppatore dati personali, oltre al conteggio anonimo dei download.

## Modifiche a questa informativa

Se l'informativa cambia, cambia con lei la data in cima, e le versioni precedenti restano visibili nella storia di questa repository. Non c'è una mailing list da avvisare, perché non c'è un elenco di utenti.

## Contatti

Domande su questa informativa: apri una [issue](../../issues) in questa repository.

---

*Synapse non tiene dati personali su nessun server, perché non c'è nessun server di Synapse. Non c'è niente da chiedere, da correggere o da cancellare, tranne la cartella sul tuo computer, che controlli tu del tutto.*
