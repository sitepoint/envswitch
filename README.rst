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
  anothervar="${somevar}"
  numbervar=123

Note the name of the configuration file (minus the .conf extension)
should not match the name of an existing shell function. If in doubt,
check the output of ``declare -F``.


Usage
=====

``envswitch -l``
~~~~~~~~~~~~~~~~

Lists any available profiles. These exist as local bash functions,
which can be called any time just by typing the name. The shell
prompt should be updated to reflect the loaded profile.

``envswitch -s``
~~~~~~~~~~~~~~~~

Show all loaded environment variables (effectively printing the
loaded profile to standard output).

``envswitch -e``
~~~~~~~~~~~~~~~~

Works the same as ``-s``, except environment variables will be printed
with ``export `` prefixed to each one, making it convenient to export
some or all environment variables quickly for use on a different
machine that does not have envswitch installed or configured.

``envswitch -h``
~~~~~~~~~~~~~~~~

Shows a summary of the above arguments.

``envreset``
~~~~~~~~~~~~

Clears all environment variables from the shell and unloads the
current profile.


.. _GNU Bash: http://www.gnu.org/software/bash/
.. _GNU Core utilities: http://gnu.org/software/coreutils
.. _GNU Sed: https://www.gnu.org/software/sed/
