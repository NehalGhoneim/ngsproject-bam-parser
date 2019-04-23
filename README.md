# ngsproject-bam-parser
Parser for bam files produces 3 types of reads                                                                                                                         1- multiple mismatches
2- supplementary reads
3- discorcondant reads
obtain reads from sra and align to reference genome and generate bam file
parse bam file and find which of the 3 types of reads obtained.


The Ostreococcus tauri, marine a unicellular species of marine green alga, is a very good model for studying physiological and genetic aspects of the adaptation of the green algal lineage to the marine environment: it has a very compact genome, is easy to culture in laboratory conditions, and can be genetically manipulated by efficient homologous recombination. In 2006, the O. tauri genome was sequenced by Derelle et al. The 12.56 Mb genome organized in 20 chromosomes showed extreme gene density and few intron-containing genes. It belongs to family Prasinophyceae which is believed to be the most primitive in the green lineage from which all other green algae, and ancestors of land plants have descended. In this study we compare genome from green algae osteorococcus specie strain "RC1559" to the reference genome from ncbi to study the mode of organellar inheritance. 
I have downloaded the SRA file of single ended genome sequenced using Illumina "SRR4026812" "Illumina Genome Analyzer II".
Using fastqc revealed that the reads of poor quality so, trimming was done. Then alignment to the indexed reference genome using BWA aligner. 
BWA has different codes , at first I used "MEM" that resulted into supplementary reads flags "0X800" that indicates repeated genome or convey chimeric/non-linear alignments. Suppose there is a chromosomal inversion with a read mapping over its junction point. The first part of the read will map normally and then be truncated. The second part of the read will map further up/downstream and in the wrong orientation. Further analysis of flags values indicated that some SAM FLag values are 2064 which encodes read reverse strand (0x10)and supplementary alignment (0x800), 
while others SAM flag values are 2048 which encodes supplementary alignment (0x800) only. 
Used website: https://broadinstitute.github.io/picard/explain-flags.html 

However, when used "aln" code that resulted into bwa file that needed to be converted to sam file. It showed no supplementary reads. This may be due to that "mem" is preferable for longer reads ( > 70 bp) and bwa mem goes a step further and will find alignments where other methods have already given up i.e other codes alow mismatch easily. 
Further, analysis of the difference between different aligners and which is the best is needed. As well as more samples needed for phylogenic analysis and how chromosomal inversion if common in this specie and the relation to biparental inheritance. 

References:
1- Blanc-Mathieu, R., Sanchez-Ferandin, S., Eyre-Walker, A., & Piganeau, G. (2013). Organellar inheritance in the green lineage: insights from Ostreococcus tauri. Genome biology and evolution, 5(8), 1503–1511. doi:10.1093/gbe/evt106
2- https://en.wikipedia.org/wiki/Ostreococcus_tauri
3- Lelandais, G., Scheiber, I., Paz-Yepes, J., Lozano, J. C., Botebol, H., Pilátová, J., … Lesuisse, E. (2016). Ostreococcus tauri is a new model green alga for studying iron metabolism in eukaryotic phytoplankton. BMC genomics, 17, 319. doi:10.1186/s12864-016-2666-6
