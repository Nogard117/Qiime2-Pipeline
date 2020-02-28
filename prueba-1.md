1 Importar Archivos
================

## Importando archivos a Qiime2

Estas notas hacen referencia al importe de secuencias PAIRED END por
medio de la opcion de manifiesto.  
Manifest nos permite importar archivos que carezcan de metadatos y/o un
archivo de barcodes, por lo cual es necesaria la elaboracion del archivo
manifiesto que contendra el ID de nuestras secuencias y la direccion de
su ubicacion, en formato de texto .tsv.

## Including Code

You can include R code in the document as follows:

    qiime tools import
    --type 'SampleData[PairedEndSequencesWithQuality]'

## Including Plots

You can also embed plots, for example:

``` 
```

Note that the `echo = FALSE` parameter was added to the code chunk to
prevent printing of the R code that generated the plot.
