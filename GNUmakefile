all: p.pdf

.PHONY: FORCE
p.pdf:  header FORCE
	scripts/latexrun p.tex

header: 
	printf '\\gdef\\therev{%s}\n\\gdef\\thedate{%s}\n' `git rev-parse --short HEAD` "`git log -1 --format='%ci' HEAD`" > rev.tex

abs: abstract.tex
	cat $< | \
	    sed -e 's/\\emph//g' | \
	    sed -e 's/\\cite{.*}//g' | \
	    sed -e 's/\\eg/e.g./g' | \
	    sed -e 's/{//g' | \
	    sed -e 's/}//g' | \
	    sed -e 's/~/ /g' | \
	    sed -e '/^%/ d' | \
	    fmt -w72 > abstract.txt

.PHONY: clean
clean:
	scripts/latexrun --clean-all p.tex
	rm -f abstract.txt