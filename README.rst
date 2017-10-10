===============================
Glances - 帮你瞅着你的主机
===============================

.. image:: https://img.shields.io/pypi/v/glances.svg
    :target: https://pypi.python.org/pypi/Glances

.. image:: https://img.shields.io/github/stars/nicolargo/glances.svg
    :target: https://github.com/nicolargo/glances/
    :alt: Github stars

.. image:: https://img.shields.io/travis/nicolargo/glances/master.svg?maxAge=3600&label=Linux%20/%20BSD%20/%20macOS
    :target: https://travis-ci.org/nicolargo/glances
    :alt: Linux 测试 (Travis)

.. image:: https://img.shields.io/appveyor/ci/nicolargo/glances/master.svg?maxAge=3600&label=Windows
    :target: https://ci.appveyor.com/project/nicolargo/glances
    :alt: Windows 测试 (Appveyor)

.. image:: https://img.shields.io/scrutinizer/g/nicolargo/glances.svg
    :target: https://scrutinizer-ci.com/g/nicolargo/glances/

.. image:: https://img.shields.io/badge/Donate-PayPal-green.svg
    :target: https://www.paypal.me/nicolargo

关注 Glances 的 Twitter: `@nicolargo`_

简介
=======

**Glances** 是一款跨平台的系统监控工具。他的主要目标是在最少的空间里展示
最多的信息。他提供命令行模式，也可以使用 web 接口。还可以动态适应用户界面
的大小，合适的展示信息。

.. image:: https://raw.githubusercontent.com/nicolargo/glances/develop/docs/_static/glances-summary.png

该工具也可以工作与客户机服务器模式（C/S 远程监控）。这一远程监控可以是终端、
可以是 web，也可以 API（XML-RPC 或 RESTful）调用。各种状态信息也可以导出
到文件，或者是时值对应的数据库(time/value)。

.. image:: https://raw.githubusercontent.com/nicolargo/glances/develop/docs/_static/glances-responsive-webdesign.png

Glances is written in Python and uses libraries to grab information from
your system. It is based on an open architecture where developers can
add new plugins or exports modules.

Glances 基于 Python 开发，使用 Python 的各种类库来获取系统信息。开放的系
统架构便于开发者开发新的插件，或者将他自己导出成一个模块。

系统需求
============

- ``python 2.7,>=3.3``
- ``psutil>=2.0.0`` (越新越好)

其他可能的依赖（Glances 有很多模块，各模块会有自身所需的依赖）:

- ``bernhard`` (Riemann 导出模块)
- ``bottle`` (Web 服务器模块)
- ``cassandra-driver`` (Cassandra 导出模块)
- ``couchdb`` (CouchDB 导出模块)
- ``docker`` (Docker 监控支持) [Linux-only]
- ``elasticsearch`` (Elastic Search 导出模块)
- ``hddtemp`` (硬盘温度监控支持) [Linux-only]
- ``influxdb`` (InfluxDB 导出模块)
- ``kafka-python`` (Kafka 导出模块)
- ``matplotlib`` (图表支持)
- ``netifaces`` (IP 插件)
- ``nvidia-ml-py3`` (GPU 插件)
- ``pika`` (RabbitMQ/ActiveMQ 导出模块)
- ``potsdb`` (OpenTSDB 导出模块)
- ``prometheus_client`` (Prometheus 导出模块)
- ``py-cpuinfo`` (Quicklook CPU 监控模块)
- ``pymdstat`` (RAID 支持) [Linux-only]
- ``pysnmp`` (SNMP 支持)
- ``pystache`` (action script 特性)
- ``pyzmq`` (ZeroMQ 导出模块)
- ``requests`` (Ports, Cloud 插件和 Restful 导出支持)
- ``scandir`` (Folders 插件) [只针对 Python < 3.5]
- ``statsd`` (StatsD 导出模块)
- ``wifi`` (wifi 插件) [Linux-only]
- ``zeroconf`` (自动搜索模式)

*Python 2.6 用户请注意*

从 2.7 版开始，Glances 不再支持 Python 2.6。请升级到 Python 2.7/3.3+ 或者降级
Glances 到 2.6.2（支持 Python 2.6 的最后版本）

*entOS Linux 6 and 7 用户请注意*

可以用过 SCLs 安装 Python 2.7, 3.3 and 3.4。参见：
https://lists.centos.org/pipermail/centos-announce/2015-December/021555.html.

安装
============

安装测试 Glances 有多种途径供您选择。

Glances Auto Install script: the total way
------------------------------------------

To install both dependencies and latest Glances production ready version
(aka *master* branch), just enter the following command line:

.. code-block:: console

    curl -L https://bit.ly/glances | /bin/bash

or

.. code-block:: console

    wget -O- https://bit.ly/glances | /bin/bash

*Note*: Only supported on some GNU/Linux distributions. If you want to
support other distributions, please contribute to `glancesautoinstall`_.

PyPI: The simple way
--------------------

Glances is on ``PyPI``. By using PyPI, you are sure to have the latest
stable version.

To install, simply use ``pip``:

.. code-block:: console

    pip install glances

*Note*: Python headers are required to install `psutil`_. For example,
on Debian/Ubuntu you need to install first the *python-dev* package.
For Fedora/CentOS/RHEL install first *python-devel* package. For Windows,
just install psutil from the binary installation file.

*Note 2 (for the Wifi plugin)*: If you want to use the Wifi plugin, you need
to install the *wireless-tools* package on your system.

You can also install the following libraries in order to use optional
features (like the Web interface, exports modules...):

.. code-block:: console

    pip install glances[action,browser,cloud,cpuinfo,chart,docker,export,folders,gpu,ip,raid,snmp,web,wifi]

To upgrade Glances to the latest version:

.. code-block:: console

    pip install --upgrade glances
    pip install --upgrade glances[...]

If you need to install Glances in a specific user location, use:

.. code-block:: console

    export PYTHONUSERBASE=~/mylocalpath
    pip install --user glances

Docker: the funny way
---------------------

A Glances container is available. It will include the latest development
HEAD version. You can use it to monitor your server and all your others
containers !

Get the Glances container:

.. code-block:: console

    docker pull nicolargo/glances

Run the container in *console mode*:

.. code-block:: console

    docker run -v /var/run/docker.sock:/var/run/docker.sock:ro --pid host -it docker.io/nicolargo/glances

Additionally, if you want to use your own glances.conf file, you can
create your own Dockerfile:

.. code-block:: console

    FROM nicolargo/glances
    COPY glances.conf /glances/conf/glances.conf
    CMD python -m glances -C /glances/conf/glances.conf $GLANCES_OPT

Alternatively, you can specify something along the same lines with
docker run options:

.. code-block:: console

    docker run -v ./glances.conf:/glances/conf/glances.conf -v /var/run/docker.sock:/var/run/docker.sock:ro --pid host -it docker.io/nicolargo/glances

Where ./glances.conf is a local directory containing your glances.conf file.

Run the container in *Web server mode* (notice the `GLANCES_OPT` environment
variable setting parameters for the glances startup command):

.. code-block:: console

    docker run -d --restart="always" -p 61208-61209:61208-61209 -e GLANCES_OPT="-w" -v /var/run/docker.sock:/var/run/docker.sock:ro --pid host docker.io/nicolargo/glances

GNU/Linux
---------

`Glances` is available on many Linux distributions, so you should be
able to install it using your favorite package manager. Be aware that
Glances may not be the latest one using this method.

FreeBSD
-------

To install the binary package:

.. code-block:: console

    # pkg install py27-glances

To install Glances from ports:

.. code-block:: console

    # cd /usr/ports/sysutils/py-glances/
    # make install clean

macOS
-----

macOS users can install Glances using ``Homebrew`` or ``MacPorts``.

Homebrew
````````

.. code-block:: console

    $ brew install python
    $ pip install glances

MacPorts
````````

.. code-block:: console

    $ sudo port install glances

Windows
-------

Install `Python`_ for Windows (Python 2.7.9+ and 3.4+ ship with pip) and
then just:

.. code-block:: console

    $ pip install glances

Android
-------

You need a rooted device and the `Termux`_ application (available on the
Google Store).

Start Termux on your device and enter:

.. code-block:: console

    $ apt update
    $ apt upgrade
    $ apt install clang python python-dev
    $ pip install bottle
    $ pip install glances

And start Glances:

.. code-block:: console

    $ glances

You can also run Glances in server mode (-s or -w) in order to remotely
monitor your Android device.

Source
------

To install Glances from source:

.. code-block:: console

    $ wget https://github.com/nicolargo/glances/archive/vX.Y.tar.gz -O - | tar xz
    $ cd glances-*
    # python setup.py install

*Note*: Python headers are required to install psutil.

Chef
----

An awesome ``Chef`` cookbook is available to monitor your infrastructure:
https://supermarket.chef.io/cookbooks/glances (thanks to Antoine Rouyer)

Puppet
------

You can install Glances using ``Puppet``: https://github.com/rverchere/puppet-glances

Usage
=====

For the standalone mode, just run:

.. code-block:: console

    $ glances

For the Web server mode, run:

.. code-block:: console

    $ glances -w

and enter the URL ``http://<ip>:61208`` in your favorite web browser.

For the client/server mode, run:

.. code-block:: console

    $ glances -s

on the server side and run:

.. code-block:: console

    $ glances -c <ip>

on the client one.

You can also detect and display all Glances servers available on your
network or defined in the configuration file:

.. code-block:: console

    $ glances --browser

and RTFM, always.

Documentation
=============

For complete documentation have a look at the readthedocs_ website.

If you have any question (after RTFM!), please post it on the official Q&A `forum`_.

Gateway to other services
=========================

Glances can export stats to: ``CSV`` file, ``JSON`` file, ``InfluxDB``, ``Cassandra``, ``CouchDB``,
``OpenTSDB``, ``Prometheus``, ``StatsD``, ``ElasticSearch``, ``RabbitMQ/ActiveMQ``,
``ZeroMQ``, ``Kafka``, ``Riemann`` and ``Restful`` server.

How to contribute ?
===================

If you want to contribute to the Glances project, read this `wiki`_ page.

There is also a chat dedicated to the Glances developers:

.. image:: https://badges.gitter.im/Join%20Chat.svg
        :target: https://gitter.im/nicolargo/glances?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge

Author
======

Nicolas Hennion (@nicolargo) <nicolas@nicolargo.com>

License
=======

LGPLv3. See ``COPYING`` for more details.

.. _psutil: https://github.com/giampaolo/psutil
.. _glancesautoinstall: https://github.com/nicolargo/glancesautoinstall
.. _@nicolargo: https://twitter.com/nicolargo
.. _Python: https://www.python.org/getit/
.. _Termux: https://play.google.com/store/apps/details?id=com.termux
.. _readthedocs: https://glances.readthedocs.io/
.. _forum: https://groups.google.com/forum/?hl=en#!forum/glances-users
.. _wiki: https://github.com/nicolargo/glances/wiki/How-to-contribute-to-Glances-%3F
