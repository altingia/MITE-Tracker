## About

IRmatcher is efficient and easy to run tool for discovering Miniature Inverted repeats Transposable Elements (MITE) in genomic sequences. It is written in python and uses ncbi's blast+ for finding inverted repeats and cdhit to do the clustering. 

Large genomes can be executed in desktop computers.

## Requirements (just follow how to install)
 - tested in macOS 10.13.1, Debian 7.6, Ubuntu 16.04, Windows 7
 - ncbi blast+ (Nucleotide-Nucleotide BLAST 2.6.0+)
 - python requirements are in requirements.txt file (bipython and pandas)

## How to install dependencies in linux or windows
```
git clone https://github.com/weizhongli/cdhit.git
cd cdhit/
make
sudo apt-get install ncbi-blast+ virtualenv
pip install -r requirements.txt
```

## How to install dependencies in macOS (OSx)
```
brew install ncbi-blast+ virtualenv
git clone https://github.com/weizhongli/cdhit.git
cd cdhit/
make openmp=no
#as stated in https://entropicevolution.wordpress.com/2015/09/19/compiling-cd-hit-under-mac-osx-yosemite/
pip install -r requirements.txt

```
## Install python packages with virtualenv (recommended)
```
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
```

# How to run

```
python miteParser.py -g /path/to/your/genome.fasta -j jobname
```

Or specify -w for specify the number of threads to use
```
python miteParser.py -g /path/to/your/genome.fasta -w 3 -j jobname
```

To run in background
```
nohup python -u miteParser.py -g /path/to/your/genome.fasta -w 3 -j jobname &
```

In order to check the program output you can use these command (ctrl+c to exit)
```
#nohup will have the program output as well as the output from cdhit execution
tail -f nohup.out
#out.log contaings a log file with timing.
tail -f results/[jobname]/out.log
```

## Command line options
| Argument  | Description | Data type  | Required or default |
| ------------- | ------------- | ------------- | ------------- |
| -g  | Genome file in fasta format  | string  | required  |
| -j  | Jobname. Result files will be created in results/jobname   | string  | required  |
| -w  | Max number of processes to use simultaneously  | int  | 1  |
| -tsd_min_len  | TSD min lenght  | int  | 2  |
| -tsd_max_len  | TSD max lenght  | int  | 10  |
| -mite_min_len  | MITE min lenght  | int  | 50  |
| -mite_max_len  | MITE max lenght  | int  | 650  |


## Results
All the results are placed in _results/[yourjobname]/_. 
Here you will find _mites.fasta_ with all the MITEs sequences 
and also _mites.gff3_ with a gff file describing the MITEs in the genome file.