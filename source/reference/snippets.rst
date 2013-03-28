.. sublime: wordWrap false

Snippets
代码片段
========

Compatibility with Textmate
与Textmate的兼容性
***************************

Sublime Text snippets are generally compatible with Textmate snippets.
Sublime Text的代码片段与Textmate的代码片段基本兼容。

File Format
文件格式
***********

Snippet files are XML files with the ``sublime-snippet`` extension.
代码片段文件是有 ``sublime-snippet`` 后缀的XML文件。

.. code-block:: xml

    <snippet>
        <content><![CDATA[]]></content>
        <tabTrigger></tabTrigger>
        <scope></scope>
        <description></description>
    </snippet>

``content``
    Actual snippet content.
    实际的代码片段内容。

``tabTrigger``
    Implicit keybinding for this snippet. Last key (implicit) is ``TAB``.
    与这段代码片段关联的隐式按键绑定。最后一个（隐式的）按键式 ``TAB`` 。

``scope``
    Scope selector to activate this snippet.
    适用于这段代码片段的作用域选择子。

``description``
    User friendly description for menu item.
    为了菜单项准备的用户友好的说明性文字。

Escape Sequences
转义序列
****************

``\$``
    Literal ``$``.

``\$``
    常量 ``$`` 。

Environment Variables
环境变量
*********************

======================      =====================================================================
``$PARAM1 .. $PARAMn``      Arguments passed to the ``insertSnippet`` command.
``$PARAM1 .. $PARAMn``      传递给 ``insertSnippet`` 命令的各个参数。
``$SELECTION``              The text that was selected when the snippet was triggered.
``$SELECTION``              代码片段被触发的时候选中的文本内容。
``$TM_CURRENT_LINE``        Content of the line the cursor was in when the snippet was triggered.
``$TM_CURRENT_LINE``        代码片段被触发的时候光标所在行的内容。
``$TM_CURRENT_WORD``        Current word under the cursor when the snippet was triggered.
``$TM_CURRENT_WORD``        代码片段被触发的时候光标所在的单词。
``$TM_FILENAME``            File name of the file being edited including extension.
``$TM_FILENAME``            正在编辑的文件名称，包含文件扩展名。
``$TM_FILEPATH``            File path to the file being edited.
``$TM_FILEPATH``            正在编辑的文件的文件路径。
``$TM_FULLNAME``            User's user name.
``$TM_FULLNAME``            用户的用户名。
``$TM_LINE_INDEX``          Column the snippet is being inserted at, 0 based.
``$TM_LINE_INDEX``          插入代码片段的列的位置，位置是从0开始计数的。
``$TM_LINE_NUMBER``         Row the snippet is being inserted at, 1 based.
``$TM_LINE_NUMBER``         插入代码片段的行的位置，位置是从1开始计数的。
``$TM_SELECTED_TEXT``       An alias for ``$SELECTION``.
``$TM_SELECTED_TEXT``       与 ``$SELECTION`` 是等价的。
``$TM_SOFT_TABS``           ``YES`` if ``translateTabsToSpaces`` is true, otherwise ``NO``.
``$TM_SOFT_TABS``           当 ``translateTabsToSpaces`` 选项是真的时候，值是 ``YES`` ，否则为 ``NO`` 。
``$TM_TAB_SIZE``            Spaces per-tab (controlled by the ``tabSize`` option).
``$TM_TAB_SIZE``            tab对应的空格数（受 ``tabSize`` 选项的控制）。
======================      =====================================================================

Fields
字域
******

Mark positions to cycle through by pressing ``TAB`` or ``SHIFT + TAB``.
标记代码片段中可以通过 ``TAB`` 或 ``SHIFT + TAB`` 循环的各个位置。

Syntax: ``$1`` .. ``$n``
语法： ``$1`` .. ``$n``

``$0``
    Exit mark. Position at which normal text editing should be resumed. By default,
    Sublime Text implicitly sets this mark at the end of the snippet's ``content`` element.
    退出标记。当循环到这个标记的时候，编辑器应该返回至正常的编辑模式。默认情况下，Sublime Text在 ``content``
    元素内容的结尾位置隐式的添加这个标记。

Fields with the same name mirror each other.
有相同名字的字域互相映射。

Place Holders
站位符
*************

Fields with a default value.
带有默认值的字域。

Syntax: ``${1:PLACE_HOLDER}`` .. ``${n:PLACE_HOLDER}``
语法： ``${1:PLACE_HOLDER}`` .. ``${n:PLACE_HOLDER}``

Fields and place holders can be combined and nested within other place holders.
字域和站位符可以遇其他的站位符进行组合和嵌套。

Substitutions
替换
**************

Syntax:
语法：

    - ``${var_name/regex/format_string/}``
    - ``${var_name/regex/format_string/options}``

``var_name``
    The field's name to base the substitution on: 1, 2, 3…
    替换展开所以来的字域的名字：1，2，3……
``regex``
    Perl-style regular expression: See the Boost library documentation for `regular expressions <http://www.boost.org/doc/libs/1_44_0/libs/regex/doc/html/boost_regex/syntax/perl_syntax.html>`_.
    Perl风格的正则表达式：关于`正则表达式 <http://www.boost.org/doc/libs/1_44_0/libs/regex/doc/html/boost_regex/syntax/perl_syntax.html>`_ ，请参考Boost库的文档。
``format_string``
    See the Boost library documentation for `format strings <http://www.boost.org/doc/libs/1_44_0/libs/regex/doc/html/boost_regex/format/perl_format.html>`_.
    参考Boost库文档的 `格式字符串 <http://www.boost.org/doc/libs/1_44_0/libs/regex/doc/html/boost_regex/format/perl_format.html>`_ 内容。
``options``
    Optional. Any of the following:
    可选的。可以选择下面的任何一个：
        ``i``
            Case-insensitive regex.
            忽略大小写敏感的正则。
        ``g``
            Replace all occurrences of ``regex``.
            替换所有匹配 ``regex`` 的内容。
        ``m``
            Don't ignore newlines in the string.
            在字符串中不要忽略换行符。
