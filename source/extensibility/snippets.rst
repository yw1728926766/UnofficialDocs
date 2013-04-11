Snippets
代码片段
========

Whether you are coding or writing the next vampire best-seller, you're likely to
need certain short fragments of text again and again. Use snippets to save yourself
tedious typing. Snippets are smart templates that will insert text for you and
adapt it to their context.
无论你是在敲代码还是撰写你的大作，你都会一遍一遍地写到一些小的重复片段。使用代码片段
保存这些冗长的部分。是一种很聪明的模板，它会根据你输入的上下文帮助你添加文本。

To create a new snippet, select **Tools | New Snippet…**. Sublime Text will
present you with an skeleton for a new snippet.
要新建一个代码片段，选择目录 **Tools | New Snippet…**。Sublime Text会介绍给你一个
框架来新建一个代码片段。

Snippets can be stored under any package's folder, but to keep it simple while
you're learning, you can save them to your ``Packages/User`` folder.
代码片段可以存储在任何一个包文件下，为了在你学习时方便，你可以将其保存在你的
目录``Packages/User``下。

Snippets File Format
代码片段文件格式
********************

Snippets typically live in a Sublime Text package. They are simplified XML files
with the extension ``sublime-snippet``. For instance, you could have a
``greeting.sublime-snippet`` inside an ``Email`` package.
代码片段一般保存在Sublime Text的包里。这里使用了扩展``sublime-snippet``简化XML的
文件。比如，你可以在包``Email``里保存``greeting.sublime-snippet``。

The structure of a typical snippet is as follows (including the default hints
Sublime Text inserts for your convenience):
典型的代码片段的结构如下（包括Sublime Text为方便你使用添加的默认提示）：

.. code-block:: xml

    <snippet>
        <content><![CDATA[Type your snippet here]]></content>
        <!-- Optional: Tab trigger to activate the snippet -->
        <tabTrigger>xyzzy</tabTrigger>
        <!-- Optional: Scope the tab trigger will be active in -->
        <scope>source.python</scope>
        <!-- Optional: Description to show in the menu -->
        <description>My Fancy Snippet</description>
    </snippet>

The ``snippet`` element contains all the information Sublime Text needs in order
to know *what* to insert, *whether* to insert it and *when*. Let's see all of
these parts in turn.
元素``snippet``包括Sublime Text需要的所有信息，以获取需要添加什么，是否添加以及
什么情况下。接下来我们看一下每一个部分。

``content``
    The actual snippet. Snippets can range from simple to fairly complex
    templates. We'll look at examples of both later.
    实际的代码片段。代码片段可以包括从最简单到相当复杂的模板。接下来，我们会看到
    它们的例子。

    Keep the following in mind when writing your own snippets:
    在编写你自己的代码片段时，你要记住以下内容：

        - If you want the get a literal ``$``, you have to escape it like this: ``\$``.
        - 如果你想输入``$``，你需要按照方式如下转义：``\$``。

        - When writing a snippet that contains indentation, always use tabs. The
          tabs will be transformed into spaces when the snippet is inserted if the
          option ``translateTabsToSpaces`` is set to ``true``.
        - 如果代码片段包括缩进，一般使用tab。选项``translateTabsToSpaces``为真时，
          代码片段添加的tab会自动转换成空格。

        The ``content`` must be included in a ``<![CDATA[…]]>`` section.
        Snippets won't work if you don't do this!
        标签``content``必须包含在块``<![CDATA[…]]>``中。如果不这么写，代码片段
        可不好用哦~

``tabTrigger``
    Defines the sequence of keys you will press to insert this snippet. The
    snippet will kick in as soon as you hit the :kbd:`Tab` key after typing
    this sequence.
    定义你在需要添加代码片段时按下的按键序列。在你按下按键序列后，再按下键盘上的`Tab`
    键，代码片段才会生效。

    A tab trigger is an implicit key binding.
    tab触发器是一个隐式的按键绑定。

``scope``
    Scope selector determining the context where the snippet will be active.
    See :ref:`scopes-and-scope-selectors` for more information.
    作用域选择子决定了代码片段在哪个范围内生效。
    详情请看:ref:`scopes-and-scope-selectors`。

``description``
    Used when showing the snippet in the Snippets menu. If not present, Sublime Text
    defaults to the name of the snippet.
    在代码片段目录显示代码片段时使用。如果没显示，Sublime Text默认使用代码片段名。

With this information, you can start writing your own snippets as described in
the next sections.
根据之前的信息，现在可以开始按照下面的章节写自己的代码片段了。

.. note::
注释：
    In the interest of brevity, we're only including the ``content``
    element's text in examples unless otherwise noted.
    为了简洁，除非另外说明，这里的例子中只包含``content``元素。

Snippet Features
代码片段特性
****************

Environment Variables
环境变量
---------------------

Snippets have access to contextual information in the form of environment variables.
Sublime Text sets the values of the variables listed below automatically.
代码片段根据环境变量获得上下文信息。Sublime Text会自动设定下面所述的变量值。

You can also add your own variables to provide extra information. These custom
variables are defined in ``.sublime-options`` files.
你也可以加上自己的变量来提供额外的信息。这些自定义变量都在文件``.sublime-options``
中定义。

======================    ====================================================================================
**$PARAM1, $PARAM2…**      Arguments passed to the ``insert_snippet`` command. (Not covered here.)
**$PARAM1, $PARAM2…**      传递给 ``insert_snippet`` 命令的各个参数。
**$SELECTION**             The text that was selected when the snippet was triggered.
**$SELECTION**             代码片段被触发的时候选中的文本内容。
**$TM_CURRENT_LINE**       Content of the line the cursor was in when the snippet was triggered.
**$TM_CURRENT_LINE**       代码片段被触发的时候光标所在行的内容。
**$TM_CURRENT_WORD**       Current word under the cursor when the snippet was triggered.
**$TM_CURRENT_WORD**       代码片段被触发的时候光标所在的单词。
**$TM_FILENAME**           File name of the file being edited including extension.
**$TM_FILENAME**           正在编辑的文件名称，包含文件扩展名。
**$TM_FILEPATH**           File path to the file being edited.
**$TM_FILEPATH**           正在编辑的文件的文件路径。
**$TM_FULLNAME**           User's user name.
**$TM_FULLNAME**           用户的用户名。
**$TM_LINE_INDEX**         Column the snippet is being inserted at, 0 based.
**$TM_LINE_INDEX**         插入代码片段的列的位置，位置是从0开始计数的。
**$TM_LINE_NUMBER**        Row the snippet is being inserted at, 1 based.
**$TM_LINE_NUMBER**        插入代码片段的行的位置，位置是从1开始计数的。
**$TM_SELECTED_TEXT**      An alias for **$SELECTION**.
**$TM_SELECTED_TEXT**      与 ``$SELECTION`` 是等价的。
**$TM_SOFT_TABS**          ``YES`` if ``translate_tabs_to_spaces`` is true, otherwise ``NO``.
**$TM_SOFT_TABS**          当 ``translateTabsToSpaces`` 选项是真的时候，值是 ``YES`` ，否则为 ``NO`` 。
**$TM_TAB_SIZE**           Spaces per-tab (controlled by the ``tab_size`` option).
**$TM_TAB_SIZE**           tab对应的空格数（受 ``tabSize`` 选项的控制）。
======================    ====================================================================================

Let's see a simple example of a snippet using variables:
接下来，我们看一个使用变量的简单的例子：

.. code-block:: perl

    ====================================
    USER NAME:          $TM_FULLNAME
    FILE NAME:          $TM_FILENAME
     TAB SIZE:          $TM_TAB_SIZE
    SOFT TABS:          $TM_SOFT_TABS
    ====================================

    # Output:
    ====================================
    USER NAME:          guillermo
    FILE NAME:          test.txt
     TAB SIZE:          4
    SOFT TABS:          YES
    ====================================


Fields
字域
------

With the help of field markers, you can cycle through positions within the
snippet by pressing the :kbd:`Tab` key. Fields are used to walk you through the
customization of a snippet once it's been inserted.
有了字域标记，你可以通过在代码片段中的某一位置按下键盘的`Tab`键来循环。一旦添加
了代码片段，字域可以通过自定义的信息帮助你走查。

.. code-block:: perl

    First Name: $1
    Second Name: $2
    Address: $3

In the example above, the cursor will jump to ``$1`` if you press :kbd:`Tab` once.
If you press :kbd:`Tab` a second time, it will advance to ``$2``, etc. You can also
move backwards in the series with :kbd:`Shift+Tab`. If you press :kbd:`Tab` after the
highest tab stop, Sublime Text will place the cursor at the end of the snippet's
content so that you can resume normal editing.
上面的例子中，当你按下一次键盘`Tab`键时，光标会跳转到``$1``。当你连续按下`Tab`两次是，会跳转
到``$2``等等。你也可以按下键盘的`Shift+Tab`键后退。如果你在最高制表位按下`Tab`键，Sublime Text
会将光标停留在代码片段内容的末尾，以便你可以重新开始编辑。

If you want to control where the exit point should be, use the ``$0`` mark.
如果你想控制退出点的位置，你可以使用``$0``标记。

You can break out of the field cycle any time by pressing :kbd:`Esc`.
你可以通过按下键盘的`Esc`键跳出字域循环。

Mirrored Fields
镜像字域
---------------

Identical field markers mirror each other: when you edit the first one, the rest
will be populated with the same value in real time.
相同的字域标记会相互映射：当你输入了第一个，剩下的立刻填充相同的值。

.. code-block:: perl

    First Name: $1
    Second Name: $2
    Address: $3
    User name: $1

In this example, "User name" will be filled out with the same value as "First Name".
这个例子中，"User name"会填充"First Name"的值。

Place Holders
占位符
-------------

By expanding the field syntax a little bit, you can define default values for
a field. Place holders are useful when there's a general case for your snippet
but you still want to keep its customization convenient.
通过扩展一些字域的语法，你可以为每一个域设定默认值。如果在你的代码片段里需要设定
一个一般的情况，你又希望不失去自定义的便捷，占位符是非常有用的。

.. code-block:: perl

    First Name: ${1:Guillermo}
    Second Name: ${2:López}
    Address: ${3:Main Street 1234}
    User name: $1

Variables can be used as place holders:
变量也可以用作占位符：

.. code-block:: perl

    First Name: ${1:Guillermo}
    Second Name: ${2:López}
    Address: ${3:Main Street 1234}
    User name: ${4:$TM_FULLNAME}

And you can nest place holders within other place holders too:
你也可以在其他的占位符里嵌套占位符：

.. code-block:: perl

    Test: ${1:Nested ${2:Placeholder}}

Substitutions
替换
-------------

.. WARNING::
.. 警告::
    This section is a draft and may contain inaccurate information.
    这部分是一个草稿，可能会有不准确的内容。

In addition to the place holder syntax, tab stops can specify more complex operations
with substitutions. Use substitutions to dynamically generate text based on a mirrored
tab stop.
除了占位符语法，制表符的设置可以使用替换设定更多复杂的操作。使用替换可以根据映射的制表符
设置动态地生成文本。

The substitution syntax has the following syntaxes:
替换的语法如下：

    - ``${var_name/regex/format_string/}``
    - ``${var_name/regex/format_string/options}``

**var_name**
    The variable name: 1, 2, 3…
    变量名：1, 2, 3…

**regex**
    Perl-style regular expression: See the `Boost library reference for regular expressions <http://www.boost.org/doc/libs/1_44_0/libs/regex/doc/html/boost_regex/syntax/perl_syntax.html>`_.
    Perl风格的正则表达式：关于`正则表达式 <http://www.boost.org/doc/libs/1_44_0/libs/regex/doc/html/boost_regex/syntax/perl_syntax.html>`_ ，请参考Boost库的文档。

**format_string**
    See the `Boost library reference for format strings <http://www.boost.org/doc/libs/1_44_0/libs/regex/doc/html/boost_regex/format/perl_format.html>`_.
    参考Boost库文档的 `格式字符串 <http://www.boost.org/doc/libs/1_44_0/libs/regex/doc/html/boost_regex/format/perl_format.html>`_ 内容。

**options**
    Optional. May be any of the following:
    可选的。可以选择下面的任何一个：
        **i**
            Case-insensitive regex.
            忽略大小写敏感的正则。
        **g**
            Replace all occurrences of ``regex``.
            替换所有匹配 ``regex`` 的内容。
        **m**
            Don't ignore newlines in the string.
            在字符串中不要忽略换行符。

With substitutions you can, for instance, underline text effortlessly:
有了替换，比如，你可以如此简单地添加文本下划线：

.. code-block:: perl

          Original: ${1:Hey, Joe!}
    Transformation: ${1/./=/g}

    # Output:

          Original: Hey, Joe!
    Transformation: =========
