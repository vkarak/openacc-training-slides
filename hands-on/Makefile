.PHONY: all clean clean-files clean-figs

LATEX = xelatex
LATEX_OPTIONS =
TARGET_EN = hands-on-slides.pdf
TARGET = $(TARGET_EN)
TARGET_BASE = $(basename $(TARGET))
SOURCES_EN = hands-on-slides.tex
INC = $(SOURCES_EN) beamerthemeCSCS.sty

CLEANFILES = $(TARGET_BASE).pdf \
	*.ps *.log *.bak *.bbl *.aux *.blg *.dvi *.toc *.out *.nav *.snm *.vrb \
	*.listing

RM = /bin/rm -f
figs = \
	cscs_images/image1.eps \
	cscs_images/image2.eps \
	cscs_images/image3.eps \
	cscs_images/image4.eps \
	cscs_images/image5.eps \
	cscs_images/image6.eps \
	cscs_images/image7.eps

all: $(TARGET)
clean: clean-files clean-figs

$(TARGET): $(figs) $(TARGET_BASE).tex $(INC)
	outfile=`mktemp .tex.XXXXXX`; \
	echo 'Rerun' > $$outfile; \
	until ! grep 'Rerun' $$outfile; do \
		$(LATEX) $(LATEX_OPTIONS) $(TARGET_BASE).tex | tee $$outfile; \
	done; \
	$(RM) $$outfile

$(TARGET_BASE).bbl: $(TARGET_BASE).bib
	$(LATEX) $(LATEX_OPTIONS) $(TARGET_BASE).tex && bibtex $(TARGET_BASE); \
	outfile=`mktemp .tex.XXXXXX`; \
	echo 'Rerun' > $$outfile; \
	until ! grep 'Rerun' $$outfile; do \
		$(LATEX) $(LATEX_OPTIONS) $(TARGET_BASE).tex | tee $$outfile; \
	done; \
	$(RM) $$outfile

# Some latex installations need the eps files as well
%.eps: %.pdf
	@echo Converting $< to $@ ...; \
	pdftops -eps $<

clean-files:
	$(RM) $(CLEANFILES)

clean-figs:
	$(RM) $(figs)
