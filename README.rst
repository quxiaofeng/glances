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

想要安装测试 Glances 的话，有多种途径供您选择。

Glances 自动安装脚本：完全版
------------------------------------------

同时安装各种依赖和新鲜出厂的 Glances（即 *master* 分支），只需要执行如下命令：

.. code-block:: console

    curl -L https://bit.ly/glances | /bin/bash

或者

.. code-block:: console

    wget -O- https://bit.ly/glances | /bin/bash

*注意*： 只支持一部分 GNU/Linux 发布版。如果你能提供其他发布版的支持，请提交到
`glancesautoinstall`_。

PyPI：极简版
--------------------

Glances 已经纳入到 ``PyPI`` 了。使用 PyPI，可以安装最新稳定版。

安装只需使用 ``pip``：

.. code-block:: console

    pip install glances

*注意*：安装 `psutil`_需要有 Python 头文件。如，在 Debian/Ubuntu 平台，需要先
安装 *python-dev* 包。在 Fedora/CentOS/RHEL （红帽系）需要先安装
*python-devel* 包。在 Windows 上，只需要用二进制安装文件安装 psutil。

*注意 2 （wifi 插件）*：如果想要用 Wifi 插件，需要系统里安装过 *wireless-tools*。

当然，你也可以安装下面的包来使用可选的其它功能（如 Web 界面，各种导出模块等）：

.. code-block:: console

    pip install glances[action,browser,cloud,cpuinfo,chart,docker,export,folders,gpu,ip,raid,snmp,web,wifi]

升级 Glances 到最新版

.. code-block:: console

    pip install --upgrade glances
    pip install --upgrade glances[...]

如果需要把 Glances 安装到自定义的位置，使用：

.. code-block:: console

    export PYTHONUSERBASE=~/自定义路径
    pip install --user glances

Docker：逗逼版
---------------------

Glances 容器也是有的。这里会是最新开发的 `HEAD` 版本。可以用这个容器来监控你的
服务器和所有其它容器！

Glances 容器可以这样使用：

.. code-block:: console

    docker pull nicolargo/glances

在*控制台模式*使用容器：

.. code-block:: console

    docker run -v /var/run/docker.sock:/var/run/docker.sock:ro --pid host -it docker.io/nicolargo/glances

另外，如果你想用自己的 `glances.conf` 文件，可以用如下 `Dockerfile` 创建：

.. code-block:: console

    FROM nicolargo/glances
    COPY glances.conf /glances/conf/glances.conf
    CMD python -m glances -C /glances/conf/glances.conf $GLANCES_OPT

还有一个方法，可以在运行 docker 时用 run 的选项加入配置：

.. code-block:: console

    docker run -v ./glances.conf:/glances/conf/glances.conf -v /var/run/docker.sock:/var/run/docker.sock:ro --pid host -it docker.io/nicolargo/glances

这里 ./glances.conf 是主机中有 `glances.conf` 配置文件的目录。

以 *Web 服务器模式* 运行这个容器（注意 `GLANCES_OPT` 选项指定
glances 起始命令的设置参数）：

.. code-block:: console

    docker run -d --restart="always" -p 61208-61209:61208-61209 -e GLANCES_OPT="-w" -v /var/run/docker.sock:/var/run/docker.sock:ro --pid host docker.io/nicolargo/glances

GNU/Linux
---------

`Glances` 已经进入了很多 Linux 发布版。大多数情况下，可以直接使用你惯用的
包管理器安装。只是使用包管理安装的 Glances 可能不是最新版。

FreeBSD
-------

安装二进制包：

.. code-block:: console

    # pkg install py27-glances

使用 ports 安装：

.. code-block:: console

    # cd /usr/ports/sysutils/py-glances/
    # make install clean

macOS 苹果电脑
-----

macOS 用户可以用 ``Homebrew`` 或者 ``MacPorts`` 安装 Glances。

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

先安装 Windows 版 `Python` （Python 2.7.9+ 或 3.4+，自带 pip），然后：

.. code-block:: console

    $ pip install glances

Android 安卓
-------

需要先刷机（root），且安装有 `Termux`_App（可以在 Google 商店安装）。

启动 Termux 并输入：

.. code-block:: console

    $ apt update
    $ apt upgrade
    $ apt install clang python python-dev
    $ pip install bottle
    $ pip install glances

运行 Glances：

.. code-block:: console

    $ glances

可以用服务器模式（-s or -w）运行 Glances，以便远程监控安卓设备。

源码
------

源码安装 Glances：

.. code-block:: console

    $ wget https://github.com/nicolargo/glances/archive/vX.Y.tar.gz -O - | tar xz
    $ cd glances-*
    # python setup.py install

*注意*： 安装 psutil 需要有 Python 头文件。

Chef
----

也可以用这份超赞的 ``Chef`` cookbook 来监控你的服务器：
https://supermarket.chef.io/cookbooks/glances (荣耀归于 Antoine Rouyer)

Puppet
------

使用 ``Puppet`` 安装 Glances： https://github.com/rverchere/puppet-glances

使用方法
=====

单机模式，简单执行：

.. code-block:: console

    $ glances

Web 服务器模式，执行:

.. code-block:: console

    $ glances -w

然后在浏览器中输入网址 URL ``http://<ip>:61208`` 监控你的主机。

远程 client/server 模式，执行如下代码：

在服务器端，运行：

.. code-block:: console

    $ glances -s

在客户端，运行：

.. code-block:: console

    $ glances -c <ip>

也可以探测并显示网络中所有可用的 Glances 服务器，或者根据配置文件查找：

.. code-block:: console

    $ glances --browser

当然了，先读文档（RTFM），一贯的。

文档
=============

完整的文档，请在 readthedocs_ 网站查看.

如果你（读了文档之后）还有问题，请在官方 Q&A `论坛`_发帖询问。

相关链接
=========================

Glances 可以把监控信息导出到： ``CSV`` 文件， ``JSON`` 文件， ``InfluxDB``， ``Cassandra``， ``CouchDB``，
``OpenTSDB``， ``Prometheus``， ``StatsD``， ``ElasticSearch``， ``RabbitMQ/ActiveMQ``，
``ZeroMQ``， ``Kafka``， ``Riemann`` 和 ``Restful`` 服务器。

怎样贡献代码？
===================

如果想向 Glances 项目提交代码，请阅读这个 `wiki`_ 页面。

这里也有一个 Glances 开发者出没的 Chat：

.. image:: https://badges.gitter.im/Join%20Chat.svg
        :target: https://gitter.im/nicolargo/glances?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge

作者
======

Nicolas Hennion (@nicolargo) <nicolas@nicolargo.com>

README 中文译者
======

曲晓峰 (@quxiaofeng) <xiaofeng.qu.hk@ieee.org>

版权文件
=======

LGPLv3。细节详见  ``COPYING`` 。

.. _psutil: https://github.com/giampaolo/psutil
.. _glancesautoinstall: https://github.com/nicolargo/glancesautoinstall
.. _@nicolargo: https://twitter.com/nicolargo
.. _@quxiaofeng: https://zhihu.com/quxiaofeng
.. _Python: https://www.python.org/getit/
.. _Termux: https://play.google.com/store/apps/details?id=com.termux
.. _readthedocs: https://glances.readthedocs.io/
.. _论坛: https://groups.google.com/forum/?hl=en#!forum/glances-users
.. _wiki: https://github.com/nicolargo/glances/wiki/How-to-contribute-to-Glances-%3F
