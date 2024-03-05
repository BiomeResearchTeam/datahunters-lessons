---
type: slides
---

# Let's manipulate the Dataframe: COLONNE NON SEMPRE PRESENTI

Quindi ritorniamo a dove eravamo rimasti nella cura del nostro progetto ERP020892.
Attualmente ci troviamo nella fase di cura delle 7 colonne che potrebbero non essere presenti. Ti ricordo che innanzitutto dobbiamo cercare se queste colonne sono presenti! Se una colonna è presente, procediamo con la verifica dell'informazione contenuta, assicurandoci che coincida con quanto abbiamo trovato nel paper che abbiamo letto. Se la colonna è assente, allora dobbiamo crearla.

Supponiamo di voler cercare se nel nostro DataFrame df esiste una colonna "body_site" che contenga l'informazione "Hands", cioè il sito di campionamento del microbioma (questa informazione è inventata per l'esempio).

```python
#riscriviamo i passaggi già visti in precedenza:
colonne = df.columns.to_list()

colonne_trovate = []

for colonna in colonne:
    if "Hands".lower() in colonna.lower():
        colonne_trovate.append(colonna)
    else:
        pass

#a questo punto possiamo misurare la lunghezza della lista colonne_trovate: se la lunghezza è maggiore di 0 
#significa che è stata trovata almeno una colonna che contiene l'informazione che stiamo cercando!
#per calcolare la lunghezza di una lista usiamo la funzione len()
if len(colonne_trovate)>0:
    #ora possiamo iterare tra le colonne trovate e visualizzare quali valori unici contiene. Questa fase è cruciale per comprendere se l'informazione ricercata, come ad esempio "Hands", è contenuta in una colonna dedicata al body_site oppure se è mescolata con altre informazioni. In quest'ultimo caso dovremo noi creare la colonna specifica per il body_site che ti ricordo essere "SKIOME_body_site"
    for colonna in colonne_trovate:
        print(colonna, df[colonna].unique())
else:
    print("nessuna colonna trovata!")

```

```out
nessuna colonna trovata!
```

Non è stata trovata nessuna colonna che contenesse l'informazione del body_site, e quindi creiamo la colonna nuova!

```python
df["SKIOME_body_site"] = "hands"
```

Notes: Ecco la parte più complicata del workshop: verificare che le 7 colonne siano presenti nei metadati, ed eventualmente se l'informazione che contengono sia giusta. Ti faccio notare che in questa slide hai scoperto l'ultima fondamentale per il workshop: `len()`. `len()` è una funzione built-in, che restituisce la lunghezza di un oggetto, come nel nostro caso una lista. 

Cosa abbiamo fatto in questa slide? Abbiamo controllato se la lista `colonne_trovate` contenesse almeno un elemento, cioè almeno il nome di una colonna. Se la lista ha una lunghezza maggiore di 0, allora per ogni `colonna` presente in `colonne_trovate` avrebbe stampato il nome della `colonna` e i valori unici contenuti in quella `colonna`. Avremmo quindi potuto così determinare se esistesse una colonna specifica per il "body_site". (Ah, ti ricordo che se esiste una colonna specifica per il "body_site" e il valore contenuto è corretto, non devi intervenire; altrimenti, se il valore è scorretto, devi creare una nuova colonna con il contenuto corretto). Se invece, come nel nostro caso, la lista `colonne_trovate` è vuota, allora viene eseguito il comando dopo `else:`: stampa la frase "nessuna colonna trovata!". A questo punto non ti resta che creare una nuova colonna contenente quell'informazione.

---

# Let's manipulate the Dataframe: COLONNE NON SEMPRE PRESENTI

Supponiamo di cercare se esiste la colonna "target_region", cercando il valore "V3-V4" che abbiamo trovato nel paper (questa informazione è inventata per l'esempio).

```python
#riscriviamo i passaggi già visti in precedenza:
colonne = df.columns.to_list()

colonne_trovate = []

for colonna in colonne:
    if "V3-V4".lower() in colonna.lower():
        colonne_trovate.append(colonna)
    else:
        pass

if len(colonne_trovate)>0:
    for colonna in colonne_trovate:
        print(colonna, df[colonna].unique())
else:
    print("nessuna colonna trovata!")

```

```out
sample_alias, skin microbiome sample V3-V4 Italy
run_title, A Comprehensive Study on the Facial Microbial Landscape with a Focus on the V3-V4 Region in Italian Elderly
```

Non è stata trovata nessuna colonna specifica che contenesse l'informazione della target_region, e quindi creiamo la colonna nuova!

```python
df["SKIOME_target_region"] = "V3-V4"
```

Notes: In questo caso abbiamo cercato se esistesse un'altra delle 7 colonne: target_region. Quindi abbiamo creato la lista `colonne_trovate` che contiene il nome delle colonne in cui il valore "V3-V4" è stato trovato. Quando abbiamo eseguito il comando `if len(colonne_trovate)>0`, la condizione era vera e quindi è stato eseguito il comando:
`for colonna in colonne_trovate:
    print(colonna, df[colonna].unique())`

Come puoi osservare, l'output fornisce il nome della colonna in cui è stato individuato "V3-V4" e il valore unico presente in quella colonna. In entrambe le colonne, puoi notare che il valore "V3-V4" è mescolato con altre informazioni, da cui possiamo dedurre l'assenza di una colonna specifica denominata "target_region". Perfetto! Allora dobbiamo crearla!

---

# Let's code!
