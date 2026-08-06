# Le immagini del README

Due serie, una per lingua: `IT/` la usa [README.it.md](../README.it.md), `EN/` la usa
[README.md](../README.md). I README cercano i file per nome — se un nome cambia da una parte,
va cambiato anche nel README che lo punta, altrimenti resta il riquadro dell'immagine rotta.

| Cosa mostra | `IT/` | `EN/` | Dove compare |
| --- | --- | --- | --- |
| la home con le categorie colorate e l'alberatura | `home.png` | `03_home_workspace_en.png` | in cima, sotto i badge |
| un postit | `postit.png` | `06_postits_en.png` | griglia dei tipi, in alto a sinistra |
| una lista con le caselle da spuntare | `liste.png` | `04_list_note_en.png` | griglia dei tipi, in alto a destra |
| un notebook con una cella Python e il suo output | `notebook.png` | `05_notebook_en.png` | griglia dei tipi, in basso a sinistra |
| una tela con dei blocchi appoggiati sopra | `board.png` | `02_infinite_board_en.png` | griglia dei tipi, in basso a destra |
| l'assistente | `ai.png` | `01_ai_sidebar_en.png` | sezione Synapse AI |

Sono banner 16:9 con la frase già stampata sopra, non schermate nude. Cambiandone una, tienile
nello stesso stile: quattro immagini in griglia con due trattamenti diversi si vedono subito.

Le due serie mostrano la stessa cosa con l'interfaccia e la frase nella lingua della cartella.
Rifacendone una, rifai la coppia: se resta indietro, un README finisce con lo scatto nella
lingua sbagliata e non se ne accorge nessuno finché non lo legge qualcuno che non parla
italiano.

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
![La home di Synapse](immagini/IT/home.png)
```

Per decidere la misura serve l'HTML — Markdown non sa dimensionare, e una schermata a piena
larghezza dentro una pagina di testo la sovrasta:

```html
<img src="immagini/IT/home.png" alt="La home di Synapse" width="860">
```

Se una schermata è illeggibile nel tema opposto, se ne mettono due e le sceglie il browser:

```html
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="immagini/IT/home-scuro.png">
  <img src="immagini/IT/home-chiaro.png" alt="La home di Synapse" width="860">
</picture>
```

## L'altra strada: senza committarle

Trascinando un'immagine dentro il riquadro di una issue (anche senza pubblicarla), GitHub la
carica e ti restituisce un indirizzo `https://github.com/user-attachments/…`. Quell'indirizzo
funziona nel README.

Comodo per una prova al volo, ma per le immagini del progetto conviene la cartella: stanno con
la loro versione, si vedono anche clonando la repository, e non dipendono da una issue che
qualcuno potrebbe cancellare.
