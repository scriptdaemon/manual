.. role:: html(code)
	:language: html
.. role:: css(code)
	:language: css
.. role:: bash(code)
	:language: bash
.. role:: path(code)
.. role:: italics(emphasis)
	:class: i

###################
Semantic Inflection
###################

.. class:: data-start-at-4

The epub spec allows for `semantic inflection <https://idpf.github.io/epub-vocabs/structure/>`__, which is a way of adding semantic metadata to elements in the ebook document. For example, an ebook producer may want to convey that the contents of a certain :html:`<section>` are part of a chapter. They would do that by using the :html:`epub:type` attribute:

.. code:: html

	<section epub:type="chapter">...</section>

#.	The epub spec includes a `vocabulary <https://idpf.github.io/epub-vocabs/structure/>`__ that can be used in the :html:`epub:type` attribute. This vocabulary has priority when selecting a semantic keyword, even if other vocabularies contain the same one.

#.	The epub spec may not contain a keyword to describe the semantics of a particular element. In that case, the `z3998 vocabulary <http://www.daisy.org/z3998/2012/vocab/structure/>`__ is consulted next.

	Keywords using this vocabulary are preceded by the :html:`z3998` namespace.

	.. code:: html

		<blockquote epub:type="z3998:letter">...</blockquote>

#.	If the z3998 vocabulary doesn’t have an appropriate keyword, the `Standard Ebooks vocabulary </vocab/1.0>` is consulted next.

	Keywords using this vocabulary are preceded by the :html:`se` namespace.

	Unlike other vocabularies, the Standard Ebooks vocabulary is organized heirarchally. A complete vocabulary entry begins with the root vocabulary entry, with subsequent children separated by :html:`.`.

	.. code:: html

		The <i epub:type="se:name.vessel.ship"><abbr class="initialism">HMS</abbr> Bounty</i>.

#.	The :html:`epub:type` attribute can have multiple keywords separated by spaces, even if the vocabularies are different.

	.. code:: html

		<section epub:type="chapter z3998:letter">...</section>

#.	In general, children elements inherit the semantics of their parent element.

	In this example, both chapters are considered to be “non-fiction,” because they inherit it from the :html:`<body>` element:

	.. code:: html

		<body epub:type="z3998:non-fiction">
			<section id="chapter-1" epub:type="chapter">
				<h2 epub:type="title z3998:roman">I</h2>
				...
			</section>
			<section id="chapter-2" epub:type="chapter">
				<h2 epub:type="title z3998:roman">II</h2>
				...
			</section>
		</body>
