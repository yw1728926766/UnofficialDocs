====================
Settings (Reference)
设置项（参考内容）
====================


Global Settings
全局设置项
===============

**Target file:** ``Global.sublime-settings``.
**对应文件：** ``Global.sublime-settings`` 。


``theme``
   Theme to be used. Accepts a file base name (e. g.: ``Default.sublime-theme``).
   系统使用的主题文件。接受主题文件的名称（例如： ``Default.sublime-theme`` ）。
``remember_open_files``
   Determines whether to reopen the buffers that were open when Sublime Text was last closed.
   设置Sublime Text启动时是否需要打开上次关闭时打开了的缓冲区。
``folder_exclude_patterns``
   Excludes the matching folders from the side bar, GoTo Anything, etc.
   与匹配模式相符的目录将不会出现在侧边栏、快速跳转面板等位置。
``file_exclude_patterns``
   Excludes the matching files from the side bar, GoTo Anything, etc.
   与匹配模式相符的文件将不会出现在侧边栏、快速跳转面板等位置。
``scroll_speed``
   Set to ``0`` to disable smooth scrolling. Set to a value between ``0`` and
   ``1`` to scroll slower, or set to a value larger than ``1`` to scroll faster.
   如果把值设为 ``0`` ，将禁止平滑滚动。取 ``0`` 到 ``1`` 之间的数值将使滑动变的比较缓慢，取大于
   ``1`` 的值使得滑动更加迅速。
``show_tab_close_buttons``
   If ``false``, hides the tabs' close buttons until the mouse is hovered over
   the tab.
   如果设置为 ``false`` ，通常情况下就不会显示标签页的关闭按钮，只有当鼠标移动到标签上时才显示。
``mouse_wheel_switches_tabs``
   If ``true``, scrolling the mouse wheel will cause tabs to switch if the
   cursor is in the tab area.
   如果设置为 ``true`` ，在标签区域滑动鼠标滚轮会触发标签页之间的切换。
``open_files_in_new_window``
   OS X only. When filters are opened from Finder, or by dragging onto the
   dock icon, this controls if a new window is created or not.
   仅在OS X平台有效。当用户从Finder中开打文件，或者把文件拖拽到dock面板的图标上，这个设置项将决定
   是否需要创建一个新窗口。


File Settings
文件设置项
=============

**Target files:** ``Base File.sublime-settings``, ``<file_type>.sublime-settings``.
**对应文件：** ``Base File.sublime-settings``， ``<file_type>.sublime-settings``。

Whitespace and Indentation
空格与缩进
**************************


``auto_indent``
   Toggles automatic indentation.
   开/关自动缩进选项。
``tab_size``
   Number of spaces a tab is considered to be equal to.
   设置tab键对应的空格数。
``translate_tabs_to_spaces``
   Determines whether to replace a tab character with ``tab_size`` number of
   spaces when :kbd:`Tab` is pressed.
   设置当用户按下 :kbd:`Tab` 键时，是否需要用 ``tab_size`` 选项所指定数目的空格进行替换。
``use_tab_stops``
   If ``translate_tabs_to_spaces`` is ``true``, will make :kbd:`Tab` and
   :kbd:`Backspace` insert/delete ``tab_size`` number of spaces per key press.
   如果 ``translate_tabs_to_spaces`` 选项为 ``true`` ，设置这个选项就使得每次按下 :kbd:`Tab`
   与 :kbd:`Backspace` 键时，将插入/删除 ``tab_size`` 选项所指定数目的空格。
``trim_automatic_white_space``
   Toggles deletion of white space added by ``auto_indent``.
   开/关对由 ``auto_indent`` 选项自动添加的只有空格的行的检测。
``detect_indentation``
   Set to ``false`` to disable detection of tabs vs. spaces whenever a buffer
   is loaded. If set to ``true``, it will automatically modify
   ``translate_tabs_to_spaces`` and ``tab_size``.
   如果设置为 ``false`` ，当系统加在缓冲区内容的时候，就会停止对tab与空格的检测。如果设置为 ``true``
   则会自动修改 ``translate_tabs_to_spaces`` 以及 ``tab_size`` 的值。
``draw_white_space``
   Valid values: ``none``, ``selection``, ``all``.
   有效值： ``none``， ``selection``， ``all`` 。
``trim_trailing_white_space_on_save``
   Set to ``true`` to remove white space on save.
   将这个选项设置为 ``true`` 就会在文件保存时候自动去处行为的空格。

Visual Settings
显示设置项
***************

``color_scheme``
   Sets the colors used for text highlighting. Accepts a path rooted at the
   data directory (e. g.: ``Packages/Color Scheme - Default/Monokai Bright.tmTheme``).
   设置文本高亮的配色方案。接受从数据目录开始的相对路径（例如：
   ``Packages/Color Scheme - Default/Monokai Bright.tmTheme``）。
``font_face``
   Font face to be used for editable text.
   设置可编辑文本的字体样式。
``font_size``
   Size of the font for editable text.
   设置可编辑字体的字体大小。
``font_options``
   Valid values: ``bold``, ``italic``, ``no_antialias``, ``gray_antialias``,
   ``subpixel_antialias``, ``directwrite`` (Windows).
   有效值：``bold``， ``italic``， ``no_antialias``， ``gray_antialias``，
   ``subpixel_antialias``， ``directwrite`` （对Windows平台有效）。
``gutter``
   Toggles display of gutter.
   开/关侧边栏选项。
``rulers``
   Columns in which to display vertical rules. Accepts a list of numeric values
   (e. g. ``[79, 89, 99]`` or a single numeric value (e. g. ``79``).
   设置标尺所在的列坐标。接受一个数字值的列表（例如 ``[79, 89, 99]`` 或者一个单一的数字值 ``79``）。
``draw_minimap_border``
   Set to ``true`` to draw a border around the minimap's region corresponding
   to the the view's currently visible text. The active color scheme's
   ``minimapBorder`` key controls the border's color.
   如果将这个值设置为 ``true`` ，就将根据视图当前可见文本的内容在迷你地图区域画一个边框。当前选中的
   配色方案中的 ``minimapBorder`` 键对应的值用于控制边框的颜色。
``highlight_line``
   Set to ``false`` to stop highlighting lines with a cursor.
   将这个值设置为 ``false`` 来阻止高亮当前光标所在行。
``line_padding_top``
   Additional spacing at the top of each line, in pixels.
   每行文字与上一行的额外距离，以像素为单位。
``line_padding_bottom``
   Additional spacing at the bottom of each line, in pixels.
   每行文字与下一行的额外距离，以像素为单位。
``scroll_past_end``
   Set to ``false`` to disable scrolling past the end of the buffer. If ``true``,
   Sublime Text will leave a wide, empty margin between the last line and the
   bottom of the window.
   设置为 ``false`` 以关闭超出缓冲区的滚动。如果设置为 ``true`` ，Sublime Text将在文本的最后一行
   与窗口下边界之间添加一大块空白区域。
``line_numbers``
   Toggles display of line numbers in the gutter.
   开/关对行号的显示。
``word_wrap``
   If set to ``false``, long lines will be clipped instead of wrapped. Scroll
   the screen horizontally to see the clipped text.
   如果设置为 ``false`` 那么对于内容很多的行，文本将被截取，而不会自动换行。在水平方向拖动滚动条可以
   查看被截取的文字。
``wrap_width``
   If greater than ``0``, wraps long lines at the specified column as opposed
   to the window width. Only takes effect if ``wrap_width`` is set to ``true``.
   如果这个值大于 ``0`` ， 系统就会在这个指定的列进行换行切分；否则会根据屏幕的宽度进行换行。这个值
   只有在 ``wrap_width`` 设置为 ``true`` 的时候才有效果。
``indent_subsequent_lines``
   If set to ``false``, wrapped lines will not be indented. Only takes effect
   if ``wrap_width`` is set to ``true``.
   如果这个值设置为 ``false`` ，被转换的行就不会进行缩进。只有在 ``wrap_width`` 为 ``true`` 时
   才有效。
``draw_centered``
   If set to ``true``, text will be drawn centered rather than left-aligned.
   如果设置为 ``true`` ，文本将居中对齐，否则为左对齐。
``match_brackets``
   Set to ``false`` to disable underlining the brackets surrounding the cursor.
   当值设置为 ``false`` 时，光标放在括号周围的时候就不会显示下划线。
``match_brackets_content``
   Set to ``false`` is you'd rather only highlight the brackets when the cursor
   is next to one.
   设置光标在括号周围时，是否要高亮括号中的内容。
``match_brackets_square``
   Set to ``false`` to stop highlighting square brackets. Only takes effect if
   ``match_brackets`` is ``true``.
   如果设置项值为 ``false`` ，就停止对方括号的配对显示。只有在 ``match_brackets`` 值为 ``true``
   时有效。
``match_bracktets_braces``
   Set to ``false`` to stop highlighting curly brackets. Only takes effect if
   ``match_brackets`` is ``true``.
   如果设置项值为 ``false`` ，就停止对花括号的配对显示。只有在 ``match_brackets`` 值为 ``true``
   时有效。
``match_bracktets_angle``
   Set to ``false`` to stop highlighting angle brackets. Only takes effect if
   ``match_brackets`` is ``true``.
   如果设置项值为 ``false`` ，就停止对尖括号的配对显示。只有在 ``match_brackets`` 值为 ``true``
   时有效。

Automatic Behavior
自动行为设置项
******************

``auto_match_enabled``
   Toggles automatic pairing of quotes, brackets, etc.
   开/关自动配对引号、括号等符号。
``save_on_focus_lost``
   Set to true to automatically save files when switching to a different file
   or application.
   如果这个值为真，那么当用户切换到一个不同的文件，或不同的应用程序时，文件的内容将会自动保存。
``find_selected_text``
   If ``true``, the selected text will be copied into the find panel when it's
   shown.
   如果设置为 ``true`` ，那么当打开搜索面板时，当前选中的文字会被自动的复制到搜索面板中。
``word_separators``
   Characters considered to separate words in actions like advancing the cursor,
   etc. They are not used in all contexts where a notion of a word separator is
   useful (e. g.: word wrapping). In such other contexts, the text might be
   tokenized based on other criteria (e. g. the syntax definition rules).
   设置在动作中用于分割单词的字符，例如光标跨单词移动的时候来界定单词的分隔符。这个单词分隔符并
   不用于所有需要区分单词的情况（例如：换行时不切分单词）。在这种情况下，文本是基于其他标准来界
   定的（例如：语法定义规则）。
``ensure_newline_at_eof_on_save``
   Always adds a new line at the end of the file if not present when saving.
   如果文本末尾没有空行，那么当保存文件的时候，会自动在文件末尾添加一个空行。

System and Miscellaneous Settings
系统与其他设置项
*********************************

``is_widget``
   Returns ``true`` if the buffer is an input field in a dialog as opposed to
   a regular buffer.
   当缓冲区为输入对话框中的输入域的时候，返回 ``true`` 。
``spell_check``
   Toggles the spell checker.
   开/关拼写检查选项。
``dictionary``
   Word list to be used by the spell checker. Accepts a path rooted at the
   data directory (e. g.: ``Packages/Language - English/en_US.dic``). You can
   `add more dictionaries <http://extensions.services.openoffice.org/en/dictionaries>`_.
   拼写检查器可选的单词列表。接受从数据目录开始的一个路径（例如： ``Packages/Language - English/en_US.dic`` ）。
   你也可以 `添加更多目录 <http://extensions.services.openoffice.org/en/dictionaries>`_ 。
``fallback_encoding``
   The encoding to use when the encoding can't be determined automatically.
   ASCII, UTF-8 and UTF-16 encodings will be automatically detected.
   控制当无法自动判断编码的时候选用的默认编码。系统可以自动检测的编码包括ASCII，UTF-8以及UTF－16.
``default_line_ending``
   Determines what characters to use to designate new lines. Valid values:
   ``system`` (OS-dependant), ``windows`` (``CRLF``) and ``unix`` (``LF``).
   控制系统使用的换行符的字符。有效选项： ``system`` （OS相关）， ``windows`` （即 ``CRLF`` ）以及
   ``unix`` （ ``LF`` ）。
``tab_completion``
   Determines whether pressing :kbd:`Tab` will insert completions.
   控制按下 :kbd:`Tab` 时是否进行补全。


Build and Error Navigation Settings
构建与错误导航设置项
***********************************

``result_file_regex``
   Regular expression used to extract error information from some output dumped
   into a view or output panel. Follows the same rules as error capturing in
   build systems.º
   用于过滤视图或输出面板中的错误信息的正则表达式。这里的正则表达式遵循与构建系统中的错误捕获相同的规则。
``result_line_regex``
   Regular expression used to extract error information from some output dumpºed
   into a view or output panel. Follows the same rules as error capturing in
   build systems.
   用于过滤视图或输出面板中的错误信息的正则表达式。这里的正则表达式遵循与构建系统中的错误捕获相同的规则。
``result_base_dir``
   Directory to start looking for offending files in based on information
   extracted with ``result_file_regex`` and ``result_line_regex``.
   设置基于 ``result_file_regex`` 以及 ``result_line_regex`` 抽取出来的信息开始搜索的文件路径。
``build_env``
   List of paths to add to build systems by default.
   默认添加到构建系统中的路径列表。


File and Directory Settings
文件与目录设置项
***************************

``default_dir``
   Sets the default save directory for the view.
   设置视图对应的默认保存路径。


Input Settings
输入设置项
**************

``command_mode``
   If set to ``true``, the buffer will ignore key strokes. Useful to emulate
   Vim.
   如果将这个值设为 ``true`` ，则缓冲区将忽略用户按键。这对模拟Vim很有帮助。
