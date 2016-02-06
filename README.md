docker-xelatex
==============

[![Docker Stars](https://img.shields.io/docker/stars/jpbernius/xelatex.svg)](https://hub.docker.com/r/jpbernius/xelatex/)
[![Docker Pulls](https://img.shields.io/docker/pulls/jpbernius/xelatex.svg)](https://hub.docker.com/r/jpbernius/xelatex/)


Docker container used for compile XeLaTex documents and deploy a generated PDF file.

```
docker run --rm -v $(shell pwd):/data jpbernius/xelatex make
```

Example Makefile
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