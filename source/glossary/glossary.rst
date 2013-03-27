.. _glossary:

========
词汇表
========

.. glossary::

    buffer
    缓冲区
        Data of a loaded file and additional metadata. Associated with one or
        more views. The distinction between *buffer* and *view* is technical.
        Most of the time, both terms can be used interchangeably.
        存放已经加载文件的内容以及文件元数据的区域称为缓冲区。缓冲区一般与一个或多个视图相关联。
        *缓冲区* 与 *视图* 只有一些细节上的差别。大多数情况下这两个术语是可以混用的。

    view
    视图
        Graphical display of a buffer. Multiple views can show the same buffer.
        显示缓冲区内容的图形区域。多个不同的视图可以显示同一块缓冲区内容。

    plugin
    插件
    	A feature impemented in Python. It can consist of a single command
    	or multiple commands. It can be contained in one *.py* file or many
    	*.py* files.
        使用Python实现的一个功能称为插件。它可以包含一个或多个命令。它可以由一个或多个 *.py*
        文件组成。

    package
    包
    	This term in ambiguous in the context of Sublime Text, because it can
    	refer to a Python package (unlikely), a directory inside ``Packages``
    	or a *.sublime-package* file. Most of the time, it means a directory
    	inside ``Packages`` containing resources that belong together to build
    	a new feature or provide support for a programming or markup language.
        在Sublime Text中这个术语的意义有点模糊，它可以指一个Python包（这种用法很少），或者
        是 ``包组`` 目录下的一个文件夹，亦或是一个 *.sublime-package* 文件。大多数情况下，
        包指的是 ``包组`` 目录下的一个文件夹，这个文件夹中包含为某个特性或者某种语言服务的各
        种资源。

    panel
    面板
        An input/output widget such as a search panel or the output panel.
        像搜索或者输出这样的，用于进行输入/输出的窗体控件称为面板。

    overlay
    覆盖层控件
        An input widget of a special kind. Goto Anything is an overlay.
        一种特殊的输入控件。快速跳转就是一种覆盖层控件。
