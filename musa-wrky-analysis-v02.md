Musa WRKY Analysis
================
Ranganath Gudimella
2023-12-15

- [Background](#background)
- [Methods](#methods)
- [Coverage of Fusarium treated musa root
  transcriptomes](#coverage-of-fusarium-treated-musa-root-transcriptomes)
- [Log Normalization of data using
  edgeR](#log-normalization-of-data-using-edger)
- [Distance Matrix](#distance-matrix)
- [Differential Expression](#differential-expression)
- [Heatmap with normalised data (Untreat vs
  1DPI)](#heatmap-with-normalised-data-untreat-vs-1dpi)
- [Heatmap with normalised data (Untreat vs
  14DPI)](#heatmap-with-normalised-data-untreat-vs-14dpi)
- [DE genes GO annotation](#de-genes-go-annotation)
- [DE genes KEGG pathway annotation](#de-genes-kegg-pathway-annotation)
- [Heatmap with foldchanges - Response to
  stress](#heatmap-with-foldchanges---response-to-stress)
- [Heatmap with foldchanges - Carbohydrate metabolic
  process](#heatmap-with-foldchanges---carbohydrate-metabolic-process)
- [Heatmap with foldchanges -
  activity](#heatmap-with-foldchanges---activity)
- [Conclusion](#conclusion)

## Background

    ## Number of genes:35276 ...

## Methods

- Map transcriptome reads to all 35276 genes using Bowtie2
- Counting the number of reads mapped using Bedtools (Raw counts)
- Raw counts are counts per million (CPM) normalised using `edgeR`
  package using non-replicate dispersion method
  (`estimateGLMCommonDisp`)
- Identify differentially expressed (based on pvalue \< 0.05) WRKY genes
  between `Untreatvs1DPI`,`Untreatvs14DPI` comparisons.
- Heatmaps were generated using `ComplexHeatmap` with log2 fold changes
  as row-wise bar plots.

## Coverage of Fusarium treated musa root transcriptomes

<img src="musa-wrky-analysis-v02_files/figure-gfm/bed-proc-1.png" style="display: block; margin: auto;" />

## Log Normalization of data using edgeR

    ##             Untreat X1DPI X14DPI
    ## Ma00_g00010    6129  4382   3014
    ## Ma00_g00020    2784  4196   1953
    ## Ma00_g00030    1206  1666   3109
    ## Ma00_g00040     695   849    688
    ## Ma00_g00050    4267  5358   3883
    ## Ma00_g00060     128   292    285

    ##         condition
    ## Untreat   Untreat
    ## X1DPI        1DPI
    ## X14DPI      14DPI

    ## An object of class "DGEList"
    ## $counts
    ##             Untreat X1DPI X14DPI
    ## Ma00_g00010    6129  4382   3014
    ## Ma00_g00020    2784  4196   1953
    ## Ma00_g00030    1206  1666   3109
    ## Ma00_g00040     695   849    688
    ## Ma00_g00050    4267  5358   3883
    ## 35167 more rows ...
    ## 
    ## $samples
    ##           group  lib.size norm.factors
    ## Untreat Untreat 136216068            1
    ## X1DPI      1DPI 133035523            1
    ## X14DPI    14DPI 117512930            1

    ##               Untreat     X1DPI    X14DPI
    ## Ma00_g00010 12.581671 12.097703 11.557942
    ## Ma00_g00020 11.443462 12.035143 10.932215
    ## Ma00_g00030 10.237210 10.703038 11.602699
    ## Ma00_g00040  9.442943  9.731319  9.428360
    ## Ma00_g00050 12.059344 12.387748 11.923327
    ## Ma00_g00060  7.011227  8.194757  8.159871

![](musa-wrky-analysis-v02_files/figure-gfm/unnamed-chunk-1-1.png)<!-- -->

## Distance Matrix

![](musa-wrky-analysis-v02_files/figure-gfm/dm-1.png)<!-- -->

## Differential Expression

    ##             Untreat X1DPI X14DPI
    ## Ma00_g00010    6129  4382   3014
    ## Ma00_g00020    2784  4196   1953
    ## Ma00_g00030    1206  1666   3109
    ## Ma00_g00040     695   849    688
    ## Ma00_g00050    4267  5358   3883
    ## Ma00_g00060     128   292    285

    ##           group  lib.size norm.factors
    ## Untreat Untreat 136216068    1.0386085
    ## X1DPI      1DPI 133035523    1.0268366
    ## X14DPI    14DPI 117512930    0.9376631

    ## Number of differential expressed genes for Untreated vs 1DPI =  85

    ## Number of differential expressed genes for Untreated vs 14DPI =  267

    ## 
    ## 
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## |  Row.names  |  PValue   |   comparison   |              name              | ncbi_gene_id |
    ## +=============+===========+================+================================+==============+
    ## | Ma00_g04500 | 1.163e-05 | Untreatvs14DPI |    Alpha-humulene synthase     |  103974400   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma00_g04650 | 0.0001275 | Untreatvs1DPI  |  SNF1-related protein kinase   |  103973426   |
    ## |             |           |                |   regulatory subunit beta-1    |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma00_g04650 | 8.746e-05 | Untreatvs14DPI |  SNF1-related protein kinase   |  103973426   |
    ## |             |           |                |   regulatory subunit beta-1    |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma01_g10240 | 5.134e-05 | Untreatvs1DPI  | Photosystem II 22 kDa protein, |  103983661   |
    ## |             |           |                |         chloroplastic          |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma01_g16150 | 0.0001459 | Untreatvs14DPI |      Polyol transporter 5      |  103990474   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma01_g16670 | 0.0002302 | Untreatvs14DPI |  Pathogenesis-related protein  |  103989972   |
    ## |             |           |                |             PR-4B              |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma01_g22640 | 1.898e-05 | Untreatvs1DPI  | Conserved hypothetical protein |  103972899   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma02_g15060 | 7.379e-08 | Untreatvs1DPI  |  Pathogenesis-related protein  |  103975649   |
    ## |             |           |                |               1C               |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma02_g15060 | 1.418e-08 | Untreatvs14DPI |  Pathogenesis-related protein  |  103975649   |
    ## |             |           |                |               1C               |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma02_g15080 | 1.243e-05 | Untreatvs14DPI |  Pathogenesis-related protein  |  103975648   |
    ## |             |           |                |               1C               |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma02_g15290 | 0.000277  | Untreatvs14DPI | Putative LOB domain-containing |  103975632   |
    ## |             |           |                |           protein 38           |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma03_g08740 | 2.295e-05 | Untreatvs1DPI  |    Inactive beta-amylase 9     |  103977706   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma03_g08740 | 0.0002211 | Untreatvs14DPI |    Inactive beta-amylase 9     |  103977706   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma03_g09160 | 0.0001553 | Untreatvs14DPI | Putative Sigma factor binding  |  103977746   |
    ## |             |           |                |    protein 1, chloroplastic    |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma03_g10560 | 0.0003967 | Untreatvs14DPI |          heavy metal           |  103977867   |
    ## |             |           |                |    transport/detoxification    |              |
    ## |             |           |                |  protein, putative, expressed  |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma03_g12480 | 4.168e-05 | Untreatvs14DPI |    MYB family transcription    |  103978129   |
    ## |             |           |                |  factor, putative, expressed   |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma03_g13090 | 0.0003971 | Untreatvs14DPI |  Putative Early nodulin-like   |  103973882   |
    ## |             |           |                |           protein 1            |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma03_g27290 | 0.0003826 | Untreatvs14DPI |   ATP-dependent DNA helicase   |  103978766   |
    ## |             |           |                |              DDM1              |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma03_g29040 | 7.644e-05 | Untreatvs14DPI |     Putative Probable LRR      |  103974784   |
    ## |             |           |                |         receptor-like          |              |
    ## |             |           |                |    serine/threonine-protein    |              |
    ## |             |           |                |        kinase At4g36180        |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma03_g29790 | 2.895e-05 | Untreatvs14DPI | Putative Receptor-like protein |  103980115   |
    ## |             |           |                |               12               |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma03_g30020 | 0.0001298 | Untreatvs14DPI |   Putative LRR receptor-like   |  103980094   |
    ## |             |           |                |    serine/threonine-protein    |              |
    ## |             |           |                |          kinase GSO1           |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma03_g30270 | 0.0001769 | Untreatvs14DPI |   Putative expressed protein   |  103979939   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma04_g29630 | 1.39e-07  | Untreatvs14DPI |  Pathogenesis-related protein  |  103982936   |
    ## |             |           |                |               1B               |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma04_g29640 | 2.92e-08  | Untreatvs14DPI | Pathogenesis-related protein 1 |  103982935   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma04_g29640 | 1.458e-05 | Untreatvs1DPI  | Pathogenesis-related protein 1 |  103982935   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma04_g30850 | 2.191e-05 | Untreatvs14DPI | Putative Protein SAR DEFICIENT |  103983454   |
    ## |             |           |                |               1                |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma04_g31080 | 0.0003089 | Untreatvs14DPI |   poor homologous synapsis 1   |  103983449   |
    ## |             |           |                |  protein, putative, expressed  |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma04_g33330 | 3.17e-05  | Untreatvs14DPI |  Probable inorganic phosphate  |  103982632   |
    ## |             |           |                |        transporter 1-4         |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma04_g33470 | 0.0002113 | Untreatvs14DPI |   Probable pectinesterase 68   |  103982622   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma04_g35410 | 0.0003949 | Untreatvs14DPI |    Uncharacterized protein     |  103982455   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma04_g36300 | 0.0001993 | Untreatvs14DPI |    Putative OsWAK14 - OsWAK    |  103983344   |
    ## |             |           |                | receptor-like protein kinase,  |              |
    ## |             |           |                |           expressed            |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma04_g37490 | 1.536e-05 | Untreatvs1DPI  |   Putative expressed protein   |  103982295   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma05_g01170 | 0.0003522 | Untreatvs14DPI |      Bidirectional sugar       |  103983637   |
    ## |             |           |                |      transporter SWEET1a       |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma05_g02390 | 5.881e-06 | Untreatvs14DPI |     Putative Phospholipase     |  103983534   |
    ## |             |           |                |   A1-Igamma3, chloroplastic    |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma05_g06200 | 5.611e-05 | Untreatvs1DPI  |   Putative expressed protein   |  103984094   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma05_g07370 | 3.867e-05 | Untreatvs1DPI  |      Hypothetical protein      |  103984196   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma05_g08370 | 0.0003678 | Untreatvs14DPI |   ZCF37, putative, expressed   |  103984279   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma05_g09980 | 1.813e-05 | Untreatvs14DPI |            Putative            |  103984658   |
    ## |             |           |                |   Naringenin,2-oxoglutarate    |              |
    ## |             |           |                |         3-dioxygenase          |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma05_g17850 | 5.442e-05 | Untreatvs14DPI |          Chitinase 6           |  103985238   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma05_g22300 | 0.0001524 | Untreatvs14DPI | Probable fructose-bisphosphate |  103985718   |
    ## |             |           |                |   aldolase 2, chloroplastic    |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma05_g22430 | 0.0001952 | Untreatvs14DPI |       CEN-like protein 1       |  103985705   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma06_g16950 | 0.0001489 | Untreatvs14DPI |    Putative Uncharacterized    |  103988427   |
    ## |             |           |                |       protein At1g24485        |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma06_g17760 | 0.0003491 | Untreatvs14DPI |   Glyceraldehyde-3-phosphate   |  103987962   |
    ## |             |           |                |      dehydrogenase GAPA1,      |              |
    ## |             |           |                |         chloroplastic          |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma06_g20070 | 0.0001952 | Untreatvs14DPI |       expressed protein        |  103988154   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma06_g32380 | 0.0003967 | Untreatvs14DPI |    Uncharacterized protein     |  103989869   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma06_g32720 | 0.0002457 | Untreatvs14DPI |   Auxin-induced protein 15A    |  103989538   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma06_g33150 | 2.375e-08 | Untreatvs14DPI |     Thaumatin-like protein     |  103989579   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma06_g33150 | 4.367e-06 | Untreatvs1DPI  |     Thaumatin-like protein     |  103989579   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma06_g37070 | 3.246e-05 | Untreatvs1DPI  |   Arogenate dehydrogenase 2,   |  103990066   |
    ## |             |           |                |         chloroplastic          |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma06_g38230 | 0.0002991 | Untreatvs14DPI |   Putative Protein POLYCHOME   |  103989966   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma07_g03290 | 0.0002946 | Untreatvs14DPI |     Putative Protein MKS1      |  103990761   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma07_g04600 | 0.0003135 | Untreatvs14DPI |   Protein DETOXIFICATION 34    |  103990644   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma07_g07080 | 2.105e-06 | Untreatvs14DPI |          Expansin-B18          |  103990411   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma07_g07900 | 9.948e-05 | Untreatvs1DPI  | Tyrosine/DOPA decarboxylase 2  |  103990339   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma07_g18500 | 0.0003611 | Untreatvs14DPI |  Putative germin-like protein  |  103973473   |
    ## |             |           |                |              2-1               |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma07_g18560 | 9.169e-06 | Untreatvs14DPI |    Alpha-humulene synthase     |  103973929   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma07_g18600 | 5.598e-05 | Untreatvs14DPI | Putative Cytochrome P450 71D8  |  103973937   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma07_g18610 | 3.844e-06 | Untreatvs14DPI |     Beta-eudesmol synthase     |  103974970   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma07_g18640 | 1.875e-05 | Untreatvs14DPI |    Alpha-humulene synthase     |  103974971   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma08_g01290 | 9.989e-05 | Untreatvs14DPI | Sphinganine C4-monooxygenase 2 |  103994110   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma08_g01550 | 0.0001261 | Untreatvs14DPI |   Calcium-dependent protein    |  103994392   |
    ## |             |           |                |           kinase 17            |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma08_g02220 | 5.835e-05 | Untreatvs14DPI |   Putative expressed protein   |  103994031   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma08_g02220 | 4.14e-05  | Untreatvs1DPI  |   Putative expressed protein   |  103994031   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma08_g02240 | 0.0001089 | Untreatvs1DPI  |   Putative receptor protein    |  103994379   |
    ## |             |           |                |          kinase ZmPK1          |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma08_g02340 | 2.92e-05  | Untreatvs14DPI |      L-type lectin-domain      |  103994377   |
    ## |             |           |                | containing receptor kinase S.4 |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma08_g03660 | 5.796e-05 | Untreatvs1DPI  |    uncharacterized secreted    |  103993925   |
    ## |             |           |                |  protein, putative, expressed  |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma08_g09780 | 0.0003378 | Untreatvs14DPI |        Glutaredoxin-C1         |  103993388   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma08_g10110 | 0.0002139 | Untreatvs14DPI | Putative E3 ubiquitin-protein  |  103993356   |
    ## |             |           |                |           ligase EL5           |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma08_g12350 | 0.0003261 | Untreatvs14DPI | Putative Protein BREAST CANCER |  103993160   |
    ## |             |           |                |    SUSCEPTIBILITY 1 homolog    |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma08_g14610 | 2.895e-05 | Untreatvs14DPI |    Uncharacterized protein     |  103974581   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma08_g14610 | 8.412e-06 | Untreatvs1DPI  |    Uncharacterized protein     |  103974581   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma08_g15300 | 6.184e-05 | Untreatvs14DPI |     Putative Probable WRKY     |  103994612   |
    ## |             |           |                |    transcription factor 42     |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma08_g16020 |  0.00012  | Untreatvs14DPI |    Uncharacterized protein     |  103994823   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma09_g13670 | 1.82e-05  | Untreatvs14DPI |            Probable            |  103997911   |
    ## |             |           |                | pectinesterase/pectinesterase  |              |
    ## |             |           |                |          inhibitor 12          |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma10_g15100 | 1.028e-05 | Untreatvs14DPI |   Putative expressed protein   |  104001014   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma10_g15370 | 0.0001232 | Untreatvs1DPI  |    Chlorophyll a-b binding     |  104001037   |
    ## |             |           |                |   protein 40, chloroplastic    |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma10_g16920 | 0.0001766 | Untreatvs14DPI | PB1 domain containing protein, |  103968458   |
    ## |             |           |                |           expressed            |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma10_g21700 | 4.47e-05  | Untreatvs14DPI |    Protein HEADING DATE 3A     |  103969848   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma10_g21700 | 0.0001226 | Untreatvs1DPI  |    Protein HEADING DATE 3A     |  103969848   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma10_g23880 | 0.0003038 | Untreatvs14DPI |           Shikimate            |  103969086   |
    ## |             |           |                | O-hydroxycinnamoyltransferase  |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma10_g24700 | 7.179e-07 | Untreatvs14DPI |   Probable DNA helicase MCM9   |  103969903   |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## | Ma10_g28920 | 0.0001582 | Untreatvs14DPI |     plant-specific domain      |  103969497   |
    ## |             |           |                |   TIGR01615 family protein,    |              |
    ## |             |           |                |           expressed            |              |
    ## +-------------+-----------+----------------+--------------------------------+--------------+
    ## 
    ## Table: Differential Expression Genes

## Heatmap with normalised data (Untreat vs 1DPI)

<img src="musa-wrky-analysis-v02_files/figure-gfm/unnamed-chunk-2-1.png" style="display: block; margin: auto;" />

## Heatmap with normalised data (Untreat vs 14DPI)

<img src="musa-wrky-analysis-v02_files/figure-gfm/unnamed-chunk-3-1.png" style="display: block; margin: auto;" />

## DE genes GO annotation

- BP = Biological process
- MF = Molecular Function
- CC = Cellular component

<img src="musa-wrky-analysis-v02_files/figure-gfm/unnamed-chunk-4-1.png" style="display: block; margin: auto;" />

## DE genes KEGG pathway annotation

    ##                                                                         mus01100 
    ##                    "Metabolic pathways - Musa acuminata (wild Malaysian banana)" 
    ##                                                                         mus01110 
    ## "Biosynthesis of secondary metabolites - Musa acuminata (wild Malaysian banana)" 
    ##                                                                         mus01200 
    ##                     "Carbon metabolism - Musa acuminata (wild Malaysian banana)" 
    ##                                                                         mus01210 
    ##       "2-Oxocarboxylic acid metabolism - Musa acuminata (wild Malaysian banana)" 
    ##                                                                         mus01212 
    ##                 "Fatty acid metabolism - Musa acuminata (wild Malaysian banana)" 
    ##                                                                         mus01230 
    ##           "Biosynthesis of amino acids - Musa acuminata (wild Malaysian banana)"

    ## 
    ## 
    ## +----------+--------------------------------+---------------------+-----------+-----------------------+
    ## |    id    |         pathways.list          |       p.value       | Annotated |       genelist        |
    ## +==========+================================+=====================+===========+=======================+
    ## | mus04016 | MAPK signaling pathway - plant | 0.0106021828389979  |     5     | 103975649, 103975648, |
    ## |          |     - Musa acuminata (wild     |                     |           | 103982936, 103982935, |
    ## |          |       Malaysian banana)        |                     |           |       103990761       |
    ## +----------+--------------------------------+---------------------+-----------+-----------------------+
    ## | mus04075 |      Plant hormone signal      | 0.0094525436131026  |     5     | 103975649, 103975648, |
    ## |          | transduction - Musa acuminata  |                     |           | 103982936, 103982935, |
    ## |          |    (wild Malaysian banana)     |                     |           |       103989538       |
    ## +----------+--------------------------------+---------------------+-----------+-----------------------+
    ## | mus04626 |  Plant-pathogen interaction -  | 0.00355157406542122 |     5     | 103975649, 103975648, |
    ## |          | Musa acuminata (wild Malaysian |                     |           | 103982936, 103982935, |
    ## |          |            banana)             |                     |           |       103994392       |
    ## +----------+--------------------------------+---------------------+-----------+-----------------------+
    ## | mus00710 |       Carbon fixation in       |  0.894355298121417  |     2     | 103985718, 103987962  |
    ## |          |   photosynthetic organisms -   |                     |           |                       |
    ## |          | Musa acuminata (wild Malaysian |                     |           |                       |
    ## |          |            banana)             |                     |           |                       |
    ## +----------+--------------------------------+---------------------+-----------+-----------------------+
    ## | mus00010 | Glycolysis / Gluconeogenesis - |  0.663252972116924  |     1     |       103985718       |
    ## |          | Musa acuminata (wild Malaysian |                     |           |                       |
    ## |          |            banana)             |                     |           |                       |
    ## +----------+--------------------------------+---------------------+-----------+-----------------------+
    ## | mus00030 |  Pentose phosphate pathway -   |  0.663252972116924  |     1     |       103985718       |
    ## |          | Musa acuminata (wild Malaysian |                     |           |                       |
    ## |          |            banana)             |                     |           |                       |
    ## +----------+--------------------------------+---------------------+-----------+-----------------------+
    ## | mus00051 |      Fructose and mannose      |  0.663252972116924  |     1     |       103985718       |
    ## |          |  metabolism - Musa acuminata   |                     |           |                       |
    ## |          |    (wild Malaysian banana)     |                     |           |                       |
    ## +----------+--------------------------------+---------------------+-----------+-----------------------+
    ## | mus00195 |     Photosynthesis - Musa      |  0.336747027883076  |     1     |       103983661       |
    ## |          |   acuminata (wild Malaysian    |                     |           |                       |
    ## |          |            banana)             |                     |           |                       |
    ## +----------+--------------------------------+---------------------+-----------+-----------------------+
    ## | mus00196 |    Photosynthesis - antenna    |  0.555848758739326  |     1     |       104001037       |
    ## |          |   proteins - Musa acuminata    |                     |           |                       |
    ## |          |    (wild Malaysian banana)     |                     |           |                       |
    ## +----------+--------------------------------+---------------------+-----------+-----------------------+
    ## | mus00350 |   Tyrosine metabolism - Musa   |  0.481329341112728  |     1     |       103990339       |
    ## |          |   acuminata (wild Malaysian    |                     |           |                       |
    ## |          |            banana)             |                     |           |                       |
    ## +----------+--------------------------------+---------------------+-----------+-----------------------+
    ## | mus00360 |   Phenylalanine metabolism -   |  0.481329341112728  |     1     |       103990339       |
    ## |          | Musa acuminata (wild Malaysian |                     |           |                       |
    ## |          |            banana)             |                     |           |                       |
    ## +----------+--------------------------------+---------------------+-----------+-----------------------+
    ## | mus00380 |  Tryptophan metabolism - Musa  |  0.481329341112728  |     1     |       103990339       |
    ## |          |   acuminata (wild Malaysian    |                     |           |                       |
    ## |          |            banana)             |                     |           |                       |
    ## +----------+--------------------------------+---------------------+-----------+-----------------------+
    ## | mus00400 |  Phenylalanine, tyrosine and   |  0.271385690907391  |     1     |       103990066       |
    ## |          | tryptophan biosynthesis - Musa |                     |           |                       |
    ## |          |   acuminata (wild Malaysian    |                     |           |                       |
    ## |          |            banana)             |                     |           |                       |
    ## +----------+--------------------------------+---------------------+-----------+-----------------------+
    ## | mus00520 |   Amino sugar and nucleotide   |  0.354001304710311  |     1     |       103985238       |
    ## |          |    sugar metabolism - Musa     |                     |           |                       |
    ## |          |   acuminata (wild Malaysian    |                     |           |                       |
    ## |          |            banana)             |                     |           |                       |
    ## +----------+--------------------------------+---------------------+-----------+-----------------------+
    ## | mus00600 | Sphingolipid metabolism - Musa |         0.5         |     1     |       103994110       |
    ## |          |   acuminata (wild Malaysian    |                     |           |                       |
    ## |          |            banana)             |                     |           |                       |
    ## +----------+--------------------------------+---------------------+-----------+-----------------------+
    ## | mus00909 |      Sesquiterpenoid and       |  0.162762509396484  |     1     |       103974971       |
    ## |          |  triterpenoid biosynthesis -   |                     |           |                       |
    ## |          | Musa acuminata (wild Malaysian |                     |           |                       |
    ## |          |            banana)             |                     |           |                       |
    ## +----------+--------------------------------+---------------------+-----------+-----------------------+
    ## | mus00940 | Phenylpropanoid biosynthesis - |  0.869412860465464  |     1     |       103969086       |
    ## |          | Musa acuminata (wild Malaysian |                     |           |                       |
    ## |          |            banana)             |                     |           |                       |
    ## +----------+--------------------------------+---------------------+-----------+-----------------------+
    ## | mus00941 | Flavonoid biosynthesis - Musa  |  0.869412860465464  |     1     |       103969086       |
    ## |          |   acuminata (wild Malaysian    |                     |           |                       |
    ## |          |            banana)             |                     |           |                       |
    ## +----------+--------------------------------+---------------------+-----------+-----------------------+
    ## | mus00945 |  Stilbenoid, diarylheptanoid   |  0.869412860465464  |     1     |       103969086       |
    ## |          |  and gingerol biosynthesis -   |                     |           |                       |
    ## |          | Musa acuminata (wild Malaysian |                     |           |                       |
    ## |          |            banana)             |                     |           |                       |
    ## +----------+--------------------------------+---------------------+-----------+-----------------------+
    ## | mus00950 |     Isoquinoline alkaloid      |  0.481329341112728  |     1     |       103990339       |
    ## |          | biosynthesis - Musa acuminata  |                     |           |                       |
    ## |          |    (wild Malaysian banana)     |                     |           |                       |
    ## +----------+--------------------------------+---------------------+-----------+-----------------------+
    ## | mus00965 |  Betalain biosynthesis - Musa  |  0.481329341112728  |     1     |       103990339       |
    ## |          |   acuminata (wild Malaysian    |                     |           |                       |
    ## |          |            banana)             |                     |           |                       |
    ## +----------+--------------------------------+---------------------+-----------+-----------------------+
    ## | mus03440 |   Homologous recombination -   |  0.896897991631315  |     1     |       103993160       |
    ## |          | Musa acuminata (wild Malaysian |                     |           |                       |
    ## |          |            banana)             |                     |           |                       |
    ## +----------+--------------------------------+---------------------+-----------+-----------------------+
    ## 
    ## Table: KEGG Pathway Enrichment

## Heatmap with foldchanges - Response to stress

<img src="musa-wrky-analysis-v02_files/figure-gfm/unnamed-chunk-6-1.png" style="display: block; margin: auto;" />

## Heatmap with foldchanges - Carbohydrate metabolic process

<img src="musa-wrky-analysis-v02_files/figure-gfm/unnamed-chunk-7-1.png" style="display: block; margin: auto;" />

## Heatmap with foldchanges - activity

<img src="musa-wrky-analysis-v02_files/figure-gfm/unnamed-chunk-8-1.png" style="display: block; margin: auto;" />

## Conclusion

- Overall distribution of counts shows 14DPI has more transcriptome
  expression compared to Untreatment or 1DPI.
- Differential expression shows 85 and 267 genes from
  `untreated vs 1DPI` & `untreated vs 14DPI` respectively.  
- GO annotation clearly show elevated levels in
  `stress responsive genes` and `transcription factor activity` in
  14DPI.
- `WRKY`,`MADS-box`,`Homeobox` and `ERF` are upregulated in 14DPI.
- KEGG pathway annotation shows genes are acting from following pathways
  `MAPK signaling pathway`,`Plant-Harmone signalling`,`plant-pathogen interaction`
  .
- **Note: Differential expression is based on non-replicated
  transcriptome data.For statistical inference, validation by replicated
  samples is necessary to support the results.**
