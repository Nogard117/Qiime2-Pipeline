Utilidades
================

## Asociar FeatureData\[Sequences\] con Taxonomy.qza

Podemos asociar la tabla FeatureData\[Sequences\] (secuencias
representativas) con el artefacto de taxonomia para optener una
tabulacion que nos muestre la secuencia en formato FASTA, el taxa
asociado y el % confidencia lo cual nos permite compararlo con un solo
click con la base de datos del NCBI

    qiime metadata tabulate
    --m-input-file taxonomy.qza
    --m-input-file rep-seqs.qza
    --o-visualization merged-table.qzv

## Generar abundancias relativas por nivel taxonomivo

Probablemente querramos generar una tabla con las abundancias relativas
por nivel taxonomico para para poder trabajar con dichos datos mas
adelante, iniciaremos colapsando nuestra FeatureData:

    qiime taxa collapse \
    --i-table feature-table.qza \        -> FeatureData[Frecuency]
    --i-taxonomy taxonomy.qza \          -> Output del proceso de clasificacion
    --p-level # \                        -> En SILVA los niveles van del 1 al 7.
    --o-collapsed-table phyla-table.qza 

Ahora convertiremos estas nuevas tablas de frecuencias en tablas de
frecuencias relativas

    qiime feature-table relative-frequency \
    --i-table phyla-table.qza \
    --o-realtive-frequency-table rel-phyla-table.qza

Este nuevo artefacto contiene nuestras frecuencias relativas, para
tenerlo en formato de texto lo expotaremos al formato .biom (el cual es
aceptado por R y Phyloseq):

    qiime tools export \
    --input-path rel-phyla-table.qza \
    --output-path relative              -> esto creara una nueva carpeta llamada relative y alli dejara el archivo

Ya convertido a formato .biom, lo convertiremos a formato de texto o CVS
(Excell) la nueva tabla .biom sera renombrada a feature-table.biom por
lo cual aconsejo renombrarla para tener mayor claridad  
Posteriormente convertiremos el archivo .biom a formato de texto de esta
manera:

    biom convert -i feature-table.biom -o rel-phyla-table.tsv --to-tsv
