DADA2
================

## Joining, Denoising y Remocion de Quimeras con DADA2

Se utiliza el plugin DADA2 el cual corta, une, filtra y genera ASVs de
nuestras secuencias.

    qiime dada2 denoise-paired \
    --i-demultiplexed-seqs dirección sequences.qza \
    --p-trim-left-f # \     (número de bases a eliminar del inicio de la seq)
    --p-trim-left-r # \
    --p-trunc-len-f # \     (tamaño deseado de la secuencia forward y reverse)
    --p-trunc-len-r # \
    --o-table table.qza \
    --o-representative-sequences rep-seqs.qza \
    --o-denoising-stats denoising-stats.qza \

Esto nos generara 3 archivos output:

  - table.qza -\> FeatureTable\[Frecuency\]
  - rep-seqs.qza -\> FeatureData\[Sequence\]
  - denois-stats.qza -\> SampleData\[DADA2Stats\]

Para observar los resultados deben generarse los archivos .qzv
correspondientes:

    qiime feature-table summarize \
    --i-table table.qza \
    --o-visualization table.qzv \
    --m-sample-metadata-file metadata.tsv     (opcional)
    
    qiime feature-table tabulate-seqs \
    --i-data rep-seqs.qza \
    --o-visualization rep-seqs.qzv
    
    qiime metadata tabulate \
    --m-input-file denois-stats.qza \
    --o-visualization denoising-stats.qzv

*Outputs*

  - metadata.qzv
  - rep-seqs.qzv
  - denoising-stats.qzv

Para observar los datos (HTML):

    qiime tools view /archivo.qzv
