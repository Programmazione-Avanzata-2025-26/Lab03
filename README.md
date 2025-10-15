# Lab 03 - Soluzione

> **💡 NOTE 💡** 
> 
> - Nella soluzione proposta, i concetti di "automobile" e "noleggio" sono rappresentati attraverso le classi: 
> `Automobile` (nel file `automobile.py`) e `Noleggio` (nel file `noleggio.py`)
> 
> - La definizione dei metodi dunder `__str__()` e `__repr__()` serve a stabilire come un oggetto viene rappresentato 
> in forma testuale (ad esempio quando lo si stampa).\
> ATTENZIONE: definire `__str__()` permette di stampare direttamente l'oggetto, quindi funziona se viene 
> eseguita un'istruzione del tipo, supponendo l'oggetto noleggio, `print(noleggio)`, ma se l'oggetto fa parte di
> una collezione, ad esempio "lista_noleggi", l'istruzione `print(lista_noleggi)`, con la sola definizione 
> `__str__()`, stamperebbe gli oggetti come indirizzi di memoria. Per evitare questo bisogna quindi definire il metodo `__repr__()`.
> 

#### Argomenti

- Lettura da file (continuazione).
- Eccezioni (continuazione).
- Classi e oggetti (metodi dunder, metodi getter e setter, collezioni di oggetti).
- Ordinamento (di oggetti).

---

## Autonoleggio

Progettare un sistema per gestire il noleggio delle automobili di un autonoleggio. L’autonoleggio è caratterizzato da 
un nome e da un responsabile e gestisce una flotta di automobili i cui dati sono memorizzati in un unico file CSV, 
`automobili.csv`, che possono essere noleggiate.

Il file `automobili.csv` contiene, riga per riga, le informazioni relative alle automobili. Ogni riga corrisponde a una 
singola automobile definita da un codice univoco, la marca, il modello, l’anno di immatricolazione e il numero 
di posti. Un esempio del file è il seguente:

```file
A1,Toyota,Yaris,2019,5
A2,Ford,Focus,2020,
A3,Fiat,500,2018,4
A4,Volkswagen,Golf,2021,5
...
```

### Implementazione

Per questo laboratorio è necessario utilizzare la classe `Autonoleggio` presente nel file `autonoleggio.py`.  
Le informazioni sulle automobili devono essere modellate tramite una classe dedicata.  
Il file `main.py` consente di interagire con il sistema tramite un menù testuale utilizzabile dalla console. 

```menu in console
--- MENU AUTONOLEGGIO ---
1. Modifica nome del responsabile dell’autonoleggio
2. Carica automobili da file
3. Aggiungi una nuova automobile (da tastiera)
4. Visualizza automobili ordinate per marca
5. Noleggia automobile
6. Termina noleggio automobile
7. Esci
Scegli un'opzione >>
```

Le operazioni disponibili devono essere gestite dai metodi della classe `Autonoleggio`.
Per leggere e modificare il nome del responsabile, si possono utilizzare direttamente gli attributi della classe oppure 
definire gli opportuni metodi getter/setter.   

Per caricare i dati dal file CSV deve essere implementato, all’interno della classe `Autonoleggio`, 
il metodo `carica_file_automobili(file_path)`, che legge il file passato come parametro, crea gli oggetti corrispondenti 
e li memorizza nel sistema. Se il file non viene trovato il metodo scatena l’eccezione `FileNotFoundError`. 

Per aggiungere una nuova automobile deve essere implementato, all’interno della classe `Autonoleggio`, il metodo 
`aggiungi_automobile(marca, modello, anno_immatricolazione, num_posti)`, che riceve come parametri la marca 
dell’automobile, il modello, l’anno di immatricolazione e il numero di posti. Il metodo crea e inserisce un nuovo 
oggetto automobile nel sistema (assegnandogli automaticamente un codice univoco formato dalla lettera `A` seguita da un 
numero intero progressivo, calcolato a partire dall’ultimo identificativo già presente nel sistema). Il metodo deve 
restituire il riferimento dell'automobile aggiunta.

La classe `Autonoleggio` deve inoltre includere il metodo `automobili_ordinate_per_marca()`, che restituisce un elenco 
delle automobili presenti nel sistema ordinate alfabeticamente in base alla marca.  

Per gestire i noleggi, la classe `Autonoleggio` deve implementare il metodo 
`nuovo_noleggio(data, id_automobile, cognome_cliente)`. Ogni noleggio sarà caratterizzato da un codice univoco, 
dalla data in cui è avvenuto, il codice univoco dell’automobile e il cognome del cliente che sta effettuando il
noleggio. Il codice univoco del noleggio sarà definito con la lettera `N` seguita da un numero intero progressivo
a partire da 1, ad esempio `N1`, `N2`, `N3`, e così via. Il codice deve essere assegnato nel momento in cui il noleggio 
viene creato. Il metodo deve restituire un riferimento al noleggio creato. Il metodo inoltre deve verificare se 
l'automobile richiesta sia già noleggiata oppure non sia presente nel sistema. Se una di queste condizioni è vera, deve 
scatenare un’eccezione (ad esempio generica, `Exception`) per indicare l’errore.

Per terminare un noleggio, la classe `Autonoleggio` include il metodo `termina_noleggio(id_noleggio)`.
Il metodo riceve come parametro il codice univoco del noleggio ed ha il compito di concludere il noleggio, rimuovendo 
ogni riferimento dal sistema. Se il codice non corrisponde ad alcun noleggio esistente, il metodo deve scatenare 
un'eccezione (ad esempio generica, `Exception`) per indicare l’errore.

> **💡 NOTA:** 
>Tutte le classi richieste dall’esercizio (esclusa la classe `Autonoleggio`) devono implementare un metodo 
> speciale di rappresentazione testuale, ovvero `__str__()` o, in alternativa, `__repr__()`, in modo che l’oggetto risulti 
> comprensibile quando viene stampato.
