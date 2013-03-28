Build Systems
=============

Build systems let you run your files through external programs and see the
output they generate within Sublime Text.

构建系统可以让您通过外部程序来运行文件，并可以在Sublime Text查看输出。

Build systems consist of two --or optionally three-- parts:

* configuration data in JSON format (the *.sublime-build* file contents)
* a Sublime Text command driving the build process
* optionally, an external executable file (script, binary file)

构建系统包括两 -- 或者说三个 --  部分

* 使用JSON格式保存配置文件 (*.sublime-build* 内容)
* 使用Sublime Text命令来驱动构建过程
* 还包括一个外部的可执行程序(脚本或者二进制)

Essentially, *.sublime-build* files are configuration data for an external
program as well as for the Sublime Text command just mentioned. In them, you
specify the switches, options and environment information you want forwarded.

从根本上来讲，*.sublime-build* 配置文件对于外部可执行程序与前面提到的Sublime Text命令是一样的。在配置文件中可以指定开关、配置以及环境变量。


The Sublime Text command then receives the data stored in the *.sublime-build*
file. At this point, it can do whatever it needs to *build* the files. By
default, build systems will use the ``exec`` command, implemented in
*Packages/Default/exec.py*. As we'll explain below, you can override this
command.

Sublime Text命令从 *.sublime-build* 中读取配置数据，然后根据需要*构建*这些文件。
构建系统缺省会使用``exec`` 命令，该命令在 *Packages/Default/exec.py* 中实现。
在后续的讲解中，我们会重写这个命令。

Lastly, the external program may be a shell script you've created to process
your files, or a well-known utility like ``make`` or ``tidy``. Usually, these
executable files will receive paths to files or directories, along with
switches and options to be run with.

外部程序可能是你用来处理文件的脚本，也可以能是类似 ``make`` 或 ``tidy`` 这类的命令。通常，这些可执行文件从配置中获取文件路径或者目录以及运行是需要的开关及选项。

Note that build systems need not call any external program at all if there
isn't any reason to; you could implement a build system entirely in a
Sublime Text command.

注意，构建系统可以完全不依赖调用外部程序，完全可以通过Sublime Text

文件格式
***********

*.构建系统* 文件使用JSON. 以下是一个例子:

.. sourcecode:: python

    {
        "cmd": ["python", "-u", "$file"],
        "file_regex": "^[ ]*File \"(...*?)\", line ([0-9]*)",
        "selector": "source.python"
    }


选项
*******

``cmd``
    Array containing the command to run and its desired arguments. If you don't
    specify an absolute path, the external program will be searched in your
    :const:`PATH`, one of your system's environmental variables.

``cmd``

    包括命令及其参数数组。如果不指定绝对路径，外部程序会在你系统的:const:`PATH` 环境变量中搜索。

    On Windows, GUIs are supressed.

    在Windows 系统中，***TBT***



``file_regex``
    Optional. Regular expression (Perl-style) to capture error output of
    ``cmd``. See the next section for details.

    
``file_regex``
    可选。 Perl格式的正则表达式可以获取``cmd``的错误输出，详情参考下一节

``line_regex``
    Optional. If ``file_regex`` doesn't match on the current line, but
    ``line_regex`` exists, and it does match on the current line, then
    walk backwards through the buffer until a line matching ``file regex`` is
    found, and use these two matches to determine the file and line to go to.

``line_regex``

    可选。当``file_regex``与该行不匹配，如果``line_regex``存在，并且确实与当前行匹配，
    则遍历整个缓冲区，直到与``file regex``匹配的行出现，并用这两个匹配决定最终要跳转的文件
    或行。


``selector``
    Optional. Used when **Tools | Build System | Automatic** is set to ``true``.
    Sublime Text uses this scope selector to find the appropriate build system
    for the active view.

``selector``    
    可选。在选定 **Tools | Build System | Automatic** 时使用。Sublime Text使用这个
    选择器自动为活动试图选择构建系统。

``working_dir``
    Optional. Directory to change the current directory to before running ``cmd``.
    The original current directory is restored afterwards.

``working_dir``
    可选。在运行``cmd``前会切换到该目录。运行结束后会切换到原来的目录。

``encoding``
    Optional. Output encoding of ``cmd``. Must be a valid python encoding.
    Defaults to ``UTF-8``.

``encoding``
    可选。输出``cmd``的编码。必须是合法的Python编码，缺省为``UTF-8``。


``target``
    Optional. Sublime Text command to run. Defaults to ``exec`` (*Packages/Default/exec.py*).
    This command receives the configuration data specified in the *.build-system* file.

    Used to override the default build system command. Note that if you choose
    to override the default command for build systems, you can add arbitrary
    variables in the *.sublime-build* file.

``target``
    可选。运行的Sublime Text命令，缺省为``exec`` (*Packages/Default/exec.py*)。该命令从
    *.build-system*中获取配置数据。

    用来替代缺省的构建系统命令。注意，如果你希望替代构建系统的缺省命令，请在*.sublime-build* 
    文件中专门设置。


``env``
    Optional. Dictionary of environment variables to be merged with the current
    process' before passing them to ``cmd``.

    Use this element, for example, to add or modify environment variables
    without modifying your system's settings.

``env``
    可选。在环境变量被传递给``cmd``前，将他们封装成词典。


``shell``
    Optional. If ``true``, ``cmd`` will be run through the shell (``cmd.exe``, ``bash``\ …).

 ``shell``
    可选。如果该选项为``true`` ，``cmd``则可以通过shell运行。    

``path``
    Optional. This string will replace the current process' :const:`PATH` before
    calling ``cmd``. The old :const:`PATH` value will be restored after that.

    Use this option to add directories to :const:`PATH` without having to modify
    your system's settings.

``path``
    可选。该选项可以在调用``cmd``前替换当前进程的' :const:`PATH` 。原来的' :const:`PATH`
    将在运行后恢复。

    使用这个选项可以在不修改系统设置的前提下将目录添加到' :const:`PATH` 中。


``variants``
    Optional. A list of dictionaries of options to override the main build
    system's options. Variant ``name``s will appear in the Command Palette for
    easy access if the build system's selector matches for the active file.

``variants``
    可选。用来替代主构建系统的备选。如果构建系统的选择器与激活的文件匹配，变量的``名称``则
    会出现在 Command Palette 中。


``name``
    **Only valid inside a variant** (see ``variants``). Identifies variant
    build systems. If ``name`` is *Run*, the variant will show up under the
    **Tools | Build System** menu and be bound to *Ctrl + Shift + B*.

``name``
    **仅在variant中是合法的** (详见 ``variants``)。用来标识系统中不同的构建系统。如果
    ``name``是*Run* ,则会显示在**Tools | Build System** 下，并且可以使用
    *Ctrl + Shift + B*调用。

使用 ``file_regex``获取错误输出
------------------------------------------

The ``file_regex`` option uses a Perl-style regular expression to capture up
to four fields of error information from the build program's output, namely:
*file name*, *line number*, *column number* and *error message*. Use
groups in the pattern to capture this information. The *file name* field and
the *line number* field are required.

``file_regex``选项用Perl的正则表达式来捕获构建系统的错误输出，主要包括四部分内容，分别是
file name*, *line number*, *column number* and *error message*. Sublime Text
在匹配模式中使用分组的方式捕获信息。*file name* 和 *line number*域是必须的。


When error information is captured, you can navigate to error instances in
your project's files with ``F4`` and ``Shift+F4``. If available, the captured
*error message* will be displayed in the status bar.

当错误信息被捕获时，你可以使用``F4`` 和 ``Shift+F4``在你的项目文件中跳转。被捕获的*错误
信息*会显示在状态栏。

平台相关选项
-------------------------

The ``windows``, ``osx`` and ``linux`` elements let you provide
platform-specific data in the build system. Here's an example::

``windows``, ``osx`` 以及 ``linux``元素可以帮助你在构建系统中设定平台相关
的选项，举例如下：


    {
        "cmd": ["ant"],
        "file_regex": "^ *\\[javac\\] (.+):([0-9]+):() (.*)$",
        "working_dir": "${project_path:${folder}}",
        "selector": "source.java",

        "windows":
        {
            "cmd": ["ant.bat"]
        }
    }

In this case, ``ant`` will be executed for every platform except Windows,
where ``ant.bat`` will be used instead.

在这个例子中，``ant``在除了Windows之外的平台中都是执行 ant ，而在Windows中则执行 
``ant.bat``

构建系统备选项
--------

如下是一个带有备选项的构建系统实例::

    {
        "selector": "source.python",
        "cmd": ["date"],

        "variants": [

            { "cmd": ["ls -l *.py"],
              "name": "List Python Files",
              "shell": true
            },

            { "cmd": ["wc", "$file"],
              "name": "Word Count (current file)"
            },

            { "cmd": ["python", "-u", "$file"],
              "name": "Run"
            }
        ]
    }


Given these settings, *Ctrl + B* would run the *date* command, *Crtl + Shift +
B* would run the Python interpreter and the remaining variants would appear
in the Command Palette whenever the build system was active.

根据以上的设定，按 *Ctrl + B* 会运行*date*命令, 按 *Crtl + Shift + B* 会运行Python
解释器，并且在构建系统激活时将剩余的备选项显示在Command Palette中。

.. _build-system-variables:

构建系统变量
**********************

Build systems expand the following variables in *.sublime-build* files:

在*.sublime-build* 中包括如下构建系统变量。

====================== =====================================================================================
``$file_path``         当前文件所在路径, 比如 *C:\\Files*.
``$file``              当前文件的完整路径, 比如  *C:\\Files\\Chapter1.txt*.
``$file_name``         当前文件的文件名, 比如  *Chapter1.txt*.
``$file_extension``    当前文件的扩展名, 比如  *txt*.
``$file_base_name``    当前文件仅包含文件名的部分, 比如  *Document*.
``$packages``          *Packages* 文件夹的完整路径.
``$project``           当前项目文件的完整路径.
``$project_path``      当前项目文件的路径.
``$project_name``      当前项目文件的名称.
``$project_extension`` 当前项目文件的扩展部分.
``$project_base_name`` 当前项目仅包括名的部分.
====================== =====================================================================================

变量用法
---------------------------

Features found in snippets can be used with these variables. For example::

可以在代码片段上中使用以上变量。例如::

    ${project_name:Default}

This will emit the name of the current project if there is one, otherwise ``Default``.

如果当前项目存在则使用该项目名称，否则则使用``Default``替代
::

    ${file/\.php/\.txt/}

This will emit the full path of the current file, replacing *.php* with *.txt*.

该例会获取当前文件的完整路径，并用*.txt*替换路径中的*.php* 

运行构建系统
*********************

Select the desired build system from **Tools | Build System**, and then select
**Tools | Build** or press ``F7``.

从**Tools | Build System**选择构建系统，然后选择**Tools | Build** ，再按``F7``。

.. _构建系统常见问题:

构建系统常见问题
*****************************

Build systems will look for executables in your :const:`PATH`, unless you specify
an absolute path to the executable. Therefore, your :const:`PATH` variable must be
correctly set.

如果你没有为构建系统指定一个可执行文件的绝对路径，构建系统怎么会在你的 :const:`PATH` 中进行查找。
所以，你需要正确设置  :const:`PATH` 。

On some operating systems, the value for :const:`PATH` will vary from a terminal
window to a graphical application. Thus, even if the command you are using in
your build system works in the command line, it may not work from Sublime Text.
This is due to user profiles in shells.

在某些操作系统中，终端和图形化应用的 :const:`PATH` 值会有所不同。所以即便你的构建系统在命令行下
可以正常工作，在Sublime Text也不见得能够正常。这与Shell中的用户设置有关。

To solve this issue, make sure you set the desired :const:`PATH` so that graphical
applications such as Sublime Text can find it. See the links below for more
information.

为了解决这个问题，请确认你正确设置了 :const:`PATH` ，以便类似Sublime Text一类的图形化应用
可以正确找到。更多内容，请参考一下链接

Alternatively, you can use the ``path`` element in *.sublime-build* files
to override the :const:`PATH` used to locate the executable specified in ``cmd``.
This new value for :const:`PATH` will only be in effect for as long as your
build system is running. After that, the old :const:`PATH` will be restored.

另外，你也可以在 *.sublime-build* 文件中设定 ``path`` 来替代:const:`PATH` ，并在 ``path``
指定的路径中查找 ``cmd`` 可执行文件。新设定的值，仅在构建系统运行期间有效，过后将会恢复为原始的
 :const:`PATH` 

.. seealso::

    `Managing Environment Variables in Windows <http://goo.gl/F77EM>`_
        Search Microsoft knowledge base for this topic.

    `Setting environment variables in OSX <http://stackoverflow.com/q/135688/1670>`_
        StackOverflow topic.
