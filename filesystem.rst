.. role:: html(code)
	:language: html
.. role:: css(code)
	:language: css
.. role:: bash(code)
	:language: bash
.. role:: path(code)
.. role:: italics(emphasis)
	:class: i

#############################################
Filesystem Layout and File Naming Conventions
#############################################

.. class:: data-start-at-2

Intro.

*****************************
XHTML file naming conventions
*****************************

#.	Filenames that require numbers do not include a leading :path:`0`.

#.	Files containing a short story, essay, or other short work in a larger collection, are named with the URL-safe title of the work, excluding any subtitles.

	=============================================================================================== =========================================
	Work                                                                                            Filename
	=============================================================================================== =========================================
	A short story named “The Variable Man”                                                          :path:`the-variable-man.xhtml`
	A short story named “The Sayings of Limpang-Tung (The God of Mirth and of Melodious Minstrels)” :path:`the-sayings-of-limpang-tung.xhtml`
	=============================================================================================== =========================================

#.	Works that are divided into larger parts (sometimes called “parts,” “books,” “volumes,” “sections,” etc.) have their part divisions contained in individual files named after the type of part, followed by a number starting at :path:`1`.

	.. class:: text corrected

		.. compound::

			:path:`book-1.xhtml`

			:path:`book-2.xhtml`

			:path:`part-1.xhtml`

			:path:`part-2.xhtml`

#.	Works that are composed of chapters, short stories, essays, or other short- to medium-length sections have each of those sections in an individual file.

	#.	Chapters *not* contained in separate volumes are named :path:`chapter-N.xhtml`, where :path:`N` is the chapter number starting at :path:`1`.

		================ =========================
		Section          Filename
		================ =========================
		Chapter 1        :path:`chapter-1.xhtml`
		Chapter 2        :path:`chapter-2.xhtml`
		================ =========================

	#.	Chapters contained in separate volumes, where the chapter number re-starts at 1 in each volume, are named :path:`chapter-X-N.xhtml`, where :path:`X` is the part number starting at :path:`1`, and :path:`N` is the chapter number *within the part*, starting at :path:`1`.

		================ =========================
		Section          Filename
		================ =========================
		Part 1           :path:`part-1.xhtml`
		Part 1 Chapter 1 :path:`chapter-1-1.xhtml`
		Part 1 Chapter 2 :path:`chapter-1-2.xhtml`
		Part 1 Chapter 3 :path:`chapter-1-3.xhtml`
		Part 2           :path:`part-2.xhtml`
		Part 2 Chapter 1 :path:`chapter-2-1.xhtml`
		Part 2 Chapter 2 :path:`chapter-2-2.xhtml`
		================ =========================

	#.	Chapters contained in separate volumes, where the chapter number does not re-start at 1 in each volume, are named :path:`chapter-N.xhtml`, where :path:`N` is the chapter number, starting at :path:`1`.

		================ =========================
		Section          Filename
		================ =========================
		Part 1           :path:`part-1.xhtml`
		Chapter 1        :path:`chapter-1.xhtml`
		Chapter 2        :path:`chapter-2.xhtml`
		Chapter 3        :path:`chapter-3.xhtml`
		Part 2           :path:`part-2.xhtml`
		Chapter 4        :path:`chapter-4.xhtml`
		Chapter 5        :path:`chapter-5.xhtml`
		================ =========================

	#.	Works that are composed of extremely short sections, like a volume of short poems, are in a single file containing all of those short sections. The filename is the URL-safe name of the work.

		============================================== =============================
		Section                                        Filename
		============================================== =============================
		A book of short poems called “North of Boston” :path:`north-of-boston.xhtml`
		============================================== =============================

	#.	Frontmatter and backmatter sections have filenames that are named after the type of section, regardless of what the actual title of the section is.

		============================================== =============================
		Section                                        Filename
		============================================== =============================
		A preface titled “Note from the author”        :path:`preface.xhtml`
		============================================== =============================

	#.	If a work contains more than one section of the same type (for example multiple prefaces), the filename is followed by :path:`-N`, where :path:`N` is a number representing the order of the section, starting at :path:`1`.

		=============================================================================== =============================
		Section                                                                         Filename
		=============================================================================== =============================
		The work’s first preface, titled “Preface to the 1850 Edition”                  :path:`preface-1.xhtml`
		The work’s second preface, titled “Preface to the Charles Dickens Edition”      :path:`preface-2.xhtml`
		=============================================================================== =============================
