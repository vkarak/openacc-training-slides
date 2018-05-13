.PHONY: all clean clean-files clean-figs

LATEX = pdflatex
LATEX_OPTIONS =
TARGET_EN = sysinfo.pdf
TARGET = $(TARGET_EN)
TARGET_BASE = $(basename $(TARGET))
SOURCES_EN = sysinfo.tex intro.tex ssh.tex compile.tex run.tex vim.tex scp.tex
INC = $(SOURCES_EN) beamerthemeCSCS.sty

CLEANFILES = $(TARGET_BASE).pdf \
	*.ps *.log *.bak *.bbl *.aux *.blg *.dvi *.toc *.out *.nav *.snm *.vrb \
	*.listing

RM = /bin/rm -f
figs = \
	cscs_images/eth_logo.eps \
	cscs_images/cscs_logo.eps \
	cscs_images/cscs_entrance_painting.eps \
	cscs_images/cscs_logo_fullname.eps \
	cscs_images/cscs_machine_room.eps \
	cscs_images/cscs_external.eps \
	cscs_images/cscs_entrance_equations.eps

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
