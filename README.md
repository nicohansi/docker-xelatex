docker-xelatex
==============

[![Docker Stars](https://img.shields.io/docker/stars/zentralorgan/xelatex.svg)](https://hub.docker.com/r/zentralorgan/xelatex/)
[![Docker Pulls](https://img.shields.io/docker/pulls/zentralorgan/xelatex.svg)](https://hub.docker.com/r/zentralorgan/xelatex/)


Docker container used for compile XeLaTex documents and deploy a generated PDF file. This is based on [vipintm/docker-xelatex](https://github.com/jpbernius/docker-xelatex)

```
docker run --rm -v $(shell pwd):/data zentralorgan/xelatex make
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

* Simple make:

```
docker run --rm -v $(shell pwd):/data moss/xelatex make
```

Another Simple Makefile
-----------------------
```
######################
#      Makefile      #
######################

filename=your_file_without_extension

pdf: 
	xelatex ${filename}
	xelatex ${filename}

text: html
	html2text -width 100 -style pretty ${filename}/${filename}.html | sed -n '/./,$$p' | head -n-2 >${filename}.txt

html:
	@#latex2html -split +0 -info "" -no_navigation ${filename}
	htlatex ${filename}

view:
	while inotifywait --event modify,move_self,close_write ${filename}.tex; \
		do xelatex -halt-on-error ${filename} &&   xelatex -halt-on-error \
		${filename}; done

clean:
	rm -f ${filename}.{ps,pdf,log,aux,out,dvi,bbl,blg,snm,toc,nav}
```


* Auto compile for each save:

```
docker run --rm -v $(shell pwd):/data moss/xelatex make view
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

* Use options:
Use options avalable in Makefile.include

```
docker run --rm -v $(shell pwd):/data moss/xelatex make <options>
```

