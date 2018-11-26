#
# Makefile to run pdflatex on different covers
#
# EXTRACMD = --shell-escape

.PHONY: cover_test
	cleancover \
	help test

cover_test:
	pdflatex  $(EXTRACMD) cover_test
	biber cover_test
	pdflatex  $(EXTRACMD) cover_test

cleanall: clean

clean: cleancover

cleancover:
	-rm cover_test.log cover_test.aux cover_test.toc cover_test.out
	-rm cover_test.bcf cover_test.run.xml
	-rm cover_test.blg cover_test.bbl cover_test.pdf

help:
	@echo "Possible commands:"
	@echo "cover_test: Test covers"
	@echo "cleancover: Clean up cover test files"

test:
	@echo "Nothing to test!"
