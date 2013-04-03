===============
命令面板
===============

命令面板由 ``.sublime-commands`` 文件中的各项组成.



文件格式 (``.sublime-commands`` 文件)
=========================================

如下是来自 ``Packages/Default/Default.sublime-commands`` 的实例::

   [
       { "caption": "Project: Save As", "command": "save_project_as" },
       { "caption": "Project: Close", "command": "close_project" },
       { "caption": "Project: Add Folder", "command": "prompt_add_folder" },
   
       { "caption": "Preferences: Default File Settings", "command": "open_file", "args": {"file": "${packages}/Default/Base File.sublime-settings"} },
       { "caption": "Preferences: User File Settings", "command": "open_file", "args": {"file": "${packages}/User/Base File.sublime-settings"} },
       { "caption": "Preferences: Default Global Settings", "command": "open_file", "args": {"file": "${packages}/Default/Global.sublime-settings"} },
       { "caption": "Preferences: User Global Settings", "command": "open_file", "args": {"file": "${packages}/User/Global.sublime-settings"} },
       { "caption": "Preferences: Browse Packages", "command": "open_dir", "args": {"dir": "$packages"} }
   ]

``caption``
   显示在命令面板中的标题.
``command``
   代执行的命令.
``args``
   Arguments to pass to ``command``. Note that to locate the packages folder
   you need to use a snippet-like variable: ``${packages}`` or $packages. This
   different to other areas of the editor due to different implementations of
   the lower level layers.

传给 ``command`` 的参数。 需要注意的是，要定位包所在目录，需要使用 ``${packages}`` 或 $packages。由于底层的实现不同，这与在编辑器的其他区域的用法略有不同。


如何使用命令面板
==============================

#. 按 :kbd:`Ctrl+Shift+P`
#. 选择命令

Entries are filtered by current context. Not all entries will be visible at all
times.

显示的选项会根据上下文不同有所区别，并不是在任何时候都会显示所有选项。
