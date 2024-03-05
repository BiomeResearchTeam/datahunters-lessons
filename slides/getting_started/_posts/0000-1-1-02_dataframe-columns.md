---
type: slides
---

# Let's start manipulating the Dataframe!

Riprendiamo da dove eravamo rimasti:

```python
print(df)
```
```out
 study_accession secondary_study_accession sample_accession  \
0      PRJEB18925                 ERP020892    SAMEA46804918   
1      PRJEB18925                 ERP020892    SAMEA46799668   
2      PRJEB18925                 ERP020892    SAMEA46802668   
3      PRJEB18925                 ERP020892    SAMEA46803418   
4      PRJEB18925                 ERP020892    SAMEA46798918   
5      PRJEB18925                 ERP020892    SAMEA46801168   

  secondary_sample_accession experiment_accession run_accession  \
0                 ERS1500521           ERX1845438    ERR1781715   
1                 ERS1500514           ERX1845431    ERR1781708   
2                 ERS1500518           ERX1845435    ERR1781712   
3                 ERS1500519           ERX1845436    ERR1781713   
4                 ERS1500513           ERX1845430    ERR1781707   
5                 ERS1500516           ERX1845433    ERR1781710   

  submission_accession    tax_id    scientific_name_exp instrument_platform  \
0            ERA787503  539655.0  human skin metagenome            ILLUMINA   
1            ERA787503  539655.0  human skin metagenome            ILLUMINA   
2            ERA787503  539655.0  human skin metagenome            ILLUMINA   
3            ERA787503  539655.0  human skin metagenome            ILLUMINA   
4            ERA787503  539655.0  human skin metagenome            ILLUMINA   
5            ERA787503  539655.0  human skin metagenome            ILLUMINA   

   ...     barcode_y center_name linker               primer       run_prefix  \
0  ...  ACTCAGATACTC        CCME     GT  GTGCCAGCMGCCGCGGTAA  s_6_1_sequences   
1  ...  AGCACGAGCCTA        CCME     GT  GTGCCAGCMGCCGCGGTAA  s_6_1_sequences   
2  ...  AGACGTGCACTG        CCME     GT  GTGCCAGCMGCCGCGGTAA  s_6_1_sequences   
3  ...  ACGGATCGTCAG        CCME     GT  GTGCCAGCMGCCGCGGTAA  s_6_1_sequences   
4  ...  AACTCGTCGATG        CCME     GT  GTGCCAGCMGCCGCGGTAA  s_6_1_sequences   
5  ...  AGCTGACTAGTC        CCME     GT  GTGCCAGCMGCCGCGGTAA  s_6_1_sequences   

  collection_timestamp_y  dna_extracted_y  physical_specimen_location_y  \
0             04/06/2010             True                        UCSDMI   
1             04/06/2010             True                        UCSDMI   
2             04/06/2010             True                        UCSDMI   
3             04/06/2010             True                        UCSDMI   
4             04/06/2010             True                        UCSDMI   
5             04/06/2010             True                        UCSDMI   

  physical_specimen_remaining_y sample_location  
0                         False          UCSDMI  
1                         False          UCSDMI  
2                         False          UCSDMI  
3                         False          UCSDMI  
4                         False          UCSDMI  
5                         False          UCSDMI  

[6 rows x 193 columns]
```

Notes: Ora che hai creato un DataFrame chiamato df, hai la possibilità di richiamarlo quante volte desideri. Tuttavia, quando il DataFrame contiene molte colonne o righe, potrebbe essere complicato esplorarne il contenuto tramite una semplice stampa. Nel nostro caso, con un numero elevato di colonne, vengono mostrate tutt le righe perché il nostro df ha effettivamente solo 6 righe, e solo alcune delle molte colonne del df per rendere più gestibile la visualizzazione.

Nella stampa del DataFrame, puoi notare una barra inversa `\` che indica che le righe stanno continuando a capo nella visualizzazione del print, ma nella realtà dei dati non ci sono interruzioni. Inoltre, puoi vedere dei puntini di sospensione `...`, che indicano che molte colonne sono omesse dalla visualizzazione.

---

# Let's start manipulating the Dataframe: .columns

Iniziamo a indagare questo DataFrame. Per esempio, una prima domanda che possiamo farci è: quali colonne ci sono nei miei metadati?

```python
colonne = df.columns
```

Notes: Per rispondere possiamo usare un metodo già predefinito in Python: `.columns`. Digitando il nome del DataFrame seguito da .columns() otteniamo il nome di tutte le colonne presenti nel DataFrame. Per usare questa informazione è utile creare una variabile, nell'esempio a sinistra abbiamo usato `colonne`, che contenga questa informazione, in modo da utilizzarla in seguito. 

---

# Let's start manipulating the Dataframe: print(colonne)

Vediamo cosa contiene la nostra variabile `colonne`.

```python
print(colonne)
```

```out
Index(['study_accession', 'secondary_study_accession', 'sample_accession',
       'secondary_sample_accession', 'experiment_accession', 'run_accession',
       'submission_accession', 'tax_id', 'scientific_name_exp',
       'instrument_platform',
       ...
       'barcode_y', 'center_name', 'linker', 'primer', 'run_prefix',
       'collection_timestamp_y', 'dna_extracted_y',
       'physical_specimen_location_y', 'physical_specimen_remaining_y',
       'sample_location'],
      dtype='object', length=193)
```

Notes: Visualizziamo le nostre colonne! Per farlo, usiamo la funzione che conosciamo già: `print()`. Come vedi, essendo 193 colonne `(length = 193)`, in questo modo non riusciamo a vedere tutti nomi delle colonne, ma come al solito troviamo i puntini di sospensione `...` che ci indicano che il nome di molte colonne è omesso dalla stampa... Ci servirebbe un modo per stampare tutti i nomi delle colonne...

---

# Let's start manipulating the Dataframe: .to_list()

Rendiamo la nostra variabile `colonne` in una lista e visualizziamola!

```python
lista_colonne = colonne.to_list()
print(lista_colonne)
```

```out
['study_accession', 'secondary_study_accession', 'sample_accession', 'secondary_sample_accession', 'experiment_accession', 'run_accession', 'submission_accession', 'tax_id', 'scientific_name_exp', 'instrument_platform', 'instrument_model_x', 'library_name_x', 'library_layout_x', 'library_strategy_x', 'library_source_x', 'library_selection_x', 'read_count', 'base_count', 'center_name_exp', 'first_public', 'last_updated', 'experiment_title_x', 'study_title_x', 'study_alias_x', 'experiment_alias_x', 'run_alias_x', 'fastq_bytes', 'fastq_md5', 'fastq_ftp', 'fastq_aspera', 'fastq_galaxy', 'sra_bytes', 'sra_md5', 'sra_ftp', 'sra_aspera', 'sra_galaxy', 'sample_alias_x', 'sample_title_x', 'first_created', 'center_name_sam', 'PRIMARY_ID', 'EXTERNAL_ID', 'SUBMITTER_ID', 'TITLE', 'TAXON_ID', 'SCIENTIFIC_NAME', 'ENA-FASTQ-FILES', 'ENA-SUBMITTED-FILES', 'organism', 'ENA-FIRST-PUBLIC_x', 'ENA-LAST-UPDATE_x', 'DESCRIPTION', 'submitted_bytes', 'submitted_md5', 'submitted_ftp', 'submitted_aspera', 'submitted_galaxy', 'submitted_format', 'ENA-CHECKLIST', 'host scientific name_x', 'latitude_x', 'physical_specimen_location_x', 'collection_timestamp_x', 'env_material_x', 'longitude_x', 'elevation_x', 'dna_extracted_x', 'physical_specimen_remaining_x', 'host subject id_x', 'sample type_x', 'DOI_left', 'body product_x', 'env biome_x', 'env feature_x', 'host taxid_x', 'body site_x', 'host common name', 'body habitat_x', 'public_x', 'anonymized name_x', 'env package_x', 'sample location', 'updated_date', 'spots.x', 'bases.x', 'experiment_ID', 'experiment', 'sample_ID_y', 'sample', 'study_ID', 'study', 'submission_ID', 'submission', 'sradb_updated', 'ReleaseDate', 'LoadDate', 'spots.y', 'bases.y', 'spots_with_mates', 'avgLength', 'size_MB', 'download_path', 'Experiment', 'LibraryName', 'LibraryStrategy', 'LibrarySelection', 'LibrarySource', 'LibraryLayout', 'InsertSize', 'InsertDev', 'Platform', 'Model', 'SRAStudy', 'BioProject', 'ProjectID', 'Sample', 'BioSample', 'SampleType_y', 'TaxID', 'ScientificName', 'SampleName', 'Tumor', 'CenterName', 'Submission', 'Consent', 'RunHash', 'ReadHash', 'Year_of_release', 'DOI', 'run_alias_y', 'experiment_alias_y', 'experiment_title_y', 'library_name_y', 'library_strategy_y', 'library_source_y', 'library_selection_y', 'library_layout_y', 'library_construction_protocol', 'platform', 'instrument_model_y', 'platform_parameters', 'sample_alias_y', 'taxon_id', 'description', 'study_alias_y', 'study_title_y', 'study_type', 'study_abstract', 'center_project_name_y', 'submission_lab', 'env_biome_y', 'env_feature_y', 'env_material_y', 'run_attribute', 'ENA-FIRST-PUBLIC_y', 'ENA-LAST-UPDATE_y', 'host_subject_id_y', 'design_description', 'env_package_y', 'Body_Site_y', 'body_site_y', 'run_date', 'run_center', 'anonymized_name', 'pcr_primers', 'sequencing_meth', 'target_gene', 'target_subfragment', 'body_habitat', 'body_product', 'elevation_y', 'host_common_name_y', 'host_taxid_y', 'latitude_y', 'longitude_y', 'title', 'experiment_center', 'samp_size_y', 'sample_center', 'illumina_technology_y', 'sample_type_y', 'public_y', 'host scientific name_y', 'barcode_y', 'center_name', 'linker', 'primer', 'run_prefix', 'collection_timestamp_y', 'dna_extracted_y', 'physical_specimen_location_y', 'physical_specimen_remaining_y', 'sample_location']
```

Notes: Guarda: abbiamo trasformato la nostra variabile `colonne` in una lista usando il metodo `to_list()`, e abbiamo immagazzinato il risultato di questo passaggio in una nuova variabile `lista_colonne`. Visualizzando `lista_colonne` abbiamo come output la lista di tutte e 193 le colonne! 

---

# Let's code!
