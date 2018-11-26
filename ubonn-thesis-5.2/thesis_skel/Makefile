# Makefile to run latex, dvips, and pdflatex on a thesis
# Can also run feynmf/feynmp/tikz on files in a directory

THESIS = mythesis
# EXTRACMD = --shell-escape
FEYNDIR = ../feynmf
FEYNFILES = $(wildcard $(FEYNDIR)/*.tex)
TIKZDIR = ../tikz
TIKZFILES = $(wildcard $(TIKZDIR)/*.tex)
ifdef file
FEYNFILES = $(FEYNDIR)/$(file).tex
TIKZFILES = $(TIKZDIR)/$(file).tex
endif
BIBTEX = biber
AWKDIR=..

.PHONY: thesis cover \
	feynmf feynmp tikz \
	cleanthesis cleancover \
	cleanfeynmf cleanfeynmp cleantikz cleanpictpdf \
	cleanblx cleanbbl \
	cleanglo \
	help test

thesis: thesis11

# - in front of bibtex means compilation continues even if there is an error
thesis09: $(THESIS).tex *.tex *.bib
	pdflatex   $(EXTRACMD) $(THESIS)
	-bibtex $(THESIS)
	# makeglossaries $(THESIS)
	pdflatex   $(EXTRACMD) $(THESIS)
	pdflatex   $(EXTRACMD) $(THESIS)

thesis11: $(THESIS).tex *.tex *.bib
	pdflatex   $(EXTRACMD) $(THESIS)
	$(BIBTEX)  $(THESIS)
	# makeglossaries $(THESIS)
	pdflatex   $(EXTRACMD) $(THESIS)
	pdflatex   $(EXTRACMD) $(THESIS)

cover:
	pdflatex   $(EXTRACMD) cover_only
	pdflatex   $(EXTRACMD) cover_only

feynmf:
	make -f ../Makefile FEYNDIR=$(FEYNDIR) FEYNFILES="$(FEYNFILES)" \
	 AWKDIR=$(AWKDIR) feynmf

feynmp:
	make -f ../Makefile FEYNDIR=$(FEYNDIR) FEYNFILES="$(FEYNFILES)" \
	 AWKDIR=$(AWKDIR) feynmp

tikz:
	make -f ../Makefile TIKZDIR=$(TIKZDIR) TIKZFILES="$(TIKZFILES)" tikz

thesis_feynmf:
	feynmf $(THESIS)

cleanall: clean cleanbbl cleanpictpdf

clean: cleanthesis cleancover \
	cleanfeynmf cleanfeynmp cleantikz \
	cleanblx cleanglo

cleanthesis:
	-rm $(THESIS).log $(THESIS).aux $(THESIS).toc
	-rm $(THESIS).lof $(THESIS).lot $(THESIS).out
	-rm $(THESIS).blg $(THESIS).bbl $(THESIS).pdf
	-rm *.aux

cleancover:
	-rm cover_only.log cover_only.aux cover_only.out
	-rm cover_only.pdf

cleanfeynmf:
	-rm *.mf *.tfm *.t1 *.600gf *.600pk *.log
	-rm feynmf_all.* feynmf_files.inp

cleanfeynmp:
	-rm *.1 *.log *.mp *.t1
	-rm feynmf_all.* feynmf_files.inp

cleantikz:
	-rm tikz/*.log tikz/*.aux

cleanpictpdf:
	-rm feynmf/*.pdf
	-rm tikz/*.pdf

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

help:
	@echo "Possible commands:"
	@echo "new [THESIS=dirname]: Set up a new thesis"
	@echo "thesis: Compile complete thesis (thesis11)"
	@echo "thesis09: Compile complete thesis - texlive 2009 + bibtex"
	@echo "thesis11: Compile complete thesis - texlive >=2011 + biber"
	@echo "feynmf: Run feynmf for all .tex files in $(FEYNDIRNAME)"
	@echo "feynmp: Run feynmp for all .tex files in $(FEYNDIRNAME)"
	@echo "tikz:   Run tikz for all .tex files in $(TIKZDIRNAME)"
	@echo "cleanthesis: Clean up thesis LaTeX output files"
	@echo "cleanfeynmf: Clean up feynmf output files"
	@echo "cleanbbl:    Clean up thesis bbl files"
	@echo "cleanblx:    Clean up thesis biber files"
	@echo "cleantikz:   Clean up tikz output files"
	@echo "cleanglo:    Clean up glossary output files"

test:
	@echo "Thesis $(THESIS)"
	@echo "Feynmf Feynman graphs dir: $(FEYNDIRNAME)"
	@echo "Feynmf Feynman graphs files: $(FEYNFILES)"
	@echo "TikZ   Feynman graphs dir: $(TIKZDIRNAME)"
	@echo "TikZ   Feynman graphs files: $(TIKZFILES)"
