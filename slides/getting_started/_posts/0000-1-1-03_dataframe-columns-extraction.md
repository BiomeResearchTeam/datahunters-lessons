---
type: slides
---

# Let's manipulate the Dataframe: column extraction

Eravamo rimasti alla nostra lista di colonne. Benissimo, e se volessimo selezionare una delle colonne del df per vederne il contenuto? Scegliamo per esempio la colonna `DOI` che contiene il link per il paper, che dovrai leggere per curare i metadati.

```python
print(lista_colonne)
```

```out
['study_accession', 'secondary_study_accession', 'sample_accession', 'secondary_sample_accession', 'experiment_accession', 'run_accession', 'submission_accession', 'tax_id', 'scientific_name_exp', 'instrument_platform', 'instrument_model_x', 'library_name_x', 'library_layout_x', 'library_strategy_x', 'library_source_x', 'library_selection_x', 'read_count', 'base_count', 'center_name_exp', 'first_public', 'last_updated', 'experiment_title_x', 'study_title_x', 'study_alias_x', 'experiment_alias_x', 'run_alias_x', 'fastq_bytes', 'fastq_md5', 'fastq_ftp', 'fastq_aspera', 'fastq_galaxy', 'sra_bytes', 'sra_md5', 'sra_ftp', 'sra_aspera', 'sra_galaxy', 'sample_alias_x', 'sample_title_x', 'first_created', 'center_name_sam', 'PRIMARY_ID', 'EXTERNAL_ID', 'SUBMITTER_ID', 'TITLE', 'TAXON_ID', 'SCIENTIFIC_NAME', 'ENA-FASTQ-FILES', 'ENA-SUBMITTED-FILES', 'organism', 'ENA-FIRST-PUBLIC_x', 'ENA-LAST-UPDATE_x', 'DESCRIPTION', 'submitted_bytes', 'submitted_md5', 'submitted_ftp', 'submitted_aspera', 'submitted_galaxy', 'submitted_format', 'ENA-CHECKLIST', 'host scientific name_x', 'latitude_x', 'physical_specimen_location_x', 'collection_timestamp_x', 'env_material_x', 'longitude_x', 'elevation_x', 'dna_extracted_x', 'physical_specimen_remaining_x', 'host subject id_x', 'sample type_x', 'DOI_left', 'body product_x', 'env biome_x', 'env feature_x', 'host taxid_x', 'body site_x', 'host common name', 'body habitat_x', 'public_x', 'anonymized name_x', 'env package_x', 'sample location', 'updated_date', 'spots.x', 'bases.x', 'experiment_ID', 'experiment', 'sample_ID_y', 'sample', 'study_ID', 'study', 'submission_ID', 'submission', 'sradb_updated', 'ReleaseDate', 'LoadDate', 'spots.y', 'bases.y', 'spots_with_mates', 'avgLength', 'size_MB', 'download_path', 'Experiment', 'LibraryName', 'LibraryStrategy', 'LibrarySelection', 'LibrarySource', 'LibraryLayout', 'InsertSize', 'InsertDev', 'Platform', 'Model', 'SRAStudy', 'BioProject', 'ProjectID', 'Sample', 'BioSample', 'SampleType_y', 'TaxID', 'ScientificName', 'SampleName', 'Tumor', 'CenterName', 'Submission', 'Consent', 'RunHash', 'ReadHash', 'Year_of_release', 'DOI', 'run_alias_y', 'experiment_alias_y', 'experiment_title_y', 'library_name_y', 'library_strategy_y', 'library_source_y', 'library_selection_y', 'library_layout_y', 'library_construction_protocol', 'platform', 'instrument_model_y', 'platform_parameters', 'sample_alias_y', 'taxon_id', 'description', 'study_alias_y', 'study_title_y', 'study_type', 'study_abstract', 'center_project_name_y', 'submission_lab', 'env_biome_y', 'env_feature_y', 'env_material_y', 'run_attribute', 'ENA-FIRST-PUBLIC_y', 'ENA-LAST-UPDATE_y', 'host_subject_id_y', 'design_description', 'env_package_y', 'Body_Site_y', 'body_site_y', 'run_date', 'run_center', 'anonymized_name', 'pcr_primers', 'sequencing_meth', 'target_gene', 'target_subfragment', 'body_habitat', 'body_product', 'elevation_y', 'host_common_name_y', 'host_taxid_y', 'latitude_y', 'longitude_y', 'title', 'experiment_center', 'samp_size_y', 'sample_center', 'illumina_technology_y', 'sample_type_y', 'public_y', 'host scientific name_y', 'barcode_y', 'center_name', 'linker', 'primer', 'run_prefix', 'collection_timestamp_y', 'dna_extracted_y', 'physical_specimen_location_y', 'physical_specimen_remaining_y', 'sample_location']
```
```python
colonna_paper = df['DOI']
print(colonna_paper)
```
```out
0    https://doi.org/10.1038/ismej.2012.8
1    https://doi.org/10.1038/ismej.2012.8
2    https://doi.org/10.1038/ismej.2012.8
3    https://doi.org/10.1038/ismej.2012.8
4    https://doi.org/10.1038/ismej.2012.8
5    https://doi.org/10.1038/ismej.2012.8
Name: DOI, dtype: object
```

Notes: Grazie alla `lista_colonne`, abbiamo potuto verificare la presenza della colonna DOI nel nostro DataFrame. Per selezionare questa colonna, dobbiamo abbandonare la `lista_colonne` e tornare a lavorare direttamente sul DataFrame (`df`). Per estrarre una colonna da un DataFrame, è sufficiente richiamare il DataFrame, nel nostro caso `df`, seguito da parentesi quadre (`[]`), all'interno delle quali dobbiamo indicare il nome della colonna desiderata tra virgolette, come ad esempio `["DOI"]`. Abbiamo utilizzato la funzione `print()` per visualizzare il contenuto della colonna. Dal momento che il nostro DataFrame è composto solo da 6 righe, vediamo ripetuto sei volte il dato `https://doi.org/10.1038/ismej.2012.8`.

---

# Let's manipulate the Dataframe: column extraction

E se volessimo estrarre solo i valori unici di una colonna? Senza vedere i valori duplicati?

```python
colonna_paper = df['DOI']
print(colonna_paper)
```
```out
0    https://doi.org/10.1038/ismej.2012.8
1    https://doi.org/10.1038/ismej.2012.8
2    https://doi.org/10.1038/ismej.2012.8
3    https://doi.org/10.1038/ismej.2012.8
4    https://doi.org/10.1038/ismej.2012.8
5    https://doi.org/10.1038/ismej.2012.8
Name: DOI, dtype: object
```
```python
colonna_paper_unici = colonna_paper.unique()
print(colonna_paper_unici)
```
```out
['https://doi.org/10.1038/ismej.2012.8']
```

Notes: Ed ecco un altro metodo molto importante: `.unique()`. Questo metodo permette di ottenere i valori unici contenuti in un insieme di dati, come ad esempio una colonna! Usando `colonna_paper_unici = df["DOI"].unique()` potrai recuperare il link da cliccare per leggere il paper relativo a questo progetto!

---

# Let's code!
