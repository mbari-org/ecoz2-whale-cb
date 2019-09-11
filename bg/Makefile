NAME=lpckw

pdf: $(NAME).pdf

%.pdf: %.tex %.bib
	pdflatex $<
	bibtex $(NAME)
	pdflatex $<

clean:
	rm -f *.aux *.bbl *.blg *.log
