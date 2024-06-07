# TCellSI
TCellSI is a tool to assess the degree of eight distinct T-cell states including Quiescence, Regulating, Proliferation, Helper, Cytotoxicity, Progenitor exhaustion, Terminal exhaustion, and Senescence based on the degree of resting, activation, and suppression using specific gene sets and a compiled reference spectrum from transcriptomic data. The major algorithm of TCellSI is shown as follows: 

![image](https://github.com/JingminYang/TstateScore/blob/main/TCSSalgorithm.jpg)
## Installation

You can install the development version of TCellSI by:

``` r
# install.packages("devtools")
devtools::install_github("VyvyanYjm/TCSS")

library(TCSS)
```

## Example tutorial

#sample_expression: Sample expression data frame in TPM format by log2-transformed RNA-seq data.
```
# exampleSample
#             ERR3502705 ERR3502706 ERR3502712
# DDX11L1     0.00000000 0.00000000   0.000000
# WASH7P      0.82670591 1.89565638   1.404927
# MIR6859-1   0.02172025 0.03816506   0.000000
# MIR1302-2HG 0.00000000 0.00000000   0.000000
# MIR1302-2   0.00000000 0.00000000   0.000000

ResultScores <- TCstate_calcScore(exampleSample) 
```
#If you want to apply this method to other types of gene set scoring, you need to prepare marker gene sets and a reference profile that you want to, then you can use the following function to calculate other scores：

```
OtherScores <- CSS_calcScore‎(exampleSample,reference=XXX, markers=XXX)
```
#Forms of gene sets and reference profile look like:
```
#gene sets : list
#$cell_state1
#[1] "XXX"  "XXX"  "XXX" ...
#$cell_state2
#[1] "XXX"   "XXX"   "XXX" ...
#$cell_state3
#[1] "XXX"   "XXX"   "XXX" ...
```
```
#reference
#            cell_state1 cell_state2 cell_state3
# DDX11L1     0.32323232 0.54567463   0.32456323
# WASH7P      0.82670591 1.89565638   1.40492732
# MIR6859-1   0.02172025 0.03816506   0.52313432
# MIR1302-2HG 0.00000000 0.00000000   0.00032302
# MIR1302-2   0.00000000 0.00000000   0.00002132
```
#output:
The output of the function is a matrix, where each row corresponds to a score name and each column represents a sample name.  
```
# ResultScores
#                      ERR3502705 ERR3502706 ERR3502712
# Quiescence             0.7721079  0.7722078  0.7482268
# Regulating             0.6513540  0.6003654  0.6041851
# Proliferation          0.6793562  0.6450539  0.6275441
# Helper                 0.6846261  0.6487488  0.6340548
# Cytotoxicity           0.6529064  0.5928662  0.6044746
# Progenitor Exhaustion  0.5308267  0.4070450  0.4134950
# Terminal Exhaustion    0.5340890  0.4552266  0.4388102
# Senescence             0.6267208  0.5927787  0.5699727
```
 

