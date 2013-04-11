Plugins
插件
=======

.. seealso::
更多信息请参考：

   :doc:`API Reference <../reference/api>`
        More information on the Python API.
   :doc:`API参考文档 <../reference/api>`
        有关Python API的更详细的信息。

   :doc:`Plugins Reference <../reference/plugins>`
        More information about plugins.
   :doc:`插件参考文档 <../reference/api>`
        有关插件的更详细的信息。


Sublime Text 2 is programmable with Python scripts. Plugins reuse existing
commands or create new ones to build a feature. Plugins are rather a logical
entity than a physical one.
Sublime Text 2可以使用Python脚本进行编程。插件可以重用已有的命令或者新建新的特性。
插件是指逻辑上的，而不是屋里存在的。

Prerequisites
预备知识
*************

In order to write plugins, you must be able to program in Python_.
要写一个插件，你必须要会用Python编程。

.. _Python: http://www.python.org


Where to Store Plugins
插件放到哪里
**********************

Sublime Text 2 will look for plugins in these places:
Sublime Text 2会在以下目录中寻找可用的插件：

* ``Packages``
* ``Packages/<pkg_name>/``
* ``Packages/<包名称>``

Consequently, any plugin nested deeper in ``Packages`` won't be loaded.
所以，存放在 ``Packages`` 更深层次的目录结构中的插件不会被加载。

Keeping plugins right under ``Packages`` is discouraged, because Sublime Text
sorts packages in a predefined way before loading them. Thus, you might get
confusing results if your plugins live outside of a package.
让插件都存放在 ``Packages``会有些让人失望，因为Sublime Text会在加载插件之前
通过预先设定的方式排序包组。因此，如果你的插件在一个包的外面，可能会有意想不到的结果。

Your First Plugin
编写第一个插件
*****************

Let's write a "Hello, World!" plugin for Sublime Text 2:
下面，我们给Sublime Text 2写一个"Hello, World!"插件吧：

#. Select **Tools | New Plugin…** in the menu.
#. 选择目录**Tools | New Plugin…**。
#. Save to ``Packages/User/hello_world.py``.
#. 保存到``Packages/User/hello_world.py``。

You've just written your first plugin. Let's put it to use:
你现在完成了你的第一个插件，下面将其投入使用：

#. Create a new buffer (``Ctrl+n``).
#. 新建一个缓冲区（``Ctrl+n``）。
#. Open the python console (``Ctrl+```).
#. 打开python命令行（``Ctrl+```）。
#. Type: ``view.run_command("example")`` and press enter.
#. 输入：``view.run_command("example")``，然后按下回车。

You should see the text "Hello, World!" in your new buffer.
你会看到你的新缓冲区内显示"Hello, World!"。

Analyzing Your First Plugin
分析你的第一个插件
***************************

The plugin created in the previous section should look roughly like this::
前面我们编写插件大致如此：

    import sublime, sublime_plugin

    class ExampleCommand(sublime_plugin.TextCommand):
        def run(self, edit):
            self.view.insert(edit, 0, "Hello, World!")


The ``sublime`` and ``sublime_plugin`` modules are both provided by
Sublime Text 2.
``sublime``和``sublime_plugin``是Sublime Text 2提供的。

New commands derive from the ``*Command`` classes defined in ``sublime_plugin``
(more on this later).
新命令继承定义在``sublime_plugin``的``*Command``类（后面会进行详细的描述）。

The rest of the code is concerned with particulars of the ``TextCommand`` or
the API that we'll discuss in the next sections.
剩下的代码是来自于``TextCommand``的细节以及我们后面要讨论的API。

Before moving on, though, we'll look at how we called the new command: We first
opened the python console, and then issued a call to ``view.run_command()``. This
is a rather inconvenient way of using plugins, but it's often useful when
you're in the development phase. For now, keep in mind that your commands
can be accessed through key bindings or other means, just as other commands are.
在向下继续之前，嗯。。我们会看到如何调用新命令：首先，我们打开python命令行，然后
调用``view.run_command()``。这样使用插件显然是很不方便的，但是在开发阶段还是比较
有用的。目前为止，你要记住，自定义的命令可以通过按键绑定或者其他方式使用，就像其
他命令一样。

Conventions for Command Names
命令名称的命名规则
-----------------------------

You might have noticed that our command is defined with the name ``ExampleCommand``,
but we pass the string ``example`` to the API call instead. This is necessary because
Sublime Text 2 normalizes command names by stripping the ``Command`` suffix and
separating ``CamelCasedPhrases`` with underscores, like this: ``camel_cased_phrases``.
你可能已经注意到了我们的命令是以``ExampleCommand``命名的，但是我们向API传入的参数却是
``example``。Sublime Text 2是通过截断``Command``的后缀，在``CamelCasedPhrases``中加入
下弧线的方式，比如``camel_cased_phrases``，来统一命令名称的。

New commands should follow the pattern mentioned above for class names.
新的命令必须要按照上面的方式命名类的名称。

Types of Commands
命令类型
*****************

You can create the following types of commands:
你可以新建以下类型的命令：

* Application commands (``ApplicationCommand``)
* 应用程序命令（``ApplicationCommand``）
* Window commands (``WindowCommand``)
* 窗口命令（``WindowCommand``）
* Text commands (``TextCommand``)
* 文本命令（``TextCommand``）

When writing plugins, consider your goal and choose the appropriate type of
commands for your plugin.
当你编写插件时，请根据你的目的选择合适的命令类型。

Shared Traits of Commands
命令之间的共享特性
-------------------------

All commands need to implement a ``.run()`` method in order to work. Additionally,
they can receive and arbitrarily long number of keyword parameters.
所有的命令都必须实现一个``.run()``方法才能运行。另外，所有命令都可以接受任意长度的
关键字参数。

Application Commands
应用程序命令
--------------------

Application commands derive from ``sublime_plugin.ApplicationCommand`` and
can be executed with ``sublime.run_command()``.
应用程序命令继承于``sublime_plugin.ApplicationCommand``，可以通过``sublime.run_command()``
执行。

Window Commands
窗口命令
---------------

Window commands operate at the window level. This doesn't mean that you cannot
manipulate views from window commands, but rather that you don't need views to
exist in order for window commands to be available. For instance, the built-in
command ``new_file`` is defined as a ``WindowCommand`` so it works too when no
view is open. Requiring a view to exist in that case wouldn't make sense.
串口命令是在窗口级生效的。这并不意味着你不能通过窗口命令控制视图，但是这也并不
是不需要你开启一些视图来让窗口命令生效。比如，内置命令 ``new_file`` 是一个 
``窗口命令`` ，然而没有视图一样可以生效。因为此时要求打开一个视图并没有意义。

Window command instances have a ``.window`` attribute pointing to the window
instance that created them.
窗口命令实例有一个 ``.window`` 属性，指向创建它们的那个窗口实例。

The ``.run()`` method of a window command does not need to take any required
arguments.
窗口命令的``.run()``方法不需要传入参数。

Text Commands
文本命令
-------------

Text commands operate at the buffer level and they require a buffer to exist
in order to be available.
文本命令是在缓冲区级生效的，并且需要存在一个缓冲区使之生效。

View command instances have a ``.view`` attribute pointing to the view instance
that created them.
视图命令实例有一个 ``.view`` 属性，指向创建它们的那个窗口实例。

The ``.run()`` method of a text command needs to take an ``edit`` instance as
a first positional argument.
窗口命令的 ``.run()`` 方法需要一个 ``edit`` 实例作为第一个入参。

Text Commands and the ``edit`` Object
文本命令和 ``edit`` 对象
-------------------------------------

The edit object groups modifications to the view so undo and macros work in a
sensible way. You are responsible for creating and closing edit objects. To do
so, you can call ``view.begin_edit()`` and ``edit.end_edit()``. Text commands get
passed an open ``edit`` object in their ``run`` method for convenience.
Additionally, many ``View`` methods require an edit object.
编辑``edit``对象组修改视图，以便撤销和宏命令是以合理的方式运行。你有责任新建和
关闭edit对象。为此，你需要调用 ``view.begin_edit()`` 和 ``edit.end_edit()``。
文本命令为了方便，在其 ``run`` 方法中获取传入的 ``edit`` 对象。另外，许多 ``View``
方法都需要一个edit对象。 

Responding to Events
事件响应
--------------------

Any command deriving from ``EventListener`` will be able to respond to events.
任何继承自``EventListener``的命令都可以响应事件。

Another Plugin Example: Feeding the Completions List
其他插件的例子：添加补全列表
----------------------------------------------------

Let's create a plugin that fetches data from Google Autocomplete service and
feeds it to Sublime Text 2 completions list. Please note that as ideas for
plugins go, this a very bad one.
接下来，我们做一个从Google自动完成服务获取数据的插件，然后添加到Sublime Text 2
的补全列表。请注意对于将其作为一个插件，这并不是什么好主意。

::

	import sublime, sublime_plugin

	from xml.etree import ElementTree as ET
	from urllib import urlopen

	GOOGLE_AC = r"http://google.com/complete/search?output=toolbar&q=%s"

	class GoogleAutocomplete(sublime_plugin.EventListener):
	    def on_query_completions(self, view, prefix, locations):
	        elements = ET.parse(
	                        urlopen(GOOGLE_AC % prefix)
	                    ).getroot().findall("./CompleteSuggestion/suggestion")

	        sugs = [(x.attrib["data"],) * 2 for x in elements]

	        return sugs

.. note::
.. 注意::
	Make sure you don't keep this plugin around after trying it or it will
	interefere with the autocompletion system.
	确保你在这次尝试以后，不要保留这个插件，否则会干扰Google的自动完成系统的。

Learning the API
学习API
****************

In order to create plugins, you need to get acquainted with the Sublime Text
API and the available commands. Documentation on both is scarce at the time of
this writing, but you can read existing code and learn from it too. In
particular, the ``Packages/Default`` folder contains many examples of
undocumented commands and API calls.
为了编写插件，你需要熟悉Sublime Text API和内置命令。在写这篇文档时，这些文档还是
比较匮乏的，但是你还是可以从现有的代码中学习的。尤其是在 ``Packages/Default`` 文
件中包含了许多非正式的例子和API调用。
