.. _extension:

Autodoc Extension
=================

Hawkmoth provides a Sphinx extension that adds :ref:`new directives
<directives>` to the Sphinx :external+sphinx:ref:`C <c-domain>` and
:external+sphinx:ref:`C++ <cpp-domain>` domains to incorporate formatted C and
C++ source code comments into a document. Hawkmoth is Sphinx
:py:mod:`sphinx.ext.autodoc` for C/C++.

For this to work, the documentation comments must of course be written in
correct reStructuredText. See :ref:`documentation comment syntax <syntax>` for
details.

Hawkmoth itself is :ref:`extensible <extending>`, and ships with some
:ref:`built-in extensions <built-in-extensions>`.

Usage
-----

Add ``hawkmoth`` to :external+sphinx:confval:`extensions` in ``conf.py``. Note
that depending on the packaging and installation directory, this may require
adjusting the :envvar:`python:PYTHONPATH`.

For example:

.. code-block:: python

   extensions.append('hawkmoth')

Configuration
-------------

The extension has a few configuration options that can be set in ``conf.py``.

See also additional configuration options in the :ref:`built-in extensions
<built-in-extensions>`.

.. py:data:: hawkmoth_root
   :type: str

   Path to the root of the source files. Defaults to the
   :external+sphinx:term:`configuration directory`, i.e. the directory
   containing ``conf.py``.

   To use paths relative to the configuration directory, use
   :func:`python:os.path.abspath`, for example:

   .. code-block:: python

      import os
      hawkmoth_root = os.path.abspath('my/sources/dir')

.. py:data:: hawkmoth_transform_default
   :type: str

   The default transform parameter to be passed to the
   :event:`hawkmoth-process-docstring` event. It can be overriden with the
   ``transform`` option of the :ref:`directives <directives>`. Defaults to
   ``None``.

.. py:data:: hawkmoth_clang
   :type: list

   A list of arguments to pass to ``clang`` while parsing the source, typically
   to add directories to include file search path, or to define macros for
   conditional compilation. No arguments are passed by default.

   Example:

   .. code-block:: python

      hawkmoth_clang = ['-I/path/to/include', '-DHAWKMOTH']

   Hawkmoth provides a convenience helper for querying the include path from the
   compiler, and providing them as ``-I`` options:

   .. code-block:: python

      from hawkmoth.util import compiler

      hawkmoth_clang = compiler.get_include_args()

   You can also pass in the compiler to use, for example
   ``get_include_args('gcc')``.

.. py:data:: cautodoc_root
   :type: str

   Equivalent to :py:data:`hawkmoth_root`.

   .. warning::

      The ``cautodoc_root`` option has been deprecated in favour of the
      :py:data:`hawkmoth_root` option and will be removed in the future.

.. py:data:: cautodoc_clang
   :type: str

   Equivalent to :py:data:`hawkmoth_clang`.

   .. warning::

      The ``cautodoc_clang`` option has been deprecated in favour of
      the :py:data:`hawkmoth_clang` option and will be removed in the
      future.
