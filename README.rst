Autotype.vim
============

:version: 0.10.0

..

    Yes, Vim will work for you.

    -- autotype.vim


Auto typing in vim.

.. figure:: https://github.com/Rykka/github_things/raw/master/image/autotype.gif
       :align: center


Install
=======

Using Vundle or NeoBundle.

``Bundle Rykka/autotype.vim``


Useage
======


AutoType [filename]
   Start auto typing filename into current buffer with filename.

   All contents of that file will be typed into current buffer.

   You can use ``Ctrl-C`` to stop.



Commands and variables
----------------------

You can define commands and variables with specific tags.
default is jinja like syntax, 
and files with '.autotype' extensions will be recongized as 
autotype filetype and highlighted.

vim commands can be used directly in these tags.

You can have a try with ``:AutoType syntax.autotype``

Syntax overview::

    This is a variable: {{ g:autotype_speed }}

    Insert a list: {{ range(10) }}
    
    You can do more things with command blocks.
    {@
    for i in range(10)
        TYPE 'LINE '.i.'\r'
    endfor
    @}

    ECHO AND HOTKEY {% ECHO 'Go to Start and type' | NORM! 0  | TYPE SOMETHING | NORM! $ %}


    Yank 
    Something ^_yy

    Then Paste 
    ^_P
    

.. NOTE:: local variables can not be used.

   You must use 'b:var' or 'g:var' instead.


Help Commands
    TYPE
        TYPE things with current cursor position.
    ECHO
        Just like ':echo', And will show a longer time.

        Strings must using single quote ``'``.

    BLINK
        A blinking 'echo'
    NORMAL
        Like ':normal', And words like \<C-W> will be convert to that
        special character

:Note: To use a special char for a command line input
       like in 'i_CTRL-R_='. 

       You must put the special char directly.
       Use ``i_Ctrl-V`` to input them, see vim help for details.

:WARNING: Behavior of using window/cmdline commands and mappings are not predictable.
             
          Use it with caution,

          And don't **EVER** run other's autotype file without checking.

Options
=======

g:autotype_speed

    Auto typing speed (char per second), default is ``30``

    A turtle? use '10'.

    A swallow? use '400' or more.

    Lighting? use '10000' or more.

g:autotype_syntax_type

    Default is 'jinja'.
        1. Command tag is '{% cmds %}'
        2. Variable tag is '{{ var }}'
        3. Command block is '{@' and '@}',
           both in single line
        4. Inline Command is ``^_cmds``
        5. To prevent exec of tags, add a '!' before the tag.

    Then the 'autotype'
        1. Command tag is '^[ cmds ^]'
        2. Variable tag is '^{ var ^}'
        3. Command block is '^[^[' and '^]^]',
           both in single line
        4. Inline Command is ``^_cmds``

    You can define your tags
    with following list of options::
        
            ["g:autotype_syn_cmd_bgn",  '{%'],
            ["g:autotype_syn_cmd_end",  '%}'],
            ["g:autotype_syn_cmds_bgn", '{@'],
            ["g:autotype_syn_cmds_end", '@}'],
            ["g:autotype_syn_var_bgn",  '{{'],
            ["g:autotype_syn_var_end",  '}}'],
            ["g:autotype_syn_cmd_once", '^_'],

    .. NOTE:: You should set g:autotype_syntax_type with your name

        And the value should be a pattern for matching.

        for example: '^' should be escaped as '\^'

g:autotype_file_directory
    The user directory for your autotype files.

    Default is ''.

    Then ``:AutoType`` will search in local path
    and the ``<autotype.vim>/autotype/`` directory.

    You can add multiple paths seperated with comma ','.

g:autotype_cursor_aug
    Used for running autocommands with ``CursorMoved,CursorMovedI``

    set ``aug_ptn`` seperate with ``,``

    default is ``'*.rst,<buffer>'``

TODO
====

1. Make autotype auto write articles.
2. Make autotype auto write programs.
