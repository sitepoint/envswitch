====================
Environment Switcher
====================

* Author: `Adam Bolte`_
* Contact: adam.bolte@sitepoint.com
* Copyright: `GPL3+`_

.. _`Adam Bolte`: https://www.sitepoint.com/author/adam-bolte/
.. _`GPL3+`:  ./COPYING

This is a small Bash script that gives the user the ability to quickly
source profiles of environment variables. This is particularly useful
for OpenStack, AWS and other IaaS providers which require various
environment variables in order to function with different accounts.


Project page
------------

https://github.com/sitepoint/envswitch


Requirements
============

* `GNU Bash`_
* `GNU core utilities`_
* `GNU sed`_

.. _GNU Bash: http://www.gnu.org/software/bash/
.. _GNU Core utilities: http://gnu.org/software/coreutils
.. _GNU Sed: https://www.gnu.org/software/sed/

These are the dependencies that were tested, and should be available
on almost any desktop or server GNU/Linux distribution.

Environment Switcher has also been reported to work with Zsh on MacOS.


Setup
=====

Place the envswitch script somewhere in your path and ensure it has
executable permissions configured. Next, in your login shell
(eg. ``~/.bashrc`` for GNU Bash, ``~/.zshrc`` for Z shell) file add
the following line:

.. code-block:: console

  eval "$(envswitch -i)"


Profile configuration
---------------------

Upon first execution of envswitch, the directory
``${HOME}/.config/envswitch`` will be created. Install environment
variables into a file under this directory with a ``.conf``
extension. eg.

.. code-block:: console

  somevar="test1"
  # This is a comment.
  anothervar="${somevar}"
  numbervar=123

Note the name of the configuration file (minus the .conf extension)
should not match the name of an existing shell function. If in doubt,
check the output of ``declare -F``.


Usage
=====

Listing and loading profiles
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Profiles exist as local shell functions, which can be called any time
just by typing the name.

A list of available profiles can be viewed like so:

``envswitch -l``

Note that the shell functions will source the associated profile file
when called, as profile contents are not automatically imported. This
is done to prevent ``declare -f`` from also exposing environment
variables.

Once a profile has been loaded, the shell prompt (``$PS1``) should be
updated to include the profile name. If this is undesirable, replace
``-i`` with ``-I`` in the login shell file to prevent it from
happening.


Show loaded environment variables
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The loaded profile can be printed to standard output with the
following command:

``envswitch -s``

This will effectively just print the unmodified profile to standard
output like so:

.. code-block:: console

  somevar="test1"
  # This is a comment.
  anothervar="${somevar}"
  numbervar=123

There is also the ``-e`` flag which is occasionally useful:

``envswitch -e``

This functions almost the same as ``-s``, except all environment
variables will be printed with an ``export `` prefixed to each one,
making it convenient to export some or all environment variables
quickly for use on a different machine that does not have envswitch
installed or configured. eg.

.. code-block:: console

  export somevar="test1"
  # This is a comment.
  export anothervar="${somevar}"
  export numbervar=123


Help
~~~~

A summary of all possible arguments can also be shown:

``envswitch -h``


Unloading a profile
~~~~~~~~~~~~~~~~~~~

To clear all environment variables from the shell and unload the
current profile:

``envreset``

Note that when switching profiles, it is not necessary to call
``envreset`` first. Any currently loaded profile will be unloaded
automatically before the new profile is imported.


Issues
======

If you encounter any bugs or would like to propose a new feature, feel
free to open an issue on GitHub, however please be patent with a
response.

Likewise, pull requests are also welcome.
