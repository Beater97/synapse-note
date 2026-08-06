# Le immagini del README

Metti qui i file, con **questi nomi esatti** — il README li cerca per nome, e finché non ci sono
mostra il riquadro dell'immagine rotta.

| File | Cosa mostra | Dove compare |
| --- | --- | --- |
| `home.png` | la home con le categorie colorate e l'alberatura | in cima, sotto i badge |
| `postit.png` | un postit | griglia dei tipi, in alto a sinistra |
| `liste.png` | una lista con le caselle da spuntare | griglia dei tipi, in alto a destra |
| `notebook.png` | un notebook con una cella Python e il suo output | griglia dei tipi, in basso a sinistra |
| `board.png` | una tela con dei blocchi appoggiati sopra | griglia dei tipi, in basso a destra |
| `ai.png` | l'assistente | sezione Synapse AI |

Sono banner 16:9 con la frase già stampata sopra, non schermate nude. Cambiandone una, tienile
nello stesso stile: quattro immagini in griglia con due trattamenti diversi si vedono subito.

**Le frasi sopra le immagini sono in italiano, anche nel README inglese.** Chi arriva da fuori
vede l'interfaccia in inglese e il fumetto in italiano. Non è grave — l'app si capisce lo stesso
— ma il giorno che rifai i banner, farne una serie in inglese è la cosa che alza di più la
qualità della pagina. In quel caso i file inglesi vanno accanto agli altri (`home-en.png`, e
così via), e il README inglese punta a quelli.

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
