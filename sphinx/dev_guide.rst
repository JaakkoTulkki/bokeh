
.. _devguide:

###############
Developer Guide
###############

.. contents::
    :local:
    :depth: 2

Architecture Overview
=====================

.. _bokehjs:

BokehJS
=======

BokehJS is the in-browser client-side runtime library that users of Bokeh
ultimately interact with.  This library is written primarily in Coffeescript
and is one of the very unique things about the Bokeh plotting system.

BokehJS Motivations
-------------------

When researching the wide field of Javascript plotting libraries, we found
that they were all architected and designed to integrate with other Javascript.
If they provided any server-side wrappers, those were always "second class" and
primarily designed to generate a simple configuration for the front-end JS.  Of
the few JS plotting libraries that offered any level of interactivity, the
interaction was not really configurable or customizable from outside the JS
itself.  Very few JS plotting libraries took large and streaming server-side
data into account, and providing seamless access to those facilities from
another language like Python was not a consideration.

This, in turn, has caused the developers of Python plotting libraries to
only treat the browser as a "backend target" environment, for which they
will generate static images or a bunch of Javascript.

Goals
-----

BokehJS is intended to be a standalone, first-class Javascript plotting
library and *interaction runtime* for dynamic, highly-customizable
information visualization.  Currently we use HTML5 Canvas, and in the
future this may be extended to include WebGL.  We are keeping a very
close watch over high-performance Javascript technologies, including
web workers, asm.js, SIMD, and parallel JS (e.g. River Trail).


.. _pythoninterface:

Python Interface
================

*Coming soon*

Properties
----------


Sessions
--------


Low-level Object Interface
--------------------------

Here is a notional diagram showing the overall object system in Bokeh. We will discuss each
of these in turn.

.. image:: /_images/objects.png
    :align: center

High Level Plotting Interface
-----------------------------



.. _developer_install:

Installation for Developers
===========================

Bokeh development is complicated by the fact that there is Python code and
Coffeescript in Bokeh itself, and there is Coffeescript in BokehJS.

It is possible to set up just for development on Bokeh, without having a
development install of BokehJS.  To do this, just run ``python setup.py install``.
This will copy the pre-built ``bokeh.js`` from the ``bokehjs/release`` directory
into the correct place in the source tree.

If you want to do development on BokehJS as well, then modify the Coffeescript
source in the ``bokehjs/`` directory, and follow the instructions below for
building/installing Coffeescript.  Then run ``python setup.py devjs``.
ONLY DO THIS IF YOU KNOW WHAT YOU ARE DOING!

If you have any problems with the steps here, please contact the developers
(see :ref:`contact`).

Coffeescript
------------

Building the Coffeescript BokehJS library has a number of requirements:

You need to have node.js and and the node package manager (npm)
installed.

We're using Grunt for our Coffeescript build tool.  Grunt will compile
coffeescript, combine js files, and support node.js require syntax on the
client side.  Install grunt by executing::

    $ npm install -g grunt-cli

We're using bower to manage client dependencies. Install bower by
executing::

    $ npm install -g bower

In order to build the javascript files that comprise bokeh.js, first install
necessary dependencies::

    $ npm install && bower install

These command will install compile and runtime dependencies into node_modules
and build subdirectories, respectively.

To compile the Coffeescript into javascript, execute grunt::

    $ grunt build

At this point bokeh can be be used as an AMD module together with require.js.
To build a single bokeh.js that may be included as a script, see below.

Grunt can concatenate the javascript files into a single bokeh.js, either
minified or unminified. To generate a minified script, execute the
command::

    $ grunt deploy

The resulting script will have the filename bokeh.min.js and be located in
the build subdirectory.

To generate an un-minified script, (useful for debugging or developing
bokehjs), execute the command::

    $ grunt devdeploy

The resulting script will have the filename bokeh.js and be located in
the build subdirectory.
