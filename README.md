# About RIFTT
A pipeline for fusion gene calling by RNA-seq data and filtering for robust fusion candidates bundled into a Singularity container.
# Requirements
- Singularity installed (version >=3.6)
- 40GB of RAM
- Obtain some files:
  - Genome reference in Fasta format (https://www.gencodegenes.org/)
  - Gene annotation file in GTF format (https://www.gencodegenes.org/)
  - STAR index (build index without '--sjdbGTFfile' and '--sjdbOverhang' parameter, see [STAR manual](https://github.com/alexdobin/STAR/blob/master/doc/STARmanual.pdf))
  - Genomic databases folder as required by FusionCatcher (download newest build: https://sourceforge.net/projects/fusioncatcher/files/data/)
# Usage
### Detection (Part1)
Define the following parameters in the helper script 'RIFTT_part1.sh' before executing:
```
threads=<integer>      # Number of threads for running the detection pipeline
outputfolder=<string>  # Path to output folder
genomebuild=<string>   # ["hg19", "hg38"]
strandness=<integer>   # [0 -> unstranded, 1 -> stranded, 2 -> reversely stranded]
ref=<string>           # Path to genome reference file in Fasta format (GENCODE)
anno=<string>          # Path to gene annotation file in GTF format (GENCODE)
starindex=<string>     # Path to folder containing the STAR index
fcdata=<string>        # Path to folder containing the genomic database as required by FusionCatcher
```
Run the helper script as follows:
```
./RIFTT_part1.sh <sample_name> <fastq_folder>
```
### Filtering (Part2)
Define the following parameters in the helper script 'RIFTT_part2.sh' before executing:
```
anno=<string>            # Path to gene annotation file in GTF format (GENCODE) as used in Part1
outputfolder=<string>    # Path to output folder generated by the detection pipeline in Part1
clintable=<string>       # Path to clinical information table in Excel format
threads=<integer>        # Divisible by 2 !
```
Run the helper script as follows:
```
./RIFTT_part2.sh
```
# Build the RIFTT Singularity container on your own
```
git clone https://github.com/pkerbs/RIFTT.git <folder>
cd <folder>
sudo singularity build RIFTT.sif RIFTT.def
```
