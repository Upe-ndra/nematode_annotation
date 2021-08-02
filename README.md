# nematode_annotation
Annotation of nematode genome using maker pipeline following a pipeline described [here](https://bioinformaticsworkbook.org/dataAnalysis/GenomeAnnotation/Intro_To_Maker.html#gsc.tab=0)

### Downloading wormbase data
Downloaded all the proteins and transcript sequences from wormbase database on (2021-06-04) for all the related species in dorylamiadaa
  
Clade I wormbase database
  
- Romanomermis culicivorax
- Soboliphyme baturini
- Trichinella britovi
- Trichinella murrelli
- Trichinella nativa
- Trichinella nativa
- Trichinella nelsoni
- Trichinella papuae
- Trichinella patagoniensis
- Trichinella pseudospiralis
- Trichinella pseudospiralis
- Trichinella pseudospiralis
- Trichinella pseudospiralis
- Trichinella pseudospiralis
- Trichinella spiralis
- Trichinella spiralis
- Trichinella sp. T6
- Trichinella sp. T8
- Trichinella sp. T9
- Trichinella zimbabwensis
- Trichuris muris
- Trichuris suis
- Trichuris suis
- Trichuris suis
- Trichuris trichiura

Concatenate all the protein sequences into one and transcript sequences into another fasta file

```
cat *all.proteins.fasta >> dorylaimia.wormbase.protein.fasta
cat *all.transcript.fasta >> dorylaimia.wormbase.trascripts.fasta
```
### Downloading the database available in uniprot database

Downloaded on (2021-06-04)

- uniprot-mermis+nigrescens.fasta
- uniprot-Romanomermis+culicivorax.fasta
- uniprot-Soboliphyme+baturini.fasta
- uniprot-Trichinella+britovi.fasta
- uniprot-Trichinella+murrelli.fasta
- uniprot-Trichinella+nativa.fasta
- uniprot-Trichinella+nelsoni.fasta
- uniprot-Trichinella+papuae.fasta
- uniprot-Trichinella+patagoniensis.fasta
- uniprot-Trichinella+pseudospiralis.fasta
- uniprot-Trichinella+spiralis.fasta
- uniprot-trichinella+sp+t6.fasta
- uniprot-trichinella+sp+t8.fasta
- uniprot-Trichinella+sp.+T9.fasta
- uniprot-Trichinella+zimbabwensis.fasta
- uniprot-Trichuris+muris.fasta
- uniprot-Trichuris+suis.fasta
- uniprot-Trichuris+trichiura.fasta


### Downloading the database available in ncbi

Downloaded all the protein and transcriptome database 
  
Transcriptome data on (2021-06-04)
  
- mermis_nigrescens_mRNA_ncbi.fasta
- Trichinella_britovi_mRNA_ncbi.fasta
- Trichinella_murrelli_mRNA_ncbi.fasta
- Trichinella_nativa_mRNA_ncbi.fasta
- Trichinella_nelsoni_mRNA_ncbi.fasta
- Trichinella_papuae_mRNA_ncbi.fasta
- Trichinella_pseudospiralis_mRNA_ncbi.fasta
- Trichinella_spiralis_mRNA_ncbi.fasta
- Trichinella_sp_T6_mRNA_ncbi.fasta
- Trichinella_sp_T8_mRNA_ncbi.fasta
- Trichinella_sp_T9_mRNA_ncbi.fasta
- Trichuris_muris_mRNA_ncbi.fasta
- Trichuris_suis_mRNA_ncbi.fasta
- Trichuris_trichiura_mRNA_ncbi.fasta

Concatenate all these into one file
```
cat *_mRNA_ncbi.fasta >> dorylaimia_mRNA_ncbi.fasta
```
Protein data on (2021-06-04)
  
- Mermis_nigrescens_protein_ncbi.fasta
- Romanomermis_culicivorax_protein_ncbi.fasta
- Soboliphyme_baturini_protein_ncbi.fasta
- Trichinella_britovi_protein_ncbi.fasta
- Trichinella_murrelli_protein_ncbi.fasta
- Trichinella_nativa_protein_ncbi.fasta
- Trichinella_nelsoni_protein_ncbi.fasta
- Trichinella_papuae_protein_ncbi.fasta
- Trichinella_patagoniensis_protein_ncbi.fasta
- Trichinella_pseudospiralis_protein_ncbi.fasta
- Trichinella_spiralis_protein_ncbi.fasta
- Trichinella_sp_T6_protein_ncbi.fasta
- Trichinella_sp_T8_protein_ncbi.fasta
- Trichinella_sp_T9_protein_ncbi.fasta
- Trichinella_zimbabwensis_protein_ncbi.fasta
- Trichuris_muris_protein_ncbi.fasta
- Trichuris_suis_protein_ncbi.fasta
- Trichuris_trichiura_protein_ncbi.fasta

Concatenate all these into one file
```
cat *_protein_ncbi.fasta >> dorylaimia_protein_ncbi.fasta
```

Installing cdbfasta
```
git clone https://github.com/gpertea/cdbfasta.git
cd cdbfasta
make
```

Separating Mermis nigrescens and non-Mermis nigrescens transcriptome dataset downloaded from NCBI
```
# Indexing files with cdbfasta
path_to_cdbfasta_folder/cdbfasta dorylaimia_mRNA_ncbi.fasta

# seperating Mermis nigrescens's and non-Mermis nigrescens's reads from transcriptome
grep "nigrescens" dorylaimia_mRNA_ncbi.fasta | sed 's/>//g'| path_to_cdbfasta_folder/cdbyank dorylaimia_mRNA_ncbi.fasta.cidx > Mermis.nigrescens_mRNA_ncbi.fasta
grep -v "nigrescens" dorylaimia_mRNA_ncbi.fasta | sed 's/>//g'| path_to_cdbfasta_folder/cdbyank dorylaimia_mRNA_ncbi.fasta.cidx > Not.Mermis.nigrescens_mRNA_ncbi.fasta
```
Now concatenate `Not.Mermis.nigrescens_mRNA_ncbi.fasta` with transcriptome data downloaded from wormbase `dorylaimia.wormbase.trascripts.fasta`
```
cat dorylaimia.wormbase.transcripts.fasta Not.Mermis.nigrescens_mRNA_ncbi.fasta > Dorylaimia.EST.Not.M.nigrescens.fasta
```
This file `Dorylaimia.EST.Not.M.nigrescens.fasta` will go to "altest_pass" category in maker configuration file
File produced above `Mermis.nigrescens_mRNA_ncbi.fasta` will go to "est_pass" category in maker configuration file
Now concatenate all the protein datasets into one and will go into "protein_pass" category in maker configuration file


