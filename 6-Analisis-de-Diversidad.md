Análisis de Diversidad
================

## Diversidad Alpha y Beta

Utilizaremos el comando core-metrics-phylogenetic para rareficar nuestra
FeatureTable\[Frecuency\] a cierta profundidad de muestro, a traves de
esto podremos generar y computar diversos indices de diversidad Alpha,
Beta, generar analizis por coordenadas (PCoA) para las metricas beta. Lo
calculado es lo siguiente:

**Alpha diversity**

  - Shannon’s diversity index (a quantitative measure of community
    richness)  
  - Observed OTUs (a qualitative measure of community richness)  
  - Faith’s Phylogenetic Diversity (a qualitiative measure of community
    richness that incorporates phylogenetic relationships between the
    features)  
  - Evenness (or Pielou’s Evenness; a measure of community evenness)

**Beta diversity**

  - Jaccard distance (a qualitative measure of community
    dissimilarity)  
  - Bray-Curtis distance (a quantitative measure of community
    dissimilarity)  
  - unweighted UniFrac distance (a qualitative measure of community
    dissimilarity that incorporates phylogenetic relationships between
    the features)  
  - weighted UniFrac distance (a quantitative measure of community
    dissimilarity that incorporates phylogenetic relationships between
    the features)

Cabe destacar que una parte fundamental de este plugin es la profundiad
de muestreo o –p-sampling-depth un sampling depth exitoso sera aquel que
tenga un valor lo mas alto posible, manteniendo el mayor numero de
muestras. Esto se debe a que puede que ciertas muestras no cumplan con
la profundiad de muestreo especificada y por lo tanto seran desechadas.
Para poder tomar una desicion de manera mas facil puede consultarse el
archivo filtered-table.qzv

    qiime diversity core-metrics-phylogenetic \
    --i-phylogeny rooted-tree.qza \
    --i-table table.qza \
    --p-sampling-depth # \ <- Aquí colocas la profundidad o esfuerzo de muestreo.
    --m-metadata-file sample-metadata.tsv \
    --output-dir core-metrics-results

**Output artifacts:**

  - core-metrics-results/rarefied\_table.qza -\>
    FeatureTable\[Frecuency\]

  - core-metrics-results/faith\_pd\_vector.qza -\>
    SampleData\[AlphaDiversity\]  

  - core-metrics-results/evenness\_vector.qza -\>
    SampleData\[AlphaDiversity\]  

  - core-metrics-results/shannon\_vector.qza -\>
    SampleData\[AlphaDiversity\]  

  - core-metrics-results/observed\_otus\_vector.qza -\>
    SampleData\[AlphaDiversity\]

  - core-metrics-results/unweighted\_unifrac\_distance\_matrix.qza -\>
    DistanceMatrix (‘phylogenetic’)  

  - core-metrics-results/weighted\_unifrac\_distance\_matrix.qza -\>
    DistanceMatrix (‘phylogenetic’)  

  - core-metrics-results/jaccard\_distance\_matrix.qza -\>
    DistanceMatrix (‘phylogenetic’)  

  - core-metrics-results/bray\_curtis\_distance\_matrix.qza -\>
    DistanceMatrix (‘phylogenetic’)

  - core-metrics-results/bray\_curtis\_pcoa\_results.qza -\>
    PCoAResults  

  - core-metrics-results/jaccard\_pcoa\_results.qza -\> PCoAResults  

  - core-metrics-results/weighted\_unifrac\_pcoa\_results.qza -\>
    PCoAResults  

  - core-metrics-results/unweighted\_unifrac\_pcoa\_results.qza -\>
    PCoAResults

**Output visualizations:**

  - core-metrics-results/unweighted\_unifrac\_emperor.qzv  
  - core-metrics-results/jaccard\_emperor.qzv  
  - core-metrics-results/bray\_curtis\_emperor.qzv  
  - core-metrics-results/weighted\_unifrac\_emperor.qzv

**Construccion de los archivos .qzv**

**Este comando se alimenta con: SampleData\[AlphaDiversity\]**

    qiime diversity alpha-group-significance \
    --i-alpha-diversity core-metrics-results/file.qza \
    --m-metadata-file sample-metadata.tsv \
    --o-visualization core-metrics-results/file.qzv

**Este comando se alimenta con: DistanceMatrix (‘phylogenetic’)**

    qiime diversity beta-group-significance \
    --i-distance-matrix core-metrics-results/file.qza \
    --m-metadata-file sample-metadata.tsv \
    --m-metadata-column (en caso de que se requiera especificar una columna) \
    --o-visualization core-metrics-results/file.qzv \
    --p-pairwise

**Este comando se aliementa de: PCoAResults**

    qiime emperor plot \
    --i-pcoa core-metrics-results/file.qza \
    --m-metadata-file sample-metadata.tsv \
    --p-custom-axes manipulacion-del-nombre-de-los-ejes \
    --o-visualization core-metrics-results/file.qzv

**Como interpretar las graficas emperor**  
<https://forum.qiime2.org/t/emperor-for-dummies/13609/2>
