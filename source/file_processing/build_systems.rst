================================
构建系统（批处理）
================================

Build systems let you run your files through external programs like
:program:`make`, :program:`tidy`, interpreters, etc.
通过构建系统，你能够使用像 :program:`make`， :program:`tidy` 这样的外部程序以及各种解释器
来运行你的文件。

Executables called from build systems must be in your :const:`PATH`. For more
information about making sure the :const:`PATH` seen by Sublime Text is set
correctly, see :ref:`troubleshooting-build-systems`.
在构建系统中调用的外部可执行程序一定要能够通过 :const:`PATH` 环境变量找到。请参考 :ref:`构建系统常见问题`
章节来了解有关如何正确设置 :const:`PATH` 环境变量的更多信息。


File Format
文件格式
===========

Build systems are JSON files and have the extension *.sublime-build*.
构建系统是以 *.sublime-build* 作为文件扩展名的JSON文件。

Example
示例
-------

Here's an example of a build system:
下面是构建系统的一个小例子：

.. code-block:: js

    {
        "cmd": ["python", "-u", "$file"],
        "file_regex": "^[ ]*File \"(...*?)\", line ([0-9]*)",
        "selector": "source.python"
    }

``cmd``
    Required. This option contains the actual command line to be executed::
    必填内容。这个选项的内容是实际执行的命令行语句::

        python -u /path/to/current/file.ext

``file_regex``
    A Perl-style regular expression to capture error information out of the
    external program's output. This information is then used to help you
    navigate through error instances with :kbd:`F4`.
    存放一段用于捕获外部程序输出的错误信息的Perl风格的正则表达式。这部分信息用于帮助你在不同
    的错误实例之间使用 :kbd:`F4` 快捷键进行跳转。


``selector``
    If the **Tools | Build System | Automatic** option is set, Sublime Text
    will automatically find the corresponding build system for the active file
    by matching ``selector`` to the file's scope.
    如果你勾选了 **Tools | Build System | Automatic** 选项，Sublime Text会自动从构建
    系统中通过 ``selector`` 选项找到适合当前文件的构建方式。

In addition to options, you can also use some variables in build systems, like
we have done above with ``$file``, which expands to the the active buffer's
file name.
除了这些选项，在构建系统中还可以使用一些变量，例如在前面使用的 ``$file`` 变量，就能自动扩充为
当前缓冲区对应的文件名。


Where to Store Build Systems
构建系统存储在哪里
============================

Build systems must be located somewhere under the *Packages* folder
(e. g. *Packages/User*). Many packages include their own build systems.
构建系统必须被放在 *包组* 文件夹下面的某个位置（例如 *Packages/User*）。许多包都含有它们自己
的构建系统。


Running Build Systems
运行构建系统
=====================

Build systems can be run by pressing :kbd:`F7` or from **Tools | Build**.
可以使用 :kbd:`F7` 快捷键来运行构建系统，也可以从 **Tools | Build** 菜单中运行。


.. seealso::

   :doc:`Reference for build systems <../reference/build_systems>`
        Complete documentation on all available options, variables, etc.

更多信息请参考

   :doc:`构建系统参考文档 <../reference/build_systems>`
        记录所有可用选项、变量的完整文档。
