Plugins
插件
=======

.. seealso::

   :doc:`API Reference <../reference/api>`
        More information on the Python API.

更多信息请参考：

   :doc:`API参考文档 <../reference/api>`
        有关Python API的更详细的信息。



Plugins are Python scripts implementing ``*Command`` classes from
``sublime_plugin``.
插件是实现了 ``sublime_plugin`` 模块中 ``*Command`` 类的Python脚本。

Where to Store Plugins
插件放到哪里
**********************

Sublime Text 2 will look for plugins in these places:
Sublime Text 2在以下这些目录中寻找可用插件：

* ``Packages``
* ``Packages/<pkg_name>``
* ``Packages/<包名称>``

Any plugin nested deeper in ``Packages`` won't be loaded.
存放在 ``Packages`` 更深层次的目录结构中的插件不会被加载。


All plugins should live inside a directory of their own and not directly
under ``Packages``.
任何插件都应该又自己单独的目录，而不应该直接放在 ``Packages`` 目录下。


Conventions for Command Names
命令名称的命名规则
*****************************

Sublime Text 2 command class names are suffixed by convention with ``Command``
and written as ``CamelCasedPhrases``.
Sublime Text 2遵循 ``CamelCasedPhrases`` 命名规则来定义命令类，同时用 ``Command`` 作为后缀。

However, Sublime Text 2 transforms the class name from ``CamelCasedPhrases``
to ``camel_cased_phrases``. So ``ExampleCommand`` would turn into ``example``
and ``AnotherExampleCommand`` would turn into ``another_example``.
然而，Sublime Text 2将类名从 ``CamelCasedPhrases`` 形式自动转换成 ``camel_cased_phrases`` 。
举例来说， ``ExampleCommand`` 将被转换为 ``example`` ，而 ``AnotherExampleCommand`` 将
转换为 ``another_example`` 。

For class definition names, use ``CamelCasedPhrasesCommand``; to call a
command from the API, use the normalized name (``camel_cased_phrases``).
对于类定义名称，可以使用 ``CamelCasedPhrasesCommand`` 命名方式；要从API中调用一个命令，请使用
标准化后的名称（ ``camel_cased_phrases`` ）。


Types of Commands
命令类型
*****************

* ``sublime_plugin.ApplicationCommand``
* ``sublime_plugin.WindowCommand``
* ``sublime_plugin.TextCommand``
* ``sublime_plugin.EventListener``

Instances of ``WindowCommand`` have a ``.window`` attribute pointing to the
window instance that created them. Similarly, instances of ``TextCommand``
have a ``.view`` attribute.
``WindowCommand`` 类的实例都有一个 ``.window`` 属性，指向创建他们的那个窗口实例。于此类似，
``TextCommand`` 类的实例拥有 ``.view`` 属性。

Shared Traits for Commands
命令之间的共享特性
--------------------------

All commands must implement a ``.run()`` method.
所有命令都必须实现一个 ``.run()`` 方法。
All commands can receive and arbitrarily long number of keyword arguments,
but they must be valid JSON types.
所有命令都可以接受任意长度的关键字参数，但是这些参数一定要是有效的JSON类型。


How to Call Commands from the API
如何利用API调用命令
*********************************

Use a reference to a ``View`` or a ``Window``, or ``sublime`` depending on
the type of command, and call ``object.run_command('command_name')``.
In addition, you can pass a dictionary where keys are names of parameters
to ``command_name``. ::

   window.run_command("echo", {"Tempus": "Irreparabile", "Fugit": "."})


 Command Arguments
 *****************

 All user-provided arguments to commands must be valid JSON types. Only
 Sublime Text can pass other types of arguments to commands (such as edit
 objects, view instances, etc.).

Use a reference to a ``View`` or a ``Window``, or ``sublime`` depending on
the type of command, and call ``object.run_command('command_name')``.
根据命令的类型来选择对 ``View`` 、 ``Window`` 或者 ``sublime`` 的引用，然后通过
``object.run_command('command_name')`` 来调用。
In addition, you can pass a dictionary where keys are names of parameters
to ``command_name``. ::
除此之外, 你可以用字典作为参数，字典中的键就是要传给 ``command_name`` 的参数名称::

   window.run_command("echo", {"Tempus": "Irreparabile", "Fugit": "."})


 Command Arguments
 命令参数
 *****************

 All user-provided arguments to commands must be valid JSON types. Only
 Sublime Text can pass other types of arguments to commands (such as edit
 objects, view instances, etc.).
 用户提供给命令的所有参数都必须是有效的JSON类型。只有Sublime Text可以给命令传递其他类型的参数
 （例如修改对象，视图实例等等）。



Text Commands and the ``edit`` Object
文本命令以及 ``修改`` 对象
*************************************

The two API functions of interest are ``view.begin_edit()``, which takes an
optional command name and an optional dictionary of arguments, and
``view.end_edit()``, which finishes the edit.
关于两个文本命令的两个较为重要的API是 ``view.begin_edit()`` 和 ``view.end_edit()`` 。
其中 ``view.begin_edit()`` 可以接受一个可选的命令名称和可选的参数字典；而 ``view.end_edit()``
用来结束编辑过程。

All actions done within an edit are grouped as a single undo action. Callbacks
such as ``on_modified()`` and ``on_selection_modified()`` are called when the
edit is finished.
在修改过程中发生的所有动作都被整合成一个单一的撤销动作。当编辑过程结束的时候，类似与
``on_modified`` 和 ``on_selection_modified()`` 的回调函数会被触发。

It's important to call ``view.end_edit()`` after each ``view.begin_edit()``,
otherwise the buffer will be in an inconsistent state. An attempt will be made
to fix it automatically if the edit object gets collected, but that often
doesn't happen when you expect, and will result in a warning printed to the
console. In other words, you should always bracket an edit in a
``try..finally`` block.
有一点非常重要，每次调用 ``view.begin_edit()`` 之后必须调用 ``view.end_edit()`` 方法，否则
缓冲将处于一种不一致状态。在不匹配发生时，系统将尝试自动进行修正，但是这种自动修正的发生频率并
没有你想象的那么多，同时会在控制台输出一条警告信息。换句话说，你应该始终使用 ``try..finally``
来包裹代码快。

The command name passed to ``begin_edit()`` is used for repeat, macro
recording, and for describing the action when undoing/redoing it. If you're
making an edit outside of a ``TextCommand``, you should almost never supply a
command name.
传递给 ``begin_edit()`` 的命令名称用于重复、宏录制以及撤销/重复过程中的动作描述。如果你在
``TextCommand`` 外面做修改，你就不该指定命令名称。

If you have created an edit object, and call a function that creates another
one, that's fine: the edit is only considered finished when the outermost call
to ``end_edit()`` runs.
你可以在开始的时候创建一个修改对象，然后调用了一个方法又创建了另外的一个修改对象：只有当最外层
的修改对象执行了 ``end_edit()`` 方法之后，系统才认为整个修改都完成了。

As well as grouping modifications, you can use edit objects for grouping
changes to the selection, so they're undone in a single step.
与群组修改类似，你也可以使用修改对象把对选中文本做的修改组合成一个群组，对它们的修改只要一步就
能撤销。


Responding to Events
对事件的响应
********************

Any subclass of ``EventListener`` will be able to respond to events. You
cannot make a class derive from both ``EventListener`` and any other type of
command.
任何 ``EventListener`` 的子类都能够响应事件。对于任何一个类，不能同时继承 ``EventListener``
和其他任何的命令类。

.. sidebar:: A Word of Warning about ``EventListener``

	Expensive operations in event listeners can cause Sublime Text 2 to become
	unresponsive, especially in events triggered frequently, like
	``on_modified`` and ``on_selection_modified``. Be careful of how much work
	is done in those and do not implement events you don't need, even if they
	just ``pass``.

.. sidebar:: 关于 ``EventListener`` 的注意事项
  在事件监听器中，尤其是处理 ``on_modified`` 和 ``on_selection_modified`` 这样的经常被
  触发的事件的监听器中，执行开销很大的操作可能会导致Sublime Text 2没有响应。所以请注意监听器
  中所编写的代码，另外，不要实现你不需要的方法，即使这个方法只有一个 ``pass``语句。

Python and the Standard Library
Python与标准库
*******************************

Sublime Text ships with a trimmed down standard library. Notable missing
modules are the *Tkinter*, *multiprocessing* and *sqlite3* modules.
Sublime Text集成了一个精简版的标准库。被裁剪掉的模块包括 *Tkinter* ， *multiprocessing*
以及 *sqlite3* 。


Automatic Plugin Reload
自动插件重载
***********************

Sublime Text will automatically reload top-level Python modules from packages
as they change (perhaps because you are editing a *.py* file). Note that
Python subpackages won't be reloaded; this can lead to confusion while
developing plugins. Generally, it's best to restart Sublime Text after you've
made changes to plugin files so all changes take effect.
当你对插件做修改的时候（比如你正在修改一个 *.py* 文件），Sublime Text会自动加载包中的顶级
Python模块。值得注意的是Python的子模块不会被自动重新加载；这一点在插件开发中可能会产生一些挺
奇葩的问题。一般来说，当你对插件文件做修改之后，最好重启以下Sublime Text，这样能保证你做的修
改能发挥作用。


Multithreading
多线程
**************

Only the ``.set_timeout()`` function is safe to call from different threads.
只有 ``.set_timeout()`` 方法可以安全的从其他线程调用。
