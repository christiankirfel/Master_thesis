#
# Makefile to run latex, dvips, and pdflatex on the thesis guide
# Can also run feynmf/feynmp/tikz on files in a directory
#
GUIDE = thesis_guide
# EXTRACMD = --shell-escape
FEYNDIR = ../feynmf
FEYNFILES = $(wildcard $(FEYNDIR)/*.tex)
TIKZDIR = ../tikz
TIKZFILES = $(wildcard $(TIKZDIR)/*.tex)
ifdef file
FEYNFILES = $(FEYNDIR)/$(file).tex
TIKZFILES = $(TIKZDIR)/$(file).tex
endif
AWKDIR=..

.PHONY: guide guide09 guide11 phdsubmit \
	feynmf feynmp tikz \
	cleanguide \
	cleanfeynmf cleanfeynmp  cleantikz cleanpictpdf \
	cleanblx cleanbbl \
	cleanglo cleanphd \
	help test

guide: guide11

guide09:
	pdflatex   $(EXTRACMD) $(GUIDE)
	bibtex     $(GUIDE)
	pdflatex   $(EXTRACMD) $(GUIDE)
	bibtex     $(GUIDE)
	makeindex  $(GUIDE)
	makeglossaries $(GUIDE)
	pdflatex   $(GUIDE)
	pdflatex   $(GUIDE)

guide11:
	pdflatex   $(EXTRACMD) $(GUIDE)
	biber      $(GUIDE)
	makeindex  $(GUIDE)
	makeglossaries $(GUIDE)
	pdflatex   $(EXTRACMD) $(GUIDE)
	pdflatex   $(GUIDE)

feynmf:
	make -f ../Makefile FEYNDIR=$(FEYNDIR) FEYNFILES="$(FEYNFILES)" \
	 AWKDIR=$(AWKDIR) feynmf

feynmp:
	make -f ../Makefile FEYNDIR=$(FEYNDIR) FEYNFILES="$(FEYNFILES)" \
	 AWKDIR=$(AWKDIR) feynmp

tikz:
	make -f ../Makefile TIKZDIR=$(TIKZDIR) TIKZFILES="$(TIKZFILES)" tikz

phdsubmit:
	pdflatex  PhD_submit
	pdflatex  PhD_submit

cleanall: clean cleanbbl cleanpictpdf

clean: cleanguide cleanphd cleanfeynmf cleanfeynmp cleantikz cleanblx cleanglo

cleanguide:
	-rm $(GUIDE).log $(GUIDE).aux $(GUIDE).toc
	-rm $(GUIDE).lof $(GUIDE).lot $(GUIDE).out
	-rm $(GUIDE).blg $(GUIDE).bbl $(GUIDE).pdf
	-rm $(GUIDE)-blx.bib $(GUIDE).bcf $(GUIDE).run.xml
	-rm $(GUIDE).ind $(GUIDE).idx $(GUIDE).ilg
	-rm $(GUIDE).acn $(GUIDE).acr $(GUIDE).alg
	-rm $(GUIDE).glg $(GUIDE).glo $(GUIDE).gls
	-rm $(GUIDE).ist
	-rm *.aux

cleanfeynmf:
	make -f ../Makefile cleanfeynmf FEYNDIR=$(FEYNDIR)

cleanfeynmp:
	-rm *.1 *.mp

	make -f ../Makefile cleanfeynmp FEYNDIR=$(FEYNDIR)

cleantikz:
	make -f ../Makefile cleantikz TIKZDIR=$(TIKZDIR)

cleanpictpdf:
	make -f ../Makefile cleanpictpdf FEYNDIR=$(FEYNDIR) TIKZDIR=$(TIKZDIR)

cleanblx:
	-rm *-blx.bib
	-rm *.bcf
	-rm *.run.xml

cleanbbl:
	-rm *.bbl

cleanglo:
	-rm *.acn *.acr *.alg
	-rm *.glg *.glo *.gls
	-rm *.ist

cleanphd:
	-rm PhD_submit.log PhD_submit.aux PhD_submit.out
	-rm PhD_submit.pdf

help:
	@echo "Possible commands:"
	@echo "guide: Compile thesis guide (guide11)"
	@echo "guide09: Compile thesis guide - texlive 2009 + bibtex"
	@echo "guide11: Compile thesis guide - texlive >=2011 + biber"
	@echo "feynmf: Run feynmf for all .tex files in $(FEYNDIR)"
	@echo "feynmp: Run feynmp for all .tex files in $(FEYNDIR)"
	@echo "tikz:   Run tikz   for all .tex files in $(TIKZDIR)"
	@echo "cleanguide:   Clean up guide  LaTeX output files"
	@echo "cleanfeynmf:  Clean up feynmf output files"
	@echo "cleanfeynmp:  Clean up feynmp output files"
	@echo "cleantikz:    Clean up tikz output files"
	@echo "cleanpictpdf: Clean up tikz and feynmp output PDF files"

test:
	@echo "Guide $(GUIDE)"
	@echo "Feynmf Feynman graphs dir: $(FEYNDIR)"
	@echo "TikZ   Feynman graphs dir: $(TIKZDIR)"
