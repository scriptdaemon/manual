.. role:: html(code)
	:language: html
.. role:: css(code)
	:language: css
.. role:: bash(code)
	:language: bash
.. role:: path(code)
.. role:: italics(emphasis)
	:class: i

########
Metadata
########

.. class:: data-start-at-10

Metadata in a Standard Ebooks epub is stored in the :path:`./src/epub/content.opf` file. The file contains some boilerplate that an ebook producer won’t have to touch, and a lot of information that they *will* have to touch as an ebook is produced.

Follow the general structure of the :path:`content.opf` file present in the tools :path:`./templates/` directory. Don’t rearrange the order of anything in there.

*****************
General URL rules
*****************

#.	URLs used in metadata are https where possible.

#.	URLs used in metadata do not contain query strings, or if a query string is required, only contain the minimum necessary query string to render the base resource.

#.	URLs used for Project Gutenberg page scans look like: :path:`https://www.gutenberg.org/ebooks/<BOOK-ID>`.

#.	URLs used for HathiTrust page scans look like: :path:`https://catalog.hathitrust.org/Record/<RECORD-ID>`.

#.	URLs used for Google Books page scans look like: :path:`https://books.google.com/books?id=<BOOK-ID>`.

#.	URLs used for Internet Archive page scans look like: :path:`https://archive.org/details/<BOOK-ID>`.

********************
The ebook identifier
********************

#.	The :html:`<dc:identifier>` element contains the unique identifier for the ebook. The identifier is always the Standard Ebooks URL for the ebook, prefaced by :html:`url:`.

	.. code:: html

		<dc:identifier id="uid">url:https://standardebooks.org/ebooks/anton-chekhov/short-fiction/constance-garnett</dc:identifier>

Forming the SE URL
==================

The SE URL is formed by the following algorithm.

(Note: A string can be made URL-safe using the :bash:`make-url-safe` tool.)

-	Start with the URL-safe author of the work, as it appears on the titlepage. If there is more than one author, continue appending subsequent URL-safe authors, separated by an underscore. Do not alpha-sort the author name.

-	Append a forward slash, then the URL-safe title of the work. Do not alpha-sort the title.

-	If the work is translated, append a forward slash, then the URL-safe translator. If there is more than one translator, continue appending subsequent URL-safe translators, separated by an underscore. Do not alpha-sort translator names.

-	If the work is illustrated, append a foreward slash, then the URL-safe illustrator. If there is more than one illustrator, continue appending subsequent URL-safe illustrators, separated by an underscore. Do not alpha-sort illustrator names.

-	Finally, *do not* append a trailing forward slash.

****************************************
Publication date and release identifiers
****************************************

There are several elements in the metadata describing the publication date, updated date, and revision number of the ebook. Generally these are not updated by hand; instead, the :bash:`prepare-release` tool updates them automatically.

#.	:html:`<dc:date>` is a timestamp representing the first publication date of this ebook file. Once the ebook is released to the public, this value doesn’t change.

#.	:html:`<meta property="dcterms:modified">` is a timestamp representing the last time this ebook file was modified. This changes often.

#.	:html:`<meta property="se:revision-number">` is a special SE extension representing the revision number of this ebook file. During production, this number will be 0. When the ebook is first released to the public, the number will increment to 1. Each time :html:`<meta property="dcterms:modified">` changes, the revision number is incremented.

***********
Book titles
***********

Books without subtitles
=======================

#.	The :html:`<dc:title id="title">` element contains the title.

#.	The :html:`<meta property="file-as" refines="#title">` element contains alpha-sorted title, even if the alpha-sorted title is identical to the unsorted title.

.. code:: html

	<dc:title id="title">The Moon Pool</dc:title>
	<meta property="file-as" refines="#title">Moon Pool, The</meta>

.. code:: html

	<dc:title id="title">Short Fiction</dc:title>
	<meta property="file-as" refines="#title">Short Fiction</meta>`

Books with subtitles
====================

#.	The :html:`<meta property="title-type" refines="#title">main</meta>` element identifies the main part of the title.

#.	A second :html:`<dc:title id="subtitle">` element contain the subtitle, and is refined with :html:`<meta property="title-type" refines="#subtitle">subtitle</meta>`.

#.	A third :html:`<dc:title id="fulltitle">` element contains the complete title on one line, with the main title and subtitle separated by a colon and space, and is refined with :html:`<meta property="title-type" refines="#fulltitle">extended</meta>`.

#.	All three :html:`<dc:title>` elements have an accompanying :html:`<meta property="file-as">` element, even if the :html:`file-as` value is the same as the title.

.. code:: html

	<dc:title id="title">The Moon Pool</dc:title>
	<meta property="file-as" refines="#title">Moon Pool, The</meta>

.. code:: html

	<dc:title id="title">The Man Who Was Thursday</dc:title>
	<meta property="file-as" refines="#title">Man Who Was Thursday, The</meta>
	<meta property="title-type" refines="#title">main</meta>
	<dc:title id="subtitle">A Nightmare</dc:title>
	<meta property="file-as" refines="#subtitle">Nightmare, A</meta>
	<meta property="title-type" refines="#subtitle">subtitle</meta>
	<dc:title id="fulltitle">The Man Who Was Thursday: A Nightmare</dc:title>
	<meta property="file-as" refines="#fulltitle">Man Who Was Thursday, The</meta>
	<meta property="title-type" refines="#fulltitle">extended</meta>

Books with a more popular alternate title
=========================================

Some books are commonly referred to by a shorter name than their actual title. For example, :italics:`The Adventures of Huckleberry Finn </ebooks/mark-twain/the-adventures-of-huckleberry-finn>` is often simply known as :italics:`Huck Finn`.

#.	Add an additional :html:`<dc:title id="title-short">` element to contain the common title, and refine it with :html:`<meta property="title-type" refines="#title-short">short</meta>`.

#.	The common title does not a corresponding :html:`file-as` element.

*************
Book subjects
*************

Library of Congress subjects
============================

The :html:`<dc:subject>` elements allow us to categorize the ebook. We use the Library of Congress categories assigned to the book for this purpose.

#.	Each :html:`<dc:subject>` has the :html:`id` attribute set to :html:`subject-#`, where # is a number starting at :path:`1`, without leading zeros, that increments with each subject.

#.	The :html:`<dc:subject>` elements are arranged sequentially in a single block.

#.	If the transcription for the ebook comes from Project Gutenberg, the value of :html:`<dc:subject>` element comes from the Project Gutenberg page for the ebook. Otherwise, the value comes from the `Library of Congress catalog <https://catalog.loc.gov>`__.

#.	After the block of :html:`<dc:subject>` elements there is a block of :html:`<meta property="meta-auth">` elements. The values of these elements represent the URLs at which each subject was found. Typically the value is the same for each element.

#.	A :html:`<meta property="meta-auth">` element is required for each individual :html:`<dc:subject>` element, even if the :html:`meta-auth` URL is the same for all of the subjects.

This example shows how to mark up the subjects for :italics:`A Voyage to Arcturus </ebooks/david-lindsay/a-voyage-to-arcturus>`, by David Lindsay:

.. code:: html

	<dc:subject id="subject-1">Science fiction</dc:subject>
	<dc:subject id="subject-2">Psychological fiction</dc:subject>
	<dc:subject id="subject-3">Quests (Expeditions) -- Fiction</dc:subject>
	<dc:subject id="subject-4">Life on other planets -- Fiction</dc:subject>
	<meta property="meta-auth" refines="#subject-1">https://www.gutenberg.org/ebooks/1329</meta>
	<meta property="meta-auth" refines="#subject-2">https://www.gutenberg.org/ebooks/1329</meta>
	<meta property="meta-auth" refines="#subject-3">https://www.gutenberg.org/ebooks/1329</meta>
	<meta property="meta-auth" refines="#subject-4">https://www.gutenberg.org/ebooks/1329</meta>

SE subjects
===========

Along with the Library of Congress categories, we include a custom list of SE subjects in the ebook metadata. Unlike Library of Congress categories, SE subjects are purposefully broad. They’re more like the subject categories in a medium-sized bookstore, as opposed to the precise, detailed, heirarchal Library of Congress categories.

It’s the producer’s task to select appropriate SE subjects for the ebook. Usually just one or two of these categories will suffice.

All SE subjects
~~~~~~~~~~~~~~~

-	Adventure

-	Autobiography

-	Childrens

-	Comedy

-	Fantasy

-	Fiction

-	Horror

-	Memoir

-	Mystery

-	Nonfiction

-	Philosophy

-	Poetry

-	Satire

-	Science Fiction

-	Shorts

-	Spirituality

-	Travel

Required subjects for certain kinds of books
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#.	Ebooks that are collections of short stories must have the SE subject :html:`Shorts`.

#.	Ebooks that are young adult or children’s books must have the SE subject :html:`Childrens`.

*****************
Book descriptions
*****************

An ebook has two kinds of descriptions: a short :html:`<dc:description>` element, and a much longer :html:`<meta property="se:long-description">` element.

The short description
=====================

The :html:`<dc:description>` element contains a short, single-sentence summary of the ebook.

#.	The description is a single complete sentence ending in a period, not a sentence fragment or restatment of the title.

#.	The description is typogrified, i.e. it contains Unicode curly quotes, em-dashes, and the like.

The long description
=====================

The :html:`<meta property="se:long-description">` element contains a much longer description of the ebook.

#.	The long description is a non-biased, encyclopedia-like description of the book, including any relevant publication history, backstory, or historical notes. It is as detailed as possible without giving away plot spoilers. It does not impart the producer’s opinions of the book. Think along the lines of a Wikipedia-like summary of the book and its history, *but under no circumstances can a producer copy and paste from Wikipedia!*

#.	The long descriptions is be typogrified, i.e. it contains Unicode curly quotes, em-dashes, and the like.

#.	The long description is in *escaped* HTML, with the HTML beginning on its own line after the :html:`<meta property="se:long-description">` element.

	.. tip::

		An easy way to escape HTML is to compose the long description in regular HTML, then insert it into the :html:`<meta property="se:long-description">` element surrounded by a :html:`<![CDATA[ ... ]]>` element. Then, run the :bash:`clean` tool, which will remove the :html:`<![CDATA[ ... ]]>` element and escape the contained HTML.

#.	Long description HTML follows the `code style conventions of this manual </contribute/manual/code-style>`__.

#.	The long description element is directly followed by: :html:`<meta property="meta-auth" refines="#long-description">https://standardebooks.org</meta>`

*************
Book language
*************

#.	The :html:`<dc:language>` element follows the long description block. It contains the `IETF language tag <https://en.wikipedia.org/wiki/IETF_language_tag>`__ for the language that the work is in. Usually this is either :html:`en-US` or :html:`en-GB`.

***************************************
Book transcription and page scan source
***************************************

#.	The :html:`<dc:source>` elements represent URLs to sources for the transcription the ebook is based on, and page scans of the print sources used to correct the transcriptions.

#.	:html:`<dc:source>` URLs are in https where possible.

#.	A book can contain more than one such element if multiple sources for page scans were used.

*********************
Book production notes
*********************

#.	The :html:`<meta property="se:production-notes">` element contains any of the ebook producer’s production notes. For example, the producer  might note that page scans were not available, so an editorial decision was made to add commas to sentences deemed to be transcription typos; or that certain archaic spellings were retained as a matter of prose style specific to this ebook.

#.	The :html:`<meta property="se:production-notes">` element is not present if there are no production notes.

********************
Readability metadata
********************

These two elements are automatically computed by the :bash:`prepare-release` tool.

#.	The :html:`<meta property="se:word-count">` element contains an integer representing the ebooks total word count, excluding some SE files like the colophon and Uncopyright.

#.	The :html:`<meta property="se:reading-ease.flesch">` element contains a decimal representing the computed Flesch reading ease for the book.

************************
Additional book metadata
************************

#.	:html:`<meta property="se:url.encyclopedia.wikipedia">` contains the Wikipedia URL for the book. This element is not present if there is no Wikipedia entry for the book.

#.	:html:`<meta property="se:url.vcs.github">` contains the SE GitHub URL for this ebook. This is calculated by taking the string :html:`https://github.com/standardebooks/` and appending the `SE identifier <#the-ebook-identifier>`__, without :html:`https://standardebooks.org/ebooks/`, and with forward slashes replaced by underscores.

*************************
The author metadata block
*************************

#.	:html:`<dc:creator id="author">` contains the author’s name as it appears on the cover.

#.	If there is more than one author, the first author’s :html:`id` is :html:`author-1`, the second :html:`author-2`, and so on.

#.	:html:`<meta property="file-as" refines="#author">` contains the author’s name as filed alphabetically. This element is included even if it’s identical to :html:`<dc:creator>`.

#.	:html:`<meta property="se:name.person.full-name" refines="#author">` contains the author’s full name, with any initials or middle names expanded, and including any titles. This element is not included if the value is identical to :html:`<dc:creator>`.

#.	:html:`<meta property="alternate-script" refines="#author">` contains the author’s name as it appears on the cover, but transliterated into their native alphabet if applicable. For example, Anton Chekhov’s name would be contained here in the Cyrillic alphabet. This element is not included if not applicable.

#.	:html:`<meta property="se:url.encyclopedia.wikipedia" refines="#author">` contains the URL of the author’s Wikipedia page. This element is not included if there is no Wikipedia page.

#.	:html:`<meta property="se:url.authority.nacoaf" refines="#author">` contains the URL of the author’s `Library of Congress Names Database <http://id.loc.gov/authorities/names.html>`__ page. It does not include the :path:`.html` file extension. This element is not included if there is no LoC Names database entry.

	.. tip::

		This is easily found by visiting the person’s Wikipedia page and looking at the very bottom in the “Authority Control” section, under “LCCN.”

		If you it’s not on Wikipedia, find it directly by visiting the `Library of Congress Names Database <http://id.loc.gov/authorities/names.html>`__.

#.	:html:`<meta property="role" refines="#author" scheme="marc:relators">` contains the `MARC relator tag <http://www.loc.gov/marc/relators/relacode.html>`__ for the roles the author played in creating this book.

	There will always be one element with the value of :html:`aut`. There may be additional elements for additional values, if applicable. For example, if the author also illustrated the book, there would be an additional :html:`<meta property="role" refines="#author" scheme="marc:relators">ill</meta>` element.

This example shows a complete author metadata block for :italics:`Short Fiction </ebooks/anton-chekhov/short-fiction/constance-garnett>`, by Anton Chekhov:

.. code:: html

	<dc:creator id="author">Anton Chekhov</dc:creator>
	<meta property="file-as" refines="#author">Chekhov, Anton</meta>
	<meta property="se:name.person.full-name" refines="#author">Anton Pavlovich Chekhov</meta>
	<meta property="alternate-script" refines="#author">Анто́н Па́влович Че́хов</meta>
	<meta property="se:url.encyclopedia.wikipedia" refines="#author">https://en.wikipedia.org/wiki/Anton_Chekhov</meta>
	<meta property="se:url.authority.nacoaf" refines="#author">http://id.loc.gov/authorities/names/n79130807</meta>
	<meta property="role" refines="#author" scheme="marc:relators">aut</meta>

*****************************
The translator metadata block
*****************************

#.	If the work is translated, the :html:`<dc:contributor id="translator">` metadata block follows the author metadata block.

#.	If there is more than one translator, the first translator is :html:`translator-1`, the second :html:`translator-2`, and so on.

#.	Each block is identical to the author metadata block, but with :html:`<dc:contributor id="translator">` instead of :html:`<dc:creator id="author">`.

#.	The `MARC relator tag <http://www.loc.gov/marc/relators/relacode.html>`__ is :html:`trl`: :html:`<meta property="role" refines="#translator" scheme="marc:relators">trl</meta>`.

#.	Translators often annotate the work; if this is the case, the additional `MARC relator tag <http://www.loc.gov/marc/relators/relacode.html>`__ :html:`ann` is included in a separate :html:`<meta property="role" refines="#translator" scheme="marc:relators">` element.

******************************
The illustrator metadata block
******************************

#.	If the work is illustrated by a person who is not the author, the illustrator metadata block follows.

#.	If there is more than one illustrator, the first illustrator is :html:`illustrator-1`, the second :html:`illustrator-2`, and so on.

#.	Each block is identical to the author metadata block, but with :html:`<dc:contributor id="illustrator">` instead of :html:`<dc:creator id="author">`.

#.	The `MARC relator tag <http://www.loc.gov/marc/relators/relacode.html>`__ is :html:`ill`: :html:`<meta property="role" refines="#illustrator" scheme="marc:relators">ill</meta>`.

*******************************
The cover artist metadata block
*******************************

The “cover artist” is the artist who painted the art the producer selected for the SE ebook cover.

#.	The cover artist metadata block is identical to the author metadata block, but with :html:`<dc:contributor id="artist">` instead of :html:`<dc:creator id="author">`.

#.	The `MARC relator tag <http://www.loc.gov/marc/relators/relacode.html>`__ is :html:`art`: :html:`<meta property="role" refines="#artist" scheme="marc:relators">art</meta>`.

************************************
Metadata for additional contributors
************************************

Occasionally a book may have other contributors besides the author, translator, and illustrator; for example, a person who wrote a preface, an introduction, or who edited the work or added endnotes.

#.	Additional contributor blocks are identical to the author metadata block, but with :html:`<dc:contributor>` instead of :html:`<dc:creator>`.

#.	The :html:`id` attribute of the :html:`<dc:contributor>` is the lowercase, URL-safe, fully-spelled out version of the `MARC relator tag <http://www.loc.gov/marc/relators/relacode.html>`__. For example, if the MARC relator tag is :html:`wpr`, the :html:`id` attribute would be :html:`writer-of-preface`.

#.	The `MARC relator tag <http://www.loc.gov/marc/relators/relacode.html>`__ is one that is appropriate for the role of the additional contributor. Common roles for ebooks are: :html:`wpr`, :html:`ann`, and :html:`aui`.

********************
Transcriber metadata
********************

#.	If the ebook is based on a transcription by someone else, like Project Gutenberg, then transcriber blocks follow.

#.	If there is more than one transcriber, the first transcriber is :html:`transcriber-1`, the second :html:`transcriber-2`, and so on.

#.	The :html:`<meta property="file-as" refines="#transcriber-1">` element contains an alpha-sorted representation of the transcriber’s name.

#.	The `MARC relator tag <http://www.loc.gov/marc/relators/relacode.html>`__ is :html:`trc`: :html:`<meta property="role" refines="#transcriber-1" scheme="marc:relators">trc</meta>`.

#.	If the transcriber’s personal homepage is known, the element :html:`<meta property="se:url.homepage" refines="#transcriber-1">` is included, whose value is the URL of the transcriber’s homepage. The URL must link to a personal homepage only; no products, services, or other endorsements, commercial or otherwise.

*****************
Producer metadata
*****************

These elements describe the SE producer who produced the ebook for the Standard Ebooks project.

#.	If there is more than one producer, the first producer is :html:`producer-1`, the second :html:`producere-2`, and so on.

#.	The producer metadata block is identical to the author metadata block, but with :html:`<dc:contributor id="producer-1">` instead of :html:`<dc:creator id="author">`.

#.	If the producer’s personal homepage is known, the element :html:`<meta property="se:url.homepage" refines="#producer-1">` is included, whose value is the URL of the transcriber’s homepage. The URL must link to a personal homepage only; no products, services, or other endorsements, commercial or otherwise.

#.	The `MARC relator tags <http://www.loc.gov/marc/relators/relacode.html>`__ for the SE producer usually include all of the following:

	-	:html:`bkp`: The producer produced the ebook.

	-	:html:`blw`: The producer wrote the blurb (the long description).

	-	:html:`cov`: The producer selected the cover art.

	-	:html:`mrk`: The producer wrote the HTML markup for the ebook.

	-	:html:`pfr`: The producer proofread the ebook.

	-	:html:`tyg`: The producer reviewed the typography of the ebook.

******************
The ebook manifest
******************

The :html:`<manifest>` element is a required part of the epub spec that defines a list of files within the ebook.

.. tip::

	The :bash:`print-manifest-and-spine` tool generates a complete manifest that can be copied-and-pasted into the ebook’s metadata file.

#.	The manifest is in alphabetical order.

#.	The :html:`id` attribute is the basename of the :html:`href` attribute.

#.	Files which contain SVG images have the additional :html:`properties="svg"` property in their manifest item.

#.	The manifest item for the table of contents file has the additional :html:`properties="nav"` property.

#.	The manifest item for the cover image has the additional :html:`properties="cover-image"` property.

***************
The ebook spine
***************

The :html:`<spine>` element is a required part of the epub spec that defines the reading order of the files in the ebook.

.. tip::

	The :bash:`print-manifest-and-spine` tool generates a draft of the spine by making some educated guesses as to the reading order. The tool’s output is never 100% correct; manual review of the output is required, and adjustments will be necessary to correct the reading order.
