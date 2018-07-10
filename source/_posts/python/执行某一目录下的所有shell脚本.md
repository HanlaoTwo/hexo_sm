---
title: 执行某一目录下的所有shell脚本
date: 2018-07-10 21:09:19
tags: python
---
#### for i in tree:会多次循环，很奇怪
```
import os

# import commands

homedir = os.path.dirname(os.path.abspath('run_sqoop.py'))


def get_shells(filedir):
    print("dirName............. ", filedir)
    tree = os.walk(filedir, topdown=True)
    for i in tree:
        nodeName = i[0]
        nodeDir = i[1]
        nodeFiles = i[2]
        print(">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>nodeName: ", nodeName)
        for file in nodeFiles:
            if (file.endswith(".sh")):
                command = nodeName + "/" + file
                print("commands:", command)
                # out = commands.getstatusoutput(command)
                # print(out)
        for shelldir in nodeDir:
            get_shells(shelldir)
        return


get_shells(homedir)
```