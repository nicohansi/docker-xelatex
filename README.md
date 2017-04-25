docker-xelatex
==============

[![Docker Stars](https://img.shields.io/docker/stars/vipintm/xelatex.svg)](https://hub.docker.com/r/vipintm/xelatex/)
[![Docker Pulls](https://img.shields.io/docker/pulls/vipintm/xelatex.svg)](https://hub.docker.com/r/vipintm/xelatex/)
[![Twitter](https://img.shields.io/twitter/url/https/hub.docker.com/r/vipintm/xelatex/.svg?style=social)](https://twitter.com/intent/tweet?text="Build latex using docker":&url=https://hub.docker.com/r/vipintm/xelatex/)


Docker container used for compile XeLaTex documents and deploy a generated PDF file. This is based on [jpbernius/docker-xelatex](https://github.com/jpbernius/docker-xelatex)

```
docker run --rm -v $(shell pwd):/data vipintm/xelatex make
```

Simple Makefile
----------------
```
######################
#      Makefile      #
######################

FILE_NAME = bibliography

LATEX = xelatex
BIBER = biber

all: clean all1
all1: clean la bib la2 la3 
no: clean la la2 

la:
    @$(LATEX) $(FILE_NAME)
bib:
    @$(BIBER) $(FILE_NAME)
la2:
    @$(LATEX) $(FILE_NAME)
la3:
    @$(LATEX) $(FILE_NAME)
show:
    @open $(FILE_NAME).pdf &


clean:
    @rm -f *.log *.aux *.dvi *.ps *.blg *.bbl *.out *.bcf *.run.xml
```

Advance Makefile
-----------------
Using [ransford/pdflatex-makefile](https://github.com/ransford/pdflatex-makefile)
```
If your main file is mypaper.tex:

$ curl -O https://raw.githubusercontent.com/ransford/pdflatex-makefile/master/Makefile.include
$ cat > Makefile
TARGET=mypaper
FIGS=img
include Makefile.include
```
