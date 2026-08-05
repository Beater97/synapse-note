# Le immagini del README

Metti qui i file, con **questi nomi esatti** — il README li cerca per nome, e finché non ci sono
mostra il riquadro dell'immagine rotta.

| File | Cosa mostrare | Dove compare |
| --- | --- | --- |
| `home.png` | la home con le categorie colorate e lo sfondo | in cima, sotto i badge |
| `postit.png` | un postit con la barra di formattazione e la colonna allegati | griglia dei tipi |
| `foglio.png` | un foglio con dentro delle formule e un totale | griglia dei tipi |
| `diagramma.png` | sorgente a sinistra, disegno a destra | griglia dei tipi |
| `tela.png` | una tela con qualche blocco e una freccia | griglia dei tipi |
| `ai.png` | la colonna dell'assistente con la traccia dei passi | sezione Synapse AI |

## Come si fanno

- **Finestra intera, non schermo intero.** `Alt+Stamp` cattura la finestra attiva: senza il
  desktop attorno, e senza la barra delle applicazioni.
- **Tema scuro.** Le schermate scure si leggono meglio dentro GitHub, che di suo è chiaro o
  scuro a seconda di chi guarda — e su fondo chiaro una schermata scura resta nitida, mentre il
  contrario abbaglia.
- **Con dentro roba vera.** Una griglia vuota o tre note che si chiamano «prova» dicono che
  l'app non la usa nessuno. Note con nomi veri, e nessun dato che non vuoi far vedere.
- **Larghezza 1600–1900 px.** Sotto si vede sgranata sugli schermi a densità doppia, sopra è
  solo peso. PNG per l'interfaccia (il JPEG sporca i bordi del testo).
- **Sotto il megabyte l'una.** Se pesano, passale da [Squoosh](https://squoosh.app) o
  [TinyPNG](https://tinypng.com): sono immagini di un README, non stampe.

## Come si mettono nel testo

Percorso relativo, che è quel che il README usa già:

```markdown
![La home di Synapse](immagini/home.png)
```

Per decidere la misura serve l'HTML — Markdown non sa dimensionare, e una schermata a piena
larghezza dentro una pagina di testo la sovrasta:

```html
<img src="immagini/home.png" alt="La home di Synapse" width="860">
```

Se una schermata è illeggibile nel tema opposto, se ne mettono due e le sceglie il browser:

```html
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="immagini/home-scuro.png">
  <img src="immagini/home-chiaro.png" alt="La home di Synapse" width="860">
</picture>
```

## L'altra strada: senza committarle

Trascinando un'immagine dentro il riquadro di una issue (anche senza pubblicarla), GitHub la
carica e ti restituisce un indirizzo `https://github.com/user-attachments/…`. Quell'indirizzo
funziona nel README.

Comodo per una prova al volo, ma per le immagini del progetto conviene la cartella: stanno con
la loro versione, si vedono anche clonando la repository, e non dipendono da una issue che
qualcuno potrebbe cancellare.
