Uncle PSL: a BLAT to SAM converter
==================================

The package performs conversion of BLAT output ([PSL](http://www.ensembl.org/info/website/upload/psl.html)) to [SAM](https://samtools.github.io/hts-specs/SAMv1.pdf) format. If the `-N` option is used then deletions larger than the specified limit are represented by the `N` CIGAR operation.

Conversion was tested on simulated reads against output generated by `bwa mem` (under the `uncle_PSL/test/data` directory).

Installation
------------

Quick install using pip:

```
pip install git+
```

Or clone the package:

```
git clone 
```

Install the package:

```
python setup.py install
```

Install the package in developer mode:

```
python setup.py develop
```

Run the tests:

```
make test
```

Build the documentation:

```
make docs
```

Issue `make help` to get a list of `make` targets.

Documentation
-------------

```
usage: uncle_psl.py [-h] [-f reads_fasta] [-N n_limit] [-H] [infile] [outfile]

Script to convert PSL files (BLAT output) to SAM format.

positional arguments:
  infile          Input PSL (default: stdin).
  outfile         Output SAM (default: stdout)

optional arguments:
  -h, --help      show this help message and exit
  -f reads_fasta  Reads in fasta format.
  -N n_limit      Use N CIGAR operation for deletions larger than this
                  parameter (None).
  -H              Use hard clipping instead of soft clipping.
```

Credits
-------

The logic is based ont the psl2sam.pl script in the [rackj](http://rackj.sourceforge.net/Scripts/index.html) package, which in turn
is based on the converter in [samtools](https://github.com/lh3/samtools-legacy/tree/master/misc).

Limitations
-----------
- SAM header is not written, but that can be easily added using [samtools view -T](http://www.htslib.org/doc/samtools.html)
- The MD flag is not added, but that can be easily done using [samtools calmd](http://www.htslib.org/doc/samtools.html).
- Mapping qualities are set to zero.
- Base qualities are not added to the SAM output.
- The `XS` flag is currently not set. 
