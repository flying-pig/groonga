.. -*- rst -*-

.. highlightlang:: none

Debian GNU/Linux
================

This section describes how to install Groonga related deb packages on
Debian GNU/Linux. You can install them by ``apt``.

We distribute both 32-bit and 64-bit packages but we strongly
recommend a 64-bit package for server. You should use a 32-bit package
just only for tests or development. You will encounter an out of
memory error with a 32-bit package even if you just process medium
size data.

jessie
------

.. versionadded:: 5.0.3

Add the Groonga apt repository.

/etc/apt/sources.list.d/groonga.list::

  deb http://packages.groonga.org/debian/ jessie main
  deb-src http://packages.groonga.org/debian/ jessie main

Install::

  % sudo apt-get update
  % sudo apt-get install -y --allow-unauthenticated groonga-keyring
  % sudo apt-get update
  % sudo apt-get install -y -V groonga

.. include:: server-use.inc

If you want to use `MeCab <http://mecab.sourceforge.net/>`_ as a
tokenizer, install groonga-tokenizer-mecab package.

Install groonga-tokenizer-mecab package::

  % sudo apt-get install -y -V groonga-tokenizer-mecab

If you want to use ``TokenFilterStem`` as a token filter, install
groonga-token-filter-stem package.

Install groonga-token-filter-stem package::

  % sudo apt-get install -y -V groonga-token-filter-stem

There is a package that provides `Munin
<http://munin-monitoring.org/>`_ plugins. If you want to monitor
Groonga status by Munin, install groonga-munin-plugins package.

Install groonga-munin-plugins package::

  % sudo apt-get install -y -V groonga-munin-plugins

There is a package that provides MySQL compatible normalizer as
a Groonga plugin.
If you want to use that one, install groonga-normalizer-mysql package.

Install groonga-normalizer-mysql package::

  % sudo apt-get install -y -V groonga-normalizer-mysql

.. note::

   If you use systemd as init, current version of Groonga does not support
   to register start-up service automatically during installation.
   If you want to register groonga-httpd/groonga-server-gqtp as
   a automatic start-up service, please execute the following commands:

   For groonga-httpd:

     % sudo systemctl enable groonga-httpd

   For groonga-server-gqtp:

     % sudo systemctl enable groonga-server-gqtp

Build from source
-----------------

Install required packages to build Groonga::

  % sudo apt-get install -y -V  wget tar build-essential zlib1g-dev liblzo2-dev libmsgpack-dev libzmq-dev libevent-dev libmecab-dev

Download source::

  % wget http://packages.groonga.org/source/groonga/groonga-6.0.2.tar.gz
  % tar xvzf groonga-6.0.2.tar.gz
  % cd groonga-6.0.2

Configure (see :ref:`source-configure` about ``configure`` options)::

  % ./configure

Build::

  % make -j$(grep '^processor' /proc/cpuinfo | wc -l)

Install::

  % sudo make install
