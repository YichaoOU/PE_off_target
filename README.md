# Quantify prime editor off-target activity

Candidate off-target locations can be predicted using casOFFinder or CHANGE-seq/GUIDE-seq assays. Then rhamp-seq experiments are performed to quantify prime editor off-target events.

# Input

1. FASTQ files, single-end or paired-end.

2. Annotation file. (.tsv)

```

Name    amplicon_sequence    gRNA_sequence

```


# Usage


### Step 1: Run Crispresso for each fastq file.

```

CRISPRessoPooled -r1 $fastq_file --name $sample_name -o ${sample_name}_results -f $annotation_tsv --quantification_window_size 1 --quantification_window_center -3 --base_editor_output --min_reads_to_use_region 3 --keep_intermediate --dump --limit_open_files_for_demux --plot_window_size 20

```

### Step 2: Summarize indel and substitution frequency.

`sample.list` contains a list of sample names used in step 1 `$sample_name`, so that the program can automatically extract crisoresso results.

```

crispressoPooled_PE_edit_frequency.py -f sample.list -i $annotation_tsv -rtt $RTT_sequence -o $output_name.stats.csv

```

# Output

Columns showing the total reads and percentages of indel and substitution. The percentage values are already multipled by 100.

```
sample  site    reads_total     is_indel_total  is_indel_percent        is_sub_total    is_sub_percent
xx      A       39445   14      0.035492457852706       15      0.038027633413613406
xx      B       61590   12      0.019483682415976103    10      0.0162364020133135
xx      C       10409   2       0.0192141416082236      12      0.1152848496493417
```

# Reference

https://hemtools.readthedocs.io/en/latest/content/CRISPR/crispressoPooled_PE.html

