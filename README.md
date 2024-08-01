# install sra toolkit in Gitpod
sudo apt-get install sra-toolkit
# configure SRA toolkit to save in current directory
vdb-config -i

# downloading data
# select an accession id from sra
# gather data using prefetch
mkdir sra_data
cd sra_data
prefetch id # creates a directory with .sra file in it
# generate reads from pre-fetched download
fastq-dump --split-files --gzip \
    -X 10000 ERR11468775

# Read QC
# FASTQC
# install FASTQC
wget https://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.12.1.zip
unzip fastqc_v0.12.1.zip
# fastq QC
/workspace/data-interpreters/FastQC/fastqc ERR11468775_1.fastq.gz ERR11468775_2.fastq.gz


# Read Trimming - Trimmomatric, fastp, cutadapt (to remove adapters)
# Install fastp
wget http://opengene.org/fastp/fastp
chmod a+x ./fastp
#trimming reads
/workspace/data-interpreters/fastp -q 20 -i ERR11468775_1.fastq.gz -I ERR11468775_2.fastq.gz \
     -o ERR11468775_1_trimmed.fastq.gz -O ERR11468775_2_trimmed.fastq.gz
