===================================
搜索与替换 - 多文件
===================================

.. _snr-search-files:

Searching
搜索
=========

To open the search panel for files, press ``Ctrl + Shift + F``. You can use the
keyboard to control the search panel and some search actions:
使用 ``Ctrl + Shift + F`` 键可以打开多文件搜索面板。搜索面板与搜索动作可以使用快捷键进行操作：

==========================	===========
Toggle Regular Expressions	``Alt + R``
开/关正则表达式选项  ``Alt + R``
Toggle Case Sensitivity		``Alt + C``
开/关大小写敏感选项   ``Alt + C``
Toggle Exact matches		``Alt + W``
开/关精确匹配选项    ``Alt + W``
Find Next					``Enter``
查找下一个         ``Enter``
==========================	===========

.. _snr-search-scope-files:

Search Scope
搜索作用域
============

The **Where** field in the search panel determines where to search. You can
define the scope of the search in several ways:
搜索面板中的 **Where** 字段决定搜索文件的范围。你可以通过以下几种方式来确定文件的搜索作用域：

* Adding individual directories (Unix-style paths, even on Windows)
* 添加一个独立的目录 （需要使用 Unix风格的文件路径，在Windows平台也是如此）
* Adding/excluding files based on a pattern
* 使用某种模式来添加/删除某些文件
* Adding  symbolic locations (``<open folders>``, ``<open files>``)
* 添加链接位置(``<open folders>``, ``<open files>``)

You can combine these filters separing them with commas, for example:
你可以在一次搜索中组合使用以上确定作用域的方式，并且在不同方式之间用逗号分隔，例如：

	/C/Users/Joe/Top Secret,-*.html,<open files>

Press the **...** button in the search panel to display a menu containing
these options.
通过在搜索面板中按 **...** 按钮来显示包含这些选项的菜单。

（译者注：Unix风格的文件路径指的是使用 */* 来区分目录结构，例如 */Users/voidmain/* ，在
Windows平台上，可以使用 */C/Users/* 来指定盘符）

.. xxx what kind of patterns are those?
.. xxx special locations?
.. xxx unix on windows too?
.. xxx link to reference to fulloptions

.. _snr-results-format-files:

Results Format
搜索结果显示方式
==================

In the search panel, you can find the following options to customize the
results format:
在搜索面板中，可以使用下面的选项来自定义搜索结果的显示方式：


* Show in Separate Buffer/Output Panel
* 在单独的缓冲区/输出面板中显示
* Show Context
* 显示上下文


.. _snr-results-navigation-files:

Navigating Results
搜索结果跳转
==================

If the search yields matches, you can move through the sequence using the
following key bindings:
一旦找到了符合要求的内容，你就可以使用以下的快捷键进行结果之间的跳转：

================	==============
Next match			``F4``
转到下一个匹配项      ``F4``
Previous match		``Shift + F4``
转到前一个匹配相    ``Shift + F4``
================	==============
