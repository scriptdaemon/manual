.. role:: html(code)
	:language: html
.. role:: css(code)
	:language: css
.. role:: bash(code)
	:language: bash
.. role:: path(code)
.. role:: italics(emphasis)
	:class: i

#########################
The structure of an ebook
#########################

.. class:: data-start-at-3

****************
Major partitions
****************

We can consider that all books, including ebooks, consist of these major partitions, in this order:

	- **Front Matter**: material which appears prior to the main content of the work, which might include such items as a dedication, an epigraph, an introduction and so on.

	- **Body Matter**: the main content of the book. This is typically divided into chapters or in the case of a collection, individual stories or articles. It may be structured at the highest level by the author into larger divisions such as volumes or parts. It may include a prologue and/or an epilogue.

	- **Back Matter**: material which follows the main content, which might include an appendix, an afterword, and so on.

These terms become important when building the Table of Contents (ToC). The 'Landmarks' section of the ToC requires items to be labelled with the appropriate partition identifier. See `ToC Patterns`_ for more information about the ToC.

.. _ToC Patterns: toc-patterns.html

******************
Sections of a Book
******************

A book may include any of the following sections, which are presented here in the order they are likely to occur in a a typical book.

Cover
=====
The cover presents the outer appearance of the book, usually consisting of an image, the title of the book and the author's name. For Standard Ebooks productions, the cover is an SVG image generated from a supplied source image, the book title and author name using the :path:`build-images` tool.

Title page
==========
The title page lists the title of the book and the author's name. or Standard Ebooks productions, the title page :path:`./text/titlepage.xhtml` includes an SVG image generated from a supplied image, the book title and author name using the :path:`build-images` tool. Using an SVG in this way avoids the need to embed any fonts.

The titlepage is always part of the front matter of the book.

Imprint
=======
The imprint contains information about the publisher of the book. In the case of Standard Ebooks, we supply a template :path:`./text/imprint.xhtml` with our standard release information and the Standard Ebooks logo. The only thing which needs to be changed in this template are the references and links for the source of the content text and page scans.

The imprint is always part of the front matter of the book.

Dedication
==========
A dedication is an inscription at the start of a work and is usually a tribute to some person or persons who the author wishes to honour. There is no template supplied by Standard Ebooks, but it can be based on dedications in other projects. It must be placed in a file :path:`./text/dedication.xhtml`.

The dedication is always part of the front matter of the book.

Epigraph
========
An epigraph is a quotation at the start of a book which may set the mood or inspire thoughts about the work to come. There is no template supplied by Standard Ebooks, but it can be based on epigraphs in other projects. It must be placed in a file :path:`./text/epigraph.xhtml`.

If the epigraph is a poem or quotation from poetry, it must follow the standards for verse described in `High-Level Structural Patterns`_

.. _High-Level Structural Patterns: high-level-structural-patterns.html

The epigraph is always part of the front matter of the book.

Acknowledgements
================
Acknowledgements are a list of persons or organizations who the author wishes to thank, generally for helping with the creation of the book. There is no template supplied by Standard Ebooks, but it can be based on acknowledgements in other projects. It must be placed in a file :path:`./text/acknowledgements.xhtml`.

The acknowledgements can be either part of the front matter or of the back matter of the book, depending on where the author placed them.

Foreword
========
A foreword is a preliminary section, generally written by someone other than the author. There is no template supplied by Standard Ebooks, but it can be based on forewords in other projects. It must be placed in a file :path:`./text/foreword.xhtml`.

The foreword is always part of the front matter of the book.

Preface
=======
A preface is a preliminary section which states the subject of the book and its aims. A preface is generally written by the author of the work. There is no template supplied by Standard Ebooks, but it can be based on prefaces in other projects. It must be placed in a file :path:`./text/preface.xhtml`.

The preface is always part of the front matter of the book.

Introduction
============
An introduction is typically found in non-fiction works. It is written by the book's author, forms part of the text of the book and sets out the book's main argument. There is no template supplied by Standard Ebooks, but it can be based on introductions in other projects. It must be placed in a file :path:`./text/introduction.xhtml`.

An introduction is part of the body matter.

The distinction between foreword, preface and introduction is a subtle one and Standard Ebooks authors should generally follow how the author has chosen to title and place these sections. However, more information on the distinction between these terms can be found at the `Writers and Editors`_ website.

.. _Writers and Editors: http://www.writersandeditors.com/preface_foreword_or_introduction_57375.htm

Prologue
========
A prologue is generally found only in works of fiction. It may introduce characters, set up background information, or bring forward a critical part of the action to which the story leads. A prologue should therefore have similar structure to the chapters of a book. There is no template supplied by Standard Ebooks, but it can be based on prologues in other projects. It must be placed in a file :path:`./text/prologue.xhtml`.

A prologue is part of the body matter.

Epilogue
========
An epilogue is generally found only in works of fiction. It would typically wind up the action or briefly tell the subsequent history of major characters. An epilogue should therefore have similar structure to the chapters of a book. There is no template supplied by Standard Ebooks, but it can be based on epilogues in other projects. It must be placed in a file :path:`./text/epilogue.xhtml`.

An epilogue is part of the body matter.

Afterword
=========
An afterword is a concluding section of a book, typically but not necessarily written b the author, which stands outside the main story of a work of fiction, or the main argument of a work of non-fiction. It may add additional information or comment on the book and its production. There is no template supplied by Standard Ebooks, but it can be based on afterwords in other projects. It must be placed in a file :path:`./text/afterword.xhtml`.

An afterword is always part of the back matter of a book.

List of Illustrations
=====================
The list of illustrations (LoI) is an index to the illustrations in a book. The items are included as part of a list and hyperlinked to the points in the text where the illustration appears. There is no template supplied by Standard Ebooks, but it can be based on LoIs in other projects. It must be placed in a file :path:`./text/loi.xhtml`.

See `List of Illustrations`_ for more information about the LoI.

.. _List of Illustrations: list-of-illustrations.html

Endnotes
========
The endnotes are a list of notes to the text, and each item is given a unique sequential number and hyperlinked to the point in the text to which the note refers. Footnotes in the original text are to be converted to endnotes.  There is no template supplied by Standard Ebooks, but it can be based on endnotes in other projects. It must be placed in a file :path:`./text/endnotes.xhtml`.

The endnotes are always part of the back matter of a book.

See Endnotes_ for more information about the endnotes.

.. _Endnotes: endnotes.html

Colophon
========
The colophon contains information about the publisher of the book, the author, the original publication date, the edition, its publication date, the cover artist and other information relevant to the particular release of a book. In the case of Standard Ebooks, we supply a template :path:`./text/colophon.xhtml` with our standard release information. Several items in this file need to be changed to match the particular work.

Copyright Page
==============
The copyright page includes information about the copyright status of the work. In the case of Standard Ebooks, all our productions are released into the public domain. We supply a standard page :path:`./text/uncopyright.xhtml` which must not be altered.

Copyright pages are usually part of the front matter of a book, but in the case of Standard Ebooks productions, it is always part of the the back matter of the book, and indeed, always the last item in the book.
