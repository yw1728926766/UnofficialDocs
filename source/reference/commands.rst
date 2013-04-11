Commands
命令
********

Overview
概览
========

.. named actions, used everywhere, take json arguments
This list of commands is a work in progress.
对命令列表的整理仍在进行中。


About Paths in Command Arguments
关于命令参数中的路径信息
================================

Some commands take paths as parameters. Among these, some support snippet-like
syntax, while others don't. A command of the first kind would take a parameter
like *${packages}/SomeDir/SomeFile.Ext* whereas a command of the second kind
would take a parameter like *Packages/SomeDir/SomeFile.Ext*.
有些命令把路径作为参数。这些命令中，有些支持代码片段那样的语法，有些则不支持。第一中类型的命令
可以接受类似 *${packages}/SomeDir/SomeFile.Ext* 这样的参数，而第二种类型的命令可以接受类似
*Packages/SomeDir/SomeFile.Ext* 这样的参数。

Generally, newer commands support the snippet-like syntax.
大体上来说，较新引入的命令支持类似代码片段的语法。

Often, relative paths in arguments to commands are assumed to start at the
``Data`` directory.
通常情况下，认为命令参数中的相对路径是相对与 ``数据`` 目录来说的。

Variables in Paths as Arguments
参数中路径包含的变量
-------------------------------

The same variables available to build systems are expanded in arguments to
commands. See :ref:`build-system-variables` for more information.
构建系统中使用的变量在参数中也可以使用。参考 :ref:`构建系统变量` 来了解更多信息。


Commands
命令列表
========

**build**
	Runs a build system.
	运行某个构件系统。

	- **variant** [String]: Optional. The name of the variant to be run.
	- **variant** [String]: 可选参数。要运行配置的名称。

**run_macro_file**
	Runs a *.sublime-macro* file.
	运行一个 *.sublime-macro* 文件。

	- **file** [String]: Path to the macro file.
	- **file** [String]: 宏文件路径。

**insert_snippet**
	Inserts a snippet from a string or *.sublime-snippet* file.
	从字符串或者 *.sublime-snippet* 文件中插入一个代码片段。

	- **contents** [String]: Snippet as a string to be inserted.
	- **contents** [String]: 要插入的代码片段的字符串内容。
	- **name** [String]: Path to the *.sublime-snippet* file to be inserted.
	- **name** [String]: 要插入的 *.sublime-snippet* 文件的路径。

**insert**
	Inserts a string.
	插入一个字符串。

	- **characters** [String]: String to be inserted.
	- **characters** [String]: 要插入的字符串内容。

**move**
	Advances the caret by predefined units.
	根据指定的单位移动光标。

	- **by** [Enum]: Values: *characters*, *words*, *word_ends*, *subwords*, *subword_ends*, *lines*, *pages*, *stops*.
	- **by** [Enum]: 可选值: *characters*, *words*, *word_ends*, *subwords*, *subword_ends*, *lines*, *pages*, *stops* 。
	- **forward** [Bool]: Whether to advance or reverse in the buffer.
	- **forward** [Bool]: 在缓冲区中向前或向后移动。
	- **word_begin** [Bool]
	- **empty_line** [Bool]
	- **punct_begin** [Bool]
	- **separators** [Bool]

**move_to**
	Advances the caret to predefined locations.
	将光标移动到指定位置。

	- **to** [Enum]: Values: *bol*, *eol*, *bof*, *eof*, *brackets*.
	- **to** [Enum]: 可选值: *bol*, *eol*, *bof*, *eof*, *brackets*.
	- **extend** [Bool]: Whether to extend the selection. Defaults to ``false``.
	- **extend** [Bool]: 是否扩展选择内容。默认值是 ``false`` 。

**new_window**
	Opens a new window.
	打开一个新的窗口。

**close_window**
	Closes the active window.
	关闭当前活跃窗口。

**switch_file**
	Switches between two files with the same name and different extensions.
	在有相同文件名、不同扩展名的两个文件之间进行切换。

	- **extensions** [[String]]: Extensions (without leading dot) for which switching will be enabled.
	- **extensions** [[String]]: 切换可以发生的文件扩展名（不包括点号）。

**close**
	Closes the active view.
	关闭当前视图。

**close_file**
	Closes the active view and, under certain circumsances, the whole application.
	关闭当前视图，在某些情况下关闭整个应用程序。
	XXX Sounds kinda wrong.
	XXX 看上去好像不对。

**toggle_sidebar**
	Shows or hides the sidebar.
	开启或关闭侧边栏。

**toggle_full_screen**
	Toggles full screen mode on or off.
	开启或退出全屏模式。

**toggle_distraction_free**
	Toggles distraction free mode on or off.
	开启或退出免打扰模式。

**left_delete**
	Deletes the character right before the caret.
	删除光标前的那个字符。

**right_delete**
	Deletes the character right after the caret.
	删除光标后的那个字符。

**undo**
	Undoes the latest action.
	撤销上次操作。

**redo**
	Reapplies the latest undone action.
	重做上次撤销的操作。

**redo_or_repeat**
	Performs the latest action again.
	再次执行上次的动作。

**soft_undo**
	Undoes each action stepping through granular edits.
	先移动到编辑位置再进行撤销操作。

**soft_redo**
	Redoes each action stepping through granular edits.
	先移动到编辑位置再进行重做操作。

**cut**
	Removes the selected text and sends it to the system clipboard. Put
	differently, it cuts.
	把当前选中的文字从缓冲区中移除，并送到系统剪贴板中。换句话说，执行剪切操作。

**copy**
	Sends the selected text to to the system clipboard.
	把当前选中的文字送到系统剪贴板中。

**paste**
	Inserts the clipboard contents after the caret.
	把剪贴板中的内容插入到光标后。

**paste_and_indent**
	Inserts the clipboard contents after the caret and indents contextually.
	把剪贴板中的内容插入到光标后同时根据上下文进行缩进。

**select_lines**
	Adds a line to the current selection.
	在当前选择的内容中添加一行。

	- **forward** [Bool]: Whether to add the next or previous line. Defaults to
	  ``true``.
	- **forward** [Bool]: 添加下一行还是上一行。默认值是 ``true`` 。

**scroll_lines**
	Scrolls lines in the view.
	在视图中滚动行。

	- **amount** [Float]: Positive values scroll lines down and negative values scroll lines up.
	- **amount** [Float]: 正值向下滚动，负值向上滚动。

**prev_view**
	Switches to the previous view.
	切换到上一个视图。

**next_view**
	Switches to the next view.
	切换到下一个视图。

**next_view_in_stack**
	Switches to the most recently active view.
	切换到最近的活跃视图。

**previous_view_in_stack**
	Switches to the view that was active before the most recently active view.
	I don't think this is very clear or even true.
	切换到最近活跃视图的前一个活跃视图。我不认为这种说法非常确切，这么说甚至是不正确的。

**select_all**
	Select the view's content.
	选择视图的全部内容。

**split_selection_into_lines**
	Unsurprisingly, it splits the selection into lines.
	不出所料的，把当前的选择切散成不同行。

**single_selection**
	Collapses multiple selections into a single selection.
	把多重选择整合成单一选择。

**clear_fields**
	Breaks out of the active snippet field cycle.
	跳出活跃代码片段域的选择。

**hide_panel**
	Hides the active panel.
	隐藏当前活跃面板。

	- **cancel** [Bool]: Notifies the panel to restore the selection to what it
	was when the panel was opened. (Only incremental find panel.)
	- **cancel** [Bool]: 当面板打开的时候恢复它之前选择的内容。（仅对增量搜索面板有效。）

**hide_overlay**
	Hides the active overlay.  Show the overlay using the show_overlay command.
	隐藏覆盖控件。使用 show_overlay 命令打开覆盖控件。

**hide_auto_complete**
	Hides the auto complete list.
	隐藏自动补全列表。

**insert_best_completion**
	Inserts the best completion that can be inferred from the current context.
	XXX Probably useless. XXX
	插入根据当前上下文能推断出的最佳补全内容。 XXX 可能没什么用。 XXX

	- **default** [String]: String to insert failing a best completion.
	- **default** [String]: 当没有找到最佳补全内容时插入的字符串。

**replace_completion_with_next_completion**
	XXX Useless for users. XXX
	XXX 对用户来说没什么用。 XXX

**reindent**
	XXX ??? XXX

	（译者注：重新进行缩进操作，常用于整理文件缩进。）

**indent**
	Increments indentation.
	增加缩进。

**next_field**
	Advances the caret to the text snippet field in the current snippet field
	cycle.
	将光标移动到下一个代码片段中的可修改区域。

**prev_field**
	Moves the caret to the previous snippet field in the current snippet field
	cycle.
	将光标移动到上一个代码片段中的可修改区域。

**commit_completion**
	Inserts into the buffer the item that's currently selected in the auto
	complete list. XXX Probably not useful for users. XXX
	向缓冲区中插入自动补全列表中当前选中项的内容。 XXX 对用户来说没很么用。 XXX


**unindent**
	Unindents.
	取消缩进。

**toggle_overwrite**
	Toggles overwriting on or off.
	开启关闭覆盖插入选项。

**expand_selection**
	Extends the selection up to predifined limits.
	将选择内容扩展到预定义的边界。

	- **to** [Enum]: Values: bol, hardbol, eol, hardeol, bof, eof, brackets, line.
	- **to** [Enum]: 可选值: bol, hardbol, eol, hardeol, bof, eof, brackets, line.

**find_under_expand**
	Adds a new selection based on the current selection or expands the
	selection to the current word.
	根据当前选中的内容增加一个新的选择或者把选择项扩展到当前单词。

**close_tag**
	Surrounds the current inner text with the appropiate tags.
	为当前内部文本添加适当的标签。

**toggle_record_macro**
	Starts or stops the macro recorder.
	开始或关闭宏录制器。

**run_macro**
	Runs the macro stored in the macro buffer.
	运行宏缓冲区中存储的宏脚本。

**show_overlay**
	Shows the requested overlay. Use the **hide_overlay** command to hide it.
	显示请求的覆盖控件。使用 **hide_overlay** 命令来隐藏覆盖控件。

	- **overlay** [Enum]:
                The type of overlay to show. Possible values:
                要显示的覆盖控件的类型。可选值：

		- *goto*: Show the `Goto Anything <http://docs.sublimetext.info/en/latest/file_management/file_management.html#goto-anything>`_ overlay.
		- *goto*: 显示 `Goto Anything（快速跳转） <http://docs.sublimetext.info/en/latest/file_management/file_management.html#goto-anything>`_ 覆盖控件。
		- *command_palette*: Show the `command palette <http://docs.sublimetext.info/en/latest/extensibility/command_palette.html>`_.
		- *command_palette*: 显示 `命令面板 <http://docs.sublimetext.info/en/latest/extensibility/command_palette.html>`_.

	- **show_files** [Bool]: If using the goto overlay, start by displaying files rather than an empty widget.
	- **show_files** [Bool]: 如果显示快速跳转面板，开始的时候显示文件列表，而不是显示一个空的控件。
	- **text** [String]: The initial contents to put in the overlay.
	- **text** [String]: 放到覆盖控件中的初始值。

**show_panel**
	Shows a panel.
	显示面板。

	- **panel** [Enum]: Values: incremental_find, find, replace, find_in_files, console
	- **panel** [Enum]: 可选值: incremental_find, find, replace, find_in_files, console
	- **reverse** [Bool]: Whether to search backwards in the buffer.
	- **reverse** [Bool]: 在缓冲区中是否后向搜索内容。
	- **toggle** [Bool]: Whether to hide the panel if it's already visible.
	- **toggle** [Bool]: 当面板已经可见时，是否隐藏面板。

**find_next**
	Finds the next occurrence of the current search term.
	找到当前搜索内容的下一个匹配项。

**find_prev**
	Finds the previous occurrence of the current search term.
	找到当前搜索内容的上一个匹配项。

**find_under**
	Finds the next occurrence of the current selection or the current word.
	找到与当前选中内容或光标所在位置档次匹配的下一个内容。

**find_under_prev**
	Finds the previous occurrence of the current selection or the current word.
	找到与当前选中内容或光标所在位置档次匹配的上一个内容。

**find_all_under**
	Finds all occurrences of the current selection or the current word.
	选中与当前选择内容或光标所在位置单词匹配的所有内容。

**slurp_find_string**
	Copies the current selection or word into the "find" field of the find
	panel.
	复制当前选中内容或当前单词到搜索面板中的 "find" 域。

**slurp_replace_string**
	Copies the current selection or word into the "replace" field of the find
	and replace panel.
	复制当前选中内容或当前单词到搜索域替换面板中的 "replace" 域。

**next_result**
	Advance to the next captured result.
	移动到下一个搜索到的结果。

**prev_result**
	Move to the previous captured result.
	移动到上一个搜索到的结果。

**toggle_setting**
	Toggles the value of a boolean setting.
	修改布尔型设置项的值。

	- **setting** [String]: The name of the setting to be toggled.
	- **setting** [String]: 要修改的设置项的名称。

**next_misspelling**
	Advance to the next misspelling
	移动到下一个错误拼写的单词的位置。

**prev_misspelling**
	Move to the previous misspelling.
	移动到上一个错误拼写的单词的位置。

**swap_line_down**
	Swaps the current line with the line below.
	交换当前行与下一行。

**swap_line_up**
	Swaps the current line with the line above.
	交换当前行与上一行。

**toggle_comment**
	Comments or uncomments the active lines.
	为当前行添加或取消注释。

	- **block** [Bool]: Whether to use a block comment.
	- **block** [Bool]: 是否使用块注释。

**join_lines**
	Joins the current line with the next one.
	把当前行与下一行连接起来。

**duplicate_line**
	Duplicates the current line.
	重复当前行内容。

**auto_complete**
	Opens the auto comeplete list.
	打开自动补全列表。

**replace_completion_with_auto_complete**
	XXX Useless for users. XXX
	XXX 对用户来说没什么用。 XXX

**show_scope_name**
	Shows the name for the caret's scope in the status bar.
	在状态栏中显示光标所在作用域的名称。

**exec**
	Runs an external process asynchronously.
	异步运行一个外部进程。

	XXX Document all options.
	XXX 为所有选项添加文档。

**transpose**
	Makes stuff dance.
	移动内容。

**sort_lines**
	Sorts lines.
	对行进行排序。

	- **case_sensitive** [Bool]: Whether the sort should be case sensitive.
	- **case_sensitive** [Bool]: 排序时是否考虑大小写。

**set_layout**
	XXX

**focus_group**
	XXX

**move_to_group**
	XXX

**select_by_index**
	XXX

**next_bookmark**
	Select the next bookmarked region.
	选择下一个被标记的区域。

**prev_bookmark**
	Select the previous bookmarked region.
	选择上一个被书签标记的区域。

**toggle_bookmark**
	Sets or unsets a bookmark for the active region(s). (Bookmarks can be
	accessed via the regions API using ``"bookmarks"`` as the key.)
	对活跃区域设置书签或取消书签。（在区域API中使用 ``"bookmarks"`` 作为键可以访问书签内容。）

**clear_bookmarks**
	Removes all bookmarks.
	清楚所有书签。

**select_all_bookmarks**
	Selects all bookmarked regions.
	选择所有被书签标记过的区域。

**wrap_lines**
	Wraps lines. By default, it wraps lines at the first ruler's column.
	环绕行。默认情况下，在第一个标尺所在的列进行环绕。

	- **width** [Int]: Specifies the column at which lines should be wrapped.
	- **width** [Int]: 设置环绕开始的列坐标。

**upper_case**
	Makes the selection upper case.
	把选择的内容改成大写。

**lower_case**
	Makes the selection lower case.
	把选择的内容改成小写。

**set_mark**
	XXX

**select_to_mark**
	XXX

**delete_to_mark**
	XXX

**swap_with_mark**
	XXX

**yank**
	XXX

**show_at_center**
	XXX

**increase_font_size**
	Increases the font size.
	增加字体大小。

**decrease_font_size**
	Decreases the font size.
	较少字体大小。

**fold**
	XXX

**unfold**
	XXX

**fold_by_level**
	XXX

**context_menu**
	Shows the context menu.
	显示上下文菜单。

.. Some regex-related and search-related commands missing. they don's seem to
.. be too useful.
.. 这里没有列出一些与正则表达式相关或与搜索相关的命令。这些命令看起来没有太大用处。
