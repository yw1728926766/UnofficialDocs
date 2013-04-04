Completions
补全
===========

Completions provide an IDE-like functionality to insert dynamic content through
the completions list or by pressing :kbd:`Tab`.
补全提供了像IDE那样的使用补全列表或者 :kbd:`Tab` 键插入动态内容的功能。

File Format
文件格式
***********

Completions are JSON files with the ``.sublime-completions`` extension.
补全信息是以 ``.sublime-completions`` 作为扩展名的JSON文件。

Structure of a Completions List
补全列表的结构
*******************************

``scope``
	Determines whether the completions are to be sourced from this file. See
	:ref:`scopes-and-scope-selectors` for more information.
	控制补全是否应该在这个文件中发挥作用。参考 :ref:`作用域与作用域选择子` 来了解更多信息。

``completions``
	Array of completions.
	补全的数组。

Here's an excerpt from the html completions::
下面是从html补全列表中截取出来的一部分::

	{
		"scope": "text.html - source - meta.tag, punctuation.definition.tag.begin",

		"completions":
		[
			{ "trigger": "a", "contents": "<a href=\"$1\">$0</a>" },
			{ "trigger": "abbr", "contents": "<abbr>$0</abbr>" },
			{ "trigger": "acronym", "contents": "<acronym>$0</acronym>" }

		]
	}


Types of Completions
补全的类型
********************

Plain Strings
纯文本字符串
-------------

Plain strings are equivalent to an entry where the ``trigger`` is identical to
the ``contents``::
当某个补全项 ``trigger`` 的内容与 ``contents`` 的内容完全一样的时候，纯文本字符串与这个补全项
是等价的。

	"foo"

	# is equivalent to:
	# 等价于：

	{ "trigger": "foo", "contents": "foo" }

Trigger-based Completions
基于触发内容的补全
-------------------------

``trigger``
	Text that will be displayed in the completions list and will cause the
	``contents`` to be inserted when validated.
	在补全列表中显示的文本，在被确认后，对应的 ``contents`` 内容被插入到缓冲区中。

``contents``
	Text to be inserted in the buffer. Can use snippet features.
	要插入到缓冲区中的文本。可以使用代码片段的特性。


Sources for Completions
补全的来源
***********************

These are the sources for completions the user can control:
用户可以控制的补全来源包括：

	* ``.sublime-completions``
	* ``EventListener.on_query_completions()``

Additionally, other completions are folded into the final list:
除此之外，其他在最终补全列表中可以显示的内容包括：

	* Snippets
	* Words in the buffer
	* 代码片段
	* 缓冲区中的单词

Priority of Sources for Completions
补全来源的优先级
-----------------------------------

	* Snippets
	* API-injected completions
	* ``.sublime-completions`` files
	* Words in buffer
	* 代码片段
	* 使用API插入的补全内容
	* ``.sublime-completions`` 文件
	* 缓冲区中的单词

Snippets will only be automatically completed against an exact match of their
tab trigger. Other sources for completions are filtered with a case insensitve
fuzzy search instead.
代码片段只有在与设置的tab触发器精确匹配时才会被插入。其他类型的补全则是使用大小写不敏感的模糊
搜索进行匹配。


The Completions List
补全列表
*********************

To use the completions list:
要使用补全列表需要：

	* Press :kbd:`Ctrl+spacebar` to open
	* Optionally, press :kbd:`Ctrl+spacebar` again to select next entry
	* Press :kbd:`Enter` or :kbd:`Tab` to validate selection
	* 按 :kbd:`Ctrl+空格` 来打开补全列表
	* 可选的, 再次按下 :kbd:`Ctrl+空格` 来选择下一个候选项
	* 按下 :kbd:`回车` or :kbd:`Tab` 来确认选择

.. note::
	The current selection in the completions list can actually be validated with
	any punctuation sign that isn't itself bound to a snippet.
.. 注释::
	补全列表中被选中的当前项可以用任何没有被绑定到代码片段触发器中的标点符号来确认插入。

Snippets show up in the completions list following the pattern:
``<tab_trigger> : <name>``. For the other completions, you will just see the
text to be inserted.
代码片段以如下形式出现在补全列表中：``<tab触发器> : <名称>`` 。对于其他补全项，你只能看到要被
插入的文本。

If the list of completions can be narrowed down to one choice, the autocomplete
dialog will be bypassed and the corresponding content will be inserted straight
away according to the priority rules stated above.
当补全列表被缩减到只有一个候选项时，系统就会绕开自动补全对话框，根据之前介绍的优先级，对应内容
会被直接插入。


Enabling and Disabling Tab Completion for Completions
为补全列表启用或禁用Tab补全
*****************************************************

The ``tab_completion`` setting is ``true`` by default. Set it to ``false`` if
you want :kbd:`Tab` to stop sourcing the most likely completion. This setting
has no effect on triggers defined in ``.sublime-snippet`` files, so snippets
will always be inserted after a :kbd:`Tab`.
``tab_completion`` 选项默认是 ``true`` 。如果你想停止 :kbd:`Tab` 键对最可能选项的索引功能，
就把这个值设置为 ``false`` 。这个设置项对定义在 ``.sublime-snippet`` 文件中的触发器没有效果，
因此按下 :kbd:`Tab` 时，代码片段一定会被插入。

With ``tab_completion`` on, The same order of priority as stated above applies,
but, unlike in the case of the completions list, Sublime Text will always
insert a completion, even if faced with an ambiguous choice.
当 ``tab_completion`` 选项开启的时候，上面介绍的优先级顺序仍然有效，但是，与补全列表不同的是，
Sbulime Text总会插入一个补全项，及时选择项存在模糊内容。

Inserting a Literal Tab
插入一个Tab（缩进）字符
-----------------------

If ``tab_completion`` is ``true``, you can press ``Shift+Tab`` after a prefix
to insert a literal tab character.
如果 ``tab_completion`` 值为 ``true`` ，你可以使用 ``Shift+Tab`` 来插入一个缩进字符。
