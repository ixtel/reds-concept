How to build the alternative formats
====================================

1. Save the elements as separate SVG files into ./raw

2. Use scour and gzip to create clean SVGZ versions of the source SVG files (svgo is not reliable, yet)

    for f in ./sources/*.svg; do python /opt/scour/scour.py --enable-id-stripping --enable-comment-stripping --shorten-ids --renderer-workaround --enable-viewboxing --set-precision=5 --indent=none  -i "$f" -o "${f/sources/svgz}"; done
    gzip -S z svgz/*.svg

2. Create the alternative formats from the cleaned SVGZ files:

    for f in ./svgz/*.svgz; do inkscape -z --export-emf="${f//svgz/emf}" "${f}"; done
    for f in ./svgz/*.svgz; do inkscape -z --export-pdf="${f//svgz/pdf}" "${f}"; done
    for f in ./svgz/*.svgz; do inkscape -z --export-png="${f//svgz/png}" "${f}"; done
