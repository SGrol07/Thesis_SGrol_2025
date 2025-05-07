This README describes the workflow of the Thesis project by Sabine Grol, in which the genetic overlap between neuroticism and white blood cell count (WBC) was investigated.

The original work was done between 03/02/2025 and 30/05/2025.

The data was obtained from the UK Biobank (ftp://ftp.sanger.ac.uk/pub/project/humgen/summary_statistics/UKBB_blood_cell_traits/ and http://www.mhi-humangenetics.org/en/resources) and the CNCR (https://ctg.cncr.nl/software/summary_statistics). They were downloaded February and March 2025.

1. Cleaning and harmonising the data
This was done according to the script "Harmonisation_script2025.txt" 
This was to filter the faulty and/or missing data and harmonise the columns so that the GWAS file has a clear structure to work with in the following analyses. Indels were deleted from the data, and missing rsIDs and MAFs were imputed with help of the 1000 genomes reference data.

2. After cleaning and harmonising the data, the first analysis ran is LDSC to calculate the global genetic correlation.
This was done using the script "LDSC_script2025.txt"
The first step is converting the GWAS data to summary statistics (sumstats). After, the sumstats files can be used to check for genetic correlation. The output was stored in the JupyterHub environment, and back-up copies were manually downloaded.

3. After LDSC has been completed, the next step is the FUMA analysis to identify the genes.
This was done on the FUMA website (https://fuma.ctglab.nl/) with the SNP2GENE function.
The Neuroticism results, done by Jack Smith on 20/03/2025 under the name NEU_Nagel, job # 598754, were downloaded for analysis.
For the WBC results, the summary statistics WBC.txt.gz file was manually uploaded. The following parameters were used:
# Section 1: After uploading the summary statistics the column names were filled in (CHR/BP/RSID/P/A1/A2)
# Section 2: Column name for N per SNP was added as "N"
# Section 3-1 to 3-3: These were ignored
# Section 4: Select Ensembl version v110, and select "all" for the gene type.
# Section 5: Uncheck "exclude MHC region", as it is necessary to include for this trait due to the immune system involvement
# Section 6: Check "include MAGMA" and select "GTEx v8: 54 tissue types" for the MAGMA gene expression analysis
The job was given the title "WBC"; runtime was 3 hours.
Plots and results were manually downloaded for further analysis.

4. Next, gene overlap for the two traits was investigated.
For this, the script "Gene_overlap_script2025" was used. Input from MAGMA was downloaded from the FUMA website and manually uploaded to JupyterHub for analysis.
The output was saved as a .csv file (Overlap_NEU_WBC.csv), which was automatically stored on JupyterHub and manually downloaded. The downloaded .csv file was converted to a .xlsx file (Overlap_NEU_WBC.xlsx) for ease of use.

5. After gene overlap, Gene-set overlap was investigated.
The script "GSA_overlap_script2025" was used for this, which is the gene overlap script but edited for the GSA files. As there was no overlap found, this output was not saved.

6. To further investigate the genes found, the GENE2FUNC function on the FUMA website was used. 
The following parameters were used:
# Genes of interest: The overlapping genes found in step 4 that had been downloaded as a list were uploaded here.
# Background genes: Only protein-coding genes were selected as background for analysis.\
# Other optional parameters: Ensembl version v110 was used, GTEx v8: 54 tissue types was used as gene expression data set, the MHC region was included, the Bonferroni method was used as multiple test correction, the maximum adjusted p-value remained at <0.05, and the minimum overlapping genes with gene-sets remained at ≥ 2.
Plots were downloaded manually from the FUMA website.

7. Lastly, to investigate the local genetic correlation, LAVA was ran.
The univariate test was ran for neuroticism and the bivariate for neuroticism and WBC. Results were stored as "Neuroticism_LAVA.txt", "Neuroticism_LAVA_univariate.txt", and "NEUvsWBC_bivar_lava.txt". These files were used to generate plots using the script "LAVA_plots_script2025". Plots generated included a full overview of the chromosomes as well as zoomed-in focus plots. The focus plots were generated as .png files and manually downloaded. The full overview plot was generated a .pdf file ("plot_NEU_vs_WBC.pdf") and manually downloaded.
Analysis of significant loci was done using the script "LAVA_analysis_script2025". Results were stored as a .csv file, "chr_loci_WBC.csv", which was manually downloaded and converted to a .xlsx file ("chr_loci_WBC.xlsx") for ease of use.