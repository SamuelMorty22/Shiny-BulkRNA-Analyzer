# BulkRNA Analysis Toolkit for Shiny

![Project Logo](link_to_logo.png) <!-- 如果有项目标志，请添加 -->

The BulkRNA Analysis Toolkit for Shiny is a comprehensive R-based package designed to simplify and enhance the analysis of bulk RNA sequencing data. It offers a user-friendly Shiny web application with interactive tools and visualizations for researchers and bioinformaticians working with gene expression data.

## Features

- **Count Matrix Generation:** Utilize featureCounts data to create count matrices for downstream analysis.
- **PCA Dimensionality Reduction:** Visualize data and reduce complexity using Principal Component Analysis.
- **Differential Gene Analysis:** Identify statistically significant differentially expressed genes.
- **Heatmap Visualization:** Create expressive heatmaps to visualize gene expression patterns.
- **Customizable Workflow:** Adapt the toolkit to your specific analysis needs with ease.

## Getting Started

To get started with the BulkRNA Analysis Toolkit, follow these steps:

1. **Installation:** Clone this repository and install the required R packages.

   ```bash
   git clone https://github.com/yourusername/your-repo.git
   ```
   
2. **Install the dependencies:** Open the ```BulkRNA.Rmd``` file and load the first section to install the dependencies:

- dplyr
- org.Hs.eg.db
- limma
- ggplot2
- circlize
- tibble
- pheatmap
- gridExtra
- ggrepel
- DESeq2
- ComplexHeatmap
- ggplotify
- clusterProfiler
- cowplot
- shiny

Within the document, you'll find instructions for installing the necessary R packages and setting up any additional configuration required for the analysis. Follow these instructions to ensure that all dependencies are correctly installed.

## Preparing Raw Data and Loading Sample Information

### Organizing Raw Data

1. Place your featureCounts output files in the project's root directory under a folder named `raw_material`. Ensure that the files contain the following standard columns:
   - Geneid
   - Chr
   - Start
   - End
   - Strand
   - Length
   - ./Fine-2-input/Fine-2-inputAligned.sortedByCoord.out.bam

2. Make sure that your gene IDs use `gene_name` as the identifier and do not use Ensembl IDs or any other identifiers.

### Loading Sample Information

1. To fill in sample information, execute the following command in R or RStudio:

   ```R
   # Load the sample information
   load_sample_info()
   ```

## Generating Count Matrix and TPM Matrix

1. Execute the following command to generate the count matrix and TPM matrix:

   ```R
   # Generate the count matrix and TPM matrix
   perform_count_matrix_and_logtpm()
   ```

   After running the command, the system will create a count_matrix folder in the root directory of your project.

   Inside the count_matrix folder, you will find the following files:

   ```count_matrix.csv```: This file contains the count matrix generated from the featureCounts data. It includes information on ```gene IDs```, ```chromosomes```, ```start``` and ```end positions```, ```strand```, ```gene length```, and the ```counts``` for each sample.
   
   ```TPM_matrix.csv```: This file contains the TPM (Transcripts Per Million) matrix generated using the TPM algorithm. It provides normalized expression values for each gene across samples.
   
Now, you have successfully generated the count matrix and TPM matrix necessary for your analysis. These files are located in the count_matrix folder and can be used for downstream analyses.

## Performing Principal Component Analysis (PCA)

To perform Principal Component Analysis (PCA) for dimensionality reduction and visualize sample differences, follow these steps:

1. Open your R or RStudio environment.

2. Execute the following command in the R console:

   ```R
   # Perform Principal Component Analysis (PCA)
   perform_PCA()
   ```
EXAMPLE: https://github.com/SamuelMorty22/Shiny-BulkRNA-Analyzer/blob/main/Shiny-BulkRNA-Analyzer/test/plots/PCA.pdf

After running the command, the system will automatically generate a PCA.pdf file. You can find the PCA.pdf file inside the ```plots``` folder located in the root directory of your project.

Now, you have successfully performed PCA to visualize sample differences, and the PCA plot is available in the PCA.pdf file located in the plots folder. This plot can be valuable for understanding the variation in your data.

## Performing Differential Expression Analysis (DEGs)

To perform Differential Expression Analysis (DEGs) with different log2fold thresholds, you can use the `perform_DEGs` function. This analysis will identify genes that are differentially expressed compared to your specified log2fold threshold.

### 2-Fold DEGs

To identify genes with at least a 2-fold change in expression, execute the following command:

```R
# Perform 2-Fold DEGs analysis
perform_DEGs(log2fold = 1)
```
### 4-Fold DEGs

To identify genes with at least a 4-fold change in expression, execute the following command:

```R
# Perform 4-Fold DEGs analysis
perform_DEGs(log2fold = 2)
```
### 8-Fold DEGs

To identify genes with at least an 8-fold change in expression, execute the following command:

```R
# Perform 8-Fold DEGs analysis
perform_DEGs(log2fold = 3)
```

After running the analysis, the system will save the generated differential gene expression data in the ./results directory. The output will include the following parameters for each gene:

 - __baseMean__: The average count (average expression level) representing a gene's average expression across all samples.
   
 - __log2FoldChange__: The logarithmic fold change in gene expression, indicating the difference in expression between two sample groups, typically expressed in log2 form.
  
 - __lfcSE__: The standard error of the log fold change, representing the estimate's precision for differential expression.
   
 - __stat__: A statistical measure used to assess the degree of expression difference for a gene, often related to hypothesis testing.
   
 - __pvalue__: The p-value from a hypothesis test, measuring the significance of observed differences. Smaller p-values indicate more significant differences.
   
 - __padj__: The adjusted p-value (usually corrected for multiple testing), accounting for the false positive rate in the context of multiple comparisons. Typically used to determine significance.
  

You can utilize this data for further downstream analysis or visualize the differentially expressed genes.

## Generating a Heatmap

To generate a heatmap for specific genes of interest, you can use the `gene_info()` function. This function allows you to input the genes you want to include in the heatmap.

```R
# Input genes for the heatmap
gene_info()
```
If you need to input multiple genes, you can separate them with spaces. For example, if you want to include genes like "DDX6," "DND1," and "NANOG," you can enter them as follows:

__"DDX6 DND1 NANOG__

After executing the gene_info() function with your selected genes, you can proceed to create a heatmap based on the provided gene expression data.