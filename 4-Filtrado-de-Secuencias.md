Filtrado
================

## Filtrando las secuencias

Existen varias formas de filtrar nuestras secuencias, las cuales pueden
ser consultadas en la pagina oficial de Qiime2, sin embargo en esta
seccion veremos el filtrado por taxonomia, el cual nos permitira
eliminar (o conservar) los taxones de interes de nuestros archivos
table.qza y rep-seqs.qza

Iniciaremos por filtrar el archivo table.qza

    qiime taxa filter-table
    --i-table table.qza
    --i-taxonomy taxonomy.qza
    --p-exclude mitochondria,chloroplast
    --o-filtered-table filtered-table.qza

Ahora filtraremos el archivo rep-seqs.qza

    qiime taxa filter-seqs
    --i-sequences rep-seqs.qza
    --i-taxonomy taxonomy.qza
    --p-exclude mitochondria,chloroplast
    --o-filtered-sequences filtered-rep-seqs.qza

**Outputs**  
\- filtered-table.qza  
\- filtered-rep-seqs.qza

Posteriormente volveremos a vincular table.qza filtrado con taxonomy.qza
para generar un nuevo barplot libre de las secuencias elegidas.

    qiime taxa barplot \
    --i-table table.qza \  <---- En este caso, volveremos a correr este comando pero con la tabla filtrada.
    --i-taxonomy taxonomy.qza \
    --m-metadata-file sample-metadata.tsv \
    --o-visualization taxa-bar-plot.qzv

PREGUNTA: Seria pertinente realizar de nuevo la clasificacion
taxonomica?
