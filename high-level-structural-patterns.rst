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
