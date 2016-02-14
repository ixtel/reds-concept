all : svgz_ emf_ pdf_

svgz_ :
	for f in sources/*.svg; do python /opt/scour/scour.py --enable-id-stripping --enable-comment-stripping --shorten-ids --renderer-workaround --enable-viewboxing --set-precision=5 --indent=none  -i "$$f" -o "$${f/sources/svgz}"; gzip -fS z "$${f/sources/svgz}"; done

emf_ :
	for f in svgz/*.svgz; do inkscape -z --export-emf="$${f//svgz/emf}" "$${f}"; done

pdf_ :
	for f in svgz/*.svgz; do inkscape -z --export-pdf="$${f//svgz/pdf}" "$${f}"; done

png_ :
	for f in svgz/*.svgz; do inkscape -z --export-png="$${f//svgz/png}" "$${f}"; pngout "$${f//svgz/png}"; done
	for f in sources/*.png; do cp "$${f}" "$${f//sources/png}"; pngout "$${f//sources/png}"; done

clean :
	rm -f svgz/*
	rm -f emf/*
	rm -f pdf/*
	rm -f png/*
