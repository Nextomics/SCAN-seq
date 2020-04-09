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
