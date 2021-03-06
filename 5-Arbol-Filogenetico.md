Arbol Filogenetico
================

## Construccion del Arbol Filogenetico

Qiime2 soporte diversas metricas de diversidad, sin embargo; para su
generacion Qiime2 necesita, aparte de una FeatureTable\[Frecuency\], un
arbol filogenetico con raiz que relacione cada uno de los features, esta
informacion sera almacenada en un artefacto Phylogeny\[Rooted\]

Para esto, el comando utiliza \> mafft \< para realizar un alineamiento
multiple de las secuencias encontradas en nuestro artefacto
FeatureData\[Sequence\] para crear un artefacto de tipo
FeatureData\[AlignedSequence\], a continuacion enmascara (o filtra) la
alineacion para remover posiciones que sean altamente variables (se
considera añaden ruido) seguido de esto se aplica \> FastTree \< para
generar el arbol filogenetico a partir del masked alignment, sin embargo
este programa genera un arbol sin raiz, por lo cual el algoritmo coloca
la raiz del arbol en un punto medio entre las dos distancias mas lejanas
entre si.

    qiime phylogeny align-to-tree-mafft-fasttree \
    --i-sequences rep-seqs.qza \
    --o-alignment aligned-rep-seqs.qza \
    --o-masked-alignment masked-aligned-rep-seqs.qza \
    --o-tree unrooted-tree.qza \
    --o-rooted-tree rooted-tree.qza

**Outputs / Tipo de Artefacto**

  - Aligned-rep-seqs.qza ——–\> FeatureData\[AlignedSequence\]
  - masked-aligned-rep-seqs.qza -\> FeatureData\[AlignedSequence\]
  - rooted-tree.qza ————-\> Phylogeny\[Unrooted\]
  - unrooted-tree.qza ———–\> Phylogeny\[Rooted\]
