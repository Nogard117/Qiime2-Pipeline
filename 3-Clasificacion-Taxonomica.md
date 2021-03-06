Clasificacion taxonomica
================

## Usando el Clasificador

Despues de tratar las secuencias con DADA2, podemos clasificarlas
utilizando una base de datos, como Green Genes o SILVA, pero ¿Por qué
clasificar antes de generar las matrices y nuestra rarefaccion alpha?

Con anterioridad generamos los archivos table.qza el cual es un archivo
tipo FeatureTable\[Frecuency\] y el archivo rep-seqs.qza el cual es tipo
FeatureData\[Sequence\]; y resulta que ambos son necesarios para la
generacion de las matrices , vectores y arboles filogeneticos necesarios
para los pasos siguientes, sin embargo, estos dos archivos puede (o no)
que contengan contaminantes tipo mitocondrias / cloroplastos y la
clasificacion taxonomica nos permitira:

  - ver si se encuentran los contaminantes
  - RETIRARLOS DE LOS ARCHIVOS ANTES MENCIONADOS.

Para la clasificacion utilizaremos la herramienta Sklearn, la cual
utiliza un algoritmo bayesiano (con el cual fue entrando o entrenaremos
nuestro clasificador, tambien es posible hacerlo por medio de blast)

    qiime feature-classifier classify-sklearn \
    --i-classifier classifier-file.qza \
    --i-reads rep-seqs.qza \
    --o-classification taxonomy.qza

**Output**  
\- taxonomy.qza

Para tabularlo y visualizarlo:

    qiime metadata tabulate \
    --m-input-file taxonomy.qza \
    --o-visualization taxonomy.qzv

**Output**  
\- taxonomy.qzv

Puede que el artefacto generado con anterioridad no nos sea de gran
ayuda y es aqui donde entra nuestro archivo de meta datos, para poder
generar una grafica de barras que compare nuestras muestras entre si.

    qiime taxa barplot \
    --i-table table.qza \
    --i-taxonomy taxonomy.qza \
    --m-metadata-file sample-metadata.tsv \
    --o-visualization taxa-bar-plot.qzv

**Output**  
\- taxa-bar-plot.qzv
