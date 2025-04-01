# Algoritmo di Dijkstra – Analisi e Implementazione

## Panoramica
Questo repository contiene l'implementazione dell'algoritmo di Dijkstra per la risoluzione di labirinti caratterizzati da ingressi e uscite multipli. L'algoritmo legge un labirinto da un file Excel denominato **"Labirinto Dijkstra.xlsx"** e ne elabora la struttura per determinare il percorso più breve tra i punti di ingresso (contrassegnati con **'E'**) e di uscita (contrassegnati con **'U'**) tramite una variante dell'algoritmo di Dijkstra.

## Contenuti del Repository
- **Labirinto Dijkstra.xlsx**  
  File Excel contenente la rappresentazione testuale del labirinto. Le celle sono valorizzate con:
  - `'0'`: Percorso libero (cella percorribile).
  - `'E'`: Ingresso.
  - `'U'`: Uscita.
- **Algoritmo di Dijkstra.ipynb**  
  Notebook Jupyter che contiene l'intero codice dell'algoritmo.
- **README.md**  
  Il presente file, contenente una descrizione dettagliata del progetto, della struttura del file Excel e dell'implementazione dell'algoritmo.

## Formato del File Excel
Il labirinto è rappresentato in un file Excel senza intestazioni (header). Ogni cella corrisponde a una posizione della griglia ed è interpretata come segue:
- **'0'**: Cella percorribile.
- **'E'**: Ingresso (cella percorribile). Le coordinate vengono salvate come posizione iniziale.
- **'U'**: Uscita (cella percorribile). Le coordinate vengono salvate come posizione finale.
- **Altri Valori**: Qualsiasi altra cella viene considerata un muro (non percorribile).

## Dettagli dell'Implementazione

### Parsing del Labirinto
- **Funzione:** `parse_maze_multiple_entrances_exits(df)`
- **Descrizione:**  
  - Converte il DataFrame derivante dal file Excel in una matrice numerica (array NumPy), impostando le celle percorribili (contenenti `'0'`, `'E'` o `'U'`) a 0, mentre le altre rimangono come muri (valore 1).
  - Estrae le coordinate degli ingressi e delle uscite, salvandole in liste separate.

### Ricerca del Percorso con l'Algoritmo di Dijkstra
- **Funzione:** `solve_maze_with_custom_entrance(maze, start, end)`
- **Descrizione:**  
  - Utilizza una coda di priorità (tramite `heapq`) per esplorare le celle del labirinto, calcolando il percorso più breve in termini di numero di passi.
  - Mantiene due dizionari, `cost_so_far` per i costi minimi e `came_from` per la ricostruzione del percorso.
  - Se viene trovato un percorso valido, esso viene ricostruito partendo dall'uscita fino all'ingresso e successivamente invertito.

### Calcolo di Tutti i Percorsi Possibili
- **Funzione:** `solve_all_paths(maze, starts, ends)`
- **Descrizione:**  
  - Per ogni combinazione ingresso/uscita, calcola il percorso (se esistente) utilizzando la funzione di Dijkstra.
  - Raccoglie informazioni quali la lunghezza del percorso, il percorso stesso (lista di coordinate) e il tempo di esecuzione per ogni calcolo.
  - Organizza i risultati in una lista per la successiva creazione di un DataFrame e in una struttura gerarchica (dizionario annidato) per una visualizzazione strutturata dei dati.

### Visualizzazione del Labirinto e del Percorso
- **Funzione:** `plot_maze_solution(maze, best_path, start_positions, end_positions)`
- **Descrizione:**  
  - Visualizza il labirinto tramite `matplotlib`, evidenziando:
    - Il percorso migliore (in rosso).
    - Gli ingressi (con marker blu).
    - Le uscite (con marker verde).
  - Imposta una legenda e rimuove la visualizzazione degli assi per una presentazione chiara.

### Flusso Principale di Esecuzione
- **Funzione:** `main()`
- **Descrizione:**  
  1. **Lettura del File Excel:**  
     Il file viene caricato in un DataFrame, assicurandosi che le stringhe (come `'E'` e `'U'`) siano correttamente interpretate.
  2. **Parsing del Labirinto:**  
     Conversione del DataFrame in una matrice numerica e identificazione degli ingressi e delle uscite.
  3. **Verifica dei Vincoli:**  
     L'esecuzione si interrompe se non sono presenti almeno un ingresso e una uscita.
  4. **Calcolo dei Percorsi:**  
     Per ogni coppia ingresso/uscita, viene calcolato il percorso e raccolte statistiche dettagliate.
  5. **Visualizzazione dei Risultati:**  
     Viene creato un DataFrame ordinato in base alla lunghezza del percorso, stampate statistiche e classificazioni gerarchiche, e infine il labirinto viene visualizzato con il percorso ottimale evidenziato.

## Istruzioni per l'Uso

### Requisiti
- **Ambiente:** Python 3.x
- **Librerie:**  
  - NumPy  
  - Pandas  
  - Matplotlib  
  - heapq (incluso in Python standard)  
  - collections (incluso in Python standard)  
  - time (incluso in Python standard)

### Procedura
1. **Verifica della presenza del file Excel:**  
   Assicurarsi che il file **"Labirinto Dijkstra.xlsx"** si trovi nella directory principale del repository.
2. **Esecuzione del Codice:**  
   - Avviare il Notebook Jupyter `Algoritmo di Dijkstra.ipynb` oppure eseguire il file Python direttamente da un ambiente di sviluppo.
   - Il programma elaborerà il file Excel, calcolerà tutti i percorsi possibili tra ogni ingresso e uscita e visualizzerà il labirinto con il percorso migliore evidenziato.
3. **Analisi dei Risultati:**  
   I risultati verranno mostrati sia in forma tabellare (utilizzando un DataFrame) che grafica, evidenziando le statistiche dei percorsi e la classificazione gerarchica delle soluzioni.

## Possibili Miglioramenti
- **Gestione della Legenda:**  
  Ottimizzare la visualizzazione della legenda per evitare duplicazioni nel caso di multipli ingressi o uscite.
- **Algoritmi Alternativi:**  
  Valutare l'impiego di un algoritmo di ricerca in ampiezza (BFS), dato che i costi di ciascun passo sono uniformi.
- **Adattamento ad Ambienti Non Interattivi:**  
  Modificare le funzioni di visualizzazione per rendere il codice compatibile anche con ambienti non interattivi.

## Conclusioni
Il repository illustra un approccio strutturato e modulare per la risoluzione di labirinti con ingressi e uscite multipli, integrando tecniche efficienti di path-finding con una chiara rappresentazione visiva e un'analisi statistica approfondita. Tale implementazione è particolarmente indicata per applicazioni di problem solving e visualizzazione grafica in contesti didattici e di ricerca.

