# Informativa sulla privacy

**Synapse note** · Ultimo aggiornamento: 6 agosto 2026

[🇬🇧 English](PRIVACY.md) · [🇮🇹 Italiano](PRIVACY.it.md)

---

## In breve

**Synapse non raccoglie niente.** Nessun account, nessuna registrazione, nessuna telemetria, nessuna statistica d'uso, nessuna segnalazione automatica degli errori. Le tue note, i tuoi allegati e le tue impostazioni stanno in una cartella sul tuo computer e non vengono mandati da nessuna parte.

Dietro a questa applicazione non c'è nessun server. Chi l'ha scritta non ha modo di sapere che l'hai installata, cosa ci scrivi dentro, né se la usi.

---

## Quali dati tiene l'app, e dove

Tutto quello che Synapse salva sta sulla tua macchina, in modo predefinito in:

```
C:\Users\<tu>\.synapse
```

Quella cartella la puoi spostare dove vuoi da Impostazioni → *Dati e backup*.

| Cosa | Dove |
| --- | --- |
| Note, cartelle, impostazioni | `notes.db`, un file SQLite standard |
| Allegati e immagini | `documenti\` |
| Immagini di sfondo | `sfondi\` |
| Archivi di password | `notes.db`, cifrati (vedi sotto) |
| Registro degli errori | `errori.log`, testo semplice, solo in locale |

Niente di tutto questo viene trasmesso, sincronizzato o copiato altrove. Se cancelli la cartella, i dati non ci sono più: non ne esiste una copia da nessuna parte.

## Gli archivi di password

Il contenuto degli archivi è cifrato con **AES-256-GCM**, con una chiave derivata dalla tua password principale tramite **Argon2id** (64 MB di memoria, 3 passate, sale diverso per ogni archivio). Ogni scrittura usa un nonce nuovo.

**La password principale non viene salvata**, né su disco né altrove. Esiste in memoria soltanto finché un archivio è aperto. Vuol dire che nessuno — chi ha scritto l'app compresa — può recuperare i tuoi segreti se la dimentichi, ed è esattamente il punto.

## Quando l'app usa la rete

Synapse funziona completamente offline. Le connessioni avvengono **solo** in questi casi, e sempre perché li hai chiesti tu:

| Cosa fai | Dove va la richiesta | Cosa viene mandato |
| --- | --- | --- |
| Usi l'assistente | `127.0.0.1:11434` — [Ollama](https://ollama.com), sulla tua macchina | la tua richiesta e la nota che hai aperto. Con un modello scaricato in locale non escono dal computer; con un modello **cloud** di Ollama, è Ollama a inoltrarli ai propri server — vedi sotto |
| Chiedi all'assistente di cercare in rete | `html.duckduckgo.com` | soltanto le parole cercate |
| Chiedi di leggere una pagina, o carichi una specifica API da un indirizzo | l'indirizzo che indichi tu | soltanto la richiesta |
| Apri una pagina web dentro un blocco della tela | il sito che apri | quello che manda un browser qualunque: quel sito ti vede, come ti vedrebbe altrove |
| Installi Ollama o Python dalla schermata di benvenuto | `ollama.com`, `python.org` | soltanto la richiesta di scaricamento |

Nient'altro. Nessuna statistica d'uso, nessun «segnale a casa», nessun controllo aggiornamenti che porti con sé un identificativo. Puoi verificarlo con un firewall: blocca l'app del tutto e tutto continua a funzionare tranne i casi qui sopra.

**In nessuno di questi casi Synapse raccoglie qualcosa.** Cosa ne fa un terzo di una richiesta che hai chiesto tu — DuckDuckGo delle parole cercate, un sito che hai aperto, Ollama con un modello cloud — lo dice l'informativa di quel terzo.

## L'assistente

Synapse parla sempre e soltanto con **un indirizzo**: `127.0.0.1:11434`, il demone di Ollama sulla tua macchina. Non contatta mai direttamente un fornitore di intelligenza artificiale, e non ha nessuna chiave per farlo.

Con un modello che hai scaricato e che gira sul tuo computer, le note vengono lette in locale, la risposta è generata in locale, e niente esce di lì.

> ### ⚠️ I modelli cloud di Ollama
>
> Ollama può servire anche **modelli cloud**, che girano sui server di Ollama. Se accedi a Ollama e ne scegli uno in Impostazioni → *Intelligenza artificiale*, il demone locale inoltra la richiesta — e con lei **il testo che hai mandato: la tua domanda e la nota che hai aperto**.
>
> Quella connessione la apre Ollama, non Synapse, e ricade nell'[informativa di Ollama](https://ollama.com/privacy). Synapse non può vederla né impedirla: dal suo lato l'indirizzo è sempre quello locale.
>
> Se vuoi la garanzia che niente esca dal tuo computer, usa un modello scaricato in locale — quelli che installi con `ollama pull`. I modelli cloud si riconoscono dal suffisso `-cloud` nel nome.

Gli altri due casi in cui l'assistente tocca la rete sono quelli già elencati: la ricerca, che manda a DuckDuckGo soltanto le parole cercate, e la lettura di una pagina, che scarica l'indirizzo che hai chiesto.

## Minori

Synapse è uno strumento di uso generale e non si rivolge ai minori. Non raccoglie dati da nessuno, di nessuna età.

## Terze parti

Synapse è costruita su librerie open source: l'elenco completo, con le licenze, è dentro l'app in Impostazioni → Informazioni → *Crediti*. Quelle librerie girano in locale e nessuna manda dati da nessuna parte.

Se installi Ollama o Python, quei programmi seguono i propri termini: non fanno parte di Synapse, e Synapse non manda loro nulla oltre a quello che le chiedi.

## Distribuzione

Se hai installato Synapse dal **Microsoft Store**, lo scaricamento lo gestisce Microsoft, con la propria informativa. Se l'hai presa da **GitHub**, vale lo stesso per GitHub. Nessuno dei due passa a chi ha scritto l'app dati personali oltre al conteggio anonimo dei download.

## Modifiche

Se questa informativa cambia, cambia con lei la data in cima, e le versioni precedenti restano visibili nella cronologia di questa repository. Non c'è nessuna lista a cui mandare un avviso, perché non c'è nessuna lista di utenti.

## Contatti

Domande su questa informativa: apri una [issue](../../issues) in questa repository.

---

*Synapse non conserva dati personali su nessun server, perché non c'è nessun server. Non c'è niente a cui chiedere accesso, niente da rettificare e niente da cancellare, tranne la cartella sul tuo computer — che è interamente tua.*
