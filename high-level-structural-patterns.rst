.. role:: html(code)
	:language: html
.. role:: css(code)
	:language: css
.. role:: bash(code)
	:language: bash
.. role:: path(code)
.. role:: italics(emphasis)
	:class: i

##############################
High Level Structural Patterns
##############################

Section should contain high-level structural patterns for common formatting situations.

Examples:

#. Headers
#. Poetry/verse
#. Plays
#. Letters
#. Images (in text; SVG format elsewhere)
#. LoI
#. Endnotes
#. ???

*******
Headers
*******

#. :html:`<hx>` tags (i.e., :html:`<h1>`–:html:`<h6>`)  are used for headers of sections that are structural divisions of a document. :html:`<hx>` tags *are not* used for headers of components that are not in the table of contents. For example, they would not be used to mark up the the title of a short poem in a chapter, where the poem itself is not a structural component of the larger ebook.

#. A section containing an :html:`<hx>` appears in the table of contents.

#. The book's title is implicitly at the :html:`<h1>` level, even if not present in the ebook. Because of the implicit :html:`<h1>`, all other sections begin at :html:`<h2>`.

#. Each :html:`<hx>` tag uses the correct number for the section's heading level in the overall book, *not* the section's heading level in the individual file. For example, given an ebook with a file named :path:`part-2.xhtml` containing:

	.. code:: html

		<section id="part-2" epub:type="part">
			<h2 epub:type="title">Part <span epub:type="z3998:roman">II</span></h2>
		</section>

	Consider this example for the file :path:`chapter-2-3.xhtml`:

	.. class:: wrong

		.. code:: html

			<section id="part-2" epub:type="part">
				<section id="chapter-2-3" epub:type="chapter">
					<h1 epub:type="title z3998:roman">III</h1>
					...
				</section>
			</section>

	.. class:: corrected

		.. code:: html

			<section id="part-2" epub:type="part">
				<section id="chapter-2-3" epub:type="chapter">
					<h3 epub:type="title z3998:roman">III</h3>
					...
				</section>
			</section>

#. Each :html:`<hx>` tag has a direct parent :html:`<section>` tag.

	#. Sections without titles:

		.. code:: html

			<h2 epub:type="title z3998:roman">XI</h2>

	#. Sections with titles but no ordinal (i.e. chapter) numbers:

		.. code:: html

			<h2 epub:type="title">A Daughter of Albion</h2>

	#. Sections with titles and ordinal (i.e. chapter) numbers:

		.. code:: css

			span[epub|type~="subtitle"]{
				display: block;
				font-weight: normal;
			}

		.. code:: html

			<h2 epub:type="title">
				<span epub:type="z3998:roman">XI</span>
				<span epub:type="subtitle">Who Stole the Tarts?</span>
			</h2>

	#. Sections titles and subtitles but no ordinal (i.e. chapter) numbers:

		.. code:: css

			span[epub|type~="subtitle"]{
				display: block;
				font-weight: normal;
			}

		.. code:: html

			<h2 epub:type="title">
				<span>An Adventure</span>
				<span epub:type="subtitle">(A Driver’s Story)</span>
			</h2>

	#. Sections that require titles, but that are not in the table of contents:

		.. code:: css

			header{
				font-variant: small-caps;
				margin: 1em;
				text-align: center;
			}

		.. code:: html

			<header>
				<p>The Title of a Short Poem</p>
			</header>

********
Play CSS
********

.. code:: css

	[epub|type~="z3998:drama"]{
		border-collapse: collapse;
	}

	[epub|type~="z3998:drama"] tr:first-child td{
		padding-top: 0;
	}

	[epub|type~="z3998:drama"] tr:last-child td{
		padding-bottom: 0;
	}

	[epub|type~="z3998:drama"] td{
		vertical-align: top;
		padding: .5em;
	}

	[epub|type~="z3998:drama"] td:last-child{
		padding-right: 0;
	}

	[epub|type~="z3998:drama"] td:first-child{
		padding-left: 0;
	}

	[epub|type~="z3998:drama"] td[epub|type~="z3998:persona"]{
		hyphens: none;
		text-align: right;
		width: 20%;
	}

	[epub|type~="z3998:drama"] td p{
		text-indent: 0;
	}

	table[epub|type~="z3998:drama"],
	[epub|type~="z3998:drama"] table{
		margin: 1em auto;
	}

	[epub|type~="z3998:stage-direction"]{
		font-style: italic;
	}

	[epub|type~="z3998:stage-direction"]::before{
		content: "(";
		font-style: normal;
	}

	[epub|type~="z3998:stage-direction"]::after{
		content: ")";
		font-style: normal;
	}

	[epub|type~="z3998:persona"]{
		font-variant: all-small-caps;
	}

******
Images
******

#.  All :html:`<img>` tags are required to have an :html:`alt` attribute that uses prose to describe the image in detail; this is what screen reading software will be read aloud.

	-  Describe the image itself in words, which is not the same as writing a caption or describing its place in the book.
	-  Alt text must be full sentences ended with periods or other appropriate punctuation. Sentence fragments, or complete sentences without ending punctuation, are not acceptable.

	For example:

	.. class:: wrong

		.. code:: html

			<img alt="The illustration for chapter 10" src="...">

	.. class:: wrong

		.. code:: html

			<img alt="Pierre's fruit-filled dinner" src="...">

	.. class:: corrected

		.. code:: html

			<img alt="An apple and a pear inside a bowl, resting on a table." src="...">

	Note that the :html:`alt` text does not necessarily have to be the same as text in the image’s :html:`<figcaption>` element.  You can use :html:`<figcaption>` to write a concise context-dependent caption.

#.  Include an :html:`epub:type` attribute to denote the type of image. Common values are :html:`z3998:illustration` or :html:`z3998:photograph`.

#.  For some images, it’s helpful to invert their colors when the ereader enters night mode.  This is particularly true for black-and-white line art and woodcuts. (Note *black-and-white*, i.e. only two colors, **not** grayscale!)  Include the :html:`se:image.color-depth.black-on-transparent` semantic in the :html`<img>` tag’s :html:`epub:type` to enable color inversion in some ereaders.
	For that sort of art, save the images as PNG files with a transparent background. You can make the background transparent by using the “Color to alpha” tool available in many image editing programs, like `the GIMP <https://www.gimp.org/>`__.

#.  :html:`<img>` tags that are meant to be aligned on the block level should be contained in a parent :html:`<figure>` tag, with an optional :html:`<figcaption>` sibling.

	- If contained in a :html:`<figure>` tag, the image’s :html:`id` attribute must be on the :html:`<figure>` tag.

#.  Some sources of illustrations may have scanned them directly from the page of an old book, resulting in yellowed, dingy-looking scans of grayscale art. In these cases, convert the image to grayscale to remove the yellow tint.

Complete HTML and CSS markup examples
=====================================

.. code:: css

	/* If the image is meant to be on its own page, use this selector... */
	figure.full-page{
		margin: 0;
		max-height: 100%;
		page-break-before: always;
		page-break-after: always;
		page-break-inside: avoid;
		text-align: center;
	}

	/* If the image is meant to be inline with the text, use this selector... */
	figure{
		margin: 1em auto;
		text-align: center;
	}

	/* In all cases, also include the below styles */
	figure img{
		display: block;
		margin: auto;
		max-width: 100%;
	}

	figure + p{
		text-indent: 0;
	}

	figcaption{
		font-size: .75em;
		font-style: italic;
	}

.. code:: html

	<figure id="image-10">
		<img alt="An apple and a pear inside a bowl, resting on a table." src="../images/image-10.jpg" epub:type="z3998:photograph"/>
		<figcaption>The Monk’s Repast</figcaption>
	</figure>

.. code:: html

	<figure class="full-page" id="image-11">
		<img alt="A massive whale breaching the water, with a sailor floating in the water directly within the whale’s mouth." src="../images/image-11.jpg" epub:type="z3998:illustration"/>
		<figcaption>The Whale eats Sailor Jim.</figcaption>
	</figure>

********
Endnotes
********

#.  All footnotes and endnotes should live in :path:`endnotes.xhtml`. The markup for that file should look like:

	.. code:: html

		<section id="endnotes" epub:type="rearnotes">
			<h2 epub:type="title">Endnotes</h2>
			<ol>
				<li id="note-1" epub:type="rearnote">
					<p>… <a href="../text/chapter-1.xhtml#noteref-1" epub:type="se:referrer">↩</a></p>
				</li>
			</ol>
		</section>

#.  The endnotes’ :html:`id` attributes should be in order and go up by one for each note. The number after the :html:`noteref-` fragment in the referrer link should match the :html:`id` attribute’s number.

#.  Each endnote’s referrer link should point to the correct chapter.

#.  Within the chapter, the link to the endnote should be placed at the appropriate point (after the punctuation if at the end of a sentence). The number in the fragment reference, :html:`id` and text should match each other and the corresponding note in :path:`endnotes.xhtml`. The markup should look like:

	.. code:: html

		<a href="../text/endnotes.xhtml#note-1" id="noteref-1" epub:type="noteref">1</a>

#.  The referrer link should go at the end of the paragraph containing the endnote’s text. If the endnote is multiple paragraphs long then it should be placed at the end of the last paragraph. If the endnote is particularly complex and ends with a quotation, song or something that’s not a paragraph, the link should be placed in an otherwise empty paragraph at the end of the endnote.

#.  If a new note is added before existing ones it can be painful to renumber the later notes. To help with that, there’s a :bash:`reorder-endnotes` tool. Call it with either :bash:`--increment` or :bash:`--decrement`, the endnote number you want to reorder from and the directory you want to reorder.
