---
id: 65
title: 'My first impressions about LaTex'
guid: 'http://rnaufal.wordpress.com/2008/08/25/my-first-impressions-about-latex/'
lj_itemid:
    - '74'
lj_permalink:
    - 'http://rnaufal.livejournal.com/18999.html'
dsq_thread_id:
    - '102752382'
categories:
    - Uncategorized
tags:
    - latex
    - tex
    - typeface
    - typesetting
---

There’s been a good time I have wanted to try the <http://en.wikipedia.org/wiki/LaTeX>. So many times some masters / doctorate friends told about it for me very well. When I started doing my post-graduate course in [Software Engineering](http://en.wikipedia.org/wiki/Software_engineering) at [ITA](http://www.ita.br/), I knew it was time to test this powerful too. And this moment has come. For those who don’t know LaTex, it was created by [Leslie Lamport](http://en.wikipedia.org/wiki/Leslie_Lamport) in the 80’s and it’s built on top of the TeX tool, which allows the author of academic works obtain high-quality typeface. The [TeX](http://en.wikipedia.org/wiki/TeX) is a typography software developed by [Donald Knuth](http://en.wikipedia.org/wiki/Donald_Knuth) in the 70’s for the publication of texts with great layout and typographical quality, particularly those with focus on mathematical equations. Knuth, at that time, developed the TeX to write his most famous books’ collection named [The Art of Computer Programming](http://en.wikipedia.org/wiki/The_Art_of_Computer_Programming), because he didn’t find a decent typesetting system at the time. Basically, the LaTeX adds a set of commands in the text that define how the system’s processing TeX will format it.  
The text is entered within several LaTeX commands, as chunks of code in any programming language. These commands define the font type, the text formatting, chapters, sections, special characters, margin size, and so on. This makes the system different from the [WYSIWYG](http://en.wikipedia.org/wiki/WYSIWYG) methodology, in which the text is written exactly as it will be seen in the final result. All LaTex command begins with a backslash `(\)`. LaTeX files are created with the **.tex** extension and the text should be compiled and the result file could be a binary [DVI](http://en.wikipedia.org/wiki/Device_independent_file_format) or PDF file. The fact of having to compile the text may represent a difficulty to the editor of the text, but the final result is very good, with high-quality typeface, as if the text had been edited by someone profession on the area.  
The major advantages that I see in using LATEX instead of a WYSIWYG common editor, such as Word or OpenOffice, are:

1. The LATEX lets you define how the text should be presented and formatted in the same way as the CSS works with HTML / XHTML. The idea is that you don’t worry about how the text should be formatted. Leave this work to TEX!
2. Mathematical formulas, displayed by LATEX, are extremely elegant.
3. LATEX manages all the numbering of chapters, sections, lists, figures and tables, footers, etcetera..
4. TEX is portable and free, so that means it works in most existing hardware.
5. You can tell the LATEX additional libraries to specify, for example, references for a second rule.
6. Do not worry about the layout, only within the structure of the document!

As a quick example, we would have the following construction in LATEX:

`\documentclass[a4paper]{article}<br></br>\begin{document}<br></br>Your text here….<br></br>\end{document}`

The code sets up a minimum LaTex file, which is defined using the article class in a A4 size paper. The tags `\begin{document} and \end{document}` must contain the text to be entered. These commands, when compiled by Tex within the **.pdf** output document option already produce an excellent final result, very different from the Word one. You can find good references on the package [here](http://www.ctan.org/pub/tex-archive/info/lshort/english/lshort.pdf). And I leave here a challenge: even if you are a fan of Word, try to create a document in LaTex once and see the final result! I bet then you won’t stop writing your texts without it!

Portuguese version: http://log4dev.com/2008/07/29/minhas-primeiras-impressoes-sobre-o-latex/