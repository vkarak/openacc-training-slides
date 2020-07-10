.PHONY: all clean clean-files clean-figs

LATEX = pdflatex
LATEX_OPTIONS =
TARGET_EN = sysinfo.pdf
TARGET = $(TARGET_EN)
TARGET_BASE = $(basename $(TARGET))
SOURCES_EN = sysinfo.tex intro.tex ssh.tex compile.tex run.tex vim.tex scp.tex repo.tex
INC = $(SOURCES_EN) beamerthemeCSCS.sty

CLEANFILES = $(TARGET_BASE).pdf \
	*.ps *.log *.bak *.bbl *.aux *.blg *.dvi *.toc *.out *.nav *.snm *.vrb \
	*.listing

RM = /bin/rm -f
figs = \
	cscs_images/eth_logo.pdf \
	cscs_images/cscs_logo.pdf \
	cscs_images/cscs_entrance_painting.pdf \
	cscs_images/cscs_logo_fullname.pdf \
	cscs_images/cscs_machine_room.pdf \
	cscs_images/cscs_external.pdf \
	cscs_images/cscs_entrance_equations.pdf

all: $(TARGET)

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

clean:
	$(RM) $(CLEANFILES)
