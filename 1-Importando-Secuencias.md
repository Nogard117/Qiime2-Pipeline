Importando Secuencias
================

## Importando archivos a Qiime2

Estas notas hacen referencia al importe de secuencias PAIRED END por
medio de la opcion de manifiesto.  
Manifest nos permite importar sequencias en formato .fastq o .fastq.gz
que carezcan de una tabla de meta datos y/o la informacion de los
barcodes asociados; para ello se elabora un archivo tipo manifiesto con
la extension .tsv o .txt, el cual contendra el ID de nuestras secuencias
y su dirección.

    sample-id forward-absolute-filepath reverse-absolute-filepath
    seq1      /home/user/directory/fileR1.fastq /home/user/directory/fileR2.fastq

Los espacios entre columnas se realizan con la tecla TAB (|\< \>|)

Posteriormente se utilizar’a el comando para importar los datos:

    qiime tools import \
    --type 'SampleData[PairedEndSequencesWithQuality]' \
    --input-path dirección manifest.tsv \
    --output-path sequences.qza \
    --input-format PairedEndFastqManifestPhred33V2

*Outputs - sequences.qza*

Una vez importadas las secuencias, debe generarse el artefacto de
visualizacion .qzv

    qiime demux summarize \
    --i-data sequences.qza \
    --o-visualization sequences.qzv

*Outputs - Sequences.qzv*

Para poder visualizarlo debera utilizarse la pagina Qiime2 View o bien,
el siguiente comando, el cual abrira una version HTML del archivo

    qiime tools view /sequences.qzv
