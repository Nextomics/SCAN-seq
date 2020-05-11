# SCAN-seq
single cell amplification and sequencing of full-length RNAs by Nanopore platform

# 01.basecalling
Nanopore rawdata basecalling use Guppy(v3.1.5) to generate the fastq data from electric signals.

```
guppy_basecaller -i /project/test/cell/ -s ./ -c /opt/ont/guppy/data/rna_r9.4.1_70bps_fast_prom.cfg -x auto -z -q 8000
```

# 02.demultiplex barcode
barcode demultiplex use [nanoplexer](https://github.com/hanyue36/nanoplexer)
```
nanoplexer -b barcode.fa -p /ouput/ input.fastq
```

# 03.QC
filter low quality reads (qscore < 7) and short reads (length <100bp) use [nanofilt](https://github.com/wdecoster/nanofilt)
```
NanoFilt.py -l 100 -q 7 raw.fastq --logfile log > clean.fastq
NanoStat.py --fastq clean.fastq --outdir ./ --name  clean.stat.xls
```

# 04.full-length reads Obtained
reads were identified, oriented and trimmed using [Pychopper](https://github.com/nanoporetech/pychopper)
```
python3 /export/pipeline/RNASeq/Software/Pychopper2/v2.0.3/bin/cdna_classifier.py -m edlib -u unclassified.fa -A aln_hits.bed -b primers.fa -c primer_config.txt -S statistics.txt -t 8 clean.fastq full_length_output.fq
```
# 05.
