# Let's manipulate the Dataframe: column extraction & check info

OK, passiamo al cuore dell'attività del workshop: avete trovato le informazioni nel paper e ora volete curare i metadati di quel progetto. Le colonne che dovrete curare per ogni progetto sono 9:

* "library_strategy": la strategia di sequenziamento (AMPLICON, WGS)
* "instrument_platform": la piattaforma di sequenziamento (ILLUMINA, ION TORRENT, ...)
* "instrument_model": modello di sequenziatore (ILLUMINA MiSeq, ILLUMINA NovaSeq, ...)
* "SKIOME_amplicon_target": amplicone targettato (16S, ITS, ...)
* "SKIOME_target_region": regione ipervariabile dell amplicone (V1, V3-V4, ...)
* "SKIOME_primer": primer (515: GTGCCAGCMGCCGCGGTAA, 805: GGACTACNVGGGTWTCTAAT, ...)
* "SKIOME_individuals_nationality": nazionalità degli individui campionati (Italy, Spain, ...)
* "SKIOME_body_site": sito del corpo campionato (hands, forehead, ...)
* "SKIOME_status": condizione o stato che si attribuisce ai soggetti campionati in base alle diverse ipotesi considerate (healthy vs disease, rural vs urban, ...)

Le prime 3 colonne ("library_strategy", "instrument_platform", "instrument_model") sono **sempre** presenti nei metadati che andrete a curare, mentre le altre 7 potrebbero essere presenti o meno. Di conseguenza, ci sono due strade che dovrete percorrere:

* Per le **COLONNE SEMPRE PRESENTI** ("library_strategy", "instrument_platform", "instrument_model") dovrete verificare che i valori contenuti in queste colonne coincidano con quelli trovati nel paper. Se corrispono, ottimo! non dovete fare nulla e potete passare alla prossima colonna. Se, invece, i valori nelle colonne sono diversi da quelli che avete trovato nel paper allora dovete modificarli.

* Per le **COLONNE POTENZIALMENTE ASSENTI** dovete innanzitutto verificare se la colonna esiste:
    * Se **ESISTE**, comportatevi come nel caso delle colonne sempre presenti: controllate che il valore contenuto sia lo stesso di quello nel paper. Se i valori coincidono, non è necessario apportare modifiche e potete passare alla prossima colonna. Se i valori sono diversi, dovrete procedere con la correzione.
    * Se **NON ESISTE** allora è necessario crearne una nuova e assegnarle il valore trovato nel paper.
              
---

# Let's manipulate the Dataframe: COLONNE SEMPRE PRESENTI

Verifichiamo che il valore delle tre colonne sempre presenti sia quello che hai trovato nel paper! Partiamo dalla colonna `library_strategy` e poi ripetiamo gli stessi comandi per tutte e 3 le colonne sempre presenti.

```python
strategia = df["library_strategy"].unique()
print(strategia)
```

```out
['AMPLICON']
```

Per verificare che il valore presente nella colonna da curare sempre presente sia lo stesso trovato nel paper, basta sfruttare quello che hai imparato finora! Quindi abbiamo estratto il valore unico dalla colonna `library_strategy` e l'abbiamo stampato. TA-DAAN: `AMPLICON`. Il valore trovato è corrisponde con quello che abbiamo letto nel paper e quindi possiamo procedere con un'altra colonna.

---

# Let's manipulate the Dataframe: COLONNE SEMPRE PRESENTI

Verifichiamo ora il valore contenuto dalla colonna `instrument_platform`!

```python
piattaforma = df["instrument_platform"].unique()
print(piattaforma)
```

```out
["VALORE SBAGLIATO"]
```

```python
df["SKIOME_instrument_platform"] = "AMPLICON"
```

```out
["AMPLICON"]
```

Supponiamo che, durante la verifica di questa colonna, abbiamo riscontrato un valore diverso da quello dichiarato nel paper. Niente di più semplice: dobbiamo creare una nuova colonna contenente il valore corretto. Per fare ciò, dobbiamo specificare il nome del DataFrame (`df`) seguito dalle parentesi quadre (`[]`), all'interno delle quali indichiamo il nome della nuova colonna. Quando crei una nuova colonna, segui il nome suggerito nella lista iniziale delle colonne da curare. Nota che, se stai curando quella particolare colonna, devi aggiungere come prefisso "SKIOME_". Questo aiuterà chi utilizzerà la raccolta a capire che la colonna è stata curata!


# Let's manipulate the Dataframe: COLONNE SEMPRE PRESENTI

Non c'è regola senza eccezioni... Può capitare che non esista una delle tre colonne che ti abbiamo detto essere sempre presenti! E allora che fare? Semplice, crea una nuova colonna e assegna il valore che hai trivato nel paper:

```python
modello = df_senza_colonne_vuote["instrument_model"].unique()
print(modello)
```

```out
---------------------------------------------------------------------------
KeyError                                  Traceback (most recent call last)
File ~/miniconda3/envs/jupyter/lib/python3.12/site-packages/pandas/core/indexes/base.py:3790, in Index.get_loc(self, key)
   3789 try:
-> 3790     return self._engine.get_loc(casted_key)
   3791 except KeyError as err:

File index.pyx:152, in pandas._libs.index.IndexEngine.get_loc()

File index.pyx:181, in pandas._libs.index.IndexEngine.get_loc()

File pandas/_libs/hashtable_class_helper.pxi:7080, in pandas._libs.hashtable.PyObjectHashTable.get_item()

File pandas/_libs/hashtable_class_helper.pxi:7088, in pandas._libs.hashtable.PyObjectHashTable.get_item()

KeyError: 'instrument_model'

The above exception was the direct cause of the following exception:

KeyError                                  Traceback (most recent call last)
Cell In[16], line 1
----> 1 modello = df["instrument_model"].unique()
      2 print(modello)

File ~/miniconda3/envs/jupyter/lib/python3.12/site-packages/pandas/core/frame.py:3893, in DataFrame.__getitem__(self, key)
   3891 if self.columns.nlevels > 1:
   3892     return self._getitem_multilevel(key)
-> 3893 indexer = self.columns.get_loc(key)
   3894 if is_integer(indexer):
   3895     indexer = [indexer]

File ~/miniconda3/envs/jupyter/lib/python3.12/site-packages/pandas/core/indexes/base.py:3797, in Index.get_loc(self, key)
   3792     if isinstance(casted_key, slice) or (
   3793         isinstance(casted_key, abc.Iterable)
   3794         and any(isinstance(x, slice) for x in casted_key)
   3795     ):
   3796         raise InvalidIndexError(key)
-> 3797     raise KeyError(key) from err
   3798 except TypeError:
   3799     # If we have a listlike key, _check_indexing_error will raise
   3800     #  InvalidIndexError. Otherwise we fall through and re-raise
   3801     #  the TypeError.
   3802     self._check_indexing_error(key)

KeyError: 'instrument_model'
```

```python
df["SKIOME_instrument_model"] = "Illumina HiSeq 2000"
```

```out
['Illumina HiSeq 2000']
```

Oh-oh! Hai tentato di estrarre il valore dalla colonna `instrument_model` e hai ottenuto una serie di errori. Non preoccuparti, l'errore è dovuto al fatto che questa colonna è assente nei metadati. Nessun problema se la colonna non esiste: puoi crearla! Hai già le competenze necessarie per farlo.

---

# Let's code!
