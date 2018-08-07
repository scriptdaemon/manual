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

*****************************
XHTML file naming conventions
*****************************

..
						<h3>The <code class="html">id</code> attribute</h3>
						<section>
							<h4><code class="html">id</code>s of <code class="html">&lt;section&gt;</code>s</h4>
							<ol>
								<li>
									<p>Each <code class="html">&lt;section&gt;</code> has an <code class="html">id</code> attribute identical to the filename containing the <code class="html">&lt;section&gt;</code>, without the trailing extension.</p>
								</li>
								<li>
									<p>In files containing multiple <code class="html">&lt;section&gt;</code>s, each <code class="html">&lt;section&gt;</code> has an <code class="html">id</code> attribute identical to what the filename <em>would</em> be if the section was in an individual file, without the trailing extension.</p>
									<figure class="corrected">
								<code class="html">&lt;body epub:type="bodymatter z3998:fiction"&gt;
		&lt;article id="the-fox-and-the-grapes" epub:type="volume se:short-story"&gt;
			&lt;h2 epub:type="title"&gt;The Fox and the Grapes&lt;/h2&gt;
			&lt;p&gt;...&lt;/p&gt;
		&lt;/article&gt;
		&lt;article id="the-goose-that-laid-the-golden-eggs" epub:type="volume se:short-story"&gt;
			&lt;h2 epub:type="title"&gt;The Goose That Laid the Golden Eggs&lt;/h2&gt;
			&lt;p&gt;...&lt;/p&gt;
		&lt;/article&gt;
	&lt;/body&gt;</code>
									</figure>
								</li>
							</ol>
						</section>
						<section>
							<h4><code class="html">id</code>s of other elements</h4>
							<p>Generally, elements that are not <code class="html">&lt;section&gt;</code>s do not have an <code class="html">id</code> attribute. However an <code class="html">id</code> attribute may be necessary if a particular element is referenced in a link in a different location in the ebook; for example, if a certain paragraph is linked from an endnote.</p>
							<ol>
								<li>
									<p><code class="html">id</code> attributes are generally used for parts of the document that a reader may wish to navigate to using a hash in the URL. That generally means major structural divisions.</p>
								</li>
								<li>
									<p><code class="html">id</code> attributes are not used as hooks for targeting CSS styling.</p>
								</li>
								<li>
									<p>If an element requires an <code class="html">id</code> attribute, the attribute's value is the name of the tag followed by <code class="path">-N</code>, where <code class="path">N</code> is the sequence number of the tag start at <code class="html">1</code>.</p>
									<figure class="corrected">
										<code class="html">&lt;p&gt;See &lt;a href="#p-4"&gt;this paragraph&lt;/a&gt; for more details.&lt;/p&gt;
	&lt;p&gt;...&lt;/p&gt;
	&lt;p&gt;...&lt;/p&gt;
	&lt;p id="p-4"&gt;...&lt;/p&gt;
	&lt;p&gt;...&lt;/p&gt;</code>
									</figure>
								</li>
							</ol>
						</section>
					</section>
					<section>
						<h3><code class="html">&lt;title&gt;</code> tags</h3>
						<ol>
							<li>
								<p>The <code class="html">&lt;title&gt;</code> tag contains an appropriate description of the local file only. It does not contain the book title.</p>
							</li>
						</ol>
						<section>
							<h4>Titles of files that are an individual chapter or part division</h4>
							<ol>
								<li>
									<p>Convert chapter or part numbers that are in Roman numerals to decimal numbers. Do not convert other Roman numerals that may be in the chapter title.</p>
									<figure>
										<code class="html">&lt;title&gt;Chapter 10&lt;/title&gt;</code>
									</figure>
								</li>
								<li>
									<p>If a chapter or part has no subtitle, the <code class="html">&lt;title&gt;</code> tag contains <code class="html">Chapter</code> followed by the chapter number.</p>
									<figure>
										<code class="html">&lt;title&gt;Chapter 4&lt;/title&gt;</code>
									</figure>
								</li>
								<li>
									<p>If a chapter or part has a subtitle, the <code class="html">&lt;title&gt;</code> tag contains <code class="html">Chapter</code>, followed by the chapter number, followed by a colon and a single space, followed by the subtitle.</p>
									<figure>
										<code class="html">&lt;title&gt;Chapter 4: The Reign of Louis XVI&lt;/title&gt;</code>
									</figure>
								</li>
							</ol>
						</section>
						<section>
							<h4>Titles of files that are not chapter or part divisions</h4>
							<ol>
								<li>
									<p>Files that are not a chapter or a part division, like a preface, introduction, or epigraph, have a <code class="html">&lt;title&gt;</code> tag that contains the complete title of the section.</p>
									<figure>
										<code class="html">&lt;title&gt;Preface&lt;/title&gt;</code>
									</figure>
								</li>
								<li>
									<p>If a file contains a section with a subtitle, the <code class="html">&lt;title&gt;</code> tag contains the title, followed by a colon and a single space, followed by the subtitle.</p>
									<figure>
										<code class="html">&lt;title&gt;Quevedo and His Works: With an Essay on the Picaresque Novel&lt;/title&gt;</code>
									</figure>
								</li>
							</ol>
						</section>
					</section>
					<section>
						<h3>Ordered/numbered and unordered lists</h3>
						<p>All <code class="html">&lt;li&gt;</code> children of <code class="html">&lt;ol&gt;</code> and <code class="html">&lt;ul&gt;</code> tags have at least one direct child block-level tag.  This is usually a <code class="html">&lt;p&gt;</code> tag, but not necessarily; for example, a <code class="html">&lt;blockquote&gt;</code> tag might also be appropriate.</p>
						<figure class="wrong">
							<code class="html">&lt;ul&gt;
		&lt;li&gt;Don’t forget to feed the pigs.&lt;/li&gt;
	&lt;/ul&gt;</code>
						</figure>
						<figure class="corrected">
							<code class="html">&lt;ul&gt;
		&lt;li&gt;
			&lt;p&gt;Don’t forget to feed the pigs.&lt;/p&gt;
		&lt;/li&gt;
	&lt;/ul&gt;</code>
						</figure>
