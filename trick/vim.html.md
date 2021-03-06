---
title: vim
layout: post
---

<body>

<div class="tagline">
The true delight is in the <i>finding out</i> rather than in the <i>knowing</i>.<br>-- Isaac Asimov
</div>
<div class="line clear">
<div id="content">

<p>Just remember: Vim’s basics are really very simple, but in combination the simple commands become very powerful.</p>
<h2>Modes</h2>
<p>You have <strong>3 modes</strong>:</p>
<ol>
<li>Command mode: all keystrokes are interpreted as commands</li>
<li>Insert mode: most keystrokes are inserted as text (leaving out those with<br>
modifier keys)</li>
<li>Visual mode: helps to visually select some text, may be seen as a submode of<br>
the the command mode.</li>
</ol>
<p><img src="./Vim Introduction and Tutorial - IMHO_files/modes.png" alt=""></p>
<p>To switch from the insert or visual mode to the command mode, type <code>&lt;Esc&gt;</code>.</p>
<p>To switch from the command mode to the insert mode type one of</p>
<ul>
<li><code>i</code> …switch to insert mode before the current position</li>
<li><code>a</code> …switch to insert mode after the current position (append)</li>
<li><code>I</code> …jump to the first non-blank character in the current line and switch<br>
to the insert mode</li>
<li><code>A</code> …jump to the last character of the current line and switch to the<br>
insert mode</li>
</ul>
<p>To switch from the command mode to the visual mode type one of</p>
<ul>
<li><code>v</code> …switch to the visual mode (character oriented)</li>
<li><code>V</code> …switch to the visual mode (line oriented)</li>
<li><code>Ctrl-v</code> …switch to the block-visual mode (select rectangles of text)</li>
</ul>
<p>All commands that take a range (for example subtitution, delete, copy or indentation) work with the visual mode too.</p>
<h2>Movement</h2>
<p>The simplest movement commands are</p>
<ul>
<li><code>h</code> …move left</li>
<li><code>l</code> …move right</li>
<li><code>k</code> …move up</li>
<li><code>j</code> …move down</li>
</ul>
<p>Obviously these commands work only in the command mode, of course you can also use the cursor keys (in all three modes).</p>
<p>There are a lot of movement commands available in Vim, I’ll only cover a few, but if you need something special very often take a look at the help, I’m sure you’ll find something usable.</p>
<p><img src="./Vim Introduction and Tutorial - IMHO_files/commands.png" alt=""></p>
<p>Vim distinguishes between screen-lines (those shown on the monitor) and real lines (those ended with a new-line).</p>
<p>So here the most important commands</p>
<ul>
<li><code>0</code> …first column of the line</li>
<li><code>^</code> …first non-blank character of the line</li>
<li><code>w</code> …jump to next word</li>
<li><code>W</code> …jump to next word, ignore punctuation</li>
<li><code>e</code> …jump to word-end</li>
<li><code>E</code> …jump to word-end, ignore punctuation</li>
<li><code>b</code> …jump to word-beginning</li>
<li><code>B</code> …jump to word-beginning, ignore punctuation</li>
<li><code>ge</code> …jump to previous word-ending</li>
<li><code>gE</code> …jump to previous word-ending, ignore punctuation</li>
<li><code>g_</code> …jump to last non-blank character of the line</li>
<li><code>$</code> …jump to the last character of the line</li>
</ul>
<p>If you remember just a few of them, you’ll get very quickly from A to B! Another important fact is, that these commands give the range for other commands.</p>
<h2>Editing</h2>
<p>Inserting text is pretty simple in Vim, just type <code>i</code> and start typing. But Vim offers quite sophisticated text-editing commands.</p>
<ul>
<li><code>d</code> …delete the characters from the cursor position up the position given by the next command (for example <code>d$</code> deletes all character from the current cursor position up to the last column of the line).</li>
<li><code>c</code> …change the character from the cursor position up to the position indicated by the next command.</li>
<li><code>x</code> …delete the character under the cursor.</li>
<li><code>X</code> …delete the character before the cursor (Backspace).</li>
<li><code>y</code> …copy the characters from the current cursor position up to the position indicated by the next command.</li>
<li><code>p</code> …paste previous deleted or yanked (copied) text after the current cursor position.</li>
<li><code>P</code> …paste previous deleted or yanked (copied) text before the current cursor position.</li>
<li><code>r</code> …replace the current character with the newly typed one.</li>
<li><code>s</code> …substitute the text from the current cursor position up to the position given by the next command with the newly typed one.</li>
<li><code>.</code> …repeat the last insertion or editing command (x,d,p…).</li>
</ul>
<p>Doubling <code>d</code>, <code>c</code> or <code>y</code> operates on the whole line, for example <code>yy</code> copies the whole line.</p>
<p>Please note, many commands are much more powerful than I describe them here. For example you can specify a buffer into some text is yanked. Typing <code>"ayy</code> copies the current line into register <code>a</code>, pasting the contents of register <code>a</code> is done by <code>"ap</code>. Vim remembers the last few yanks and deletions in automatic registers, to show the contents of the registers type <code>:registers</code>, you can also use them to paste some older text.</p>
<h2>Visual Block</h2>
<p>Using the visual block-mode it’s possible to insert characters on each line of the selection easily.</p>
<p>Suppose you have selected a rectangle (using <code>Ctrl-v</code>), you can insert text in front of it by typing <code>I</code> (switch to insert mode) and inserting your text. As soon as you leave the insert mode, the text will be added to all the other selected lines. Use <code>A</code> to enter text <strong>after</strong> the selection.</p>
<p>Another useful feature is to substitute the whole block with a new text. For that matter select a block and type <code>s</code>, Vim enters the insert mode and you can type. After you leave the insert mode, Vim inserts the text in the remaining lines.</p>
<p>If you’d like to append some text at the end of some lines, use <code>Ctrl-v$</code> and select the lines. The difference between the former variant is, that the <code>$</code> explicitly says “end of line” whereas a selection with <code>Ctrl-v</code> operates on the columns, ignoring the text.</p>
<p>Using <code>Ctrl-v</code>:</p>
<pre> This is a testNEWLY INSERTED
 This is a     NEWLY INSERTED
 This is       NEWLY INSERTED
</pre>
<p>Using <code>Ctrl-v$</code>:</p>
<pre> This is a testNEWLY INSERTED
 This is aNEWLY INSERTED
 This isNEWLY INSERTED
</pre>
<h2>Text-objects</h2>
<p>Vim commands operate on <strong>text-objects</strong> these are characters, words, characters delimited by parentheses, sentences and so on.</p>
<p>For me the most important one is the <strong>inner word</strong>: <code>iw</code>. To select the current word, just type <code>viw</code> (<code>v</code> for selection mode, and <code>iw</code> for the <strong>inner word</strong>), similar for deletion: <code>diw</code>.</p>
<p>The difference between inner-word/block and a-word/block etc is that the inner variant selects only the contents like the characters of the word (no blank afterwards) or the contents of the parentheses but not the parentheses. The a-variant selects the parentheses or a blank after a word too.</p>
<ul>
<li><code>iw</code> …inner word</li>
<li><code>aw</code> …a word</li>
<li><code>iW</code> …inner <span class="caps">WORD</span></li>
<li><code>aW</code> …a <span class="caps">WORD</span></li>
<li><code>is</code> …inner sentence</li>
<li><code>as</code> …a sentence</li>
<li><code>ip</code> …inner paragraph</li>
<li><code>ap</code> …a paragraph</li>
<li><code>i(</code> or <code>i)</code> …inner block</li>
<li><code>a(</code> or <code>a)</code> …a block</li>
<li><code>i&lt;</code> or <code>i&gt;</code> …inner block</li>
<li><code>a&lt;</code> or <code>i&gt;</code> …a block</li>
<li><code>i{</code> or <code>i}</code> …inner block</li>
<li><code>a{</code> or <code>a}</code> …a block</li>
<li><code>i"</code> …inner block</li>
<li><code>a"</code> …a block</li>
<li><code>i`</code> …inner block</li>
<li><code>a`</code> …a block</li>
</ul>
<p>Here a quick visualisation of the commands the color and the <span style="color: red">[ ]</span> mark the selected text:</p>
<table>
<tbody><tr>
<th>Command </th>
<th>Text Object </th>
</tr>
<tr>
<td> <code>iw</code> </td>
<td> This is a <span style="color: red">[</span><span style="background-color: yellow">test</span><span style="color: red">]</span> sentence. </td>
</tr>
<tr>
<td> <code>aw</code> </td>
<td> This is a <span style="color: red">[</span><span style="background-color: yellow">test </span><span style="color: red">]</span>sentence. </td>
</tr>
<tr>
<td> <code>iW</code> </td>
<td> This is a <span style="color: red">[</span><span style="background-color: yellow">…test…</span><span style="color: red">]</span> sentence. </td>
</tr>
<tr>
<td> <code>aW</code> </td>
<td> This is a <span style="color: red">[</span><span style="background-color: yellow">…test… </span><span style="color: red">]</span>sentence. </td>
</tr>
<tr>
<td> <code>is</code> </td>
<td> …sentence. <span style="color: red">[</span><span style="background-color: yellow">This is a sentence.</span><span style="color: red">]</span> This… </td>
</tr>
<tr>
<td> <code>as</code> </td>
<td> …sentence. <span style="color: red">[</span><span style="background-color: yellow">This is a sentence. </span><span style="color: red">]</span>This… </td>
</tr>
<tr>
<td> <code>ip</code> </td>
<td> End of previous paragraph.<br><br><span style="color: red">[</span><span style="background-color: yellow">This is a paragraph. It has two sentences.</span><span style="color: red">]</span><br><br>The next. </td>
</tr>
<tr>
<td> <code>ap</code> </td>
<td> End of previous paragraph.<br><br><span style="color: red">[</span><span style="background-color: yellow">This is a paragraph. It has two sentences.<br><br></span><span style="color: red">]</span>The next. </td>
</tr>
<tr>
<td> <code>i(</code> or <code>i)</code> </td>
<td> 1 * (<span style="color: red">[</span><span style="background-color: yellow">2 + 3</span><span style="color: red">]</span>) </td>
</tr>
<tr>
<td> <code>a(</code> or <code>a)</code> </td>
<td> 1 * <span style="color: red">[</span><span style="background-color: yellow">(2 + 3)</span><span style="color: red">]</span> </td>
</tr>
<tr>
<td> <code>i&lt;</code> or <code>i&gt;</code> </td>
<td> The &lt;<span style="color: red">[</span><span style="background-color: yellow">tag</span><span style="color: red">]</span>&gt; </td>
</tr>
<tr>
<td> <code>a&lt;</code> or <code>i&gt;</code> </td>
<td> The <span style="color: red">[</span><span style="background-color: yellow">&lt;tag&gt;</span><span style="color: red">]</span> </td>
</tr>
<tr>
<td> <code>i{</code> or <code>i}</code> </td>
<td> some {<span style="color: red">[</span><span style="background-color: yellow"> code block </span><span style="color: red">]</span>} </td>
</tr>
<tr>
<td> <code>a{</code> or <code>a}</code> </td>
<td> some <span style="color: red">[</span><span style="background-color: yellow">{ code block }</span><span style="color: red">]</span> </td>
</tr>
<tr>
<td> <code>i"</code> </td>
<td> The "<span style="color: red">[</span><span style="background-color: yellow">best</span><span style="color: red">]</span>" </td>
</tr>
<tr>
<td> <code>a"</code> </td>
<td> The<span style="color: red">[</span><span style="background-color: yellow"> “best”</span><span style="color: red">]</span> </td>
</tr>
<tr>
<td> <code>i`</code> </td>
<td> The `<span style="color: red">[</span><span style="background-color: yellow">best</span><span style="color: red">]</span>` </td>
</tr>
<tr>
<td> <code>a`</code> </td>
<td> The<span style="color: red">[</span><span style="background-color: yellow"> `best`</span><span style="color: red">]</span> </td>
</tr>
</tbody></table>
<p>Try them out and remember the ones you need regularly (in my case <code>iw</code> and <code>i(</code>) they are the real time-savers!</p>
<h2>Undo and Redo</h2>
<p>Don’t be afraid to try the various commands, you can undo almost anything using <code>u</code> in the command mode – even undo is undoable using <code>Ctrl-r</code>.</p>
<p>Vim 7.0 introduced undo-branches, but I didn’t have time to dig deeper.</p>
<h2>External commands</h2>
<p>In Vim it’s easy to include the output of external commands or to filter the whole line or just a part through an external filter.</p>
<p>To issue an external command type <code>:!command</code>, the output will be shown and that’s it.</p>
<p>To filter the text through an external command type <code>:!sort %</code>.</p>
<p>To insert the output of the external command in the current file type <code>:r!command</code> (for example <code>:r!which ls</code>).</p>
<p>Search for “filter” for more information <code>:h filter</code>.</p>
<h2>Searching and Replacing</h2>
<p>Searching in Vim is very easy. Type <code>/</code> in the command mode and insert the term you search, and Vim will search the file (in forward direction) for the term. Use <code>?</code> for the backward direction. Using <code>n</code> or <code>N</code> you can repeat the search in the same or opposite direction.</p>
<p>If the option “incsearch” is set, Vim immediately jumps to the matching text when you enter something. If “hlsearch” is set, it highlights all matches. To remove the highlight type <code>:nohl</code>.</p>
<p>Replacing something isn’t very hard too, but you should have a good understanding of regular expressions.</p>
<p>To substitute a regular expression with some other text, type <code>:%s/old/new/gc</code> this command takes the whole file <code>%</code>, and substitutes <code>s</code> the word "old@ with “new” and looks for more than one occurrence within one line <code>g</code> and asks if it really should replace the shown one <code>c</code>.</p>
<p>To replace some text only in a selected area, select the area, and type <code>:s/old/new/g</code>. This should look like <code>:'&lt;,'&gt;s/old/new/g</code> in the command line. You’ll understand <code>'&lt;</code> and <code>'&gt;</code> after the “Marks” section.</p>
<h2>Completion</h2>
<p>While you are typing, it’s pretty common to use the same word over and over again. Using <code>Ctrl-p</code> Vim searches the currently typed text backwards for a word starting with the same characters as already typed. <code>Ctrl-x Ctrl-l</code> completes the whole line.</p>
<p>If you’re not sure how to type some word and you’ve enabled spell-checking (<code>:set spell</code>), you can type <code>Ctrl-x Ctrl-k</code> to do a dictionary lookup for the already typed characters. Vim’s completion system has much improved during the last major update (Vim 7.0).</p>
<p>Note the completion commands work only in the <strong>insert mode</strong>, they have other meanings in the command mode!</p>
<h2>Marks</h2>
<p>You can set marks within your documents to jump quickly between different positions of a document or even many documents.</p>
<p>Vim automatically sets various marks like</p>
<ul>
<li><code>{0-9}</code> are the last 10 positions of closed files (0 the last, 1 the last but one)</li>
<li><code>&lt;</code> and <code>&gt;</code> are the left and right position of marked texts</li>
<li><code>(</code> and <code>)</code> are the start or end of the current sentence</li>
<li><code>{</code> and <code>}</code> are the start or end of the current paragraph</li>
<li><code>[</code> and <code>]</code> are the first or last character of the last yanked or changed text</li>
<li><code>.</code> position of the last change</li>
<li><code>'</code> or <code>`</code> position before the last jump</li>
<li><code>"</code> position before the last exit of the file (local to a file)</li>
<li><code>^</code> position of the last insert-stop</li>
</ul>
<p>To set a manual mark, use <code>m{a-zA-Z}</code> (<code>m</code> followed by either a,b..z or A,B,..Z), and to jump to one of the marks (manual or automatic) you can choose between <code>'</code> and <code>`</code></p>
<ul>
<li><code>'</code> …sets the cursor to the first non-blank character in the marked line</li>
<li><code>`</code> …sets the cursor to the exact position where the mark was set</li>
</ul>
<p>There is a little difference between lower-case and upper-case characters:</p>
<ul>
<li><code>{a-z}</code> are local to a file</li>
<li><code>{A-Z}</code> are stored and available over sessions (associated with a file)</li>
</ul>
<p>You can use <code>L</code> for your work-log and <code>T</code> for your time-table for example, and quickly update the information there.</p>
<p>For example you can jump to the last known position of a file before it was closed by typing <code>`"</code> (it’s easy to configure Vim to do it automatically at start).</p>
<p>To get a list of all marks Vim knows about type <code>:marks</code>. To delete marks use <code>:delmarks</code> (<code>:delmarks a b c</code> removes marks <code>a</code> and <code>b</code> and <code>c</code>, to delete all marks use <code>:delmarks!</code>).</p>
<h2>Tabs, Buffers and Windows</h2>
<p>Vim 7.0 has introduced tabs. We all know and love tabs, so it’s not much to say here. (Just a note: tabs in Vim are a bit different than in other programs, you could also think of them as many Vim instances in a tabbed terminal window. The difference is, that each tab-page can have it’s own layout. For example I could split my screen of the first tab, and view the same file in one window at the second tab… . So Vim-tabs are a bit more powerful.)</p>
<p>To open many files in tabs via the command line use <code>vim -p *.txt</code>.</p>
<p>To switch between tabs use the mouse (in gVim) or type <code>gt</code>.</p>
<p>To create a new empty tab type <code>:tabnew</code>, or open a file in a new tab <code>:tabe xyz</code>.</p>
<p>Buffers and Windows are a bit harder to understand. A window is what you see when you open Vim, when you open the help system (by typing <code>:help buffers</code>), you’ve got two windows. So they are no actual windows, but view-ports that Vim offers.</p>
<p>You can open a window and split the current one horizontally using <code>:sp</code> or vertically using <code>:vsp</code>. This way Vim shows you the same <strong>buffer</strong> in two different windows. You can open a new file too, using <code>:sp file</code> or <code>:vsp file</code>. To switch between windows use the mouse or type <code>Ctrl-w {hjkl}</code> in the command mode.</p>
<p>A buffer is a file (most of the time), but isn’t necessarily visible. So there are usually more buffers than windows. To show a different buffer in the current window, you can switch them using <code>:b NUMBER</code>, where the buffer number can be looked up using <code>:buffers</code>. In the standard configuration Vim forces you to save the currently shown buffer before it allows you to switch to another buffer, so don’t be frustrated by it’s complains. (Type <code>:set hidden</code> to enable unsaved buffers, but be careful).</p>
<p>Here my notes from the help-file:</p>
<ul>
<li><code>:b N</code> switch to buffer N</li>
<li><code>:buffers</code> show buffer list. Explanation:
<ul>
<li><code>%</code> current window</li>
<li><code>#</code> alternate buffer (switch using <code>:e#</code> or <code>:b#</code>)</li>
<li><code>a</code> active (loaded and visible)</li>
<li><code>h</code> hidden (loaded but not visible)</li>
<li><code>+</code> modified</li>
</ul></li>
<li><code>:bd</code> unload the buffer and remove it from bufferlist (don’t close Vim,<br>
even on the last buffer)</li>
<li><code>:bun</code> unload the buffer but stay in bufferlist</li>
<li><code>:sp #N</code> split current window and edit buffer N</li>
<li><code>:w</code> write the current buffer to disk</li>
<li><code>:e file</code> load a file from disk</li>
<li><code>:q</code> closes current window (and Vim if it’s the last one)</li>
<li><code>:new</code> new empty window</li>
<li><code>:on</code> close all windows but the active one (<code>Ctrl-W o</code>)</li>
<li><code>Ctrl-W {h,j,k,l}</code> move between windows</li>
</ul>
<p>Allow modified buffers to be hidden when the option ‘hidden’ is set. Buffers are automatically saved if the option ‘hidden’ is not set, but ‘autowrite’ is set.</p>
<h2>Macros</h2>
<p>Vim allows to replay some commands using <code>.</code> (a dot). For more than one command use macros.</p>
<p>You can start macro-recording using <code>q</code> and one of {0-9a-zA-Z}, so for example <code>qq</code> records the macro to buffer “q”. Hit <code>q</code> when you are finished recording.</p>
<p>Now you can replay the macro at any time using @q.</p>





</body></html>
