Commands
========

Commands are ubiquitous in Sublime Text: key bindings, menu items and macros
all work through the command system. They are found in other places too.

命令在Sublime Text中无处不在：按键绑定，菜单项包括宏等它们都是工作在命令系统里的。因此，命令随处可见。

Some commands are implemented in the editor's core, but many of them are
provided as python plugins. Every command can be called from a python plugin.

一些命令可以通过编辑器内核接口来实现，但是更多的是作为python的插件来提供。任何命令都可以通过python插件来调用。

Command Dispatching
*******************

Normally, commands are bound to the application object, a window object or a
view object. Window objects, however, will dispatch commands based on input
focus, so you can issue a view command from a window object and the correct
view instance will be found for you.

通常，命令都绑定在应用对象，窗口对象或者视图对象里。不过，窗口对象根据输入焦点来分发命令，因此你可以通过窗口对象发起一个
命令并且会为你返回一个正确的视图实例。

Anatomy of a Command
********************

Commands have a name separated by underscores, like ``hot_exit`` and can take
a dictionary of arguments whose keys must be strings and whose values must
be JSON types. Here's a few examples of commands run from the Python console:

命令名通常被下划线所分割，就像``hot_exit``,而且是一个以字符串为关键字JSON类型为值的字典。下面是一些运行在python控制台下
的命令例子:

::


   view.run_command("goto_line", {"line": 10})
   view.run_command('insert_snippet', {"contents": "<$SELECTION>"})
   view.window().run_command("prompt_select_project")


.. seealso::

   :doc:`Reference for commands <../reference/commands>`
        Command reference.
