## conda env create
conda create -n sptran python=3.8

## pip installs
pip install sinkhorn-transformer
pip uninstall axial-positional-embedding
pip install axial-positional-embedding==0.2.1
pip uninstall local-attention
pip install local-attention==1.8.6


## conda install pytorch
conda install pytorch==1.13.1 torchvision==0.14.1 torchaudio==0.13.1 pytorch-cuda=11.7 -c pytorch -c nvidia

# alternatively 
#pip install torch==1.13.1+cu117 torchvision==0.14.1+cu117 torchaudio==0.13.1 --extra-index-url https://download.pytorch.org/whl/cu117

## pip installs
# numpy 1.24.3 installed by pytorch install
#pip install numpy==1.21.5

# pandas 2.0.3 installed by pyensembl install 
# pandas==2.0.3
pip install gffutils==0.11.0
pip install tqdm==4.62.2
pip install pyfaidx==0.6.3.1
pip install PyVCF3==1.0.0
pip install pyensembl==2.3.13

# download necessary files
1. Download the model weights file
https://drive.google.com/file/d/1d8n4vHDSbXqpPc_JFEswLomSUDBgHvno/view?usp=drive_link
Move the downloaded file to ./model/weights


2. Download the genome assembly file from Ensemble
https://hgdownload.soe.ucsc.edu/goldenPath/hg38/bigZips/hg38.fa.gz
Decompress the file and place the decompressed file in ./data/data_package

3. Download the genome annotation file - DO NOT DECOMPRESS THIS FILE
https://ftp.ebi.ac.uk/pub/databases/gencode/Gencode_human/release_44/gencode.v44.annotation.gtf.gz
Place the downloaded file in ./data/data_package (Do not decompress)
Rename the file to hg38.annotation.gtf.gz

# after downloading files, it is necessary to build the annotation db
pyensembl install --reference-name hg38 --annotation-name gencode.v38 --gtf "data/data_package/hg38.annotation.gtf.gz"

# run the test case
python sptransformer.py --input data/example/input38.vcf --output data/example/output38.tsv --reference hg38 --vcf vcf --svemb yes

# run on your data
python sptransformer.py --input data/clinvar/clinvar_sample.csv --output data/clinvar/clinvar_sample.tsv --reference hg38 --vcf csv --svemb yes
