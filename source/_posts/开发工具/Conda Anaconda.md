---
title: Conda Anaconda
date: 2018-07-10 21:09:19
tags: 开发工具
---
```
C:\ProgramData\Miniconda3;
C:\ProgramData\Miniconda3\Library\mingw-w64\bin;
C:\ProgramData\Miniconda3\Library\usr\bin;
C:\ProgramData\Miniconda3\Library\bin;
C:\ProgramData\Miniconda3\Scripts;
C:\Program Files (x86)\py\Scripts\;
C:\Program Files (x86)\py\;
D:\oracle\product\10.2.0\client_1\bin;
C:\Program Files (x86)\Common Files\NetSarang;
C:\Program Files (x86)\Intel\iCLS Client\;
C:\Program Files\Intel\iCLS Client\;%SystemRoot%\system32;%SystemRoot%;%SystemRoot%\System32\Wbem;%SYSTEMROOT%\System32\WindowsPowerShell\v1.0\;
C:\Program Files (x86)\Intel\Intel(R) Management Engine Components\DAL;
C:\Program Files\Intel\Intel(R) Management Engine Components\DAL;
C:\Program Files (x86)\Intel\Intel(R) Management Engine Components\IPT;
C:\Program Files\Intel\Intel(R) Management Engine Components\IPT;%MAVEN_HOME%\bin;%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;%CATALINA_HOME%\lib;%CATALINA_HOME%\bin;
C:\Program Files\TortoiseSVN\bin;
```
These Miniconda installers contain the conda package manager and Python. Once Miniconda is installed, you can use the conda command to install any other packages and create environments, etc. For example:

```
$ conda install numpy

$ conda create -n py3k anaconda python=3
```
There are two variants of the installer: Miniconda is Python 2 based and Miniconda3 is Python 3 based. Note that the choice of which Miniconda is installed only affects the root environment. Regardless of which version of Miniconda you install, you can still install both Python 2.x and Python 3.x environments.

The other difference is that the Python 3 version of Miniconda will default to Python 3 when creating new environments and building packages. So for instance, the behavior of

```
$ conda create -n myenv python
```
will be to install Python 2.7 with the Python 2 Miniconda and to install Python 3.6 with the Python 3 Miniconda. You can override the default by explicitly setting python=2 or python=3. It also determines the default value of CONDA_PY when using conda build.

We have 32-bit Mac OS X binaries available, please contact us for more details at sales@continuum.io.

Note: If you already have Miniconda or Anaconda installed, and you just want to upgrade, you should not use the installer. Just use conda update. For instance
```
$ conda update conda
```