.. role:: html(code)
	:language: html
.. role:: css(code)
	:language: css
.. role:: bash(code)
	:language: bash
.. role:: path(code)
.. role:: italics(emphasis)
	:class: i

########################
XHTML and CSS Code Style
########################

The :bash:`clean` tool in the Standard Ebooks toolset formats XHTML code according to our style guidelines. The vast majority of the time its output is correct and no further modifications to code style are necessary.

****************
XHTML formatting
****************

#.	The first line of all XHTML files is:

	.. code:: html

		<?xml version="1.0" encoding="utf-8"?>

#.	The second line of all XHTML files is (replace :html:`xml:lang="en-US"` with the `appropriate language tag <https://en.wikipedia.org/wiki/IETF_language_tag>`__ for the file):

	.. code:: html

		<html xmlns="http://www.w3.org/1999/xhtml" xmlns:epub="http://www.idpf.org/2007/ops" epub:prefix="z3998: http://www.daisy.org/z3998/2012/vocab/structure/, se: https://standardebooks.org/vocab/1.0" xml:lang="en-US">`

#.	Tabs are used for indentation.

#.	Tag names are lowercase.

#.	Tags whose content is `phrasing content <https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Content_categories#Phrasing_content>`__ are on a single line, with no whitespace between the opening and closing tags and the content.

	.. class:: wrong

		.. code:: html

			<p>
				It was a dark and stormy night...
			</p>

	.. class:: corrected

		.. code:: html

			<p>It was a dark and stormy night...</p>

Attributes
==========

#.	Attributes are in alphabetical order.

#.	Attributes, their namespaces, and their values are lowercase, except for values which are IETF language tags. In IETF language tags, the language subtag is capitalized.

	.. class:: wrong

		.. code:: html

			<section EPUB:TYPE="CHAPTER" XML:LANG="EN-US">...</section>

	.. class:: corrected

		.. code:: html

			<section epub:type="chapter" xml:lang="en-US">...</section>

#.	The string :html:`utf-8` is lowercase.

**************
CSS formatting
**************

#.	The first two lines of all CSS files are:

	.. code:: css

		@charset "utf-8";
		@namespace epub "http://www.idpf.org/2007/ops";

#.	Tabs are used for indentation.

#.	Selectors, properties, and values are lowercase.

Selectors
=========

#.	Selectors are each on their own line, directly followed by a comma or a brace with no whitespace inbetween.

#.	Complete selectors are separated by exactly one blank line.

	.. class:: wrong

		.. code:: css

			abbr.name{
				white-space: nowrap;
			}


			strong{
				font-weight: normal;
				font-variant: small-caps;
			}

	.. class:: corrected

		.. code:: css

			abbr.name{
				white-space: nowrap;
			}

			strong{
				font-weight: normal;
				font-variant: small-caps;
			}

#.	Closing braces are on their own line.

Properties
==========

#.	Properties are each on their own line (even if the selector only has one property) and indented with a single tab.

	.. class:: wrong

		.. code:: css

			abbr.name{ white-space: nowrap; }

	.. class:: corrected

		.. code:: css

			abbr.name{
				white-space: nowrap;
			}

#.	Properties are in alphabetical order, *where possible*.

	This isn’t always possible if you’re attempting to override a previous style in the same selector, and in some other cases.

#.	Properties are directly followed by a colon, then a single space, then the property value.

	.. class:: wrong

		.. code:: css

			blockquote{
				margin-left:	1em;
				margin-right:	1em;
				border:none;
			}

	.. class:: corrected

		.. code:: css

			abbr.name{
				margin-left: 1em;
				margin-right: 1em;
				border: none;
			}

#.	Property values are directly followed by a semicolon, even if it’s the last value in a selector.

	.. class:: wrong

		.. code:: css

			abbr.name{
				white-space: nowrap
			}

	.. class:: corrected

		.. code:: css

			abbr.name{
				white-space: nowrap;
			}
