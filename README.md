git-difftool
============

Python wrapper around 'git diff' for convinient viewing of changes

License
=======

Distributed under the Boost Software License, Version 1.0.
(See accompanying file LICENSE_1_0.txt or copy at
http://www.boost.org/LICENSE_1_0.txt)

Compatibility
=============

Git 1.7.2 or greater is required.

I have this working on cygwin and Ubunto 10 with git updated to 1.8.0 and python 2.6. 

You may need to do some tweaking in order to adopt it for other systems.

What it does
============

For some reason 'git diff/difftool' is only capable to run multiple
visual diffs - one per each changed file. This is kinda not convenient. 
This script is a yet another attempt to solve this problem. 
Once invoked, it will create copies of local and remote files in two separate
directories. It is also may run a visual diff tool of your choice 
(mine is WinMerge). 

How it works
============

Here is the approximate algorithm: 

1. Create a temporary directory (hereafter TMP)
2. Configure a new difftool in the local repository. The new tool is
   git-difftool itself with the option --diffmode and the temporary
   directory as a parameter
3. Run 'git diff' with a command line arguments propagated from 
   the git-difftool's command line.
4. The git-difftool running in 'diffmode' by git will collect diffs in
   TMP/local and TMP/remote sub-directories.
5. Once 'git diff' is terminated - launch the visual diff tool with 
   TMP/local and TMP/remote as arguments

Limitations
===========

1. Since os.link() does not exist on windows versions of python (din't check
   python 3 yet) git-difftool copies files. This is costly operation, it may 
   take much time and space for big diffs.
2. In-place editing will change files in the temporary directory and not in 
   the repository.
3. The temporary directory is not cleaned up after the script ends.

Author
======

Dimitry Kloper <kloper@users.sf.net>


