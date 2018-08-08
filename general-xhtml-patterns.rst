.. role:: html(code)
	:language: html
.. role:: css(code)
	:language: css
.. role:: bash(code)
	:language: bash
.. role:: path(code)
.. role:: italics(emphasis)
	:class: i

######################
General XHTML Patterns
######################

.. class:: data-start-at-5

Intro.

************************
The :html:`id` attribute
************************

:html:`id` attributes of :html:`<section>` elements
===================================================

#.	Each :html:`<section>` has an :html:`id` attribute identical to the filename containing that :html:`<section>`, without the trailing extension.

#.	In files containing multiple :html:`<section>` elements, each :html:`<section>` has an :html:`id` attribute identical to what the filename *would* be if the section was in an individual file, without the trailing extension.

	.. class:: corrected

		.. code:: html

			<body epub:type="bodymatter z3998:fiction">
				<article id="the-fox-and-the-grapes" epub:type="volume se:short-story">
					<h2 epub:type="title">The Fox and the Grapes</h2>
					<p>...</p>
				</article>
				<article id="the-goose-that-laid-the-golden-eggs" epub:type="volume se:short-story">
					<h2 epub:type="title">The Goose That Laid the Golden Eggs</h2>
					<p>...</p>
				</article>
			</body>

:html:`id` attributes of other elements
=======================================

#.	Elements that are not :html:`<section>` elements do not have an :html:`id` attribute, unless a part of the ebook, like an endnote, refers to a specific point in the book, and a direct link is desirable.

#.	:html:`id` attributes are generally used to identify parts of the document that a reader may wish to navigate to using a hash in the URL. That generally means major structural divisions.

#.	:html:`id` attributes are not used as hooks for CSS styling.

#.	If an element that is not a :html:`<section>` requires an :html:`id` attribute, the attribute’s value is the name of the tag followed by :path:`-N`, where :path:`N` is the sequence number of the tag start at :path:`1`.

	.. class:: corrected

		.. code:: html

			<p>See <a href="#p-4">this paragraph</a> for more details.</p>
			<p>...</p>
			<p>...</p>
			<p id="p-4">...</p>
			<p>...</p>

********************
:html:`<title>` tags
********************

#.	The :html:`<title>` tag contains an appropriate description of the local file only. It does not contain the book title.

Titles of files that are an individual chapter or part division
===============================================================

#.	Convert chapter or part numbers that are in Roman numerals to decimal numbers. Do not convert other Roman numerals that may be in the chapter title.

	.. class:: corrected

		.. code:: html

			<title>Chapter 10</title>

#.	If a chapter or part is only an ordinal and has no title or subtitle, the :html:`<title>` tag is :html:`Chapter` followed by the chapter number.

	.. class:: corrected

		.. code:: html

			<title>Chapter 4</title>
			...
			<h2 epub:type="title z3998:roman">IV</h2>
			...
			<p>The chapter body...</p>

#.	If a chapter or part has a title or subtitle, the :html:`<title>` tag is :html:`Chapter`, followed by the chapter number in decimal, followed by a colon and a single space, followed by the title or subtitle.

	.. class:: corrected

		.. code:: html

			<title>Chapter 6: The Reign of Louis XVI</title>
			...
			<h2 epub:type="title z3998:roman">
				<span>VI</span>>
				<span epub:type="subtitle">The Reign of Louis <span epub:type="z3998:roman">XVI</span></h2>
			...
			<p>The chapter body...</p>

Titles of files that are not chapter or part divisions
======================================================

#.	Files that are not a chapter or a part division, like a preface, introduction, or epigraph, have a :html:`<title>` tag that contains the complete title of the section.

	.. class:: corrected

		.. code:: html

			<title>Preface</title>

#.	If a file contains a section with a title or subtitle, the :html:`<title>` tag contains the title, followed by a colon and a single space, followed by the title or subtitle.

	.. class:: corrected

		.. code:: html

			<title>Quevedo and His Works: With an Essay on the Picaresque Novel</title>

************************************
Ordered/numbered and unordered lists
************************************

#.	All :html:`<li>` children of :html:`<ol>` and :html:`<ul>` tags have at least one direct child block-level tag. This is usually a :html:`<p>` tag, but not necessarily; for example, a :html:`<blockquote>` tag might also be appropriate.

	.. class:: wrong

		.. code:: html

			<ul>
				<li>Don’t forget to feed the pigs.</li>
			</ul>

	.. class:: corrected

		.. code:: html

			<ul>
				<li>
					<p>Don’t forget to feed the pigs.</p>
				</li>
			</ul>
