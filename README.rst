Kios
====

.. contents::

Introduction
------------

Kios is a tool to collect and store TCP/UDP port usage data. Currently Kios supports netstat on
Windows platform as the only source of port data and SQLite as the only database backend.

Ports bound to loopback interfaces are ignored.

Installation
------------

Releases are available from PyPI at https://pypi.org/project/kios/

Usage
-----

Add application and associate executable to track (more than one executable
per app is supported)::

    kios add Application1 application1.exe

Then use command *scan* to periodically execute *netstat*, look for
ports listened on by *application1.exe* and save protocol/number data, associating
it with *Application1*. Use optional positional argument next to *scan* to
override default scan interval, which is 5 seconds::

    kios scan 10

**Note**, that this command requires elevated privileges. If it is not desirable to run
Kios as administrator (it is not), then use *netstat* output captured in a file with
command *import*::

    kios import D:\out.txt

To capture output in a compatible format, execute *netstat* with arguments given below::

    netstat -a -b -n > C:\out.txt

Use command *list* to print all tracked applications::

    C:\>kios list
    Known applications:
     Application1

Command *show* is used to print all information gathered on a specified application::

    C:\>kios show Application1
    Data for Application1
    Ports:
     IPv4   TCP     1
     IPv4   UDP     2
     IPv6   TCP     3
     IPv6   UDP     4
    Executables:
     application1.exe

It is possible to un-track executable with command *remove*::

    kios remove application1.exe

and delete **all** information associated with a specified app using command *purge*::

    kios purge Application1

To get information about optional arguments not mentioned here, use

::

    kios --help

and

::

    kios COMMAND --help

License
-------

Kios is released under version 2.0 of the `Apache License`_.

.. _Apache License: http://www.apache.org/licenses/LICENSE-2.0