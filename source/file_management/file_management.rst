===================================
文件导航与文件管理
===================================

随意跳转
=============

Goto Anything lets you **navigate files** swiftly. Open it with :kbd:`Ctrl+P`.
As you type into the input area, names of open files and files in open
directories will be searched, and a preview of the best match will be shown.
This preview is *transient*, that is, it won't become the actual active buffer
until you perform some operation on it. Transient views go away when you press
:kbd:`Esc`. You will find transient views in other situations. They are like
ghosts or something.

“随意跳转” 可以让你方便的在文件之间切换，使用 :kbd:`Ctrl+P` 启动该功能。你在输入栏输入，ST则会
对已经打开的文件或者目录进行搜索，并给出匹配最佳的搜索结果的预览。如果你不进行任何操作，将不会
真正加载这些文件。可以按 :kbd:`Esc` 取消预览界面。快捷预览界面形似鬼魅，你在使用ST的其他功能时也会遇到哦。

Goto Anything lives up to its name --there's more to it than locating files:

“随意跳转”正如其名，其功能不仅限于查找文件：

To perform a **fuzzy search**, append ``#`` and then keep typing, like this:
::

	island#treasure

还可以在输入一些内容后接上 ``#`` 再接着输入来进行 **模糊搜索** ，，比如说:
::

    island#treasure


This instructs Sublime Text to perform a fuzzy search for *treasure* in the
file whose name matches *island*. Pressing :kbd:`Ctrl+;` will open Goto
Anything and type ``#`` for you.

Sublime Text会进行在所有文件名匹配 *island* 的文件中搜索 *treasure* 关键字。使用组合键 :kbd:`Ctrl+;` 可以打开“随意跳转” 功能并输入 ``#`` 

And there's more:

To **search symbols** in the active buffer, press :kbd:`Ctrl+R`. The operator
``@`` can be used as explained above too.

可以通过按下组合键 :kbd:`Ctrl+R` 在活动缓冲区中进行**符号搜索** 。操作符 ``@`` 与之前提到的用法相同。

To **go to a line number**, press :kbd:`Ctrl+G`. The operator ``:`` can be
used as explained above too.

可以通过按下组合键 :kbd:`Ctrl+G` 来跳转到指定的行号。操作符  ``:`` 与之前提到的用法相同。

Searching for symbols will only work for file types that have symbols defined
for them.

符号搜索的功能只能在那些已经定义了符号的文件类型中使用。

侧边栏
=======

The sidebar gives you an overview of your project. Files and folders added to
the sidebar will be available in Goto Anything and project-wide actions.
Projects and the sidebar are closely related. There's always an open project,
whether it's implicit or explicit.

侧边栏可以提供一个项目的概览视图。添加到侧边栏的文件和目录均可以通过“随意跳转”功能访问，并且响应
项目范围内的指令。项目与侧边栏是密切相关的。不管以显式或是隐式的方式，总是有一个项目存在于侧边栏中。

To **open or close** the sidebar, press :kbd:`Ctrl+K, Ctrl+B`.

可以通过组合键:kbd:`Ctrl+K, Ctrl+B`来打开或关闭侧边栏。

The sidebar can be navigated with the arrow keys, but first you need to give
it the **input focus** by pressing :kbd:`Ctrl+0`. To return input focus to the
buffer, press :kbd:`Esc`. Alternatively, you can use the mouse to the same
effect, but why would you?

在侧边栏可以使用方向键来在文件间切换，但是首先需要通过按组合键 :kbd:`Ctrl+0` 使其获得 **输入焦点** 。
如果希望缓冲区重新获得输入焦点，则需要按 :kbd:`Esc` 键。同样，你也可以使用鼠标达到同样的效果，但是
你有必要这么做吗？

The sidebar also provides basic file management operations through the context
menu.

侧边栏可以通过菜单的方式提供基本的文件管理操作。

项目
========

Projects group sets of files and directories you need to work on as a unit.
Once you've set up your project the way that suits you by adding folders, save
it and give it a name.

项目可以将你需要的文件和目录组织成一个单元。当你将项目需要的目录均添加进来以后，你可以这些保存
成一个项目并命名该项目。

To save a project, go to **Project | Save Project As...**.

保存项目可以使用菜单中的  **项目 | 项目另存为...**.

To quickly switch between projects, press :kbd:`Ctrl+Alt+P`.

可以使用组合键 :kbd:`Ctrl+Alt+P` 在项目间快速的切换。

Project data are stored in JSON files with a `.sublime-project` extension.
Wherever there's a `.sublime-project` file, you will find an ancillary
`.sublime-workspace` file too. The second one is used by Sublime Text and you
shouldn't edit it yourself.

项目数据保存在一些以 `.sublime-project` 为扩展名的JSON文件中。只要有 `.sublime-project` 
文件，相应的都会有一个 `.sublime-workspace` 文件。后者是Sublime Text使用，用户请不要进行修改。

Project files can define settings specific to that project only. More on that
in the `official documentation`_.

项目文件可以根据项目进行特殊的设定。更多细节可以参考 `官方文档`_。

.. _官方文档: http://www.sublimetext.com/docs/2/projects.html

You can open a project from the **command line** by passing the *.sublime-
project* file as an argument.

在命令行模式下，可以通过将 *.sublime-project* 文件做为参数来打开整个项目。

.. TODO: talk about settings related to projects
