# Quantify gene KO effect using MSK KO village data

## A brief summary

This dataset includes the scRNA-seq data in 5 time points (day -1, day 3, day 7, day 11, and day 18). The cells have been annotated by the knockout genotype, cell type, and some summary statistics such as read depth and cell cycle assignment. There are 39 knock out genotypes (including WT). Each genotype has one to four clones (e.g., named as 47_WT, 110_WT and 111_WT). 

Here is brief summary.

Statistics | Day 1 (G) | Day 3 (H)  | Day 7 (I) | Day 11 (J) | Day 18 (L)
--- | --- | --- | --- | --- | --- 
number of cells | 19.000 | 20,654 | 20,962 | 12,802 | 33,837
number of clones | 86 | 86 | 86 | 84 | 84
number of genotypes | 39 | 39 | 39 | 38 | 38

### Additional details of knockout genotypes

For genotypes without special suffix (e.g, het and e), they represent the homozygous knockout of the corresponding gene.

* HHEXhet, PDX1het, GATA6het and GATA4het represent heterozygous knockout of HHEX, PDX1, GATA6 and GATA4.

* TET1/2/3 is the homozygous knockout of TET1, TET2 and TET3.

* QSER1TET1 is the homozygous knockout of QSER1 and TET1.

* HHEXe and ONECUT1e stand for the homozygous deletion of one of the HHEX and ONECUT1 enhancers.

HHEXe and ONECUT1e are expected to express lower level of HHEX and ONECUT1 transcripts, but for the other lines, you may or may not see a decrease in mRNA level, because the way to generate the knockout is to introduce frameshift mutations, which result in malfunctional and instable proteins but may not affect RNA abundance.


## Analysis Workflow (inside `codes/`)

1. [**0_process_metadata.Rmd**](code/0_process_metadata.Rmd)  
   Process and clean cell metadata.

2. [**1_cell_type_composition.Rmd**](code/1_cell_type_composition.Rmd)  
   Examine genotype-specific cell type composition and identify genotypes associated with significant changes in cell type composition compared with WT cells.

3. [**2_pca_anova.Rmd**](code/2_pca_anova.Rmd)  
   Perform PCA on pseudobulk samples and quantify proportion of variance attributed to relevant technical and biological factors.

4. [**3a_prepare_DE.Rmd**](code/3a_prepare_DE.Rmd)  
   Identify genotypes for which pseudobulk-level differential expression (DE) analysis could be performed.

5. [**3b_pseudobulk_DE.Rmd**](code/3b_pseudobulk_DE.Rmd)  
   Run pseudobulk-level DE analysis for KO genotypes vs WT, conditioned on a given cell type.

6. [**3c_process_DE_res.Rmd**](code/3c_process_DE_res.Rmd)  
   Collect DE results from different cell types and save as text files.

7. [**3d_nDEGs.Rmd**](code/3d_nDEGs.Rmd)  
   Check the number of DE genes using the pseudobulk approach.
   
8. [**3e_cell-level-DE.Rmd**](code/3e_cell-level-DE.Rmd)  
   Run cell-level DE analysis for KO genotypes vs WT, conditioned on a given cell type.

9. [**3f_nDEGs_cell-level.Rmd**](code/3f_nDEGs_cell-level.Rmd)  
   Check the number of DE genes using the cell-level approach.

10. [**3g_compare-DE.Rmd**](code/3g_compare-DE.Rmd)  
  Compare the DE results using the pseudobulk and cell-level approaches in terms of their -log10(p-value).

11. [**4_genotype-plots.Rmd**](code/4_genotype-plots.Rmd)  
   Time-point–specific visualizations of UMAP embeddings, cell type compositions, and number of DE genes for each genotype.


## Output Folders (inside `outs/`)

- **anova/**  
  Contains results from PCA and ANOVA analyses, including variance partitioning by technical and biological factors.

- **cell_type_composition/**  
  Stores processed data and plots related to genotype-specific cell type compositions and statistical comparisons with WT.

- **differential_expression/**  
  Holds pseudobulk-level differential expression results, including per–cell type DE gene tables and summary statistics.

- **genotype_plots/**  
  Contains time-point–specific visualizations for each genotype, including UMAP embeddings, and cell type proportion bar plots.
