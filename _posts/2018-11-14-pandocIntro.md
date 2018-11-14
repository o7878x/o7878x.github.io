---
laytou: post
title: "Pandoc Introduction"
date: 2018-11-14
excerpt: "Introduce a useful command line tool and its basic usages"
tags: [Pandoc, usage]
comments: true
---

# Usages About Pandoc

## Introduction
If you need to convert files from one markup format into another, **pandoc** is your swiss-army knife. **Pandoc** can convert documents in (serveral dialects of) Markdown, reStructureedText, textile, HTML, DocBook, LaTeX, MediaWiki markup, TWiki markup, TikiWiki markup, Creole 1.0, Vimwiki markup, roff man, OPML, Emacs Org-Mode, Eamcs Muse, txt2tags, Microsoft Wrod docx, LibreOffice ODT, EPUB, or Haddock markup to to

- HTML formats
  XHTML, HTML5, and HTML slide shows using SLidy, reveal.js, Slideous, S5, or DZSlides

- Word processor formats
  Mircrosoft Wrod docs OpenOffice/LibreOffice ODT, OpenDocument XML, Microsoft PowerPoint

- Ebooks
  EPUB version 2 or 3, FictionBook2

- PDF
  via pdflatex, xelatex, lualatex, pdfroff, wkhtml2pdf, prince, or weasyprint.

## Installing
1. Windows
   There is a package installer at pandoc's download page. And if you prefer not to use the msi installer, we also provide a zip file that contains pandoc's binaries and documentation. Simply unzip this file and move the binaries to a directory of your choice.

2. Linux
   There is a binary package for amd64 architecture on the download page. This provides both *pandoc* and *pandoc-citeproc*. The executables are statically linked and have no dynamic dependencies or dependencies on external data files.

   Note: because of the static linking, the pandoc binary from this package cannot use lua filters that require external lua modules written in C.
   
   Both a tarball and a deb installer are provided. To install the deb:
```
sudo dpkg -i $DEB
```

## Usages
Assume there is a file *test1.md* existing inside current working directory.

To convert it to HTML, use this command:
```
pandoc test1.md -f markdown -t html -s -o test1.html
```

To create a LaTeX document, you just neede to change the command slightly:
```
pandoc test1.md -f markdown -t latex -s -o test2.tex
```

If you want to crete a PDF, you'll need to have LaTeX installed.
```
pandoc test1.md -s -o test1.pdf
```
