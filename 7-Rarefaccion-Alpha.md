Rarefaccion Alpha
================

## Generacion de la curva de rarefaccion Alpha

The value that you provide for –p-max-depth should be determined by
reviewing the “Frequency per sample” information presented in the
table.qzv file that was created above. In general, choosing a value that
is somewhere around the median frequency seems to work well, but you may
want to increase that value if the lines in the resulting rarefaction
plot don’t appear to be leveling out, or decrease that value if you seem
to be losing many of your samples due to low total frequencies closer to
the minimum sampling depth than the maximum sampling depth.

    qiime diversity alpha-rarefaction \
    --i-table table.qza \
    --i-phylogeny rooted-tree.qza \
    --p-max-depth ### \
    --m-metadata-file sample-metadata.tsv \
    --o-visualization alpha-rarefaction.qzv
